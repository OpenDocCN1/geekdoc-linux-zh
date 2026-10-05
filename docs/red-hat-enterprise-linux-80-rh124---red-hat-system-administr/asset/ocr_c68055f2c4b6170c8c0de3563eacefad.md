...output omitted...

Press q to quit the man page.

1.3. Use the gedit + command to open the manual file. The missing line next to + option open a file passed as an argument at the end of the last line.

```
[student@workstation ~]$ gedit + manual
```

the quick brown fox just came over to greet the lazy poodle!

Confirm that the file is opened with the cursor at the end of the last line in the file. Press Ctrl+Q to close the application.

+   Read the su(1) man page.
Note when the user uses the su command assumes the user is root. If the su command is followed by a single dash (-), it starts a child shell. Without the dash, a non-login child shell is created that matches the user's current environment.

```
[student@workstation ~]$ man 1 su
```

SU(1) User Commands SU(1)
NAME
su - run a command with substitute user and group ID
SYNOPSIS
su [options] [-] [user [argument...]]]]

DESCRIPTION
allows to run commands with a substitute user and group ID.
When called without arguments, it defaults to running an interactive shell as root.
...output omitted...
OPTIONS
...output omitted...
-, -1, --login
Start the shell as a login shell with an environment similar to a real login
...output omitted...

> NOTE
Note that comma-separated options on a single line, such as -, -1, and --login, all result in the same behavior.

Press q to quit the man page.

+   3. The man command also has its own man pages.

```
[student@workstation ~]$ man man
```