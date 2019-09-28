---
layout: post
title: First thing to do after installing Ubuntu
categories: ubuntu set-up
image: https://images.unsplash.com/photo-1527355839959-04c7c437c723?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=e726c0089874533e149913145571d8c0&auto=format&fit=crop&w=1953&q=80
---

You just installed the latest Ubuntu distro (right now 18.04) are you are dying to know what should you do first, right? This is in my list.

## The basics

```bash
# Update the system
sudo apt update
sudo apt full-upgrade

# Enable additional software!
# Go to "Software & Updates" and be sure to include all the repos in there.
# And since you are there, choose a server that is close-by.

# Install media codecs
sudo apt install ubuntu-restricted-extras

# Install video player
sudo apt install vlc

# Install graphics editor
sudo apt install gimp
```

## Programing

- I have more than 1 workspace in Slack. To manage them, I use the snap package.

```
sudo snap install slack
```

- [nvm](https://github.com/creationix/nvm) to manage different node versions
- [rbenv](https://github.com/rbenv/rbenv#basic-github-checkout) to manage different ruby versions

- I am going to need a shell, and to me there is nothing that beats zsh.

```
sudo apt install zsh
```

- [Antigen](https://github.com/zsh-users/antigen/wiki/Installation) is a great way to manage extension and plugins in zsh, so that comes next

- Once installed, set up your .zshrc. This is mine:

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

- A good looking terminal I have been using lately is called [Hyper](https://hyper.is), but there are other alternatives, like [Terminator](https://gnometerminator.blogspot.com/p/introduction.html)

- You are using Linux so you must program, in some sort or way. You are gonna need either [Sublime Text](https://www.sublimetext.com/docs/3/linux_repositories.html), [Visual Studio Code](https://code.visualstudio.com/download) or [Atom](https://flight-manual.atom.io/getting-started/sections/installing-atom/).

## Install other 3rd party software

- Time to install [Chrome](https://www.google.com/chrome/). Unless you are happy enough with Firefox, of course.
- I want to hear music. Time to download [Spotify](https://www.spotify.com/de/download/linux/).
- Everyone loves animated GIFs. Go make some with [Peek](https://github.com/phw/peek).

## Other settings

- Go to "Settings -> Devices -> Displays" and set those night lights. We all need a good night sleep.
