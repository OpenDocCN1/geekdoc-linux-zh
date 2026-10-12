# History

tcsh also has a history feature, which is similar to the history feature under bash. Every command that you enter into the command prompt is saved into what is called "History." History is stored in a file in your home directory, and the default filename under tcsh is .history. Every time you execute a command at the prompt, that command is added to your history file. The name for your history file is stored in the shell variable histfile. If you want tcsh to store your history in a different file, simply change the value of the histfile variable. The number of commands that are stored in your history is dictated by the shell variable savehist; you might want to set this variable to a preferred amount in your .login file. History is useful for going back and seeing what commands you executed previously and also for re-executing any commands.

The history command can be used to get a list of all the commands in your history file. There are two different methods of calling the history command. The first method is with the following syntax:

```
history [-hrc] [n]
```

The -h option causes history to not output the line numbers and timestamps that are usually outputted by default. The -r command causes history to display all your history in reverse, outputting the most recent commands first. The -c option clears your current history, allowing you to start fresh. You can also specify exactly how many commands to display by passing the n parameter. To try out the history command, simply type it at the command prompt:

```
$ history
```

You should get a listing of previously entered commands. Each command should also have a number and a timestamp associated with it. Now try the history command with the n parameter to specify exactly how many commands to display. To tell history to display only the fifty most recent commands, try the following:

```
$ history 50
```

You should get the last fifty entries in the history list dumped to your screen.

The other method of invoking the history command is with the following syntax:

```
history -SLM [filename]
```

The -S option writes your history list to any file that you specify for filename. The -L option appends any history file you specify to your current history list. Finally, the -M option is used for merging any history file you specify with your current history list. The merge is performed based on the timestamp of each command.