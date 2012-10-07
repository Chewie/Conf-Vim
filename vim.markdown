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
* Switch to buffer containing file *foo*: :b foo (autocompletion works)
* Switch to nth buffer: :b{1,2,3...}

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
* Search for word cursor with * and #
* next and previous occurence with n and N
* Go to specific character on a line with f and F
* Go just before (unTil) that character with t and T

### The almighty sed

* Arguably the most powerful command in vim
* `:s/<regexp>/<replacement>/[options]`
* The / separator is arbitrary, you can choose something else
* The g option allows multiple substitutions on a given line
* As a global command, it works on ranges (eg :%s for the whole file)

## Macros

### What are macros

* Macros are sets of commands recorded to a register
* A great way to repeat a complex task multiple times

### Registering and running macros

* Start recording with q followed by the name of the register (any letter)
* Perform your actions as usual, while they are recorded
* Stop recording with q
* Execute a macro with @ followed by the name of the register
* Example : `qaddq` stores the macro to delete a line in register a
* You can then run it with [count]@a

## Global commands

### Syntax

* `:[range]g/<regexp>/<command>`
* Executes the Ex command `<command>` on every line matching regexp in the range
  (whole file by default)
* :v or :g! executes the command for lines *not* matching the pattern

### A few examples

* Delete all blank lines: `:g/^\s*$/d`
* Add bar to end of lines beginning with foo: `:g/^foo/s/$/bar/
* Run a macro on matching lines: `:g/<pattern>/normal @q`

## Auto completion

### Different kinds of completions

* Whole lines: ^x ^l
* Words in the current files: ^x ^n
* Tags: ^x ^]
* File names: ^x ^f
* Omni completion: ^x ^o
* Switch to next and previous suggestions with ^n and ^p

### Omnicompletion and tags

* New since Vim 7.0
* Syntax aware completion for programming languages
* Works out of the box for some languages (python, ruby...)
* Needs a tags file for others (php, C, C++...)

### Fun with tags

* Even if you don't use completion, having a tags file is useful
* Use ctags program to generate tags file: `ctags -R`
* Jump to definition of function *foo* : :tag foo
* Call tag on word under cursor: ^]
* Go to previous jump point: ^t

# Configuring vim

## Vim runtime overview

### The .vim architecture

* .vim/autoload: automatically loaded functions
* .vim/plugin: general purpose plugins
* .vim/ftplugin: filetype specific plugins
* .vim/ftdetect: filetype detection scripts
* .vim/colors: colorschemes
* .vim/syntax: syntax highlighting files
* .vim/after: scripts guaranteed to be run after the others

## The absolute minimum

### It's dangerous to go alone, take this!

```vim
set nocompatible
syntax on
filetype plugin indent on
set backspace=2
```

## The tabs vs spaces holy war

### Disclaimer

* Both choices are valid ones
* Some languages give you the choice (C, php...)
* Some languages made that choice for you (make, python, go...)
* The important thing is to be consistent across a team

### General considerations

* expandtab: whether a `'\t'` or spaces are inserted upon pressing the Tab key
* tabstop: length of the `'\t'` character (default 8)
* softtabstop: amount of spaces inserted when pressing Tab (default 0)
* shiftwidth: level of indentation (default 8)
* softtabstop and shiftwidth can differ, although that is not desirable
* **Never** set tabstop != 8

### Way of the space

```vim
set expandtab
set tabstop=8
set softtabstop=n
set shiftwidth=n
```

With n being the value you desire (I personally like 4)

### Church of the Holy Tab

```vim
set noexpandtab
set tabstop=8
set softtabstop=0
set shiftwidth=8
```

## Mappings

### What are mappings?

* Mappings are shortcuts for sequences of commands
* They can exist for every mode, though you should avoid insert mode mappings
* Mappings can be recursive or non recursive
* Example: cnoremap is a command mode, non recursive mapping

### The leader key

* The leader key is a key left for personnal mappings
* By default the leader key is `"\"`
* you can remap it with `let mapleader = "X"` (I like ",")

### Several map commands

* nnoremap j gj
* nnoremap k gk
* noremap ; :
* nnoremap Y y$

# A word on plugins

## What are plugins?

### A set of predefined commands and mappings

* Plugins are bundles that bring a set of features
* Plugins can be written in VimL, or more recently in python and ruby
* They are sets of files that can be copied in the .vim folder
* ...Or you can use a plugin manager like pathogen or vundle

## Three types of plugins

### Proper credit

* The "three types of plugins" idea comes from Drew Neil of vimcasts.org
* http://vimcasts.org/blog/2012/08/on-sharpening-the-saw/
* Go visit his site because it is awesome

### Make it like other editors

* Give the feel of another editor
* Awful plugins with insert mode mappings and horrendous startup times
* Run away from those plugins

### Extend vim's core

* New colorschemes, syntax highlighting, omnicompletion...
* Those plugins are good

### Sharpen the saw

* Give new operators, new motions, new features altogether
* Those are good too

## When should I start using plugins?

### Vim as a minimalist editor

* Some people advocate the minimalist approach
* You can be effective with a 5 lines .vimrc
* Learn how to work without plugins

### Try to get comfortable

* Learn vanilla Vim first
* Read the doc of every plugin you install
* Don't overdo it

## A personal non exhaustive list

### Pathogen

* Written by Tim Pope
* Plugin manager
* Each plugin is installed in a separate folder in .vim/bundle, rather than
  scattered accross the .vim architecture

### Surround

* Written by Tim Pope (again!)
* Adds a new motion for surroundings
* Add or delete quotes, parentheses, brackets...
* Change a pair of surroundings for another

### Syntastic

* Written by Martin Grenfell
* Syntax checking on the fly
* Get rid of most of the edit/compile/edit cycle

### NERDCommenter

* Written by Martin Grenfell (again!)
* Loads of mappings for easy code commenting
* Why isn't it installed by default again?

### Tagbar

* Written by Jan Larres
* Displays tags of the current file in a window

# Going beyond

## What we've seen

### The absolute minimum

* For the sake of our sanity, we didn't cover every command and mapping
  available
* Try to understand the *idea* behind each concept rather than blindly learning
  they commands

### The best is still to be discovered!

* Marks: :help mark-motions
* Visual mode: :help visual
* And so many more!

## Where to learn more

### :help

* Vim comes with excellent documentation
* When in doubt (or if bored), run :help

### vimcasts.org

* Loads of short videos presenting vim concepts
* Gotta watch'em all

### Online communities

* Mailing lists: http://www.vim.org/maillist.php
* IRC: #vim@freenode
* Reddit: /r/vim

### My vim configuration

* My configs file are available at https://github.com/Chewie/configs
* Don't just copy the vimrc, try to understand every command
* Give feedback!
