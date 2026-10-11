```
# echodate translations into pig Latin
# Copyright (C) 2004 Prentice-Hall
# This file is distributed under the same license as the echodate package.
# Arnold Robbins <arnold@example.com> 2004
#
# # fuzzy
msgid ""
msgstr ""
"Project-Id-Version: echodate 1.0\n"
"Report-Msgid-Bugs-To: arnold@example.com\n"
"POT-Creation-Date: 2003-07-14 18:46+0000\n"
"PO-Revision-Date: 2003-07-14 19:00+0\n"
"Last-Translator: Arnold Robbins <arnold@example.com>\n"
"Language-Team: Pig Latin <piglist@li.example.org>\n"
"MIME-Version: 1.0\n"
"Content-Type: text/plain; charset=ASCII\n"
"Content-Transfer-Encoding: 8bit"

# : ch13-echodate.c:19
msgid "Enter a Date/Time as YYYY/MM/DD HH:MM:SS : "
msgstr "Entera Atoday/Imeatay YYYY/MM/DD HH:MM:SS : "

# : ch13-echodate.c:32
#. c-format
msgid "Got: %s"
msgstr "Otgya: %s"
```

While it would be possible to do a linear search directly in the portable object file, such a search would be slow. For example, `awk` has approximately 350 separate messages, and the GNU coreutils have over 670. Linear searching a file with hundreds of messages would be noticeably slow. Therefore, GNU gettext uses a binary format for fast message lookup. `msgfmt` does the compilation, producing a *message object* file:

```
$ msgfmt piglat.po -o piglat.mo
```

As program maintenance is done, the strings used by a program change: new strings are added, others are deleted or changed. At the very least, a string's location in the source file may move around. Thus, translation `.po` files will likely get out of date. The `msgmerge` program merges an old translation file with a new `.pot` file. The result can then be updated. This example does a merge and then recompiles:

```
$ msgmerge piglat.po echodate.pot -o piglat.new.po  *Merge files*
$ mv piglat.new.po piglat.po  *Rename the result*
$ vi piglat.po  *Bring translations up to date*
$ msgfmt piglat.po -o piglat.mo  *Recreate .mo file*
```

Compiled `.mo` files are placed in the file `base/locale/category/textdomain.mo`. On GNU/Linux systems, `base` is `/usr/share/locale`. `locale` is the language, such as `es`, `fr`, and so on. `category` is a locale category; for messages, it is LC_MESSAGES.