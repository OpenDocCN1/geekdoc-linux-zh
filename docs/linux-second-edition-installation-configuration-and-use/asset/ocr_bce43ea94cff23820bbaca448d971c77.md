# ALPHABETICAL COMMAND REFERENCE 479

# set

set displays all variables known to the shell (including the environment variables which can be displayed with printenv). set -x causes the bash to display, prior to the execution of each command, the internal command line after resolution of alias abbreviations and file name expansion. set is not a Linux command, but a command of the bash shell.

# setfont charset

setfont reads a character set file from the /usr/lib/kbd/consolefonts directory and activates this character set in the VGA text mode, setfont cannot be used over X. Using character sets are default8x16 (for 25-line text mode) and default8x9 (for 50-line text mode).

# setterm [option]

setterm allows you to modify various terminal settings. When the command is executed without specifying an option, it displays a list of all possible options. Important options:

+   -blank n activates the screen saver after n minutes without input activity.

+   -clear clears the screen.

+   -inverscreen on or off inverts the screen display (black text on a white background) or reverts to the normal setting.

Some additional options which are of interest in shell programming (changes to letter types, and so on) are described on page 432.

# shutdown [options] time [message]

shutdown is the safest way to terminate Linux. You must specify either a time of day (hh:mm), the number of minutes from the current time of day onward (+m) or the keyword now (that is, immediately). shutdown can only be executed by root. Often Linux is configured in such a way that users without root privileges can restart the computer with [Alt]+[Ctrl]+Del.

shutdown informs all others that the system is going to be shut down shortly and no longer allow new logins. Subsequently, all processes are warned that they will be stopped shortly. Some programs (such as emacs, vi ...) react to this warning by saving all open files in backup copies.

+   -c aborts an already started shutdown process (provided this is still possible).

+   -f same as -n, but faster.