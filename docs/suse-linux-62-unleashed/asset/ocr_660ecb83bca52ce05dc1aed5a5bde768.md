# Appendixes
PART V

list of desired newsgroups in the .newsrc file in your home directory and can be started
from the command line of your console or terminal window:

```
# tin -nqr
```

# top

You can display CPU processes with the top command. This command can be used to print
the most active or system resource-intensive processes or programs.

# touch

You can use the touch command to create a file or update its timestamp.

# tput

Change or reset terminal settings. The tput command, found under the /usr/bin directory,\uses terminal capabilities found in the terminfo database under the /usr/lib directory.
This database contains character sequences recognized by different terminals. You can use
tput in a variety of ways. One handy feature is the reset option, which can help you clear
um a terminal window if your display becomes munged because of spurious control codes
echoed to the screen.

# tr

The tr command is used to transliterate characters from the standard input. The tr
command, a text filter, translates sets of characters you specify on the command line. The
classic example is to translate a text file from all uppercase to lowercase:

```
# cat uppercase.txt ; tr A-Z a-z lowercase.txt
```

# twm

This is the Tab window manager for X11 from which the fwm window manager and others
are descended. Although this window manager does not support virtual desktops, you can
customize its menus and windows. The twm window manager is usually started from the
contents of your .xinitrc in your home directory.

# ulimit

Show resource limit settings with ulimit. This is a built-in command for the bash or ksh
shell and can be used to set limits on a number of system resources. This command is
similar to the limit command of the tsh or csh shells.