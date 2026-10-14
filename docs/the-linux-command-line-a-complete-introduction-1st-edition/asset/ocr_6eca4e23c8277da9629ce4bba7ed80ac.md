A screen like this should appear:

```
~
~
~               VIM - Vi Improved
~               version 7.1.138
~               by Bram Moolenaar et al.
~               Vim is open source and freely distributable
~               Sponsor Vim development!
~               type :help sponsor<Enter>    for information
~               type :q<Enter>                to exit
~               type :help<Enter> or <F1>      for on-line help
~               type :help version<Enter> for version info
~               Running in Vi compatible mode
~               type :set nocompatible      for Vim defaults
~               type :help cp-default<Enter> for info on this
~
```

Just as we did with nano earlier, the first thing to learn is how to exit. To exit, we enter the following command (note that the colon character is part of the command):

```
:q
```

The shell prompt should return. If, for some reason, vi will not quit (usually because we made a change to a file that has not yet been saved), we can tell vi that we really mean it by adding an exclamation point to the command:

```
:q!
```

*Note: If you get "lost" in vi, try pressing the ESC key twice to find your way again.*

# Editing Modes

Let’s start up vi again, this time passing to it the name of a nonexistent file. This is how we can create a new file with vi:

```
[me@linuxbox ~]$ rm -f foo.txt
[me@linuxbox ~]$ vi foo.txt
```