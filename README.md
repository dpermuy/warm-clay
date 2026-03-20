# Warm Clay

A warm, earthy color theme — available for Warp, macOS Terminal, Air, and VS Code.

![Warm Clay preview](screenshot.png)

## Supported targets

| Terminal | File |
|---|---|
| [Warp](https://www.warp.dev) (macOS) | `warm_clay.yaml` |
| [Terminal](https://support.apple.com/guide/terminal/welcome/mac) (macOS) | `Warm Clay.terminal` |
| [VS Code](https://code.visualstudio.com) | `vscode/` |
| [Air](https://air.dev) | `Warm-Clay-Colorized.json` |

---

## Installation

### Warp

1. Copy `warm_clay.yaml` to `~/.warp/themes/`:
   ```
   cp warm_clay.yaml ~/.warp/themes/
   ```
2. In Warp, open **Settings → Appearance → Themes** and select **Warm Clay**.

### macOS Terminal

1. Double-click `Warm Clay.terminal` — this imports the profile into Terminal automatically.
2. Open **Terminal → Settings → Profiles**, select **Warm Clay**, and click **Default** to make it your default profile.

### Air

1. Copy `Warm-Clay-Colorized.json` to `~/Library/Application Support/JetBrains/Air/themes/`:
   ```
   cp Warm-Clay-Colorized.json ~/Library/Application\ Support/JetBrains/Air/themes/
   ```
2. Restart Air if it is already open, then open the theme picker and select **Warm Clay**.

### VS Code

1. Build the extension:
   ```
   cd vscode
   npx vsce package
   ```
2. In VS Code, open **Extensions** (`Cmd+Shift+X`), click `···` → **Install from VSIX...**, and select `warm-clay-1.0.0.vsix`.
3. Open Command Palette (`Cmd+Shift+P`), run **Preferences: Color Theme**, and select **Warm Clay**.

---

## Color palette

| Role | Hex |
|---|---|
| Background | `#442f29` |
| Foreground | `#e7e0de` |
| Accent / Cursor | `#7ebab5` |
| Black | `#2a1c17` |
| Red | `#b46a55` |
| Green | `#7ebab5` |
| Yellow | `#c8956c` |
| Blue | `#7ebab5` |
| Magenta | `#b46a55` |
| Cyan | `#9ecfca` |
| White | `#e7e0de` |
