# Warm Clay VS Code Theme Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a VS Code color theme extension that ports the Warm Clay palette to VS Code's workbench UI and syntax highlighting, installable via a single `code --install-extension` command.

**Architecture:** A minimal VS Code extension in `vscode/` containing `package.json` (manifest) and `warm-clay-color-theme.json` (all color definitions). No build toolchain — `npx vsce package` zips it into a `.vsix`. The generated `.vsix` is gitignored; source files are versioned.

**Tech Stack:** VS Code Extension API (theme-only, no code), `@vscode/vsce` (packaging)

---

## File Map

| File | Action | Responsibility |
|---|---|---|
| `vscode/package.json` | Create | Extension manifest — name, engine version, theme contribution |
| `vscode/warm-clay-color-theme.json` | Create | All workbench UI and syntax token colors |
| `vscode/README.md` | Create | Install and font setup instructions |
| `vscode/.vscodeignore` | Create | Exclude docs/specs from the .vsix artifact |
| `.gitignore` | Modify | Add `*.vsix` |

---

## Source Palette Reference

All hex values come from `warm_clay.yaml` plus two derived colors:

```
Background:       #442f29
Foreground:       #e7e0de
Accent/Teal:      #7ebab5
Light Cyan:       #9ecfca
Lightest Cyan:    #b0dbd7
Red/Terracotta:   #b46a55
Bright Red:       #c87d6a
Yellow/Sand:      #c8956c
Bright Yellow:    #d4a87a
Black (darkest):  #2a1c17
Dark Brown:       #3a2620   (derived)
Muted Brown:      #5a3d35
Comment Brown:    #7a5a50   (derived)
Bright White:     #f0ebe9
```

---

## Task 1: Extension Scaffold

**Files:**
- Create: `vscode/package.json`
- Create: `vscode/.vscodeignore`
- Modify: `.gitignore`

- [ ] **Step 1: Add `*.vsix` to `.gitignore`**

Open `.gitignore` (create if absent) and append:
```
*.vsix
```

