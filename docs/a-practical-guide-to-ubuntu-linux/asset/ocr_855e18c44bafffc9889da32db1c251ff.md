# 140 CHAPTER 4 INTRODUCTION TO UBUNTU LINUX

```
$ sammy: ls --help
File: coreutils.info, Node: Top, Next: Introduction, Up: (dir)
coreutils
***********************************
This manual documents version 7.4 of the GNU core utilities, including
t standard programs for text and file management.

Copyright (1994-1999, 2008-2009) Free Software Foundation, Inc.
Permission is granted to copy, distribute and/or modify thisndocument under the terms of the GNU Free License,
Version 1.3 or any later version published by the Free Software
Foundation with no longer restrictions, with no Back-Cover Texts. A copy of the license is included
in the section entitled "GNU Free Documentation License"

Menu:
Introduction: Caveats, overview, and others.
Common options.
Output of entries files:
coreutils.info --help --
Welcome to coreutils version 4.13. Type H for help, M for menu item.
```

Figure 4-30 The initial screen displayed by the command coreutils

# man and man info display displays complete and up-to-date information on GNU utilities than man. When a man page displays abbreviated information on a utility that is covered by info, the man page refers to info. The man utility frequently displays the only information available on non-GNU utilities. When info displays information on non-GNU utilities, it is frequently a copy of the man page.

Because the information on this screen is drawn from an editable file, the page may differ from the screens shown in this section. You can press any of the following-keys while the initial screen is displayed:

+   * h to go through an interactive tutorial on info
* ? to list commands
* SPACE to scroll through the menu of items for which information is available
* m followed by the name of the menu you want to display or a SPACE to display a list of menus
* q or CONTROL-C to quit

The notation info uses to describe keyboard keys may not be familiar to you. The notation C-h is same as CONTROL-H. Similarly, M-x means hold the META or ALT key and press x. (On some systems you need to press ESCAPE and then duplicate the function of META-X).

After giving the command coreutils, press the SPACE bar a few times to scroll through the display. Type sleepRETURN search for the string sleep. When you type /, the cursor moves to the bottom line of the window and displays Search for string [string], where string is the last string you searched. Press RETURN to search for string or enter the string you want to search. Typing displays sleep on that line, and pressing RETURN displays the next occurrence of sleep.