# EXPLANATION (CONTINUED)

7 The cdpath variable is assigned a list of path elements. When changing directories, if you specify just the directory name, and that directory is not a subdirectory directly below the current working directory, the shell will search the cdpath directory entries to see if it can find the directory in any of those locations and then will change the directory.

8 The ignoreeof variable prevents you from logging out with ^D. UNIX utilities that accept input from the keyboard, such as the mail program, are terminated by pressing ^D. Often, on a slow system, the user will be tempted to press ^D more than once. The first time, the mail program would be terminated, the second time, the user is logged out. By setting ignoreeof, you are required to type logout to log out.

9 The aliases are set to give a shorthand notation for a single command or group of commands. Now when you type the alias, the command(s) assigned to it will be executed. The alias for the more command is m. Every time you type m, the more command is executed. The status alias prints the date and a summary of the user's disk usage. The cd alias creates a new prompt every time the user changes directory. The new prompt will contain the number of the current history event (\!) and the current working directory, $cwd surrounded by < > (see "Aliases" on page 418).

# The .login File.

The .login file is executed one time when you first log in. It normally contains environment variables and terminal settings. It is the file where window applications are usually started. Because environment variables are inherited by processes spawned from this shell and only need to be set once, and terminal settings do not have to be reset for every process, those settings belong in the .login file.

# EXAMPLE 9.2

```
(The .login File)
1 stty -istrip
2 stty erase ^h
3 stty kill ^u
#
# If possible start the windows system.
# Give a user a chance to bail out
#
4 if ( $TERM == "linux" ) then
5     echo "Starting X windows. Press Ctrl-C \
to exit within the next 5 seconds "
    sleep 5
    startx
6 endif
7 
8 set autologout=60
```