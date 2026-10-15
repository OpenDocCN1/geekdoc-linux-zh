
# EXPLANATION (CONTINUED)

+   6 Ends the pathmunge definition.
+   7 If the user's UID equals 0 (in other words, if he or she is a superuser), then . . .
+   8 . . . calls the pathmunge() function, which adds the /sbin directory to the PATH.
+   9 Adds the /usr/sbin directory to the PATH.
+   10 Adds the /usr/local/sbin directory to the PATH.
+   11 Adds the /usr/X11R6/bin directory to the end of the PATH. Because this line is not inside the if statement, it will always be executed.
+   12 Removes the pathmunge() function definition from memory.
+   13 Sets the maximum coredump size to 0—this effectively stops the user from generating coredump files.
+   14 Sets the USER variable to the user's login name.
+   15 Sets the LOGNAME variable to the same value as USER.
+   16 Sets the MAIL variable to the user's incoming mailbox file.
+   17 Sets the HOSTNAME variable to this system's hostname.
+   18 Sets the history list size to a maximum of 1,000 commands.
+   19 If the INPUTRC variable has no value and $HOME/.inputrc does not exist, then sets the INPUTRC variable to /etc/inputrc.
+   20 Exports all variables set in this script.
+   21 This for loop will cycle through all the files in the /etc/profile.d directory.
+   22 If the user has read permission on the file currently being processed by the for loop . . .
+   23 . . . then source the file.

/etc/bashrc. The /etc/bashrc file is used on some UNIX releases, such as Red Hat Linux, to run bash commands whenever a bash shell is run. This file should contain settings that are not passed automatically to child processes, such as command aliases.

## EXAMPLE 16.19

```
1 $ cat /etc/bashrc
2 alias ls="ls -F"
3 alias grep="grep -i"
```

## EXPLANATION

+   1 The contents of the /etc/bashrc file are displayed.
+   2 An alias for the ls command is defined as ls -F. When ls is typed, ls -F will be executed, modifying the display of ls.
+   3 An alias for the grep command is defined as grep -i. When the grep command is used, it will be case insensitive.

If you wish to use /etc/bashrc and your UNIX doesn't source it automatically, you can include it in the user's personal .bashrc file in his or her home directory.

## EXAMPLE 16.20

```
1  $ cat .bashrc
2  if [ -f /etc/bashrc ]
    then
3      . /etc/bashrc
    fi
4  alias dir=ls
```

## EXPLANATION

+   1 The .bashrc file, found in the user's home directory, is sourced.
+   2 If the /etc/bashrc file exists and is a regular file, then go to line 3. Some machines run /etc/bashrc automatically; on those machines this if statement will not be required.
+   3 The dot command sources the /etc/bashrc file (runs the commands from the file in context of the current shell process; i.e., does not create a child process).
+   4 An alias for the dir command is defined. Notice that this is a personal alias created by the user in his .bashrc file.

/etc/csh.login. The /etc/csh.login file is sourced by the C and TC shells during the login process. Example 16.21 is an /etc/csh.login file from a Red Hat Linux system. Like the .login file, this file is run at login time by the login shell, and not by any child shells spawned thereafter. It is used to set environment variables for the shell and any other commands that will be executed by the login shell.

## EXAMPLE 16.21

```
# cat /etc/csh.login
# System-wide environment and startup programs, for login setup
1 if ($?PATH) then
2     setenv PATH "$PATH:/usr/X11R6/bin"
else
3     setenv PATH "/bin:/usr/bin:/usr/local/bin:/usr/X11R6/bin"
endif
4 limit coredumpsize unlimited
5 setenv HOSTNAME `/bin/hostname`
6 set history=1000
7 if ( -f $HOME/.inputrc ) then
8     setenv INPUTRC /etc/inputrc
endif
```

## EXAMPLE 16.21 (CONTINUED)

```
9 if ( $?tcsh ) then
10   bindkey "^[[3~" delete-char
    endif
```

## EXPLANATION

+   1 If the PATH variable has been set, the ? evaluates to true.
+   2 /usr/X11R6/bin is added to the PATH environment variable.
+   3 Otherwise, the PATH is assigned an initial value of /bin:/usr/bin:/usr/local/bin:/usr/X11R6/bin.
+   4 The limit command restricts an upper limit on the size of a coredump.
+   5 The HOSTNAME variable is assigned the output of the hostname command, the system's hostname.
+   6 The history list size is set to a maximum of 1,000 commands.
+   7 The .inputrc file sets editing modes, key bindings, and so forth for the Readline library. This line checks to see if $HOME/.inputrc exists.
+   8 If $HOME/.inputrc does exist, then set the INPUTRC variable to /etc/inputrc.
+   9 If tcsh is the current shell, ? will return true, and line 10 will be executed.
+   10 The bindkey command sets an escape sequence for the Delete key used in command-line editing.

/etc/csh.cshrc. The /etc/csh.cshrc file is sourced by the C and TC shells whenever they are run. C and TC shells can be started at login time (if it has been specified as a user's login shell) when running a C or TC shell script, or when opening a shell window that runs the C or TC shell. The example /etc/csh.cshrc file given below is from a Red Hat Linux system. The /etc/csh.cshrc file should include items that are not exported to child processes, such as setting a umask or setting the prompt. Note that in the C and TC shell the prompt variable is local, which means it will not be passed to child processes.

## EXAMPLE 16.22

```
# cat /etc/csh.cshrc
1 umask 022
2 if ($?prompt) then
3   if ($?tcsh) then
4     set prompt='[\$\$@\$\%] '
5   else
    set prompt='\! -n\u @'hostname -s'\!'
  endif
endif
```
