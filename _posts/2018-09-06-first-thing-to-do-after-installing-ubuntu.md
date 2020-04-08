---
layout: post
title: First thing to do after installing Ubuntu
categories: ubuntu set-up
image: https://images.unsplash.com/photo-1527355839959-04c7c437c723?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=e726c0089874533e149913145571d8c0&auto=format&fit=crop&w=1953&q=80
---

I just installed the latest Ubuntu release (right now 19.10). These are the first things I do, to set up my system:

* Activate additional drivers. Some parts of my computer might not work without the propertary drivers, for instance, your WiFi card.

* Set up displays. Currently I am using 3 monitors, one of them in portrait. I also like to set up "night lights" to get a better sleep.

* Set up Wifi. I am going to need internet to do the setup.

* Install and setup Timeshift. Important tool to turn back time, if something were to go wrong.

```bash
sudo apt install timeshift
```

* Full system update.

```bash
sudo apt update
sudo apt full-upgrade
```

* Enable additional software. Go to "Software & Updates" and be sure to include all the repos in there. And since you are there, choose a server that is close-by.

* Install media codecs.

```bash
sudo apt install ubuntu-restricted-extras
```

* Install git

```bash
sudo apt install git
```

* Install my favorite shell, zsh, and configure it

```bash
# Install
sudo apt install zsh

# Set up as default shell (You need to log out and in again, for it to work)
chsh -s $(which zsh)

# Download antigen
curl -L git.io/antigen > antigen.zsh
```

This is my default .zshrc file.

```bash
source ~/antigen.zsh

# Load the oh-my-zsh's library.
antigen use oh-my-zsh

# Bundles from the default repo (robbyrussell's oh-my-zsh).
antigen bundle git
antigen bundle heroku
antigen bundle pip
antigen bundle lein
antigen bundle command-not-found

# Syntax highlighting bundle.
antigen bundle zsh-users/zsh-syntax-highlighting

# Load the theme.
#antigen theme robbyrussell
antigen theme https://github.com/denysdovhan/spaceship-prompt spaceship

# Tell Antigen that you're done.
antigen apply
```

* A good looking terminal I have been using lately is called [Hyper](https://hyper.is), but there are other alternatives, like [Terminator](https://gnometerminator.blogspot.com/p/introduction.html)

```bash
sudo apt install terminator
```

* Set up an SSH key

```bash
ssh-keygen
```

* [Google Chrome](https://www.google.com/chrome/) is my default web browser

* Set up workspaces with Gnome extensions

```bash
sudo apt install gnome-tweaks chrome-gnome-shell
```

* Other software that I used regularly, that can be installed in any order.

    * vlc
    * gimp
    * Slack
    * Discord
    * Spotify
    * Peek
    * Flameshot
    * Visual Studio Code
    * Synlogdy Drive client
    * Dropbox
    * Unity3D
    * GitKraken
    * Filezilla
    * Hexchat
    * Remarkable