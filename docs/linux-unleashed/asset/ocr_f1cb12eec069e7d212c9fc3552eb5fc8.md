**NOTE**

Some setup programs automatically make a copy of the .profile file in your home directory for you when they create your login. However, not all routines do this, so you should check your home directory first. Remember that all files starting with a period are hidden and can only be displayed with the ls -A or ls -a command.

![](bbox=[0.82, 0.11, 0.95, 0.25])

# bash Command Summary

Some of the most useful commands built into the bash shell are summarized in Table 11.2.

**TABLE 11.2. THE BASH COMMANDS WE'VE USED IN THIS CHAPTER.**

| bash command | What it's used for |
|---|---|
| alias | Used to set bash aliases (command nicknames that can be defined by the user). |
| bg | Background command. Forces a suspended process to continue to execute in the background. |
| cd | Change working directory. This command changes the current working directory to the directory specified as an argument. |
| exit | Terminates the shell. |
| export | Causes the value of a variable to be made visible to all subprocesses that belong to the current shell. |
| fc | Fix command. Used to edit the commands in the current history list. |
| fg | Foreground command. Forces a suspended process to continue to execute in the foreground. |
| help | Displays help information for bash built-in commands. |
| history | Brings up a list of the last n commands that were entered at the command prompt, where n is a configurable variable specifying the number of commands to remember. |
| Kill | Used to terminate another process. |
| pwd | Print working directory. Prints the directory in which the user is currently working. |
| unalias | Used to remove aliases that have been defined using the alias command. |