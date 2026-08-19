---
title: "When to use brand brand context or a brand kit"
slug: "when-to-use-brand-context-or-a-brand-kit"
abstract: "Learn when to use a brand context or brand kit to guide AI-assisted work in SitecoreAI."
---
# When to use brand context or a brand kit

[Brand context](brand-context.md) and [brand kits](https://doc.sitecore.com/sai/en/users/sitecoreai/design-components/brand-kits.html) both provide SitecoreAI with information about your brand, but they are built from different sources and designed for different needs.

- Use **brand context** when Agentic studio chats or agents need broad business and marketing context about your brand, such as its audiences, offerings, messaging, content guidelines, and supporting evidence.
- Use a **brand kit** when you want SitecoreAI to work from brand knowledge and established guidelines created from your uploaded brand documents, such as tone of voice, writing rules, visual guidelines, and localization preferences.

You can use both when a task benefits from broader brand context as well as established brand knowledge and guidelines.

## Use brand context to ground AI tasks

Each brand context you [add](add-brand-context.md) to SitecoreAI organizes information into default [folders](brand-context.md#generated-folders-and-files) like *Audiences*, *Messaging* and *Content Guidelines*.

For details about the generated structure, see [Brand context folders and files](brand-context-folders-and-files.md).

Brand context is useful for tasks such as:

- Planning campaigns for specific audiences or buyer journey stages.
- Developing messaging and value propositions.
- Comparing products, capabilities, or integrations.
- Creating audience-specific content.
- Supporting claims with proof points and customer evidence.
- Combining information from different areas of the brand into one response.

In [Agentic studio](use-brand-context-in-agentic-studio.md), you can select a brand context to provide relevant brand information to chats and agents while they work.

## Use a brand kit to apply brand knowledge and guidelines

A brand kit is created from uploaded brand documents. It includes retrievable brand knowledge from those documents and [predefined sections](https://doc.sitecore.com/sai/en/users/sitecoreai/design-components/brand-kits.html#understanding-the-brand-kit-sections) that organize selected information into areas such as *Global Goals*, *Brand Context*, *Dos and Don'ts*, *Grammar Guidelines*, and *Glossary and Localization*.  
  
> [!note]
>
> The *Brand Context* section in a brand kit is part of that brand kit. It is different from the [brand context](brand-context.md) feature.

You can edit the content in these sections, but you cannot add, remove, or rename the sections.

In SitecoreAI, you can [assign a brand kit to a site](https://doc.sitecore.com/sai/en/users/sitecoreai/ai-capabilities-in-sitecoreai/assign-a-brand-kit-to-a-site.html) to use it in:

- [Content generation and optimization](https://doc.sitecore.com/sai/en/users/sitecoreai/ai-capabilities-in-sitecoreai/optimize-content-with-ai.html) - uses *Brand Context*, *Tone of Voice*, and *Dos and Don'ts* sections guide generated or optimized content.
- [AI-assisted translation](https://doc.sitecore.com/sai/en/users/sitecoreai/ai-capabilities-in-sitecoreai/translation-in-sitecoreai.html) - uses *Glossary and Localization* to translate or preserve defined terms. When no glossary entry applies, *Dos and Don'ts* guide terminology and phrasing.

You can also use a brand kit in:

- [Brand Assistant](https://doc.sitecore.com/sai/en/users/sitecoreai/plan-campaign-strategy/using-the-brand-assistant.html) - uses brand kit sections and knowledge from uploaded brand documents.
- [Agentic studio](https://doc.sitecore.com/sai/en/users/sitecoreai/working-with-agentic-studio/agentic-studio-settings/tools-available-to-chats-and-agents.html) - lets chats and agents retrieve relevant brand knowledge and guidelines as context.

## Compare brand context and brand kits

|  | Brand context | Brand kit |
| --- | --- | --- |
| **Primary role** | Gives AI a broad understanding of the brand | Guides how the brand should communicate |
| **Best for** | Providing agents with general-purpose brand information | Applying approved brand guidelines consistently |
| **How it is applied** | Selected in an Agentic studio chat or agent | Selected in an Agentic studio chat or agent and used in supported [AI capabilities](../ai-capabilities-in-sitecoreai/ai-capabilities-in-sitecoreai.md) |
| **Structure** | Generated files and folders that provide a starting structure | Brand knowledge and predefined brand kit sections |
| **Customization** | Edit, add, rename, or delete files and folders | Edit content within the predefined sections and manage the source documents|


The two features are complementary. Brand context gives chats and agents structured information from across the brand to help them understand and reason about a task. A brand kit provides brand knowledge and established guidelines that help SitecoreAI keep outputs aligned with the brand.

Use both when a task benefits from both types of context.
