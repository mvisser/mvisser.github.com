---
layout: post
title: Vim Quickfix
---

A lot of people I know use Vim, but some of them complain that Vim doesn't have
the same features as an IDE. They complain that it doesn't seem to find compiler
errors, or seem to be able to nicely search across files.

The fact of the matter is, their approach to Vim has been to view it as a text
editor, and only that, when it can do so much more!  Vim *does* have great
integration with compilers and it *does* search nicely across many files, but
first you need to know the right commands and how to use them.

Using Make
----------

Vim has awesome support for integrating with your favourite language's compiler
or lint program.  Many file types come with awesome integration in Vim already,
while some are rather agnostic about what you want to use.  There are a few
magic options and commands that you'll want to use to get Vim acquainted with
your preferred environment:

* The `:compiler` command can tell Vim which compiler or lint program  you're
  going to use.  This tells Vim what format the error messages are going to be
  in, as well as setting a few other options Vim needs to know about.  These
  files can be written on your own, but Vim has a pretty nice collection of them
  already in `$VIMRUNTIME/compiler`. If you're using Java, for example, you may
  want to use `:compiler ant` to tell Vim you're using Ant as your build
  program.
* The `'makeprg'` option tells Vim what command to run when you use `:make`
  command (more on that later). Using the same Java example, you'll want to set
  this like so:

    set makeprg=ant

  You may have to use a full path to Ant if the program is not in your path.

So now you have introduced Vim to your compiler or lint program. They're getting
acquainted, so it's time to take their relationship to the next level. To do
this, use the `:make`(-out? Ha-ha.) command. If everything has been set up right
(except your source code - you need to actually have a compiler error or
warning), you should see Vim magically take you to the first error or warning
the compiler found. YAY! Vim is now doing something useful!

It would be crazy to think that Vim would make you recompile with `:make` every
time you want to see the next error, so now we get to use `:cnext` and `:cprev`
to go through the error list.  Every time you use one or the other, Vim goes to
the next (or previous) error in the error list and gives you the error message
at the bottom of the screen.  You can then fix the error as you see fit.

This is fine and all, but what if you want to see *all* of the errors. Well,
this is where the quick-fix list really comes in to play.  The `:cwin` command
opens a special, new, un-editable window. This window displays a list of all
your compiler errors with line numbers and possibly character positions.  You
can move around the buffer as usual, but when you pres *enter*, Vim jumps to the
error your cursor was on!  Now you can view all of your errors, and pick out a
specific error's position if you need to. Isn't that awesome!?!?!

Don't Forget Grep Too!
----------------------

Vim doesn't just use quick-fix's awesomeness for compilers, though!  Vim also
let's you do this with `grep`.

The relevant option is `'grepprg'`. Vim gives you two commands to use `grep`,
though. One runs the external grep program that you set with the `'grepprg'`
option - `:grep`.  The other is `:vimgrep`. While they both behave the same way
on the surface, the first is usually faster. This is because `:vimgrep` actually
uses an internal procedure within Vim to search all of the files, and it's not
quite as fast as the actual `grep` program. You can use either like so:

    :[vim]grep /pattern to search/ file

There are a few things to note:
* The pattern can use all of Vim's regular expression goodness if you use Vim's
  internal `grep`. If not, all of `grep`'s regex rules apply.
* The `file` can be any file name, or a *glob*.  Pro tip: use something like
  `**/*.c` to glob for all C files recursively through the whole directory tree
  when using Vim's internal `grep`. With the external `grep`, you can use any
  options that `grep` normally has inserted before the pattern, i.e. `:grep -r
  /pattern/`.

What If I Want Multiple Lists?
------------------------------

If you want to have multiple lists, you want to use *Location Lists*. These are
basically the same as quickfix, except you can have one per window. The
`:lmake`, `:lgrep`, and `:lvimgrep` commands will do the same as `make` or `grep`,
but use a Location List instead.


Hope you found this information useful, and Happy Vimming!
