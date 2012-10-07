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
