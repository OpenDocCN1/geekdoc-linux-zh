# finger 373

+   - Terminal name (prepended with an asterisk*) if you write permission is denied).
- Idle time.
- Login time.
- Host name if logged in remotely.

The following example shows the output from the finger command with no arguments.

```
castle% finger
Login             Name            TTY      Idle    When    Where
winsor             ???         console  Thu 15:38 :0
castle%
```

Idle time is displayed in minutes if it is a single integer, in hours and if a colon (:) is present, or in days if a d is present.

When you specify one or more username arguments, more detailed information is shown for each user, whether the user is logged in or not read mail. username must be that of a local user and can be a first or last name or an account name. Information is presented in multiline format follows:

+   - The user's full name.
- The user's home directory and login shell.
- The user logged in if currently logged in or the time user last logged in, and the terminal from which the user logged in.
- Last time the user received mail and the last time the user read mail.
- The first line of the $HOME/.project file if it exists.
- The contents of the $HOME/.plan file if it exists.

> Note — When the comment (GECOS) field in /etc/passwd includes a comma, finger does not display the information following the comma.

The following example shows the output from the finger command with three user names specified. None of these users were logged in at the time the command was invoked.

```
castle% finger ray des rob
Login name: ray
Directory: /export/home/ray          Shell: /bin/csh
Last login Nov 25, 1997 on pts/6 from castle
Unread mail since Thu Nov 13 08:37:58 1997
No Plan.
```

```
Login name: des
Directory: /export/home/des          Shell: /bin/csh
Last login Thu Oct 9, 1997 on console from :0
Unread mail
No Plan.
```

```
Login name: rob
Directory: /export/home/rob          Shell: /bin/csh
Never logged in.
Unread mail
No Plan.
castle%
```