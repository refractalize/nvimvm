# nvimvm - a Neovim version manager

```console
> nvimvm
Usage: nvimvm <command>

Commands:
  versions
    List available versions
  installed
    List installed versions
  install <version>
    Install a version (but don't use it)
  use <version>
    Use a version
  path <version>
    Print the path to a version
  remove <version>
    Remove a version
```

## Install

### Zsh

This repo contains a zsh plugin which most zsh package managers will pick up:

```
antigen bundle refractalize/nvimvm
```

```
zgen load refractalize/nvimvm
```

Or otherwise download this repo and `source $REPO/nvimvm.plugin.zsh`

### Others

```sh
REPO=... # somewhere to put nvimvm
git clone https://github.com/refractalize/nvimvm.git $REPO
PATH=$HOME/.local/share/nvimvm/bin:$REPO/bin:$PATH
```

## Features

### Enumerate all available neovim versions

```console
> nvimvm versions
nightly (nightly-3f188bc533bc22f1d13dce33ab5d63973c3ff22a, 2024-01-21T14:47:59Z)
v0.9.5
stable (stable-8744ee8783a8597f9fce4a573ae05aca2f412120, 2023-12-30T13:31:44Z)
v0.9.4
v0.9.2
v0.9.1
v0.9.0
v0.8.3
v0.8.2
v0.8.1
v0.8.0
v0.7.2
```

### Use a version

Use a parcicular version of neovim for all shells. This will download it if not already downloaded.

```console
> nvimvm use v0.9.5
Downloading v0.9.5
######################################################################### 100.0%
Using v0.9.5
> nvim --version
NVIM v0.9.5
Build type: Release
LuaJIT 2.1.1692716794

   system vimrc file: "$VIM/sysinit.vim"
  fall-back for $VIM: "/usr/local/share/nvim"

Run :checkhealth for more info
```

**NOTE** that `zsh` will cache the paths of executables, so you may need to run `rehash` to ensure it finds the new `nvim` instance. See https://zsh.sourceforge.io/Guide/zshguide03.html

### Install tagged versions

Install and use tagged versions like `nightly` and `stable`.

```console
> nvimvm install nightly
Downloading nightly-3f188bc533bc22f1d13dce33ab5d63973c3ff22a
######################################################################### 100.0%
> nvimvm use nightly
Using nightly-3f188bc533bc22f1d13dce33ab5d63973c3ff22a
```

### Tracks git SHA of tagged versions

`nvimvm` tracks the git SHA of tagged versions such as `nighly` or `stable`, allowing you for specify exactly which version you want to use.

```console
> nvimvm installed
* nightly-2fce95ec439a1121271798cf00fc8ec9878813fa (2024-01-17T05:14:37Z)
  nightly-3f188bc533bc22f1d13dce33ab5d63973c3ff22a (2024-01-21T14:47:59Z)
  nightly-d65c6a0bafada059e87a11a4bcd129afc16d2e5d (2023-12-13T05:14:36Z)
  stable-8744ee8783a8597f9fce4a573ae05aca2f412120 (2023-12-30T13:31:44Z)
  stable-d772f697a281ce9c58bf933997b87c7f27428a60 (2023-10-09T20:51:23Z)
  v0.9.4
  system
> nvimvm use nightly-3f188bc533bc22f1d13dce33ab5d63973c3ff22a
Using nightly-3f188bc533bc22f1d13dce33ab5d63973c3ff22a
```

### Support for [direnv](https://direnv.net/)

You can use [direnv](https://direnv.net/) to specify which version of neovim should be used in a particular directory:

```
# .envrc
# We want to use nvim v9.5.0 in this directory
PATH_add $(nvimvm path v9.5.0)
```

### Use the system version

Use whatever the system version is, not managed by `nvimvm`.

```
> nvimvm use system
Using system
```
