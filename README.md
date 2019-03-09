Source Files for the Outdex Blog
================================

This repository holds the source files for the Outdex blog.
The `master` branch holds the source files, the gh-pages branch is used for the output files.
The source files are simple markdown files that are automatically converted to HTML via [Pelican](http://docs.getpelican.com/), a static website generator implemented in Python.
They are then uploaded to Github with [ghp-import](https://github.com/davisp/ghp-import).


System Requirements
-------------------

If you want to generate the website from the source files, you need all of the following.

1.  Recent version of Python3.

1.  Pelican 4.0 or higher.
    
    - Linux users might already have it their repository.
    - On OSX and Windows (and Linux, if necessary) you can install Pelican via Python's package manager `pip` (but see the next section on how to use `pip` in a smarter way).

    ~~~~~
    pip install pelican
    ~~~~~

1.  The ghp-import script.
    Again you can install it via pip

    ~~~~~
    pip install ghp-import
    ~~~~~

    or use your package manager if you're on Linux.

1.  A number of Python3 libraries:
    - `pygments`, version 2.3 or higher
    - `typogrify` library, version 2.0.7 or higher
    - *beautifulsoup4*; in Debian, the library is called `python3-bs4`

    As before, use pip or your package manager to install these dependencies.

1.  At least version 2.2 of `pandoc` and 0.14 of `pandoc-citeproc`.
    Linux users should definitely install those from their repositories.
    Everybody else is referred to [pandoc's install guide](https://pandoc.org/installing.html).

1.  A recent-ish version of the `make` tool.
    This is usually already installed on Linux and OSX.
    If it isn't, make sure you have the basic tools for compiling software installed.
    On Debian and Ubuntu, the following should work:

    ~~~~
    sudo aptitutde install build-essential
    ~~~~

    On Windows, install [GnuWin32](http://gnuwin32.sourceforge.net/packages/make.htm) or [MinGW](http://www.mingw.org/).
    The `make` binary also has to be in your PATH, which happens automatically on Linux and OSX but not Windows.
    

A Note on `pip` Installations
------------------------------

Python's `pip` has the nasty habit of scattering the install files across various system folders.
A better solution is to create a *virtual environment* in your home directory that holds all the files related to working with pelican:

~~~~~
mkdir ~/.outdex_env
virtualenv -p python3 ~/.outdex_env
~/.outdex_env/bin/pip3 install pelican ghp-import
~~~~~

You then have to make the pelican script accessible through your shell, either by adding `~/.outdex_env` to your PATH or by symlinking it to a folder in your PATH (e.g. `/usr/local/bin` or `~/bin`).

If that sounds like too much of a hassle, install `pipsi`, which automatically creates and manages virtual environments.


File Structure
--------------

Once you've cloned the repository, you'll see a couple of files and folders.
The most important ones are:

- *content*: the markdown files for the website
- *output*: the actual website generated by Pelican
- *pelicanconf.py*: contains various settings for site creation; do not change unless you know what you're doing
- *publishconf.py*: allows you to override certain settings in the final creation phase; do not change unless you know what you're doing
- *Makefile*: set of instructions for building the website


Workflow
--------

Creating a new post is easy.

1.  Go to the folder *content* and then the folder for the appropriate category (`Discussions`, `News`, or `Tutorials`).
1.  Create a new markdown file.
1.  Make sure the markdown file starts with a well-formed header with the first few lines consisting of
    - `Title:`,
    - `Author:`, (or `Authors:` if there's multiple; name should be comma-separated)
    - `Date:` (in format YYYY-MM-DD),
    - `Tags:` (comma-separated list),
    - finally, an empty line.

To test things locally before you upload them, you have to

1.  open a terminal and navigate to the root folder of the repository (the one with *pelicanconf.py*),
1.  run `make devserver`, and
1.  open a browser and load [http://localhost:8000](http://localhost:8000).

If everything is fine, kill the server process to end the testing phase.
Now only two things remain to be done:

1.  upload the website by running `make github`, and
1.  sync the source files to the repository:
    - `git add .`
    - `git commit`
    - `git push origin master`

To Do
-----

- [ ] set up email for submissions
- [ ] fix summary breaking math; should always end immediately after first paragraph
- [ ] maybe switch commenting system to `staticman`?
- [ ] expand pandoc reader to handle Pelican's `{filename}`-hooks
- [ ] adapt filter for pandoc to automatically include tikz and forest code as svgs
- [ ] design pandoc filter for converting glossed examples to HTML tables
- [ ] Categories should not be treated as tags
- [ ] automatically convert posts to PDF and embed download link
- [ ] create favicon from logo
