
# rxvt

rxvt is a color-capable, memory-efficient terminal emulator for X11 with nearly all of the features of the xterm client and additional features, such as background pixmap support for the terminal window. Its name is now wterm, and it can be started in the background:

```
# wterm &
```

# sax

The sax command is used to configure XFree86 and generate a working XF86Config configuration file for SuSE Linux. Because the SuSE 6.2 installation does not configure X11, the root operator must run sax for the first time from the console to configure X11. Later, the sax command can be used during an X11 session, and it can be launched from an X11 terminal window to fine-tune any settings.

# sed

This is the stream editor, a non-interactive text editor designed to change or manipulate streams of text. The sed command can be used to perform global search-and-replace operations on streams of text (through pipes, example).

```
# cat employees.txt | sed 's/Bill/William/g' >newemployees.txt
```

This changes all instances of Bill to William in the original file and creates a new file.

# sendfax

Use this to send fax documents. The sendfax program, part of the mget+sendfax software package, dials out and sends prepared fax-format graphics documents. This program is usually run by the fax spool shell script.

# set

The set command is used to change an environment variable. In some shells, the set -o vi command allows you to bring back previous commands you have in your history file. It is common to place the set command in your .profile. Some environment variables require an equals sign, and some, as in the example set -o vi, do not.

# setfdprm

setfdprm sets floppy drive parameters. This command, most often run by the root operator, is used to set the current floppy device, usually in preparation for a low-level format.

# setserial

The setserial command is used to configure or fine-tune specific serial ports in your computer. This command can also be used to report on a serial port's status or identity.

# shutdown

The shutdown command is used to shut down (halt) or reboot SuSE Linux. For example, to shut down the system immediately, use

```
# shutdown -h 0
```

or

```
# shutdown -h now
```

You can also use the -t option to specify a number of seconds and the -r option to reboot:

```
# shutdown -t 60 -r
```

By including a text message on the command, you can also add a message to be sent to all users of your system. See the shutdown man page for more information.

# slrn

A news reading program, the slrn newsreader provides an easy-to-use interface for Usenet news. It has some advantages over the tin newsreader by providing custom colors for different parts of messages and support for mouse clicks and function keys.

# sort

The sort command comes in handy whenever you need to generate alphabetical lists of the information from your files. Information can also be listed in reverse order. See the sort manual page for more information.

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

tail prints to standard output the last 10 lines of a given file. If no file is given, it reads from standard input. If more than one file is given, it prints a header consisting of the file's name enclosed in left and right arrows (== <>) before the output of each file. The default value of ten 10 lines can be changed by placing a # in the command. The syntax for the command follows:

```
tail [-# of lines to see] [<filename(s)]
```

# talk

The talk command is used to have a "visual" discussion with someone else over a terminal. The basic idea behind this visual discussion is that your input is copied to the other person's terminal, and the other person's input is copied to your terminal. Thus, both people involved in the discussion see the input from both themselves and the other person.

# taper

A tape archiving and backup program, the taper command features a friendly interface to the tar and gzip programs to provide archive backups and compression.

# tar

tar is an archiving program designed to store and extract files from an archive file. A tarred file (called a tar file) can be archived to any medium, including a tape drive or a hard drive. The syntax of a tar command is tar <action> <optionalfunctions> <file(s)/directory(ies). If the last parameter is a directory, all subdirectories under the directory are also stored.

# tcsh

This enhanced csh shell has all the features of the csh shell with many improvements, such as command-line editing, job control, and command history. This shell is run by the symbolic link (csh) found under the /bin directory.

# telnet

Start and run a Telnet session with telnet. You can use the telnet command to log in to remote computer systems, to run programs, or to retrieve data.

# tin

This is a Usenet news reading program. The tin newsreader, like the slrn newsreader, provides a menu for reading Usenet news, allowing you to quickly browse, save, post, or reply to messages found in a specific Usenet newsgroup. The tin reader looks for a list of desired newsgroups in the .newsrc file in your home directory and can be started from the command line of your console or terminal window:

```
# tin -nqr
```

# top

You can display CPU processes with the top command. This command can be used to print the most active or system resource-intensive processes or programs.

# touch

You can use the touch command to create a file or update its timestamp.

# tput

Change or reset terminal settings. The tput command, found under the /usr/bin directory, uses terminal capabilities found in the terminfo database under the /usr/lib directory. This database contains character sequences recognized by different terminals. You can use tput in a variety of ways. One handy feature is the reset option, which can help you clear a terminal window if your display becomes munged because of spurious control codes echoed to the screen.

# tr

The tr command is used to transliterate characters from the standard input. The tr command, a text filter, translates sets of characters you specify on the command line. The classic example is to translate a text file from all uppercase to lowercase:

```
# cat uppercase.txt ; tr A-Z a-z lowercase.txt
```

# twm

This is the Tab window manager for X11 from which the fwm window manager and others are descended. Although this window manager does not support virtual desktops, you can customize its menus and windows. The twm window manager is usually started from the contents of your .xinitrc in your home directory.

# ulimit

Show resource limit settings with ulimit. This is a built-in command for the bash or ksh shell and can be used to set limits on a number of system resources. This command is similar to the limit command of the tsh or csh shells.
