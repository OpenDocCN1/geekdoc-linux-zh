```
-v/f/sh.vim fooscript
1 #!/bin/bash
2
3 # Script to test editing with vim
4














  "fooscript" 4L, 48C                          4,0-1  All
```

# Displaying a buffer in tabs

We can open files in tabs, too. It works much like the :e command. To open a file in a tab, we type :tabe followed by the name of the file.

Switching tabs is easy. To cycle through the tabs forward, we type gt. To cycle backwards, we type GT. If support is enabled, tabs can be selected by clicking on them and new tabs can be opened by double clicking on the tab bar at the top of the screen.

It's also possible to start vim with multiple files loaded in tabs adding the -p option to the command line. For example:

```
@melinuxbox ~]$ vim -p file1 file2
```

To close tabs, we use :q command just closing a window. When only one tab remains, vim leaves tabbed mode and the display returns to its usual state.

There are a lot of tab-related features in vim. See the help topic for full details.

**Help topics:** tabpage

# Color Schemes

vim if we return to the buffer containing our shell script, we would see the effects of our sh.vim file. When syntax highlighting is turned on (:syn on will do the trick) it assumes the current color scheme. Vim ships with a different of ones. To see the name of the current scheme, type this command:

162 Vim, with Vigor