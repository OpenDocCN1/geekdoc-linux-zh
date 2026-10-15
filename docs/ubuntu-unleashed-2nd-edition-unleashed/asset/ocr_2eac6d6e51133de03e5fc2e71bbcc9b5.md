In this example, x will not start: You don’t see a desktop displayed, nor does the computer seem to respond to keyboard input. The X server might either be hung in a loop, repeatedly failing, or might exit to a shell prompt with or without an error message.

The X server only attempts to restart itself in runlevel 2, so to determine whether the X server is hung in a loop, try switching to runlevel 1.

# TIP

If you are working on a multi-user system and might inadvertently interrupt the work of other users, ask them to save their current work; then change to a safer runlevel, such as single user mode.

Change to runlevel 1 by running the command telinit 1. This switch to runlevel 1 will stop the X server from attempting to restart itself.

Now you can easily examine the error and attempt to fix it.

First, try to start the X server “naked” (without also launching the window manager). If you are successful, you will get a gray screen with a large X in the middle. If so, kill X with the Ctrl+Alt+Backspace key combination, and look at your window manager configuration. (This configuration varies according to which window manager you have chosen.)

Let us assume that X won’t run “naked.” If we look at the log file for Xorg (it’s clearly identified in the /var/log directory), we’ll pay attention to any line that begins with (EE), the special error code. We can also examine the error log file, .xsession-error, in our home directory if such a file exists.

If we find an error line, the cause of the error might or might not be apparent to us. The nice thing about the Linux community is that it is very unlikely that you are the first person to experience that error. Enter the error message (or better, a unique part of it) into http://www.google.com/linux and discover what others have had to say about the problem. You might need to adjust your search to yield usable results, but that level of detail is beyond the scope of this chapter. Make adjustments and retest as before until you achieve success.

Fix the X configuration and start X with startx. Repeat as necessary.

# CAUTION

Before making any changes to any configuration file, always make a backup copy of the original, unmodified file. Our practice is to append the extension .original to the copy because that is a unique and unambiguous identifier.

If you need to restore the original configuration file, do not rename it, but copy it back to its original name.