# VS Code Setup

*Last updated 2022-10-31*
This guide covers how I personally have set up and managed my VS Code setup. VS Code is my default editor of choice.

## Core Settings
We want to set up code boundaries so the code is easy to read on a variety of devices:
```
{
	"editor.rulers": [
		90,
		120
	]
}
```
We also want to support formatters when saving files:
```
{
	"editor.formatOnSave": true
}
```

### Code Collaboration and Versioning
I install the following extensions to help with this:
- **GitLens**: allows insights on every line of code around the history and versioning of the code.
- **LiveShare Extension Pack**: allows for collaboration right in VS Code. *Note: its been buggy so far, but the co-editing feature is worth the fuss right now*


### Language-Specific Plugins
- Golang:
	- Go
- Ruby:
	- Ruby
		- *see settings below* (re: [this link](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby))
	- ruby-solargraph
		- required me to run `sudo gem install solargraph` first
	- ***settings:*
		- enable linting via Rubocop
		- enable using `bundler` as the rubocop execution tool
		- apply this setting: `"ruby.rubocop.useBundler": true`
- JavaScript/TypeScript:
	- ESLint
	- Colorize
	- 

### Comments and Navigation
To help navigate the lists of notes, todo's, and fixme's, I also use a couple extensions to help with that:
- **Comment Anchors**: provides a tab that keeps track of your comments and tags
- **Better Comments**: highlights your comments so they're easier to see

### Style, Look, and Feel
- Default Theme: Visual Studio Dark
- Icons: Material Icon Theme
- Errors: Error Lens

## My settings.json
```
{
	"editor.fontFamily": "'FiraCode NF'",
	"editor.formatOnSave": true,
	"editor.rulers": [
		80,
		120
	],
	"files.associations": {
		"*.go": "go"
	},
	"gitlens.advanced.messages": {
		"suppressGitMissingWarning": true
	},
	"go.toolsManagement.autoUpdate": true,
	"ruby.format": "rubocop",
	"ruby.lintDebounceTime": 850,
	"ruby.lint": {
		"rubocop": {
			"useBundler": true
		}
	},
	"ruby.useBundler": true,
	"ruby.useLanguageServer": true,
	"workbench.colorTheme": "Visual Studio Dark",
	"workbench.iconTheme": "material-icon-theme"
}
```