---
layout: post
title: Blogging With VIM
---

My favourite text editor is VIM.  There are many favourite text editors to
choose from, but this one is mine.  Call me crazy, call me insane, but I find it
very intuitive, very configurable, and very consistent.  I use VIM all day at
work to code and I'm comfortable with it, so why wouldn't I want to write
everything else with it too?

So what are my options?

1. Use a web-based engine like Blogger and write posts one the web.

   This would be okay, but most browsers don't exactly allow you to edit using
   VI-style key-bindings. I could copy and paste the text, but that is kind of
   painful too. The best solution I've seen is to use a browser plug-in like
   [Pentadactyl][1], which lets you spawn your
   editor to edit text fields (along with allowing you to browse almost
   completely mouse-less using VI-style key-bindings - more to follow in another
   post).

2. Use an engine that allows you to edit a text file for each post.

   This is what I chose. To use Jekyll, which lets me write markdown files.
   This lets me write posts in my favourite editor, and host the site where I
   choose.


I opted to go with option 2, but either way, you want to edit plain-language
text in VIM - great! Here are some options you want to look at.

- Setting `nocompatible`.  If you use VIM at all, this is pretty much a
  no-brainer, and should be in your `.vimrc` already.
- `filetype plugin indent on` will get you all of the awesome settings for
  file-types. Markdown, Textile, or some other format should now work nicely
  with a default VIM install.
- `syntax on` will give you some nice syntax highlighting if you're using a
  format more structured than plain-text.
- `spell` - You want to use spell.  Spell-checking in your text-editor is
  awesome.  I even use it sometimes while writing code.  VIM is smart enough to
  know when you're writing something that should be plain-text and when you
  aren't (if the syntax definitions are written correctly.) With your language
  set correctly in VIM, you get awesome spell-checking and simple
  grammar-checking for free in your favourite text editor. How could you
  complain!
- `lbr` - This sets VIM so that words break at sensible points on the edge
  of the screen, even if there is no hard line wrap, the soft line wrap goes on
  word endings. This makes your writing a lot more readable if you don't
  hard-wrap your lines.
- If you do decide to hard-wrap lines, `textwidth` is exactly what you need.
  Set `textwidth` to the line length you want, and use the `gq` command to
  format lines, paragraphs, or the whole document (you probably don't want to do
  the whole document... )
- `formatoptions` decide how VIM should format your paragraphs.  This option is
  generally set to a sane default, but you can find out how to tweak it by
  looking at `:help fo-table`. You can have VIM auto-format as you type with
  `fo+=a`.  VIM will format numbered and bulleted lists with `2` and `n` added
  respectively.

Hopefully these settings can at least get you started with writing your posts in
VIM! There are of course many other things you can do to make your life easy,
such as reading in template files with `:r`, and using macros and mappings to
generate text for you.

Happy Vimming!

[1]: http://dactyl.sourceforge.net/ "Pentadactyl Firefox Plugin"
