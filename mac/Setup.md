# Mac OS Setup

*Last Updated 2022-11-13 based on [this](https://sourabhbajaj.com/mac-setup/) and [this](https://www.stuartellis.name/articles/mac-setup/).*
This guide covers how I set up my Mac for personal and professional development.

## Browsers
- [Chrome](https://www.google.com/chrome/): for work and transferring bookmarks and passwords

## System
- [NerdFonts](https://www.nerdfonts.com/): setup Fira Code font w/ ligatures
	- drag-n-drop into system fonts
- [Docker Desktop](https://www.docker.com/): so you can manage docker and run it in the background on startup
	- turn off those usage statistics!

## Terminal
- [iTerm2](https://iterm2.com/): better experience than built-in terminal
	- enable nerdfonts
	- pastel color scheme
- [brew.sh](https://brew.sh/): package manager for MacOS
	- `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
- `brew install`:
	- zsh
	- antigen
		- watch out for the caveat!
	- tmux
- Set up .theme
```
function sp {
  git branch > /dev/null 2>&1 || return 1
  git config user.initials
}

POWERLEVEL9K_DIR_BACKGROUND='237'
POWERLEVEL9K_CUSTOM_GIT_PAIR="echo \$(sp)"
POWERLEVEL9K_CUSTOM_GIT_PAIR_BACKGROUND="clear"
POWERLEVEL9K_CUSTOM_GIT_PAIR_FOREGROUND="blue"
POWERLEVEL9K_CUSTOM_GIT_PAIR_ICON="\uf7af"
POWERLEVEL9K_DIR_DEFAULT_BACKGROUND="clear"
POWERLEVEL9K_DIR_DEFAULT_FOREGROUND="012"
POWERLEVEL9K_DIR_FOREGROUND='010'
POWERLEVEL9K_DIR_HOME_BACKGROUND="clear"
POWERLEVEL9K_DIR_HOME_FOREGROUND="012"
POWERLEVEL9K_DIR_HOME_SUBFOLDER_BACKGROUND="clear"
POWERLEVEL9K_DIR_HOME_SUBFOLDER_FOREGROUND="012"
POWERLEVEL9K_DIR_PATH_SEPARATOR="%F{cyan}/%F{blue}"

POWERLEVEL9K_DIR_ETC_BACKGROUND="clear"
POWERLEVEL9K_ETC_ICON='%F{blue}\uf423'
POWERLEVEL9K_DIR_WRITABLE_FORBIDDEN_FOREGROUND="red"
POWERLEVEL9K_DIR_WRITABLE_FORBIDDEN_BACKGROUND="clear"

POWERLEVEL9K_GO_ICON="\uf7b7"
POWERLEVEL9K_GO_VERSION_BACKGROUND='clear'
POWERLEVEL9K_GO_VERSION_FOREGROUND='081'

POWERLEVEL9K_JAVA_ICON="\ue738"
POWERLEVEL9K_JAVA_VERSION_BACKGROUND='clear'
POWERLEVEL9K_JAVA_VERSION_FOREGROUND='001'
POWERLEVEL9K_JAVA_VERSION_PROJECT_ONLY=true
POWERLEVEL9K_JAVA_VERSION_FULL=false

POWERLEVEL9K_HOME_ICON="\ufb26"

POWERLEVEL9K_INSTALLATION_PATH=$ANTIGEN_BUNDLES/romkatv/powerlevel10k

POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(root_indicator dir dir_writable_joined
custom_git_pair vcs_joined)
POWERLEVEL9K_LEFT_SEGMENT_SEPARATOR=''
POWERLEVEL9K_LEFT_SUBSEGMENT_SEPARATOR='%F{blue}\uf460%F{blue}'

POWERLEVEL9K_LINUX_MANJARO_ICON="\uf312 "
POWERLEVEL9K_LINUX_UBUNTU_ICON="\uf31b "

POWERLEVEL9K_MODE='nerdfont-complete'

POWERLEVEL9K_MULTILINE_FIRST_PROMPT_PREFIX=""
POWERLEVEL9K_MULTILINE_LAST_PROMPT_PREFIX=" \uf101 "

POWERLEVEL9K_NODE_VERSION_PROJECT_ONLY=true
POWERLEVEL9K_NODE_VERSION_BACKGROUND='clear'
POWERLEVEL9K_NODE_VERSION_FOREGROUND='green'

POWERLEVEL9K_NVM_BACKGROUND='clear'
POWERLEVEL9K_NVM_FOREGROUND='green'

POWERLEVEL9K_RBENV_BACKGROUND='clear'
POWERLEVEL9K_RBENV_FOREGROUND='red'

POWERLEVEL9K_AWS_BACKGROUND='clear'
POWERLEVEL9K_AWS_FOREGROUND='cyan'

POWERLEVEL9K_PYENV_BACKGROUND='clear'
POWERLEVEL9K_PYENV_FOREGROUND='yellow'

POWERLEVEL9K_OS_ICON_BACKGROUND='clear'
POWERLEVEL9K_OS_ICON_FOREGROUND='cyan'

POWERLEVEL9K_KUBECONTEXT_SHOW_ON_COMMAND='kubectl|helm|kubens|kubectx'
POWERLEVEL9K_KUBECONTEXT_BACKGROUND='clear'
POWERLEVEL9K_KUBECONTEXT_FOREGROUND='cyan'

POWERLEVEL9K_PROMPT_ADD_NEWLINE=true
POWERLEVEL9K_PROMPT_ON_NEWLINE=true

POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status pyenv go_version node_version
rbenv aws kubecontext os_icon)
POWERLEVEL9K_RIGHT_SEGMENT_SEPARATOR=''
POWERLEVEL9K_RIGHT_SUBSEGMENT_SEPARATOR='%F{blue}\uf104%F{blue}'

POWERLEVEL9K_SHORTEN_DELIMITER='%F{blue}…%F{blue}'
POWERLEVEL9K_SHORTEN_DIR_LENGTH=3
POWERLEVEL9K_SHORTEN_STRATEGY="none"

POWERLEVEL9K_STATUS_ERROR_BACKGROUND="clear"
POWERLEVEL9K_STATUS_ERROR_FOREGROUND="001"
POWERLEVEL9K_STATUS_OK_BACKGROUND="clear"
POWERLEVEL9K_STATUS_BACKGROUND="clear"
POWERLEVEL9K_CARRIAGE_RETURN_ICON="\uf071"

POWERLEVEL9K_TIME_FORMAT="%D{%H:%M \uE868  %d.%m}"

POWERLEVEL9K_VCS_CLEAN_BACKGROUND='clear'
POWERLEVEL9K_VCS_CLEAN_FOREGROUND='green'
POWERLEVEL9K_VCS_MODIFIED_BACKGROUND='clear'
POWERLEVEL9K_VCS_MODIFIED_FOREGROUND='yellow'
POWERLEVEL9K_VCS_UNTRACKED_BACKGROUND='clear'
POWERLEVEL9K_VCS_UNTRACKED_FOREGROUND='green'
```
- Set up .zshrc
```
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]];
then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

source /opt/homebrew/share/antigen/antigen.zsh
source ~/.theme

antigen use oh-my-zsh
antigen bundle StackExchange/blackbox
antigen bundle brew
antigen bundle command-not-found
antigen bundle common-aliases
antigen bundle docker
antigen bundle docker-compose
antigen bundle git
antigen bundle tmux
antigen theme romkatv/powerlevel10k
antigen apply

# I use insiders, rather than stable
alias code=code-insiders

# I use my dotfiles repo to manage these things,
# e.g.
#
# `config pull origin master`
# and
# `config add -A`
#
# like you would with GIT
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'

# load keychain into ssh
ssh-add --apple-load-keychain 2>/dev/null;

eval "$(rbenv init - zsh)"
eval "$(pyenv init - zsh)"
eval "$(goenv init - zsh)"
eval "$(jenv init - zsh)"

export PATH="$HOME/.jenv/bin:$PATH"

# let's have shorthand to print terminal colors:
alias colors='for i in {0..255}; do print -Pn "%K{$i}  %k%F{$i}${(l:3::0:)i}%f " ${${(M)$((i%6)):#3}:+"\n"}; done'
```

## Development Environment
- `brew install`
	- languages:
		- pyenv
		- pyenv-virtualenv
		- nodeenv
		- goenv
		- rbenv
		- jenv
			- manage it by reading their readme
			- to get JDK I installed Zulu's openjdk v8
	- utilities:
		- awscli
		- postgresql
		- git
		- sourcetree
		- tree
		- fzf
		- ack
		- docker
		- minikube
- `brew install` recommended, but only in trial right now:
	- dash - not tested, but suggested
	- devutils - not tested, but suggested
- [Code Insiders](https://code.visualstudio.com/insiders/): I prefer getting features earlier and trying them out
	- otherwise `brew install code`
	- that's why I alias: `alias code=code-insiders`
	- [[VS Code Setup]]