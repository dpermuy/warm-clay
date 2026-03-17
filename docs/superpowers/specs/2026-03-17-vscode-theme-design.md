# VS Code Theme: Warm Clay — Design Spec

**Date:** 2026-03-17
**Status:** Approved

---

## Overview

A VS Code color theme extension that ports the Warm Clay terminal palette to VS Code. Ships as a `.vsix` extension for one-command personal install. JetBrains Mono font is set separately by the user in their VS Code `settings.json`.

---

## Structure

The extension lives in a `vscode/` subdirectory of the warm-clay repo:

```
vscode/
  package.json                  # VS Code extension manifest
  warm-clay-color-theme.json    # All workbench + token color definitions
  README.md                     # Brief install instructions
```

The generated `warm-clay.vsix` artifact is gitignored. Source files are versioned.

**`package.json` skeleton:**
```json
{
  "name": "warm-clay",
  "displayName": "Warm Clay",
  "description": "A warm, earthy color theme for VS Code",
  "version": "1.0.0",
  "publisher": "local",
  "engines": { "vscode": "^1.70.0" },
  "categories": ["Themes"],
  "contributes": {
    "themes": [{
      "label": "Warm Clay",
      "uiTheme": "vs-dark",
      "path": "./warm-clay-color-theme.json"
    }]
  }
}
```

**Build & install:**
```sh
cd vscode
npx vsce package
code --install-extension warm-clay.vsix
```

**VS Code engine target:** `"engines": { "vscode": "^1.70.0" }` in `package.json`. This targets VS Code 1.70+ (August 2022), which covers all modern installs.

---

## Source Palette

From `warm_clay.yaml`:

| Role | Hex |
|---|---|
| Background | `#442f29` |
| Foreground | `#e7e0de` |
| Accent / Teal | `#7ebab5` |
| Light Cyan | `#9ecfca` |
| Lightest Cyan | `#b0dbd7` |
| Red / Terracotta | `#b46a55` |
| Bright Red | `#c87d6a` |
| Yellow / Sand | `#c8956c` |
| Bright Yellow | `#d4a87a` |
| Black (darkest) | `#2a1c17` |
| Dark Brown | `#3a2620` (derived: midpoint between black and background) |
| Bright Black / Muted | `#5a3d35` |
| Comment Brown | `#7a5a50` (derived: lightened muted brown for legibility) |
| White | `#e7e0de` |
| Bright White | `#f0ebe9` |

---

## Workbench UI Color Mappings

| Surface | Color |
|---|---|
| Editor background | `#442f29` |
| Sidebar / panel background | `#3a2620` |
| Title bar / activity bar | `#2a1c17` |
| Editor foreground | `#e7e0de` |
| Active accent (tabs, borders) | `#7ebab5` |
| Cursor (`editorCursor.foreground`) | `#7ebab5` |
| Line highlight (`editor.lineHighlightBackground`) | `#5a3d3540` (muted brown at 25% opacity) |
| Active tab background | `#442f29` |
| Inactive tab background | `#3a2620` |
| Tab group header background | `#2a1c17` |
| Selection highlight | `#7ebab533` (teal at 20% opacity, 8-digit hex) |
| Button background | `#7ebab5` |
| Button foreground | `#2a1c17` |
| Status bar background | `#3a2620` |
| Status bar foreground | `#e7e0de` |
| Status bar (debugging) | `#b46a55` background, `#f0ebe9` foreground |
| Input background | `#3a2620` |
| Scrollbar slider (`scrollbarSlider.background`, `.hoverBackground`, `.activeBackground`) | `#5a3d3580`, `#5a3d35aa`, `#5a3d35cc` |
| Editor gutter (`editorGutter.background`) | `#3a2620` |

---

## Syntax Token Color Mappings

| Token | Color | Rationale |
|---|---|---|
| Keywords (`if`, `return`, `class`, `import`) | `#b46a55` terracotta | Warm, distinct from strings |
| Strings | `#c8956c` sand/yellow | Earthy warm tone |
| Functions & method calls | `#9ecfca` light cyan | Cool contrast against warm bg |
| Types, classes, interfaces | `#7ebab5` teal | Accent color for structural elements |
| Variables (plain) | `#e7e0de` foreground | Neutral, readable |
| Comments | `#7a5a50` lightened muted brown | Recedes visually while remaining legible on `#442f29` bg |
| Numbers & boolean constants | `#d4a87a` bright yellow | Numerically distinct |
| Punctuation & operators | `#b0dbd7` lightest cyan | Subtle but legible |
| Parameters | `#c87d6a` bright red/terracotta | Slightly warmer than foreground |
| Built-ins & language constants | `#7ebab5` teal | Consistent with type role |

---

## Font

JetBrains Mono is not bundled in the extension. The user sets it once in VS Code `settings.json`:

```json
{
  "editor.fontFamily": "JetBrains Mono",
  "editor.fontSize": 13,
  "editor.fontLigatures": true
}
```

JetBrains Mono must be installed on the system separately (download from jetbrains.com/mono).

---

## Out of Scope

- Light theme variant
- Publishing to VS Code Marketplace
- Bundling font or settings profile in the extension
