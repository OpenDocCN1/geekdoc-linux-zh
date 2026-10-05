# startx

The startx command is a shell script used by SuSE Linux to initiate an X11 session. Like the traditional startx command included with XFree86, startx obeys command options, such as color-depth settings (to start a 16-bpp session):

```
# startx --bpp 16
```

However, SuSE, Inc., provides a modified version of startx that can also be used to launch various window managers for an X11 session. For example, to start an X11 session with the afterstep window manager, use startx, as shown in the following:

```
# startx afterstep
```

The default window manager is KDE, but startx can be used to start several types of window managers.

# strings

The strings command outputs all text strings found inside binary programs. This can be useful to view the contents of files when you don't have a viewer program for a file's format or for looking at the contents of a binary program (such as search for help text). For example, use the following code to look at all strings inside the pico editor:

```
# strings /usr/bin/pico < less
```

# su

su enables a user to temporarily become another user. If a user ID is not given, the computer thinks you want to be the superuser, or root. In either case, a shell is spawned that makes the new user—complete with that user ID, group ID, and any supplemental groups of that new user. If you are not root and the user has a password (and the user should!), it prompts for a password. root can become any user at any time without knowing passwords. Technically, the user just needs to have a user ID of 0 (which makes a user superuser) to log on as anyone else without a password.

# sudo

The sudo command is a flexible system for allowing selected users to use selected commands as root, according to the /etc/sudoers file.

# tail

tail prints to standard output the last 10 lines of a given file. If no file is given, it reads from standard input. If more than one file is given, it prints a header consisting of the file's