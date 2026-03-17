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

**Build & install:**
```sh
cd vscode
npx vsce package
code --install-extension warm-clay.vsix
```

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
| Active accent (tabs, borders, cursor) | `#7ebab5` |
| Selection highlight | `#7ebab5` at ~20% opacity |
| Button background | `#7ebab5` |
| Button foreground | `#2a1c17` |
| Status bar background | `#3a2620` |
| Status bar foreground | `#e7e0de` |
| Input background | `#3a2620` |
| Scrollbar / gutter | muted `#5a3d35` |

---

## Syntax Token Color Mappings

| Token | Color | Rationale |
|---|---|---|
| Keywords (`if`, `return`, `class`, `import`) | `#b46a55` terracotta | Warm, distinct from strings |
| Strings | `#c8956c` sand/yellow | Earthy warm tone |
| Functions & method calls | `#9ecfca` light cyan | Cool contrast against warm bg |
| Types, classes, interfaces | `#7ebab5` teal | Accent color for structural elements |
| Variables (plain) | `#e7e0de` foreground | Neutral, readable |
| Comments | `#5a3d35` muted brown | Recedes visually |
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
