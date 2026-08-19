---
title: "Brand context"
slug: "brand-context"
abstract: "Learn what brand context is and how SitecoreAI generates it from a website URL or an existing site."
---
# Brand context

*Brand context* is structured, reusable information that provides AI agents with a broad understanding of your brand, helping them generate more grounded, consistent, and brand-aligned responses.

SitecoreAI builds this brand context from a source you provide and organizes what it learns into editable Markdown files. These files cover key areas such as your audiences, products or services, messaging, content guidelines, and customer evidence.

You can add more than one brand context to support different brands, websites, regions, business units, or other brand needs.

## Why use brand context?

AI agents produce better results when they have reliable information about the brand they are working with.

Without brand context, an AI agent might understand the task you give it, but not necessarily know:

- Who your most important audiences are.
- What products, services, or capabilities you offer.
- How you position your brand and communicate its value.
- Which terminology, style, and content standards it should follow.
- Which evidence it can use to support brand claims.

This information is often spread across websites, product pages, brand guidelines, customer stories, and other sources.

Brand context in SitecoreAI brings this information into a structured, reusable form so teams can review, maintain, and use it across supported AI workflows.

## How brand context works

SitecoreAI organization admins or owners can add one or more brand contexts. Each brand context is created from a single source: either a brand website URL or an existing SitecoreAI site.

After you provide a source:

1. SitecoreAI analyzes the source and related publicly available information to identify useful brand and marketing details.
2. SitecoreAI organizes that information into a standard set of folders and editable brand context files.
3. Admins or owners review the generated information and update it as needed.
4. Users can select a brand context for [use in Agentic studio](use-brand-context-in-agentic-studio.md).
5. The AI agent or chat uses the relevant brand information from the selected brand context in the background. Users do not need to manually select individual files or folders to provide context.

## Generated folders and files

Each brand context includes generated folders and editable Markdown files that organize different aspects of the brand.

When you open a brand context in SitecoreAI, the file explorer shows the generated folders and files so you can review, edit, and refine the information.

![The folders and files generated for the brand context focus on different aspects of the brand.](images/brand-context-generated-folder-and-files.png)

The generated structure covers five areas of brand knowledge.

| Folder | Initial files | What it covers |
| --- | --- | --- |
| **Audiences** | Audience Strategy, Buyer Journey Map, Industry Verticals, Persona Profiles | Audience segments, needs, journeys, and personas |
| **Messaging** | Competitive Positioning, Messaging Framework, Proof Points, Value Propositions | Positioning, differentiation, key messages, and value |
| **Product** | Capabilities Matrix, Integrations & Ecosystem, Product Portfolio | Products, services, capabilities, and ecosystem |
| **Content Guidelines** | Channel Guide, Content Standards, Style Guide | Channel guidance, content standards, style, and terminology |
| **Customer Evidence** | Case Studies, Evidence Framework, Success Metrics, Testimonials | Evidence that can support brand claims |

These areas help AI understand who the brand serves, what it offers, how it communicates, and what supports its claims. 
For details about the generated folders, the files they contain, and how each type of information can be used, see [Brand context folders and files](brand-context-folders-and-files.md).

## Editing brand context

Generated brand context provides a starting point that admins and owners can review, refine, and maintain over time.

The information generated depends on the brand and the information available from the source. It can include details found directly in the source as well as interpretations based on publicly available information. Some areas might contain limited information or might not apply to every brand.

Admins and owners can edit the generated files to:

- Correct or remove generated information.
- Add information that was not available from the source.
- Replace generated interpretations with approved brand guidance.
- Add internal guidelines or preferences.
- Keep the information current as the brand evolves.

For example, an admin might update a generated **Persona Profiles** file with new audience details that are relevant to the brand.

![Admins can review and refine every generated file after creation.](images/brand-context-editable-file.png)

Edits become part of the brand context that AI agents can use during future supported AI-assisted work.

## Related tasks

To add and manage brand context, use the following task guides:

- [Add brand context](add-brand-context.md)
- [View and edit brand context files](view-and-edit-brand-context-files.md)
- [Manage brand context folders and files](manage-brand-context-folders-and-files.md)
- [Delete brand context](delete-brand-context.md)
- [Rename brand context](rename-brand-context.md)
- [Retry a failed brand context analysis](retry-a-failed-brand-context-analysis.md)
- [Use brand context in Agentic studio](use-brand-context-in-agentic-studio.md)
