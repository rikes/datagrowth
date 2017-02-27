---
layout: post
title: 2 months of vim and tmux
description: "For over two months I've been using terminal in Linux using tmux, vim and vimwiki. I'm converted now and I'm not going back to 'normal' editors. Unless..."
modified: 2017-02-27
comments: true
tags: [Linux, ROS, vim, tmux]
image:
  feature: vim_wiki.png
---

For the last two months I've been using 3 tools to effectively work with the terminal on Linux. In this post I'll try to sum up my experience so far and show you all the tools that I'm using at the moment.

In the post I will add some commands that I find useful everyday. Please bare in mind that in 2 months I barely scratched the surface of both vim and tmux.

<!-- more -->

# A bit of a background

Almost all my life I was relying on IDEs(in the recent years mainly Visual Studio) or text editors(Notepad++, Sublime text, Atom, Visual Studio Code). In November last year I started working as a R&D engineer at Terabee where I'm working a lot with ROS (Robot Operating System).

The thing about ROS is that it usually requires you to run many programs from the terminal at the same time. Being fed up with constantly cycling over multiple terminal windows I was desperate to find something to make my workflow smoother. That's how I found [tmux](https://tmux.github.io/).

<figure class="center">
  <img src="{{site.url}}/images/tmux.gif" alt="tmux and vimwiki in action">
	<figcaption>Some tmux in action</figcaption>
</figure>

#tmux

I usually have multiple windows open at once in tmux. In first window I keep my vimwiki (more on that later) and a separate pane for git (only for my vimwiki repo).

My second windows usually contains multiple panes for running ROS nodes, working with topics etc.

Third window is my development window, usually it has only one pane that sometimes I split vertically inside vim.

Sometimes my fourth window is for writing and running unit tests (depending on the project)

I'm quite flexible with the setup, so I will often add or remove windows depending on my needs.

## Basic tmux commands that I use

* Split pane vertically     `ctrl-b+%`
* Split pane horizontally   `ctrl-b+"`
* Create new window         `ctrl-b+c`
* Delete pane               `ctrl-b+x`
* Move to the next window   `ctrl-b+n`
* Rename current window     `ctrl-b+,`
* Go to window[0]           `ctrl-b+0`
* Enable scroll             `ctrl-b+[` (q to exit scrollig)
* Kill window               `ctrl-b+&`
* Zoom pane                 `ctrl-b+Z`
* Go to previous window     `ctrl-b+p`
* Go to next window         `ctrl-b+n`
* Switch panes              `ctrl-b+arrow keys`
* Enter command mode        `ctrl-b+:`
* Synchronize panes         `setw synchronize-panes`

##tmux-resurrect

[tmux-ressurect](https://github.com/tmux-plugins/tmux-resurrect) can be used to preserve the tmux session. It allows to preserve windows and panes as well as paths and vim sessions. It's trivial to use:

* Save session              `ctrl-b+s`
* Reload session            `ctrl-b+r`

I only wish it supported restoring bash history better but hopefully it will get there in the future!

#vim

It's crazy how much *I still don't know about vim*. I don't think I even use 1% of its functionality. Currently I use it as you would use any other text editor with an advantage of seamless integration with the terminal.

I will be learning more and more about vim as I go. I heard stories about vim scripting functionality. Currently I'm hoping to explore vim in more detail as on of the projects in [1PPM]({{site.url}}//1ppm/12-Technical-Challanges/).

## Basic commands

If you want to give vim a try then hopefully some of those command will give you a head start:

### Basics

* open file                         `:e filename`
* start vim with two files vsplit   `vim -O file1.txt file2.txt`
* highlight syntax for xml          `:set filetype=xml`
* set autoindent                    `:set autoindent_ | _:set ai`
* spellcheck                        `:setlocal spell spelllang=en_gb`
* Set tab width to 4 spaces         `:set tabstop=4`

### Tabs and splits

* edit a file in a new tab  `:tabedit {file}`
* next tab                  `:tabn`
* previous tab              `:tabp`
* split open file           `:vsplit filename` or `:split filename`

### Modes

* exit insert mode                  `esc` or `ctrl-[` 
* go to normal mode for one command `ctrl-o`

### Navigation

* Go to beginning of a line `^ or 0`  (normal mode)
* Go to the end of a line   `$`       (normal mode)
* Go to the top of window   `H`       (normal mode)
* Go to last line of file   `G`       (normal mode)

##vimwiki

[Vimwiki](https://github.com/vimwiki/vimwiki) is a personal wiki for vim. It comes with very nice syntax highlighting and although it allows for exporting documents to html I don't usually do that as I find really easy to navigate from within vim.

I keep the wiki with all the files as a private repository on gitlab so that I can easily access it anywhere. At the time of writing this post I have 61 files in my wiki and on average I make a single commit to it every day. 

<figure class="center">
  <img src="{{site.url}}/images/vim_wiki.png" alt="Vim wiki commits graph">
	<figcaption>My personal wiki commits graph</figcaption>
</figure>

# Minimizing customization

I'm trying to minimize customization of both vim and tmux to minimum, mainly for two reasons:

* If I was to lose my configs I would be super confused and it could take time to restore the settings (I would probably keep it as a repository to be honest)
* If I have to work on unfamiliar PC I can do majority of work straight away without having to waste time on customizing things again

# The setup is... **antisocial**

I don't believe tmux and vim can work efficiently for pair programming (unless both developers are really used to the tools and share the same configurations). 

Because you can switch context so quickly in tmux it might become very difficult to follow your train of thoughts, especially if you are working with less experienced people. In such case, do everyone a favour and switch to some neat visual editor where both of you can be equally productive.

# Going forward

I will definitely keep using the tools mentioned in this post as they greatly improve my workflow. I'll also eventually step up the game with some additional plugins (I've been heavily considering [Syntastic](https://github.com/vim-syntastic/syntastic) for vim).

The other day someone at Hacker News posted [terminals are sexy](https://github.com/k4m4/terminals-are-sexy) curated list of terminal tools. I'm confident that I will find there couple of things that will end up in my toolbox.

# What about you?

As I mentioned couple of times I'm just starting out here. Do you have any recommendations? Are there any terminal tools you cannot live without?
