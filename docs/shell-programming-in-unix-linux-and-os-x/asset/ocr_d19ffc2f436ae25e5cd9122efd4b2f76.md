# More on Subshells 229

# Start up a new shell
#

```
/bin/sh
$
```

The HOME directory is set to /usr2/data, and then the variables BIN, RPTS, and DATA are defined relative to this HOME (a good idea in case you ever have to move the directory structure somewhere else: all you'd have to change in the program is the variable HOME).

Next, PATH is modified to include the database bin directory and the CPATH variable is set to search the current directory, the HOME directory, and the RPTS directory (which presumably subdirectories).

After exporting these variables, /bin/sh, is invoked. From that point on, this new shell processes any user-entered commands until either the user types exit or uses the Ctrl+d sequence. Upon exit, control returns to db, which in turn returns to your login shell.

```
$ db
DB: echo $HOME
/usr2/data
DB: cd rpts
/usr2/data/rpts
DB: ps
PID TID TIME COMMAND
123 13 0:01 sh
761 13 0:01 sh
765 13 0:03 ps
DB: exit
$ echo $HOME
/users/steve
$
```

Run it

Try out CDPATH
It works
See what processes are running

Your login shell
Subshell running db
New shell run from db

Done for now

Back to normal

The execution of db is depicted in Figure 10.7 (where we've shown only the exported variables of interest for simplicity's sake, not all that exist in the environment).