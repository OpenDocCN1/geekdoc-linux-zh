The whatis command might be able to help you quickly find out what a program is with a summary line derived from the program's manual page. For example, to find out what is who, you can enter the following:

```
# whatis who
```

Your screen clears, and the whatis command displays a summary like so:

```
who (1)  - show who is logged on
```

Press Q to quit the whatis command. However, unlike the locate command, you must first build a database of the command summaries with the makewhatis command, which is found under the /usr/sbin directory. To do this, make sure you're logged in as root, and enter the following:

```
# makewhatis
```

The makewhatis command, like the updatedb command, takes a few minutes to build the whatis database, which is called whatis and is found under the /usr/man/man1 directory. The makewhatis command has several options but does not have a manual page. To see a quick summary, use the following:

```
# makewhatis -?
```

You need to periodically update the whatis database to keep track of any newly installed programs. See Hour 24 for tips on how to make OpenLinux do this automatically.

Now you see how whereis and whatis can help you find programs or figure out what they do. But what if you want to do something but can't remember which program does what? In this case, you can turn to the apropos command.

For example, if you can't remember which command searches for files, you can enter the following:

```
# apropos search
```

```
apropos (1)      - search the whatis database for strings
badblocks (8)    - search a device for bad blocks
bsearch (3)      - binary search of a sorted array
conflict (8)     - search for alias/password conflicts
find (1)         - search for files in a directory hierarchy
hcreate, hdestroy, hsearch (3) - hash table management
lfind, lsearch (3) - linear search of an array
lkbdb (1)        - search bibliographic databases
lookbib (1)      - search bibliographic databases
lsearch (n)      - See if a list contains a particular element
manpath (1)      - determine user's search path for man pages
strbrk (3)       - search a string for any of a set of characters
strspn, strcspn (3) - search a string for a set of characters
tsearch, tfind, tdelete, twalk (3) - manage a binary tree
```

![](bbox=[0.9, 0.5, 1.0, 0.7])