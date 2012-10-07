% Ergonomic editing with vim
% Kévin "Chewie" Sztern

# The philosophy of vim

## A brief history

### In the beginning: vi

* Written by Bill Joy in 1976
* Based on the _visual_ command of ex
* Part of the _Single UNIX Specification_
* Several modern vi clones exist nowadays
* nvi, Elvis, svicc, bvi, VILE..

### Vi iMproved

* (Arguably) the most popular clone is Vim
* Charityware written by Bram Moolenaar in 1991
* Almost 100% compatible with vi
* Used as vi implementation in most Linux distributions

## Design and principles

### What vim is

* Vim is a text editor
* Vim excels in writing and manipulating text
* Vim is designed to be ergonomic

### What vim is not

* Vim is not betraying the UNIX philosophy!
* Vim is not an IDE : no debugger or shell integration
* The shell is just a ctrl-z away
* See :help design-not

### A modal editor

* Vim has 6 different modes
* Only one of them is about inserting text
* Most of your time will be spent in the normal mode

### Commands form a language

* [operator][count][motion]
* All operators work with the same motions
* Understanding the command language makes learning easier
* Examples: "delete a word" is daw, "copy inside quotes" is yi'

# The basics

## Moving around

### Relative movement

* Forget arrow keys
* Character wise: hjkl
* word wise: web and WEB
* Beginning and end of lines: 0, ^ and $
* Up and down half a page: ^u and ^d
* First and last line: gg and G

### Cursor positionning

* Top, Middle and Bottom of the screen: HML
* Align cursor to top, mid or bottom: zt, zz, zb

## Modifying text

### Entering insert mode

* Entering insert mode before or after the cursor: i and a
* At beginning or end of line: I and A
* Next and previous line: o and O
* Change operator leaves you in insert mode
* Leave insert mode for normal mode: Esc (rebind it to Caps Lock)

### Three basics operators

* Delete operator: d
* Change operator: c
* Copy (yank) operator: y
* Several other operators: v,=,~,g?...

### Motions

* Regular movement
* Text objects: words, sentences, [] blocks...
* Marks
* Searches

### Text objects

* Prefixed with a or i for "around" and "inner"
* words and sentences: w,W,s
* Blocks: `(,[,<,{,",'`
* XML tags: t
* b and B are shorthands for ( and {

## Working with multiple files

### Buffers, windows, tabs

* A buffer is an *instance of a file*
* A window is a *view on a buffer*
* A buffer can be viewed by multiple windows at the same time
* A tab is a *collection of windows*
* See :help windows

### Switching buffers

* Don't forget to :set hidden
* open a new buffer: :e(dit)
* Delete a buffer: :bd(elete)
* List all buffers: :ls
* Previous and next buffer: :bp(rev) and :bn(ext)
* Go to nth buffer: :b{1,2,3...}

### Managing windows

* Windows commands begin with ^w
* Split horizontally or vertically with ^w s and ^w v
* Change active window with ^w hjkl
* Close window with ^w c

### A word on tabs

* Tabs in vim are not like any other text editors!
* New since Vim 7.0
* Create a tab with :tabe(dit)
* Switch between tabs with gt and gT
* Close tab with :tabc(lose)
* As always, see :help tabpage

# Advanced vimming

## Search and replace

### The search options

* Forward and backward search with / and ?
* next and previous occurence with n and N

### The almighty sed

## Macros

### What are macros

### Registering and running macros

## Global commands

### Syntax

### A few examples

## Auto completion

### Different kinds of completions

### Omnicompletion and tags

### Fun with tags

# Configuring vim

## Vim runtime overview

### The .vim architecture

## The absolute minimum

### It's dangerous to go alone, take this!

## The tabs vs spaces holy war

### Disclaimer

### General considerations

### Way of the space

### Church of the Holy Tab

## Mappings

### What are mappings?

### The leader key

### Several map commands

# A word on plugins

## What are plugins?

### A set of predefined commands and mappings

## Three types of plugins

### Make it like other editors

### Extend vim's core

### Sharpen the saw

## When should I start using plugins?

### Vim as a minimalist editor

### Try to get comfortable

## A personal non exhaustive list

### Surround

### Syntastic

### NERDCommenter

### Tagbar

# Going beyond

## What we've seen

### The absolute minimum

### The best is still to be discovered!

## Where to learn more

### :help

### vimcasts.org

### Online communities
