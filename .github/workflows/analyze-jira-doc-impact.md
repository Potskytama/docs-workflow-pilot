---
description: Analyze a Jira ticket against docs content and TOC to identify likely documentation impact.

on:
  workflow_dispatch:
    inputs:
      jira_key:
        description: Jira key, for example ABC-123
        required: true
        type: string

permissions:
  contents: read
  copilot-requests: write

engine: copilot

tools:
  edit:
  bash:
    - cat
    - head
    - tail
    - sed
    - grep
    - sort
    - uniq
    - wc
    - find
    - jq
    - rg

steps:
  - name: Validate Jira secrets
    shell: bash
    env:
      JIRA_BASE_URL: ${{ secrets.JIRA_BASE_URL }}
      JIRA_EMAIL: ${{ secrets.JIRA_EMAIL }}
      JIRA_API_TOKEN: ${{ secrets.JIRA_API_TOKEN }}
    run: |
      test -n "$JIRA_BASE_URL"
      test -n "$JIRA_EMAIL"
      test -n "$JIRA_API_TOKEN"

  - name: Fetch Jira issue
    id: jira
    shell: bash
    env:
      JIRA_BASE_URL: ${{ secrets.JIRA_BASE_URL }}
      JIRA_EMAIL: ${{ secrets.JIRA_EMAIL }}
      JIRA_API_TOKEN: ${{ secrets.JIRA_API_TOKEN }}
    run: |
      curl -sS \
        -u "$JIRA_EMAIL:$JIRA_API_TOKEN" \
        -H "Accept: application/json" \
        "$JIRA_BASE_URL/rest/api/3/issue/${{ inputs.jira_key }}" > jira-issue.json

      jq -r '.fields.summary // ""' jira-issue.json > jira-summary.txt
      jq -r '
        .fields.description.content // []
        | map(
            .content // []
            | map(.text // "")
            | join(" ")
          )
        | join(" ")
      ' jira-issue.json > jira-description.txt

      jq -r '.fields.components // [] | map(.name) | join(" ")' jira-issue.json > jira-components.txt
      jq -r '.fields.labels // [] | join(" ")' jira-issue.json > jira-labels.txt

  - name: Build deterministic candidate set
    shell: bash
    run: |
      cat jira-summary.txt jira-description.txt jira-components.txt jira-labels.txt > jira-search-source.txt

      tr '[:upper:]' '[:lower:]' < jira-search-source.txt \
        | sed -E 's/[^a-z0-9]+/\n/g' \
        | sed '/^$/d' \
        | awk 'length($0) >= 4' \
        | sort -u \
        | head -n 20 > terms.txt

      : > matches.txt
      find docs -type f \( -name "*.md" -o -name "toc.json" \) | sort > docs-files.txt

      while IFS= read -r term; do
        rg -i -l "$term" docs --glob "*.md" --glob "toc.json" >> matches.txt || true
        grep -i "$term" docs-files.txt >> matches.txt || true
      done < terms.txt

      SUMMARY=$(cat jira-summary.txt)
      if [ -n "$SUMMARY" ]; then
        rg -i -l "$SUMMARY" docs --glob "*.md" --glob "toc.json" >> matches.txt || true
      fi

      sort -u matches.txt > unique-matches.txt

post-steps:
  - name: Upload analysis inputs and outputs
    if: always()
    uses: actions/upload-artifact@v4
    with:
      name: jira-doc-impact-${{ inputs.jira_key }}
      path: |
        jira-issue.json
        jira-summary.txt
        jira-description.txt
        jira-components.txt
        jira-labels.txt
        terms.txt
        docs-files.txt
        unique-matches.txt
        ai-analysis.md
        ai-analysis.json
---

# Analyze Jira Documentation Impact

Use the deterministic context that was prepared in the workflow steps.

Primary inputs:

- `jira-issue.json`
- `jira-summary.txt`
- `jira-description.txt`
- `jira-components.txt`
- `jira-labels.txt`
- `terms.txt`
- `docs-files.txt`
- `unique-matches.txt`
- `docs/toc.json`

Your task is to review the Jira issue and the candidate docs, then produce two files:
- `ai-analysis.md`
- `ai-analysis.json`

Read `unique-matches.txt` first, then inspect the most relevant matched Markdown files and `docs/toc.json`.

Treat the deterministic search results as candidate files, not final truth.

Your goals:
- identify which files are most likely affected
- distinguish likely primary files from related context files
- decide whether this is mainly a `create`, `update`, `restructure`, or `delete` documentation task
- decide whether a net-new topic is likely needed
- decide whether `docs/toc.json` likely needs updating
- identify the likely documentation changes needed
- list open questions or assumptions that require human review

Use this rubric:
- Prefer precision over breadth.
- Do not list every loosely related file as a primary file.
- If the Jira wording indicates a new topic, say so explicitly even if several related files already exist.
- If navigation is likely affected, call that out even when `docs/toc.json` did not appear in deterministic matches.
- If the deterministic results are noisy, narrow them down.

Write `ai-analysis.json` in this exact shape:

    {
      "jira_key": "",
      "summary": "",
      "action_type": "create",
      "net_new_topic": true,
      "toc_update_likely": true,
      "primary_files": [],
      "related_context_files": [],
      "recommended_changes": [],
      "open_questions": [],
      "assumptions": [],
      "confidence": "medium"
    }

Allowed values:
- `action_type`: `create`, `update`, `restructure`, `delete`
- `confidence`: `low`, `medium`, `high`

Write `ai-analysis.md` as a concise human-readable report with these sections:
1. `Summary`
2. `Primary Files`
3. `Related Context`
4. `Navigation Impact`
5. `Recommended Doc Changes`
6. `Open Questions`
7. `Confidence`

If no matched file is truly primary, say so clearly and recommend a net-new topic.
