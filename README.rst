=============
Hodgepodgedoc
=============

http://narusemotoki.github.io/hodgepodgedoc/en/index.html
http://narusemotoki.github.io/hodgepodgedoc/ja/index.html

Setup
=====
::

  $ sudo apt-get install gettext
  $ sudo easy_install sphinx-gettext-helper sphinx

Documentation
=============

Create source
-------------
You will write in English under the source directory.
Use reStructuredText.

Preparation of translation
--------------------------

source/*.rst -- generate --> locale/ja/LC_MESSAGES/*.po
::

  $ make generate

Translate
---------

Don't need the translation English, because English makes use of the source. You translate from English to Japanese in locale/ja/LC_MESSAGES/\*.po

Generate an HTML
----------------
::

  $ make genetate

You try to check build/html
