# Windows Developer Setup

A fresh Windows does take some time to set up properly for modern development.
You need a good termal, git, bash tools, package manager, etc. This document 
should provide guidance on setting up a nice Windows developer environment.

## Table of Contents

- [A Word about Ubuntu Linux](#a-word-about-ubuntu-linux)
- [General Development](#general-development)
    - [Package Management](#package-management-chocolatey)
    - [Terminal](#terminal-cmder)
    - [Node and npm](#node-and-npm)
    - [Version Control](#version-control-git)
    - [Code Editors](#code-editors)
        - [Visual Studio Code](#visual-studio-code)
        - [Atom](#atom)
        - [Sublime Text](#sublime-text)
        - [Visual Studio 2017](visual-studio-2017)
    - [Ruby](#ruby)
    - [Basic Tools](#basic-tools)
        - [Chrome](#chrome)
- [DevOps](#devops)
    - [Docker](#docker)
    - [VirtualBox](#virtualbox)
    - [SSH](#ssh)
    - [Azure CLI](#azure-cli)
    - [AWS CLI](#aws-cli)

## A Word about Ubuntu Linux

While [Bash on Windows](https://docs.microsoft.com/en-us/windows/wsl/about) is 
not flawless, it is an amazing tool that can make development more fun and 
easier than ever! Keep in mind much development can be easy enough on Windows 
itself. Use the tool as much as you care to. Here's a how-to:

- Ensure that you're running Windows 10 (build 14311 or above)
- Enable Developer Mode (Settings - Update & security > For developers)
- Search for “Windows Features” and choose “Turn Windows features on or off” 
  and enable Windows Subsystem for Linux.
- To get Bash installed, open Command Prompt and type “bash”

## General Development

Here are my general setup guidelines

### Package Management - Chocolatey

Chocolatey is a powerful package manager for Windows, working like homebrew. 
Let's set this one up first by running the following in CMD.exe:

```bash
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

Once done, you can install packages by running cinst (short for choco install).

###### Bonus: Use Windows 10 & OneGet

Windows 10 comes with OneGet, a universal package manager that can use 
Chocolatey to find and install packages. To install, run:

```
Get-PackageProvider -name chocolatey
```

Once done, you can look for all Chrome packages by typing `Find-Package -Name 
Chrome` or install it by typing `Install-Package -Name GoogleChrome`.

### Terminal - CMDer

The PowerShell in Windows 10 made a lot of improvements, but it's even better 
when paired with [CMDer](https://github.com/cmderdev/cmder) or 
[Hyper](https://hyper.is/), both powerful tools to do more command-line things.

Install either with the following:

```
cinst cmder -pre
cinst hyper
```

Even if you don't want to use either, you should enable your PowerShell to 
execute scripts. Run the following in PowerShell:

```
Set-ExecutionPolicy Unrestricted -Scope CurrentUser
```

_TODO(Chris): Add more about profiles (PowerShell and CMDer, WinBash, etc.)!_

### Node and npm

A bunch of tools are powered by Node and installed via npm. This applies to you 
even if you don't care about Node development. Do the following:

```
cinst nodejs.install
```

In the future, you might want to update npm -- `npm i -g npm` doesn't always 
work, so use `npm-windows-upgrade` instead:

```
npm install -g npm-windows-upgrade
npm-windows-upgrade
```

### Version Control - Git

Obviously :)

```
cinst git.install
cinst poshgit

# Restart PowerShell / CMDer before moving on - or run
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")

cinst Git-Credential-Manager-for-Windows
cinst github
```

### Code Editors

I won't join the war debating which editor is the best, but if you're looking 
for an editor and not a full IDE, chances are that you'll end up using one of 
these three.

#### Visual Studio Code

```
cinst visualstudiocode
```

#### Atom

```
cinst Atom
```

#### Sublime Text

```
cinst SublimeText3
cinst sublimetext3-contextmenu
cinst SublimeText3.PackageControl
cinst SublimeText3.PowershellAlias
```

#### Visual Studio 2017

For those that want to do Windows development, you should also install Visual 
Studio 2017 (Community if you're not paying for it):

```
cinst visualstudio2017community
```

### Ruby

Even if you don't care about Ruby at all, bear in mind that it's preinstalled 
on OS X (and easy to install on Unix), so many dev tools might be trying to 
leverage it. For example, GitHub pages are compiled using Jekyll - if you want 
to get in on that, install Ruby.

```
cinst ruby
cinst ruby.devkit
```

### Basic Tools

Recognize these?

```
cinst vlc
cinst GoogleChrome
cinst 7zip.install
cinst sysinternals
```

#### Chrome

In chrome, I like to set up environments depending on my work -- am I using the
web personally, for my professional development, or for my job. Below are some
simple instructions to get profiles set up:

- Open Chrome
- Top right, click "Profile"
- Click "Manage people"
- Choose a name and a photo
    - Optionally (I do this), check "Create a desktop shortcut for this user" 
      so I can pin it to the taskbar
- Click "Save". A new window will open for this profile

## DevOps

If you're working with/on DevOps, the following is likely useful to you.

### Docker

```
const docker-for-windows
```

### VirtualBox

```
cinst virtualbox
cinst virtualbox.extensionpack
cinst vagrant
```

### SSH

If you've installed any of the terminals above, then you simply run `ssh` from 
your terminal.

### Azure CLI

```
cinst azure-cli
```

### AWS Cli

```
cinst awscli
cinst awstools.powershell
```

_TODO(Chris): Add sections for language-specific setups I use! Quick notes: nvm, go-env, virtualenv, etc._