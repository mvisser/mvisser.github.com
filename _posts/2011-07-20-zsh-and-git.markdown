---
layout: post
title: "Git Info in ZSH Prompt"
---

Git is awesome.  ZSH is also awesome.  Why can't they work together!?!?!  The
truth is they can! Introducing my ZSH prompt with git info!

The magic all begins with one awesome line in your `~/.zshrc`:

    autoload -Uz vcs_info

This one line gets you all the ZSH goodness to get info about the git repository
you're in right inside your prompt. The rest is just telling ZSH how you want it
to show you the info.

    # give us some awesome colour stuffs
    autoload colors zsh/terminfo

    # style the git messages
    zstyle ':vcs_info:*:prompt:*' enable git
    zstyle ':vcs_info:*:prompt:*' check-for-changes true
    zstyle ':vcs_info:*:prompt:*' use-prompt-escapes true
    zstyle ':vcs_info:*:prompt:*' stagedstr '%F{green} staged %f'
    zstyle ':vcs_info:*:prompt:*' unstagedstr '%F{yellow} unstaged %f'
    zstyle ':vcs_info:*:prompt:*' actionformats "(%s:%b%u%c - %a)" "[%R/%S]"
    zstyle ':vcs_info:*:prompt:*' formats       "( %F{green}%s%f:%F{14}%b%f%u%c )" "[%R/%S]"
    zstyle ':vcs_info:git:prompt:*' formats       "( %F{red}git%f:%F{14}%b%f%u%c )" "[%R/%S]"
    zstyle ':vcs_info:*:prompt:*' nvcsformats ""

    # make sure ZSH knows about git before it shows the prompt
    precmd () { vcs_info 'prompt' }


I prefer to have the information about my git repository on the right side of my
prompt.  If you didn't know ZSH could do this now you do!

    # set the prompt to show git stuff!
    RPROMPT='%B${vcs_info_msg_0_}$b'

If you copy and paste this directly, you should get something that looks as
awesome as this:

![Fancy git prompt][1]

How's that for class. Useful and elegant.  It also contains information if
you're resolving a merge conflict or editing during a rebase, but since those
situations are a little harder to reproduce, I think I'll hold off on the
screen-shots for now.

Happy hacking!

[1]: /images/git-prompt-staged.jpg
