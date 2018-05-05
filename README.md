# CrashCourse

This is the site source for TartanHacks CrashCourse. We're using Jekyll to build
and compile our site. We're not using GitHub Pages, though, because we wanted to
host the site from <http://scottylabs.com/crashcourse>.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

## Local Development

Make sure you have a recent version of Ruby installed and run

```console
$ gem install bundler
$ bundle install
```

If that failed, and you're on OS X, you might have to run this:

```
gem install nokogiri -v 1.6.8.1 -- --with-xml2-include=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/usr/include/libxml2 --use-system-libraries
```

and then re-run `bundle install`.

Once you've done that, you can preview the site locally by running

```console
$ jekyll serve
```

This will compile the static files, including all Sass assets. Then, in your
browser, navigate to <http://localhost:4000/> to view the generated site.


### I want to...

This is a typical Jekyll project. The [Jekyll documentation][jekyll] online is
really well put together; you should give it a skim. In the mean time, here's a
list of points where you might want to look:

#### ... change the style of the site.

Since this is a Jekyll site, the repetitive content is pulled out into
_templates_. These files are located in `_includes/` and `_layouts/`. Altering
these files will alter all files based off of them. You can tell if a file is
based off another file if it includes the line `layout: <something>` or `{%
include <something> %}` somewhere inside it.

To change the stylesheets, you should look in `assets/css/`. Here' you'll see
that we're using Sass, which is a CSS preprocessor. This just means we're using
a language that compiles to CSS, instead of writing CSS directly. Look it up
online for more information. The `main.scss` file `@import`s the files which are
located in the folder `_sass/`. To change the styles, you'll want to change
the files located in there.


#### ... add information about a talk.

First, you'll have to make a talk page:

```
cd _talks
mkdir TITLE-OF-TALK
cat _template.md | sed -e 's/my-fancy-talk/TITLE-OF-TALK/' > TITLE-OF-TALK/index.md
```

Now fill in the template (things like description, title, etc.).

Finally, add a timeslot for the event by editing `_data/days.yml`. Make sure you
follow the same structure as what's already there.

#### ... add content to the site.

Any file or folder that doesn't start with an underscore will end up being a
web page visible to users. To add content, simply create a file that doesn't
have a leading underscore.

Jekyll allows you to write content using Markdown, a language that compiles to
HTML. You should probably use Markdown, not HTML, to create content.


#### `post-receive` hook

We're compiling the Jekyll site in production using the `post-receive` Git hook.
A copy of this hook has been added here for posterity's sake. However, if you
make changes to the post-receive in this repo, those changes won't be reflected
in production. You have to copy it there manually.


### Dependencies

This site depends on nginx the TartanHacks site's nginx config. In particular,
it needs to forward traffic coming in through `/crashcourse` to `www/` in this
folder.

Jekyll depends on `ruby` and `gem` being available, preferably at version 2.0 or
higher. It also needs ruby-dev for building native extensions. These
dependencies were met by running

```console
sudo apt-get install ruby ruby-dev
```


## License

MIT License. See LICENSE. (c) 2018 ScottyLabs



[jekyll]: http://jekyllrb.com/
