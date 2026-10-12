
Such reason may be as simple as preferring an alternative name for some commands. Or, you may want to abbreviate a command to save keystrokes. Or maybe there are certain parameters that you always pass to a certain command and you would like those parameters to be passed automatically.

Aliases are created using the alias command. For example, to create an alias for ls so that the -l option is passed automatically, you would type the following command:

```
$ alias ls 'ls -l'
```

Now whenever you invoke ls on the command line, ls will be expanded to the form 'ls -l' and the expanded command will be executed. The concept here is very similar to the wildcard expansion concept. The expansion of the command takes place behind the scenes in both cases and is not displayed to the user. You will notice a slight difference in the alias command under bash: the equal sign is not used when assigning aliases under the C shell. If you try to create an alias using the equal sign, it will not work.

Aliases are killed by either logging out or by using the unalias command. To remove the ls alias using the unalias command, type the following:

```
$ unalias ls
```

As you become more familiar with using tcsh, you will most likely start to use several aliases regularly. You can set up aliases to be created when you log in by adding them to the tcsh startup scripts. These scripts are covered later in this chapter. Some of the common aliases you might want to have set to help speed up typing when you log in automatically are

```
alias ll 'ls -l'
alias la 'ls -a'
alias md 'mkdir'
alias rd 'rmdir'
alias rr 'rm -rf'
```

You can get a list of all the current aliases that are set by typing the alias command by itself, without passing any arguments.

## Command-Line Completion

One of the most useful and commonly used features of tcsh is known as command-line completion. Command-line completion under tcsh is similar to bash's command-line completion, with a few minor differences.

The main idea behind command-line completion is this: tcsh tries to complete your current command based on a partially typed command. The key used to perform command-line completion is the Tab key. If you type part of a command on the command line, pressing the Tab key will tell tcsh to try to complete your command based on what available commands match what you have typed. Under bash, if more than one command matches what you have typed, pressing the Tab key again will show you the current matches. Unfortunately, this feature is not available under tcsh.

The main reasons for using command-line completion are to save keystrokes and also to locate commands when you can't remember exactly how they are spelled. The following is a simple example of using command-line completion.

Say you would like to execute the history command in order to see all your previous commands. With command-line completion, you don't have to type every letter. First, just type h and then press Tab. Nothing should happen. That means there is more than one command in your path that begins with an h, and therefore you need to give tcsh more information. Continue typing the next character in the history command, i. Now press Tab once again. The search has been narrowed down to all commands in your path that begin with hi. If nothing happens this time, that means there is more than one command in your path that begins with hi. You need the next letter to make your command more specific. Type the s and again press Tab. This time there shouldn't be any commands other than history that begin with his, and therefore the rest of the history command will be filled in automatically on the command line. You should now have a command line that looks like this:

```
$ history
```

Now press the Enter key and you should get a list of your most recent commands.

## Spelling Correction

Spelling correction is a very nice feature of tcsh. tcsh can usually correct the spelling mistakes for filenames, commands, and variables, as well as completing any parts and listing them.

Spelling is corrected using either the spell-word editor command or the spell-line editor command. The spell-word editor command is usually bound to Alt+S and Alt+s, although you can change the binding using the bindkey command. The spelling correction feature is used to correct the spelling in individual words. Key binding and using the bindkey command are covered later in this chapter. The spell-line editor command is usually bound to Alt+S and it corrects the spelling of the entire input buffer.

Several shell variables help customize the spelling correction feature, including the correct variable and the autocorrect variable. The correct variable can either be set to the value of cmd, which tells tcsh to correct spelling mistakes in only the command name, or to all, which tells tcsh to correct spelling mistakes in the entire line. If the autocorrect shell variable is set, tcsh will attempt to correct spelling mistakes during command-line completion before each completion attempt.

## Pipes

Pipes is another feature found in both bash and tcsh, and again, both shells treat pipes the same for the most part.

## Input and Output Redirection

Another very useful feature of tcsh, which is also found in bash, is known as output and input redirection. Input redirection allows you to redirect where the input for a command is coming from and output redirection allows you to redirect where the output for a command is going.

The < character is used for performing input redirection. Here is an example of using input redirection to direct the input of a file to a command:

```
$ command < inputfilename
```

In the preceding case, whatever content the file inputfilename contains will be sent to command as input. The command would receive the data from the file just as it would receive data from the keyboard.

The > character is used for performing output redirection. Output redirection is often used to store the results of a command to a file. If you wanted to store the results of the preceding command to a file, you could use the following:

```
$ command < inputfilename > outputfilename
```

After running the command you should not see any immediate output. Instead, open the output file and all the output should be inside that file.

With the output redirection operator, all data within any file you direct output to is erased. There is an operator you can use instead if you want to append the output from a command to a file. It is represented by the >> character. Here is an example of using it:

```
$ command >> outputfilename
```

The output from the command would be added onto the end of the file outputfilename. The append operator is useful for writing log files.

## History

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
