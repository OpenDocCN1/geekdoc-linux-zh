If you want to create an xterm session from within the `.xinitrc` file (you will need an xterm or other utility to start other tasks within XFree86), add the following line:

```bash
xterm -e /bin/bash
```

In this case, the `bash` shell is invoked within the xterm. You can, of course, use any shell you want.

If you create `.xinitrc` files for your own use, place them in your home directory. You can, for example, use a `.xinitrc` file like this:

```bash
#!/bin/sh

xterm -fn 7x13bold -geometry 80x32+10+10 &
xterm -fn 7x13bold -geometry 80x32+30+50 &
oclock -geometry 70x70-7+7 &
xsetroot -solid SteelBlue &
exec fvwm
```

This starts two xterms and the clock and places them on the desktop, then sets the background color to steel blue and finally starts the desktop manager. Two important notes: The last command in the script is preceded by the `exec` command and the last command is not sent to background. If you send the last command to background or forget the `exec` command, X starts up, and then immediately shuts down!

# # Summary

All of the previous steps will help you set up XFree86 properly, and after following them your XFree86 session should start up without a problem. The specifics of working with X are beyond the scope of this book. If you are not sure how to use X, check the documentation files that came with the release or consult a user-oriented book.

However, if you followed the steps outlined previously, your X system should now be functional and you can start working with the X system as your primary interface to Linux. After you've worked in X, it's hard to go back to character-based terminals!

From here, there are a number of chapters that you can go to that are related to this topic:

Wabi, a way to run Windows applications under Linux, is discussed in Chapter 23, “Wabi.”

Ghostscript, which lets you see PostScript files onscreen and send them to the printer, is discussed in Chapter 24, “Ghostscript and Ghostview.”

Programming under Linux is discussed in Part V, starting with Chapter 25, “gawk.”

System administration is discussed in Part VI, starting with Chapter 32, “System Administration Basics.”