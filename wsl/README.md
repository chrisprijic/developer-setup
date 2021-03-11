# Windows WSL Developer Setup

A fresh Windows does take some time to set up properly for modern development.
You need a good termal, git, bash tools, package manager, etc. This document 
should provide guidance on setting up a nice Windows developer environment,
specific to WSL

## Table of Contents

- [Enable WSL and Install Ubuntu](#enable-wsl-and-install-ubuntu)
- [WSL2](#wsl2)
- [General Development](#general-development)
    - [Package Management - Windows](#package-management-chocolatey)
    - [Package Management - Ubuntu](#package-management-ubuntu)
    - [Terminal](#terminal-cmder)
    - [Node and npm](#node-and-npm)
    - [Version Control](#version-control-git)
    - [Code Editors](#code-editors)
        - [Visual Studio Code](#visual-studio-code)
    - [Ruby](#ruby)
    - [Basic Tools](#basic-tools)
- [DevOps](#devops)
    - [Docker](#docker)
    - [AWS CLI](#aws-cli)

## Enable WSL and Install Ubuntu

- Ensure that you're running Windows 10 (build 14311 or above)
- Enable Developer Mode (Settings - Update & security > For developers)
- Search for “Windows Features” and choose “Turn Windows features on or off” 
  and enable Windows Subsystem for Linux
- Reboot
- Go to the Windows Store and install Ubuntu. On launch, you'll create your user and set your password

## WSL2

Complete the following after installing WSL and Ubuntu:

Documentation:

- [Announcement](https://ubuntu.com/blog/ubuntu-on-wsl-2-is-generally-available)
- [Installation](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

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

### Package Management - Ubuntu

Ubuntu comes with `apt-get`. 'nuff said.

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

I then set up Ubuntu with CMDer:

1. Open CMDer, and go to settings
2. Go to "Startup > Tasks", and create a new one, called bash::ubuntu
3. Use the command `%windir%\system32\bash.exe ~ -cur_console:p`
4. Save and move to "Startup"
5. Choose "Specified named task" and choose "{bash:ubuntu}"
6. Close all and open again. This should open a terminal to your Ubuntu WSL!

### Node and NPM

Check out the [NVM repo](https://github.com/nvm-sh/nvm#installation-and-update) 
to install NVM for node version management. The command looks like:

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/<VERSION>/install.sh | bash
```

After re-opening your terminal, you can type the following to install your desired 
version:

```
nvm i <VERSION>
```

### Version Control -- git

By default, Ubuntu WSL comes with git!

### Code Editors

I won't join the war debating which editor is the best, but if you're looking 
for an editor and not a full IDE, chances are that you'll end up using one of 
these three.

#### Visual Studio Code

```
cinst visualstudiocode
```

Once this is done, start it up and install the WSL Remote Extension (by 
Microsoft). The first time you run VS Code from your Ubuntu terminal, it will
run some startup code only this first time. You can do this by opening a 
directory using

```
code .
```

### Ruby

Check out the [RVM_Ubuntu repo](https://github.com/rvm/ubuntu_rvm#install) to
install RVM for ruby version management. After restarting your terminal, install
your version of Ruby with the following:

```
rvm i <VERSION>
```

### Basic Tools

You can follow typical window setup [here](../windows/README.md#basic-tools).

## DevOps

If you're working with/on DevOps, the following is likely useful to you.

### Docker

I follow [this tutorial] to get docker wired up to Docker for Windows so I can
use a universal environment. It basically flows like this:

```
# Update the apt package list.
sudo apt-get update -y

# Install Docker's package dependencies.
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

# Download and add Docker's official public PGP key.
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Verify the fingerprint.
sudo apt-key fingerprint 0EBFCD88

# Add the `stable` channel's Docker upstream repository.
#
# If you want to live on the edge, you can change "stable" below to "test" or
# "nightly". I highly recommend sticking with stable!
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# Update the apt package list (for the new apt repo).
sudo apt-get update -y

# Install the latest version of Docker CE.
sudo apt-get install -y docker-ce

# Allow your user to access the Docker CLI without needing root access.
sudo usermod -aG docker $USER

echo "export DOCKER_HOST=tcp://localhost:2375" >> ~/.bashrc && source ~/.bashrc
```

Then I boot my terminal again. 

```
sudo nano /etc/wsl.conf

# Now make it look like this and save the file when you're done:
[automount]
root = /
options = "metadata"
```

After all this, I do a *full* Sign Out/Sign In for Windows. I can then run

```
docker info
```

and all should be working fine.

#### If you require `sudo` for `docker`:

Check out the link [here](https://forums.docker.com/t/can-only-run-docker-as-root-in-wsl2/100165).

You can also add your user to the docker group:

```
sudo usermod -aG docker $USER
```

Lastly, try

```
unset DOCKER_HOST
```

If the above works running `docker info` and `docker run hello-word` then you can
remove the need for `export DOCKER_HOST=tcp://localhost:2375` from your env.

### AWS CLI

```
sudo apt-get install awscli
```