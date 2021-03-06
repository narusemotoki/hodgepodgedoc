=======================
GitHub Pages and Sphinx
=======================
This document is hosted on GitHub Pages. GitHub Pages is possible to host a static file, it's good to Sphinx. Sphinx is documentation tool, this document is also using the Sphinx.

Here I will documenting how to publish a document on GitHub which was made by Sphinx.

This document is written how to write a document in English, to be translated in Japanese. If you wish a different language, please substitute each en, ja, Engilish and Japanese.

------
Sphinx
------

Install Sphinx
==============
If you use Ubuntu, execute the commands below. Other OS users, please run the equivalent command.

::

  $ sudo apt-get install gettext
  $ sudo easy_install sphinx-gettext-helper sphinx

Create project
==============
Sphinx has the setup command. Please execute this.

::

   $ sphinx-quickstart

When you execute this, the program will have a few questions, and then responded to it.
I answered [y] only this question, and using default others.

::

    You have two options for placing the build directory for Sphinx output.
    Either, you use a directory "_build" within the root path, or you separate
    "source" and "build" directories within the root path.
    > Separate source and build directories (y/N) [n]:

It will be structured as below.

::

   .
   ├── Makefile
   ├── build
   ├── make.bat
   └── source
        ├── _static
        ├── _templates
        ├── conf.py
        └── index.rst

Multilingual
============
Change in order to extract the documentation in multiple languages​​.

in Makefile

Add under the "# Internal variables".

::

    ENSPHINXOPTS   = -d $(BUILDDIR)/doctrees $(PAPEROPT_$(PAPER)) -D language=en source
    JASPHINXOPTS   = -d $(BUILDDIR)/doctrees $(PAPEROPT_$(PAPER)) -D language=ja source
    HTMLSPHINXOPTS   = -d $(BUILDDIR)/doctrees $(PAPEROPT_$(PAPER)) source

Rewrite the section "html:".

::

    html:
            $(SPHINXBUILD) -b html $(ENSPHINXOPTS) $(BUILDDIR)/html/en
            $(SPHINXBUILD) -b html $(JASPHINXOPTS) $(BUILDDIR)/html/ja
            @echo
            @echo "Build finished. The HTML pages are in $(BUILDDIR)/html/$(LANGUAGE)."

Add generate.

::

    generate:
            rm -rf $(BUILDDIR)/*
            $(SPHINXBUILD) -b gettext $(I18NSPHINXOPTS) $(BUILDDIR)/locale
            cd source; sphinx-gettext-helper -p ../$(BUILDDIR)/locale --update --build --statistics -l ja
            $(SPHINXBUILD) -b html $(ENSPHINXOPTS) $(BUILDDIR)/html/en
            $(SPHINXBUILD) -b html $(JASPHINXOPTS) $(BUILDDIR)/html/ja

Please note that you must use the tab to indent a Makefile. Sorry, I don't use Windows, I don't know how to write make.bat.

Write documentation
===================
Make a \*.rst file in the source directory, write in reStructuredText format. Please refer to external websites for reStructuredText. Will write the English in rst file. And then will run this command.

::

    $ make generate

Then locale directory is created, and translation file (\*.mo) is generated in it. Will write in this way to this file.

::

    msgid "This document generated by Sphinx."
    msgstr "このドキュメントはSphinxによって生成されました。"

Will run this command again.

::

    $ make generate

Please check the build/html/en and build/html/ja. Document has been generated. We repeat this procedure.

1. write a rst file
2. run "$ make generate"
3. write a mo file
4. run "$ make generate"
5. check the HTML
6. return to 1

Please make sure that if it is no longer reflected in the HTML, you do not erase incorrectly the msgid or msgstr.
Also, if "#, fuzzy" is written, you must erase it. This indicates that there is a possibility that the source is changed, must be re-translation.

------------
GitHub Pages
------------
