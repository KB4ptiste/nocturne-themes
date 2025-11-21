# Nocturne Palette (v1.1)

Revision focused on:
- Darker editor background so the code area feels deeper.
- Clear separation between editor vs explorer/chat.
- Stronger contrast between JSON property names and values.

## Core UI roles

| Role                                                | Hex      | Notes |
|-----------------------------------------------------|----------|-------|
| **Editor background (file content)**                | `#322541` | Dark violet; main code canvas. |
| **Sidebar / explorer / chat / panels background**   | `#3E2E50` | Slightly lighter violet; separates peripheral UI from editor. |
| **Deep accents / selection background**             | `#261C31` | Used for selections, active row, some headers. |
| **Primary foreground text & icons**                 | `#E5DFEC` | Soft off-white with lavender tint; high contrast on `#322541`. |
| **Muted / secondary text, comments, docstrings**    | `#977DB5` | Darker lavender; readable but clearly secondary. |

## Semantic / accent roles

| Role                                                | Hex      | Notes |
|-----------------------------------------------------|----------|-------|
| Links / info / namespaces                           | `#80FFEA` | Bright cyan, information / hints. |
| Strings / added code / success                      | `#8AFF80` | Green for strings, success, added diff. |
| Modified ranges / attributes / doc emphasis         | `#FFCA80` | Warm amber for modified / highlighted regions. |
| Keywords / special identifiers, callouts            | `#FF80BF` | Hot pink for keywords & important identifiers. |
| Constants / property names / headings               | `#B399FF` | Violet accent for constants and JSON property keys. |
| Errors / deletions / failure                        | `#FF9580` | Coral red for errors, removed diff. |

---

## VS Code `colors` snippet (Nocturne v1.1)

```jsonc
{
  "name": "Nocturne",
  "type": "dark",
  "colors": {
    // Core layout
    "editor.background": "#322541",
    "editor.foreground": "#E5DFEC",
    "sideBar.background": "#3E2E50",
    "activityBar.background": "#3E2E50",
    "panel.background": "#3E2E50",
    "titleBar.activeBackground": "#3E2E50",
    "titleBar.inactiveBackground": "#3E2E50",

    // Editor details
    "editor.selectionBackground": "#261C31",
    "editor.inactiveSelectionBackground": "#3E2E50",
    "editor.lineHighlightBackground": "#261C31",
    "editorLineNumber.foreground": "#977DB5",
    "editorCursor.foreground": "#E5DFEC",

    // Status / tabs
    "statusBar.background": "#261C31",
    "tab.activeBackground": "#322541",
    "tab.inactiveBackground": "#3E2E50"
  },
```

## VS Code `tokenColors` snippet (property names vs values)

```jsonc
  "tokenColors": [
    // JSON / object property names (left side)
    {
      "scope": [
        "support.type.property-name.json",
        "support.type.property-name.json.comments",
        "meta.object-literal.key"
      ],
      "settings": {
        "foreground": "#B399FF"
      }
    },

    // Strings (right side values)
    {
      "scope": [
        "string.quoted.double.json",
        "string.quoted.single.json",
        "string.quoted.double",
        "string.quoted.single"
      ],
      "settings": {
        "foreground": "#8AFF80"
      }
    },

    // Keywords
    {
      "scope": [
        "keyword",
        "storage.type",
        "storage.modifier"
      ],
      "settings": {
        "foreground": "#FF80BF"
      }
    },

    // Constants
    {
      "scope": [
        "constant",
        "variable.other.constant"
      ],
      "settings": {
        "foreground": "#B399FF"
      }
    },

    // Errors / invalid
    {
      "scope": [
        "invalid",
        "markup.deleted"
      ],
      "settings": {
        "foreground": "#FF9580"
      }
    }
  ]
}
```
