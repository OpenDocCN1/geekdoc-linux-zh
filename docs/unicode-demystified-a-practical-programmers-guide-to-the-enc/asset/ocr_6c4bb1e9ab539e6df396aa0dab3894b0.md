The default string used for watch messages when who is unset is "%n has %l\nfrom %m", which generates the following line:

```
$ jenny has logged on on tty2 from local
```

As in bash and zsh, this variable contains the PID number of the current shell.

# All the Variables in the Following List Are Available in tcsh.

The variables in the following list are all available in tcsh. Variables that are also available in other shells are marked with a shell box, such as

# Shell Variables That Act as Switches

The following shell variables act as switches; their values are not significant. If the variable has been declared, the shell takes the specified action. If not, the action is not taken or negated. You can set these variables in your .tcshrc file, in a script, or from the command line.

When, the shell attempts spelling correction automatically, just before each attempt at completion.

Normally pushes the new working directory onto the directory stack. This means you can end up with duplicate entries on this stack. If the duunique variable is set, the shell looks for and deletes any entries that duplicate the one it is about to push.

When you call tcsh with the -x option, it sets the echo variable. You can also set echo using set. In either case, when you declare echo, tcsh displays each command before it executes that command.

The file variable enables the filename completion feature when running tcsh (and or is linked to tcsh). Filename completion is a tcsh feature that complements the filename generation facility. If flec is set, you can enter a partial filename on the command line and press TAB to cause the shell to complete it, or can press CONTROL-D to list all the filenames that match the prefix you entered. Refer to "Substitution" on page 691.

When the command is in the history list are displayed as entered, without interpretation by the shell.

When set, you cannot CONTROL-D to exit from the shell, you cannot accidentally log out. When this variable is declared, you must use exit or logout to leave a shell.

When set, the shell lists all jobs whenever a job is suspended.

When, the ls-F builtin shows the type of file each symbolic link points to instead of marking the symbolic link with an @ symbol.