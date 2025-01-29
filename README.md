# Run VSCode or shell command when files are saved

Fork from [vscode-save-and-run](https://github.com/wk-j/vscode-save-and-run)

Extends the original extension to execute VS Code extension commands or terminal-commands 

Extends the fork to debounce command running so that simultaneous
matching file saves only run the command once.

![](https://github.com/wk-j/vscode-save-and-run/raw/master/images/save-and-run.png)

## Features

- Configure multiple commands (terminal or command from VS Code extension) that run when a file is saved
- Regex pattern matching for files that trigger commands running

## Note

- Commands only get run when saving an existing file. Creating new files, and Save as... don't trigger the commands.
- For Ubuntu user, you have to install xclip

  ```
  sudo apt-get install xclip
  ```

## Configuration

Add "saveAndRunExt" configuration to user or workspace settings.

- "commands" - array of commands that will be run whenever a file is saved.
  - "match" - a regex for matching which files to run commands on
  - "cmd" - command to run. Can include parameters that will be replaced at runtime (see Placeholder Tokens section below).

## Sample Config

```json
"saveAndRunExt": {
	"commands": [
		{
			"match": ".*",
			"isShellCommand" : false,
			"cmd": "myExtension.amazingCommand"
		},
		{
			"match": "\\.txt$",
			"cmd": "echo 'Executed in the terminal: I am a .txt file ${file}.'"
		}
	]
}
```

## Commands

The following commands are exposed in the command palette

- `Save and Run Ext : Enable`
- `Save and Run Ext : Disable`

## Placeholder Tokens

Commands support placeholders similar to tasks.json.

- `${workspaceRoot}`: workspace root folder
- `${file}`: path of saved file
- `${relativeFile}`: relative path of saved file
- `${fileBasename}`: saved file's basename
- `${fileDirname}`: directory name of saved file
- `${fileExtname}`: extension (including .) of saved file
- `${fileBasenameNoExt}`: saved file's basename without extension
- `${cwd}`: current working directory

### Environment Variable Tokens

- `${env.Name}`

## License

[Apache](https://github.com/wk-j/vscode-save-and-run/blob/master/LICENSE)
