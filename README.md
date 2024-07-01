# vscode-snippets

Example script installation steps:

1. Install multi-line command
2. Go to default settings and try to open it in JSON. If you can't do so in a non-read only mode, then navigate to multi-line command section of settings and click the "open settings JSON (paraphrasing)" button
3. Include the following block: Ctrl+Shift+P -> ? ("multiline?")

```json
"multiCommand.commands": [
    {
      "command": "multiCommand.selectLineAndLog",
      "sequence": [
        "cursorLineEnd",
        "editor.action.trimTrailingWhitespace",
        "cursorHomeSelect",
        "editor.action.insertSnippet",
        {
          "name": "Log Variable"
        }
      ]
    }
  ]
```

4. Go to keybindings.json and include the following block:

Cursor: Ctrl+Shift+P -> "keybindings" (cursor?) OR "Open Keyboard Shortcuts" (VSCode classic)

```json
[
    {
        "key": "ctrl+alt+p",
        "command": "extension.multiCommand.execute",
        "args": { "command": "multiCommand.selectLineAndLog" },
        "when": "editorTextFocus"
    }
]
```

5. Go to `Snippets: Configure user snippets`: (ctrl+shift+p) > Configure user snippets and include the following for javascript, javascriptreact, typescript, and typescriptreact:

```json
{
    "Log Variable": {
        "prefix": "logvar",
        "body": [
            "console.log(`$TM_SELECTED_TEXT=${$TM_SELECTED_TEXT}`);"
        ],
        "description": "Log selected variable"
    }
}
```

And the following for python:

```json
{
    "Log Variable": {
        "prefix": "logvar",
        "body": [
            "print(f'{$TM_SELECTED_TEXT=}');"
        ],
        "description": "Log selected variable"
    }
}
```