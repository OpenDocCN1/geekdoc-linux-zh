To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

# Vim Basics

If you just want to get the hang of it, here’s a bare-bones tutorial.

Vim is a modal editor. All this means is that when you are using vim, the program will behave differently depending on whether you are in command mode or editing mode.

Let’s go. Create and edit a file with vim. On your command line, issue the following:

```
[alberto@digital alberto]$ vim tutorial
~
~
~
"tutorial" [New File]
```

A graphical version of vim can be started from within KDE by issuing the command gvim (graphical vim).

On issuing the command, the editor will take over your terminal. Empty lines are marked by a tilde (~) character. Vim is currently in its command mode. It is waiting for you to tell it what to do.

When in command mode, you can move around the document (assuming there’s some text to navigate, which won’t be the case in a new document) and issue commands. Table 13.1 is a list of all the cursor moving commands. (As you can see, some are mapped to special keys on your keyboard.)