- [ ] **Step 2: Create `vscode/package.json`**

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
    "themes": [
      {
        "label": "Warm Clay",
        "uiTheme": "vs-dark",
        "path": "./warm-clay-color-theme.json"
      }
    ]
  }
}
```

- [ ] **Step 3: Create `vscode/.vscodeignore`**

```
docs/**
*.md
.gitignore
```

- [ ] **Step 4: Validate the JSON is well-formed**

Run:
```sh
node -e "require('./vscode/package.json'); console.log('OK')"
```
Expected: `OK`

- [ ] **Step 5: Commit**

```bash
git add vscode/package.json vscode/.vscodeignore .gitignore
git commit -m "feat: add VS Code extension scaffold"
```

---

## Task 2: Workbench UI Colors

**Files:**
- Create: `vscode/warm-clay-color-theme.json` (skeleton + UI colors section)

- [ ] **Step 1: Create theme JSON with workbench colors**

Create `vscode/warm-clay-color-theme.json`:

```json
{
  "name": "Warm Clay",
  "type": "dark",
  "colors": {
    "editor.background": "#442f29",
    "editor.foreground": "#e7e0de",
    "editorCursor.foreground": "#7ebab5",
    "editor.lineHighlightBackground": "#5a3d3540",
    "editor.selectionBackground": "#7ebab533",
    "editor.selectionHighlightBackground": "#7ebab520",
    "editor.findMatchBackground": "#c8956c50",
    "editor.findMatchHighlightBackground": "#c8956c30",

    "editorLineNumber.foreground": "#5a3d35",
    "editorLineNumber.activeForeground": "#b0dbd7",
    "editorGutter.background": "#3a2620",

    "editorIndentGuide.background1": "#5a3d3560",
    "editorIndentGuide.activeBackground1": "#7ebab580",

    "scrollbarSlider.background": "#5a3d3580",
    "scrollbarSlider.hoverBackground": "#5a3d35aa",
    "scrollbarSlider.activeBackground": "#5a3d35cc",

    "activityBar.background": "#2a1c17",
    "activityBar.foreground": "#e7e0de",
    "activityBar.inactiveForeground": "#5a3d35",
    "activityBarBadge.background": "#7ebab5",
    "activityBarBadge.foreground": "#2a1c17",

    "sideBar.background": "#3a2620",
    "sideBar.foreground": "#e7e0de",
    "sideBarTitle.foreground": "#b0dbd7",
    "sideBarSectionHeader.background": "#2a1c17",
    "sideBarSectionHeader.foreground": "#e7e0de",

    "editorGroupHeader.tabsBackground": "#2a1c17",
    "tab.activeBackground": "#442f29",
    "tab.activeForeground": "#e7e0de",
    "tab.inactiveBackground": "#3a2620",
    "tab.inactiveForeground": "#5a3d35",
    "tab.activeBorderTop": "#7ebab5",
    "tab.border": "#2a1c17",

    "titleBar.activeBackground": "#2a1c17",
    "titleBar.activeForeground": "#e7e0de",
    "titleBar.inactiveBackground": "#2a1c17",
    "titleBar.inactiveForeground": "#5a3d35",

    "statusBar.background": "#3a2620",
    "statusBar.foreground": "#e7e0de",
    "statusBar.border": "#2a1c17",
    "statusBar.debuggingBackground": "#b46a55",
    "statusBar.debuggingForeground": "#f0ebe9",
    "statusBar.noFolderBackground": "#2a1c17",

    "panel.background": "#3a2620",
    "panel.border": "#2a1c17",
    "panelTitle.activeForeground": "#7ebab5",
    "panelTitle.activeBorder": "#7ebab5",
    "panelTitle.inactiveForeground": "#5a3d35",

    "terminal.background": "#442f29",
    "terminal.foreground": "#e7e0de",
    "terminal.ansiBlack": "#2a1c17",
    "terminal.ansiRed": "#b46a55",
    "terminal.ansiGreen": "#7ebab5",
    "terminal.ansiYellow": "#c8956c",
    "terminal.ansiBlue": "#7ebab5",
    "terminal.ansiMagenta": "#b46a55",
    "terminal.ansiCyan": "#9ecfca",
    "terminal.ansiWhite": "#e7e0de",
    "terminal.ansiBrightBlack": "#5a3d35",
    "terminal.ansiBrightRed": "#c87d6a",
    "terminal.ansiBrightGreen": "#9ecfca",
    "terminal.ansiBrightYellow": "#d4a87a",
    "terminal.ansiBrightBlue": "#9ecfca",
    "terminal.ansiBrightMagenta": "#c87d6a",
    "terminal.ansiBrightCyan": "#b0dbd7",
    "terminal.ansiBrightWhite": "#f0ebe9",

    "input.background": "#3a2620",
    "input.foreground": "#e7e0de",
    "input.border": "#5a3d35",
    "input.placeholderForeground": "#5a3d35",
    "inputOption.activeBorder": "#7ebab5",

    "button.background": "#7ebab5",
    "button.foreground": "#2a1c17",
    "button.hoverBackground": "#9ecfca",

    "dropdown.background": "#3a2620",
    "dropdown.foreground": "#e7e0de",
    "dropdown.border": "#5a3d35",

    "list.activeSelectionBackground": "#5a3d35",
    "list.activeSelectionForeground": "#e7e0de",
    "list.hoverBackground": "#5a3d3550",
    "list.focusBackground": "#5a3d3570",
    "list.highlightForeground": "#7ebab5",

    "focusBorder": "#7ebab5",
    "selection.background": "#7ebab533",

    "badge.background": "#7ebab5",
    "badge.foreground": "#2a1c17",

    "progressBar.background": "#7ebab5",

    "notifications.background": "#3a2620",
    "notifications.foreground": "#e7e0de",
    "notificationLink.foreground": "#7ebab5",

    "editorWidget.background": "#3a2620",
    "editorWidget.border": "#5a3d35",
    "editorSuggestWidget.background": "#3a2620",
    "editorSuggestWidget.border": "#5a3d35",
    "editorSuggestWidget.selectedBackground": "#5a3d35",

    "peekViewEditor.background": "#3a2620",
    "peekViewResult.background": "#2a1c17",
    "peekView.border": "#7ebab5",
    "peekViewEditor.matchHighlightBackground": "#c8956c40",

    "diffEditor.insertedTextBackground": "#7ebab520",
    "diffEditor.removedTextBackground": "#b46a5520"
  },
  "tokenColors": []
}
```

- [ ] **Step 2: Validate JSON is well-formed**

Run:
```sh
node -e "require('./vscode/warm-clay-color-theme.json'); console.log('OK')"
```
Expected: `OK`

- [ ] **Step 3: Commit**

```bash
git add vscode/warm-clay-color-theme.json
git commit -m "feat: add workbench UI colors to theme"
```

---

## Task 3: Syntax Token Colors

**Files:**
- Modify: `vscode/warm-clay-color-theme.json` — fill in `tokenColors` array

- [ ] **Step 1: Replace the empty `tokenColors` array with full token definitions**

Replace `"tokenColors": []` with:

```json
"tokenColors": [
  {
    "name": "Comments",
    "scope": ["comment", "punctuation.definition.comment"],
    "settings": { "foreground": "#7a5a50", "fontStyle": "italic" }
  },
  {
    "name": "Keywords",
    "scope": [
      "keyword",
      "keyword.control",
      "keyword.operator.new",
      "storage.type",
      "storage.modifier"
    ],
    "settings": { "foreground": "#b46a55" }
  },
  {
    "name": "Strings",
    "scope": [
      "string",
      "string.quoted",
      "string.template"
    ],
    "settings": { "foreground": "#c8956c" }
  },
  {
    "name": "String escape sequences",
    "scope": "constant.character.escape",
    "settings": { "foreground": "#d4a87a" }
  },
  {
    "name": "Functions and methods",
    "scope": [
      "entity.name.function",
      "meta.function-call.generic",
      "support.function"
    ],
    "settings": { "foreground": "#9ecfca" }
  },
  {
    "name": "Types, classes, interfaces",
    "scope": [
      "entity.name.type",
      "entity.name.class",
      "entity.other.inherited-class",
      "support.class",
      "entity.name.namespace",
      "entity.name.type.interface"
    ],
    "settings": { "foreground": "#7ebab5" }
  },
  {
    "name": "Variables",
    "scope": [
      "variable",
      "variable.other.readwrite",
      "meta.definition.variable"
    ],
    "settings": { "foreground": "#e7e0de" }
  },
  {
    "name": "Parameters",
    "scope": ["variable.parameter"],
    "settings": { "foreground": "#c87d6a" }
  },
  {
    "name": "Constants and built-ins",
    "scope": [
      "constant.language",
      "support.constant",
      "variable.language.this",
      "variable.language.self"
    ],
    "settings": { "foreground": "#7ebab5" }
  },
  {
    "name": "Numbers",
    "scope": ["constant.numeric"],
    "settings": { "foreground": "#d4a87a" }
  },
  {
    "name": "Booleans and null",
    "scope": [
      "constant.language.boolean",
      "constant.language.null",
      "constant.language.undefined"
    ],
    "settings": { "foreground": "#d4a87a" }
  },
  {
    "name": "Punctuation and operators",
    "scope": [
      "punctuation",
      "keyword.operator"
    ],
    "settings": { "foreground": "#b0dbd7" }
  },
  {
    "name": "Tags (HTML/JSX)",
    "scope": [
      "entity.name.tag",
      "meta.tag"
    ],
    "settings": { "foreground": "#b46a55" }
  },
  {
    "name": "Tag attributes",
    "scope": ["entity.other.attribute-name"],
    "settings": { "foreground": "#c8956c" }
  },
  {
    "name": "Object keys / properties",
    "scope": [
      "meta.object-literal.key",
      "support.type.property-name"
    ],
    "settings": { "foreground": "#9ecfca" }
  },
  {
    "name": "CSS properties",
    "scope": ["support.type.property-name.css"],
    "settings": { "foreground": "#9ecfca" }
  },
  {
    "name": "CSS values",
    "scope": ["support.constant.property-value.css"],
    "settings": { "foreground": "#c8956c" }
  },
  {
    "name": "Decorators / annotations",
    "scope": [
      "meta.decorator",
      "entity.name.function.decorator"
    ],
    "settings": { "foreground": "#d4a87a", "fontStyle": "italic" }
  },
  {
    "name": "Import / module paths",
    "scope": ["string.quoted.double.import", "string.quoted.single.import"],
    "settings": { "foreground": "#c8956c" }
  },
  {
    "name": "Invalid / deprecated",
    "scope": ["invalid", "invalid.deprecated"],
    "settings": { "foreground": "#c87d6a", "fontStyle": "underline" }
  }
]
```

- [ ] **Step 2: Validate JSON is well-formed**

Run:
```sh
node -e "require('./vscode/warm-clay-color-theme.json'); console.log('OK')"
```
Expected: `OK`

- [ ] **Step 3: Commit**

```bash
git add vscode/warm-clay-color-theme.json
git commit -m "feat: add syntax token colors to theme"
```

---

## Task 4: README and Final Build

**Files:**
- Create: `vscode/README.md`

- [ ] **Step 1: Create `vscode/README.md`**

```markdown
# Warm Clay — VS Code Theme

A warm, earthy color theme for VS Code.

## Install

1. Build the extension:
   ```sh
   cd vscode
   npx vsce package
   ```
2. Install:
   ```sh
   code --install-extension warm-clay.vsix
   ```
3. Open the Command Palette (`Cmd+Shift+P`), run **Preferences: Color Theme**, and select **Warm Clay**.

## Font

This theme pairs well with [JetBrains Mono](https://www.jetbrains.com/mono/). After installing the font, add to your VS Code `settings.json`:

```json
{
  "editor.fontFamily": "JetBrains Mono",
  "editor.fontSize": 13,
  "editor.fontLigatures": true
}
```
```

- [ ] **Step 2: Install `vsce` and build the extension**

Run:
```sh
cd vscode && npx vsce package --allow-missing-repository
```
Expected: `Packaged: warm-clay-1.0.0.vsix` (file created in `vscode/`)

If `vsce` prompts about missing license, it's fine — this is personal use.

- [ ] **Step 3: Verify the `.vsix` was created**

Run:
```sh
ls vscode/*.vsix
```
Expected: `vscode/warm-clay-1.0.0.vsix`

- [ ] **Step 4: Install the extension**

Run:
```sh
code --install-extension vscode/warm-clay-1.0.0.vsix
```
Expected: `Extension 'warm-clay' was successfully installed.`

- [ ] **Step 5: Activate the theme in VS Code**

Open VS Code, open Command Palette (`Cmd+Shift+P`), run **Preferences: Color Theme**, select **Warm Clay**.

- [ ] **Step 6: Commit source files (not the .vsix)**

```bash
git add vscode/README.md
git commit -m "feat: add VS Code theme README and complete extension"
```

---

## Final Check

- [ ] Theme appears in VS Code theme picker as "Warm Clay"
- [ ] Editor background is warm brown (`#442f29`)
- [ ] Syntax colors are visible and match palette (keywords terracotta, strings sand, functions cyan)
- [ ] Comments are legible but receded
- [ ] Terminal panel matches the Warm Clay ANSI palette
- [ ] `warm-clay.vsix` is listed in `.gitignore` and not tracked by git
