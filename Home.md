# My Obsidian Vault

This is the home document for your published vault.

Put Markdown files and folders beside this file, edit `assets/site-config.json`, and run `tools/Update Content Index.cmd`. The reader builds its navigation from those files and displays them without requiring separate HTML exports.

> [!NOTE] Ready to Customize
> Edit `assets/css/palette.css` to change the colors. Edit `assets/site-config.json` to change the site name, subtitle, home document, icon, and sidebar text.

## Basic Setup

1. Replace this page with your own introduction.
2. Add Markdown documents and PDFs beside it or inside content folders.
3. Update `assets/site-config.json`.
4. Run `tools/Update Content Index.cmd` after adding, moving, renaming, or deleting documents.
5. Run `tools/Open Local Site.cmd` to preview the result.

Here is a minimal configuration:

```json
{
  "siteTitle": "Field Notes",
  "siteSubtitle": "A published Obsidian vault",
  "homeDocument": "Home.md",
  "loadingText": "Opening document…",
  "sidebarNote": "Last updated as the archive changes.",
  "icon": "assets/images/site-icon.svg",
  "themeStorageKey": "field-notes-theme",
  "excludedFiles": ["README.md", ".gitignore", ".nojekyll", "LICENSE"],
  "excludedFolders": [".git", ".github", ".obsidian", "tools", "Drafts"],
  "attributions": [
    {
      "text": "Background adapted from ",
      "label": "Example Archive",
      "url": "https://example.com/source",
      "suffix": "."
    },
    {
      "text": "Source material licensed under ",
      "label": "Example Licence",
      "url": "https://example.com/licence",
      "suffix": ".",
      "rel": "license noopener"
    }
  ]
}
```

## Writing Documents

Start each document with a level-one heading. That heading becomes its title in the navigation.

```markdown
# Document Title

Write the opening text here.

## A Section

- Lists, **emphasis**, and [ordinary links](Another Note.md) work normally.
- Obsidian links such as [[Another Note]] and [[Folder/Another Note|custom labels]] also work.
```

Format a callout by placing `>` at the beginning of every line:

```markdown
> [!NOTE] Optional Guidance
> This is supporting information rather than a hard requirement.
```

Add one or more credits to the bottom of the sidebar with the `attributions` list:

```json
"attributions": [
  {
    "text": "Image courtesy of ",
    "label": "Example Archive",
    "url": "https://example.com/source",
    "suffix": "."
  }
]
```

For the complete setup, customization, publishing, and licensing instructions, read [[README.md]].
