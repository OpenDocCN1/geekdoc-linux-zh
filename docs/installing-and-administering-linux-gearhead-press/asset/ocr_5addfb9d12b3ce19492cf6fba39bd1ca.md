When a new shell is invoked in this manner, the previous shell (usually, but not always, the login shell) will “sleep” until you go back to it by entering the `exit` command.

You can also invoke a new shell by entering the following:

```
$ newshellname (-options) commandname (-options) [arguments]<Enter>
```

or

```
$ newshellname (-options) scriptname<Enter>
```

This action spawns a new shell, which in turn will execute either a new command/program or a new script. Once the command/program or script has executed, then control will pass from the new shell back to the original shell. Until then, the original shell will “sleep.”

Table 12.2 lists a few of the several options that can be invoked along with either the sh or bash shell commands.

You will notice that when a new shell is invoked that is the same as the login shell, the user prompt will not change (have a look at Figure 12.1). As it is invoked, the new shell will read the same environment files as the previous shells. You can check that a new shell has been invoked by entering the `ps` command with no options or arguments. The new shell will have the same name as the previous shell but will have a different process ID number (PID).

# Table 12.2 Options Available for Use with bash or sh Shells

| OPTION | EXPLANATION |
|:-|:-|
| -c | The additional commands following the -c can be run with the shell command. |
| -r | Start a restricted shell; that is, a shell that has approximately a dozen restrictions. Examples: you cannot cd between directories; you cannot set or unset the SHELL, PATH, ENV, or BASH_ENV variables (and so on). |
| -i | The shell will be run interactively; you can test this capability with startup files or scripts. |
| -- | (no spaces between them) indicates “that’s the end of the options”; any arguments after the -- will be treated like filenames or other arguments (not as options). You can use -- as well. |