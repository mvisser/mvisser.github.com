---
layout: post
Title: "Jekyll Setup With Github Hosting"
---

I'm going to document how I set up this blog with github hosting and Jekyll,
and the issues I came across while doing so. So far, I like the experience, but
setting up things like pygments was a bit confusing and for some reason didn't
really work on my local machine, which was a bit disappointing. At any rate,
the blog is set up and running!

Create a Repository Supporting Jekyll
-------------------------------------

The first step to the entire process is to create a repository on github. These
are the steps I followed:

1. **Add a new repository to github**, and give the required information.
    - The name of the repository should be `username.github.com`.

2. **Create the repository locally**, with the same name as above. If you are
   creating a simple HTML site, then just create the site as needed.  Look in
   to opting out of Jekyll by adding a specific file, `.nojekyll`.

   If you're creating a site using Jekyll, you'll want to add a few extra files
   and folders to get yourself started:

    * `_posts` is where all of your posts will go. They can be written in html,
      markdown, or textile.
    * `_layouts` is where all of your layout html will go. Use this to create
      the general HTML page for your home page and posts page.  I have two
      layouts: one for the homepage that lists all blog posts, and one for each
      specific post.  The reasons I did this were purely asthetic and you can
      use the same layout for both if you wish.
    * `_config.yml`  This is where all of your configuration goes.  [The Jekyll
      Documentation](https://github.com/mojombo/jekyll/wiki/configuration)
      describes the many options given to you very well.

    Now add everything to the repository for your first commit with the following
    commands inside the `username.github.com` directory.

        $ git init .
        $ touch .gitignore
        $ git add .
        $ git commit

3. **Add styling to your page!** This part was definitely fun for me. I haven't
   played around with CSS a whole lot since high-school because I've mostly been
   using frameworks at work or haven't bothered with it.  You can add your
   stylesheet wherever you want, but I opted to

4. **Add content!**  As stated before

5. **Push to github!** Commit your changes and push to github.  They should
   generate the page and start hosting it at `http://username.github.com`!
   You're done!


Set up Pygments
---------------

You can use pygments to highlight your code, which I've opted to not do for the
time being. You must obviously have pygments installed on your local machine
for this to work. Since the way to do this varies a lot from system to system,
I'll leave it to you.

Okay, now that you have pygments installed, execute:

    $ pygmentize -S default -f html > code.css

This will generate a css file to highlight code after it's run through pygments.


Now you can highlight code that you have in your posts with the following snippet

    {{ "{% highlight c " }}%}
    #include<stdio.h>
    int main(int argc, char * argv[] ){
        printf( "Hello World!");
    }
    {{ "{% endhighlight " }}%}

Not too hard, right?  I had some issues getting this to work on my local
machine, which was a little bit frustrating. For some reason, pygments decided
to eat all of the text it was given and output nothing.  C'est la vie. I
decided to not use pygments with my site until I could get it working locally.
It seems, though, that github will always try to pygmentize, since it
over-rides your setting for pygments.

Tips &  Tricks
--------------

Here are some tips and tricks for writing a blog in Markdown in Jekyll. I'll be
updating these as I go.

### Escaping Liquid Tags ###

If you want to escape the liquid tags (like when I entered the `highlight` tag,
you can use something like the following

    {{ "{{" }} {{ '"{% tag ' }}{{ "}}" }}%}

There is a distinction between single and double quotes. If you want to display
a double quote, you must do something like

    {{ "{{ '" }}{{ '"' }}{{'" }}' }}

The escaping gets more and more confusing the further you go... I wouldn't
recommend doing it often...


Reflection
----------

So the process was mostly painless, wasn't it?

I like the way things are laid out with Jekyll. Once you have your styling and
templates set up, it's very easy to just write your post in something easily
readable and editable, like markdown, and get on your way making content.  I
also like that I can do all of my work locally in my own editor, and the site
can be deployed to github hosting with just a `git push`.  It doesn't get too
much easier than this to have a nice, custom site up and running.  Hopefully
you like the content I have to offer!
