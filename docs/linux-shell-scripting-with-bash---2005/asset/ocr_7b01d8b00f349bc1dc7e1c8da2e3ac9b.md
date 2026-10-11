Other useful switches include:

+   - -cursor—Shows or hides the input cursor
+   - -repeat—Turns a console's keyboard repeating on or off
+   - -appcrskeys—Turns cursor key application mode on or off
+   - -linewrap—Turns a console's line wrapping on or off

These can be turned on or off. For example, to hide the input cursor, type this

```
$ setterm -cursor off
```

There are other attributes to control features like power saving and Tab usage. See the reference section at the end of this chapter for a complete list of switches.

# tput

You can use the `setterm` command for any terminal display, but an attempt to use a feature specific to the console is ignored. Instead, there is an old command called `tput` (*terminal put*) that works much the same as `setterm` but works with all text-only displays.

`tput` has one parameter; a screen attribute code based on the `terminfo` terminal database. These codes are different from the `setterm` switches. You can find a complete list on the `terminfo` manual page (`$ man 5 terminfo`).

```
$ tput cols # width of display
80
$ tput clear # clear the screen
```

# select Menus

The built-in `select` command creates simple menus. `select` is a special loop. The command is followed by a list of arguments and displays them as numbered options. When the user selects an item by typing that number, the argument is assigned to the `select` variable and the commands inside the `select` statement are executed. See Listing 13.1.

```
Listing 13.1 select_demo.sh
#!/bin/bash
# # select_demo.sh: a simple select menu
#
shopt -s -o nounset

declare -i
SCRIPT=${0##*/}

printf "\$\n" "Select a document type:"
```