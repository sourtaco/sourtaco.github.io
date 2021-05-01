---
layout: post
title: "Setting up Haskell and Neovim"
date: 2021-04-30
tags: vim nvim neovim ide
---

# The basics

To set up Haskell, I just followed the [directions](https://www.haskell.org/platform/mac.html).

I'm going to use [neovim](https://wiki.haskell.org/Vim) and the [Haskell Language Server](https://github.com/haskell/haskell-language-server#coc) configured to use [coc.nvim](https://github.com/neoclide/coc.nvim) for LSP support.

I'll be using the recommended default configurations for now, and see how far that gets me.

# Keep it Clean

To manage my vim plug-ins, I use [Plug](https://github.com/junegunn/vim-plug). I also like to keep things organized, 
so I break out various configs into separate files. Here is an example of my `init.vim` file:

```vim
call plug#begin('~/.config/nvim/')
Plug 'dracula/vim', { 'as': 'dracula' }
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'gennaro-tedesco/nvim-jqx'
Plug 'vim-airline/vim-airline'
Plug 'vimwiki/vimwiki'
call plug#end()

source $HOME/.config/nvim/theme.vim
source $HOME/.config/nvim/vimwiki.vim
source $HOME/.config/nvim/coc.vim
```

# Distributed Bonus

I work across several machines and use [syncthing](https://syncthing.net/) to keep my nvim
setups standard across the board. The one caveat is that I don't want
to sync installed  `Plug`s, just their configs. So I keep a `.dont_sync` file in the nvim config folder to tell it basically only sync `.vim`, `.json` and itself:

```
!/*.vim
!/*.json
!/.dont_sync
*
```


and have my `.stignore` file load it:

```sh
#include .dont_sync
``` 


That has to be done because you can't sync an `.stignore` file, but you can sync
the files it includes.
