# Obsidian GitHub Web Hosting

A small static reader that publishes Markdown and PDF files directly from a GitHub repository. It supports Obsidian wiki links, standard Markdown links, nested folders, callouts, light and dark themes, mobile navigation, and inline PDF viewing.

No HTML export is required when notes change. The only generated file is `assets/content-manifest.json`, which supplies the navigation tree.

> [!NOTE] GitHub Sites
> You copy this template site at https://github.com/TechInTheKitchen/Obsidian-GitHub-Web-Hosting

## Quick Start

1. Copy your Obsidian Markdown folders and publishable PDFs into the root beside `Home.md`.
2. Edit `assets/site-config.json` with your site title, subtitle, home document, and icon.
3. Edit `assets/css/palette.css` to choose colors, or select a ready-made palette from `assets/palettes/`.
4. Double-click `tools/Update Content Index.cmd` whenever files are added, removed, renamed, or retitled.
5. Double-click `tools/Open Local Site.cmd` to test locally.
6. Commit the publishable files to a GitHub repository and enable GitHub Pages from the repository root on your chosen branch.

## Files You Are Expected to Edit

- `assets/site-config.json` controls branding and content discovery.
- `assets/css/palette.css` contains the complete user-editable color palette.
- `assets/palettes/` contains optional, ready-made palettes; each includes light and dark modes.
- `assets/images/site-icon.svg` is the default header icon and favicon.
- `Home.md` is the default opening document.
- Your Markdown folders and PDFs are the actual site content.

Ordinary customization should not require changes to `index.html`, `assets/css/viewer.css`, or `assets/js/app.js`.

## Site Configuration

`assets/site-config.json` supports:

- `siteTitle`: Header title and browser-title suffix.
- `siteSubtitle`: Smaller text beneath the title.
- `homeDocument`: Repository-relative path to the opening Markdown file.
- `loadingText`: Message shown while a document loads.
- `sidebarNote`: Optional note beneath the navigation tree.
- `icon`: Repository-relative SVG or PNG path.
- `themeStorageKey`: Browser-storage name for the visitor's theme preference.
- `excludedFiles`: Filenames the index generator should ignore.
- `excludedFolders`: Folder names the index generator should ignore at any depth.
- `attributions`: Optional list of credit lines displayed at the bottom of the sidebar. Each entry may use `text`, a linked `label` and `url`, and `suffix`; use `rel` when a link needs a value such as `license noopener`.

Use forward slashes in configured paths, for example `00 Start Here/Welcome.md`.

### Example site configuration

Copy this structure into `assets/site-config.json` and replace the example values. JSON does not allow comments, so keep the property names and punctuation intact.

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

Use an empty list when no attribution is required:

```json
"attributions": []
```

## Colors and Backgrounds

All theme colors are in `assets/css/palette.css`. The dark theme is under `:root`; the light theme is under `:root[data-theme="light"]`.

The default `palette.css` is **Burlap**. Four alternate, complete palettes are available in `assets/palettes/`:

| File | Look |
| --- | --- |
| `paper-ink.css` | Near-white paper and neutral charcoal |
| `field-grey.css` | Cool slate and steel blue |
| `olive-archive.css` | Aged ledger paper and field green |
| `high-contrast.css` | Strong light/dark separation for long reading |

To use one, open `index.html` and change only the palette stylesheet line. For example:

```html
<link rel="stylesheet" href="assets/palettes/field-grey.css">
```

Keep `assets/css/viewer.css` linked after the palette. The header's light/dark button continues to work; each preset defines both modes. To customize a preset, copy its contents into `assets/css/palette.css` and restore the original stylesheet path in `index.html`. This keeps the preset file available as an untouched reference.

To add a background image, put it in `assets/images` and change this variable in both theme sections:

```css
--page-background-image: url("../images/my-background.webp");
```

Leave it as `none` for a flat background. `--page-background-wash` controls how strongly the theme color covers the image so text remains readable.

## Content and Links

The reader accepts `.md` and `.pdf` files. The index generator uses the first Markdown `# Heading` as the displayed title, falling back to the filename.

Supported links include:

```markdown
[[Another Note]]
[[Folder/Another Note|Custom label]]
[[Another Note#A Heading]]
[[#A Section|Jump to this page's section]]
[Standard link](Folder/Another%20Note.md)
```

A link beginning with `#` targets a heading in the current document. The label after `|` is optional, just as in Obsidian.

Use normal Markdown for page structure:

```markdown
# Document Title

An opening paragraph with **bold text** and *emphasis*.

## Section Heading

- First item
- Second item

| Result | Meaning |
| --- | --- |
| 1–3 | Complication |
| 4–6 | Success |

![Map description](assets/images/map.webp)
```

Obsidian callouts such as `[!NOTE]`, `[!TIP]`, `[!IMPORTANT]`, `[!WARNING]`, and `[!CAUTION]` receive themed formatting. Include the blockquote marker on every line:

```markdown
> [!NOTE] Optional title
> This text appears inside the callout.
>
> A blank quoted line creates a second paragraph.
```

Link to an indexed PDF just as you would link to another file:

```markdown
[Open the printable character sheet](Play Aids/Character Sheet.pdf)
```

## Local Testing

Browsers prohibit the reader from fetching Markdown when `index.html` is opened as a `file:` URL. Use `tools/Open Local Site.cmd` instead. The launcher checks for Node.js on `PATH`, in the standard `C:\Program Files\nodejs` and `C:\Program Files (x86)\nodejs` folders, and then in the runtime bundled with Codex. To install Node.js normally, run this from an administrator Command Prompt or PowerShell window:

```Powershell
winget install --id OpenJS.NodeJS.LTS --exact
```
After installation, close and reopen the terminal, then verify:
```Powershell
node --version
npm --version
```
The launcher chooses the first available port from 8765 through 8775 and keeps its terminal window open while the site is running.

## GitHub Pages

Publish `index.html`, `404.html`, `.nojekyll`, `assets`, and your content. The `tools` folder is ignored by default because it is only needed locally. If you want the maintenance utilities stored in GitHub, remove `tools/` from `.gitignore`.

In the GitHub repository, open **Settings → Pages**, select **Deploy from a branch**, choose the branch containing the site, and choose the repository root. The reader uses relative URLs and works under both a `github.io/repository-name` path and a custom domain.

## Updating the Reader

Editing existing Markdown content does not require regenerating the index. Run the index updater after:

- Adding or deleting a document
- Renaming or moving a document
- Changing its first `# Heading`
- Adding or removing a PDF

Commit `assets/content-manifest.json` along with those changes.

## Licence

The reusable reader, maintenance scripts, and template files are released under the [MIT License](LICENSE). You may use, modify, redistribute, and sell projects built with them as long as the MIT copyright and permission notice is retained.

The MIT License does **not** automatically apply to Markdown documents, PDFs, fonts, images, trademarks, or other material added to a site. Give published content its own licence and preserve any required third-party attribution.
