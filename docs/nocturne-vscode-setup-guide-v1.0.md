# Nocturne VS Code Theme Setup Guide (v1.0)

Goal:  
Turn the Nocturne palette into a proper VS Code theme extension (`.vsix`) you can install and keep in a Git repository.

---

## 1. Repository & folder structure

You want a repo that can eventually hold VS Code, Terminal, browser themes, etc.

Minimal structure focused on VS Code first:

```text
nocturne-themes/
  vscode-nocturne/
    package.json
    README.md
    themes/
      Nocturne-color-theme.json
```

You can expand later:

```text
nocturne-themes/
  vscode-nocturne/
  windows-terminal/
  firefox/
  chrome/
  razer/
```

For now, we’ll assume:

- **Repo root**: `nocturne-themes`
- **VS Code theme folder**: `vscode-nocturne`

Place the scaffold files I gave you into `vscode-nocturne`:

```text
vscode-nocturne/
  package.json
  README.md
  themes/
    Nocturne-color-theme.json
```

Git commands (from the `nocturne-themes` directory):

```bash
git init
git add .
git commit -m "Initial Nocturne VS Code theme scaffold"
```

---

## 2. Where to run commands

Use any terminal:

- **Windows**:  
  - Command Prompt  
  - PowerShell  
  - Windows Terminal  
- **Inside VS Code**:  
  - Menu: `Terminal` → `New Terminal`  
  - It opens at the workspace folder by default.

Throughout this guide, when you see commands like:

```bash
cd vscode-nocturne
vsce package
```

you run them in **a terminal**, not inside a text editor or GUI.

---

## 3. Install Node.js (required for npm & vsce)

### Step 3.1: Install Node.js

1. Download the **LTS** version of Node.js from the official website.
2. Run the installer:
   - Accept defaults.
   - Ensure it adds Node to your `PATH` (the Windows installer does this automatically in current versions).
3. Finish installation.

### Step 3.2: Verify Node & npm

Open a **new** terminal (important, so PATH is refreshed):

```bash
node -v
npm -v
```

Expected:

- `node -v` prints something like `v20.x.x`
- `npm -v` prints something like `10.x.x`

If either command is “not recognized”, then Node is not correctly in PATH. In that case:

- Close that terminal.
- Open a new one.
- If it still fails, reinstall Node and ensure “Add to PATH” is selected.

---

## 4. Install `vsce` (VS Code Extension packaging tool)

`vsce` is what creates the `.vsix` file from your folder.

From **any terminal**:

```bash
npm install -g @vscode/vsce
```

What should happen:

- It downloads and installs `vsce` globally.
- At the end, running:

  ```bash
  vsce --version
  ```

  should print a version number.

Typical failure cases:

1. **“npm: command not found”**  
   → Node/npm are not installed or PATH is broken. Fix Node first.

2. **Permission errors (`EACCES`, `EPERM`)**  
   → On some systems, global installs can complain.  
   Workarounds:
   - On Windows: run terminal as Administrator and re-run the command.

3. **“vsce: command not found” after install**  
   → Your global npm bin folder is not in PATH.  
   Easiest solution on Windows: close the terminal, reopen it, and try again.  
   If it still fails, reinstall Node with default options.

---

## 5. Prepare the VS Code theme folder

Go to your theme folder:

```bash
cd path\to\nocturne-themes
cd vscode-nocturne
```

You should see:

```text
package.json
README.md
themes/
  Nocturne-color-theme.json
```

### Step 5.1: Edit `package.json`

Open `package.json` in your editor.

Example:

```json
{
  "name": "nocturne-theme",
  "displayName": "Nocturne",
  "description": "Minimal VS Code theme scaffold using the Nocturne palette as a base.",
  "version": "1.0.0",
  "publisher": "your-name-here",
  "engines": {
    "vscode": "^1.90.0"
  },
  "categories": ["Themes"],
  "contributes": {
    "themes": [
      {
        "label": "Nocturne",
        "uiTheme": "vs-dark",
        "path": "./themes/Nocturne-color-theme.json"
      }
    ]
  }
}
```

Change:

- `"publisher": "your-name-here"` → e.g. `"publisher": "karlene"` or any unique string.

Do **not** change `path` unless you move the file.

### Step 5.2: Edit `themes/Nocturne-color-theme.json`

This file defines all your colors. It already has a minimal structure. You map your Nocturne palette into:

- `"colors"`: UI elements (editor background, sidebar, status bar).
- `"tokenColors"`: syntax highlighting (keywords, strings, comments, etc.).

You can keep refining this later. For packaging, it just needs to be valid JSON.

Common failure:  
Missing commas, stray trailing commas, or invalid hex like `#3E2E5`.  
If you break JSON, `vsce package` will fail or VS Code will behave weirdly.

---

## 6. Package the extension as a `.vsix`

From **inside** `vscode-nocturne` (where `package.json` lives):

```bash
vsce package
```

Expected output:

- `vsce` reads `package.json`.
- If everything is valid, it prints something like:

  ```text
  ✔ Packaging...
  ✔ Created: nocturne-theme-1.0.0.vsix
  ```

Now you have a file like:

```text
vscode-nocturne/
  nocturne-theme-1.0.0.vsix
```

If it fails, common issues:

1. **Missing `publisher` field**  
   → Add `"publisher": "your-id"` to `package.json`.

2. **Invalid `engines.vscode` range**  
   → If your VS Code is older, change:

   ```json
   "engines": {
     "vscode": "^1.70.0"
   }
   ```

3. **Invalid JSON**  
   → Open both `package.json` and `Nocturne-color-theme.json` in VS Code and run “Format Document.” If the formatter chokes, you broke the JSON.

---

## 7. Install the `.vsix` in VS Code

Two ways: CLI or GUI.

### Option A: CLI

From the folder with the `.vsix`:

```bash
code --install-extension nocturne-theme-1.0.0.vsix
```

If `code` is “not recognized”:

- VS Code might not be in PATH.
- In VS Code, open Command Palette (`Ctrl+Shift+P`) and search:
  - “Shell Command: Install 'code' command in PATH” (if available).
- Then re-open your terminal and try again.

### Option B: VS Code GUI

1. Open VS Code.
2. Go to Extensions view (`Ctrl+Shift+X`).
3. Click the `...` menu → **Install from VSIX...**
4. Select `nocturne-theme-1.0.0.vsix`.
5. Activate it:
   - `Ctrl+K`, then `Ctrl+T` → Choose **Nocturne**.

---

## 8. Iterating on the theme

Once installation works:

1. Edit `themes/Nocturne-color-theme.json`.
2. Bump version in `package.json`:

   ```json
   "version": "1.0.1"
   ```

3. Rebuild:

   ```bash
   vsce package
   ```

4. Reinstall the new `.vsix` (same steps).

Keep commits small and focused so you can roll back when you hate something.

---

You now have:

- A reproducible way to generate a VS Code theme from your Nocturne palette.
- A structure that can be extended later for terminals, browsers, and everything else.
