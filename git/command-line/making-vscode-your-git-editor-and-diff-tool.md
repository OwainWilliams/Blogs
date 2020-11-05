# Making VSCode your Git editor and diff tool

To set Visual Studio Code as your default editor enter this command into command line:

`git config --global -e`

```text
[user]
	email = your@email.com
	name = YourName
	signingKey = ""
[core]
	longpaths = true
	autocrlf = true
	safecrlf = warn
	editor = code --wait
[gpg]
	program = gpg
[commit]
	gpgSign = false
[tag]
	forceSignAnnotated = false

```

 By the way switch `--wait` holds shell until Visual Studio Code is closed. Make sure \[core\] has the editor as code.

### Making VS Code your Diff Tool

To set Visual Studio Code as your `difftool`, you need to go into global git config file. Which you can access through previous mentioned command `git config --global -e`, then you need to add those entries \(or replace existing ones\).

```text
[diff]
    tool = vscode
[difftool "vscode"]
    cmd = code --wait --diff $LOCAL $REMOTE
```





[https://blog.soltysiak.it/en/2017/01/set-visual-studio-code-as-default-git-editor-and-diff-tool/](https://blog.soltysiak.it/en/2017/01/set-visual-studio-code-as-default-git-editor-and-diff-tool/)

