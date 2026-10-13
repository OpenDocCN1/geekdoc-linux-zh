Table 2.1 Manual page categories.

| Section | Description |
|---|---|
| 1 | User Commands |
| 2 | System Calls |
| 3 | Subroutines |
| 4 | Devices |
| 5 | File Formats |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | System Administration |
| 9 | New |

# info

The info command sets up a structured way to look through different manual pages. When you type the info command, you'll see the set of options shown in Figure 2.3. Move your cursor using your keyboard arrow keys to the option or command of your choice, and press Enter. In most cases, the info utility then takes you to a subsequent screen containing a set of subsidiary options. Continue to choose the desired option until you get to the command manual section that you need.

```
```
File: dir  Node: Top          This is the top of the INFO tree

This (the Directory node) gives a menu of major topics.
Typing "q" exits, "?" lists all Info commands, "d" returns here,
"u" gives a primer for first-timers
"m" (or Return) visits the Emacs topic, etc.

In Emacs, you can click mouse button 2 on a menu item or cross reference
to select it.

* Menu:
Texinfo documentation system      Standalone Info-reading program.
texinfo: (info-texinfo)            The GNU documentation format.
texinfo: (texinfo)                 The GNU documentation format.
install-info: (texinfo)Invoking install-info. Update info/dir entries.
makeinfo: (texinfo)                Translate Texinfo source.
texi2dvi: (texinfo)Format with texi2dvi. Print Texinfo documents.
texindex: (texinfo)Format with texindex. Sort Texinfo index files.

Miscellaneous
Autoconf: (autoconf)               Create source code configuration scripts.
Bfd: (bfd)                         The Binary File Descriptor library.
Binutils: (binutils)               The GNU binary utilities.
Concurrent Versions System
CVSclient: (cvsclient)             The client/server protocol used by CVS
File utilities: (fileutils)        GNU file utilities
Finding Files: (find)              Listing and operating on files
                                   that match certain criteria.
GIT: (git)                         GNU Interactive Tools
GDB: (gdb)                         The GNU debugger.

ESC ESC
```
```

Figure 2.3 Getting structured command help.