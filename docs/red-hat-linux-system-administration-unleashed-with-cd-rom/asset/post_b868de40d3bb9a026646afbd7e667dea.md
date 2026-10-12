
The more you use bash, the more key-dependent upon wildcards you will be. In fact, after you start using them regularly, you won't know how you got by without them.

## Aliases

Aliases are a very useful feature of the bash shell that saves you time while also allowing you to customize commands to your liking. Aliases allow you to create your own commands, using the existing commands as the base. There are several reasons for using aliases. You may prefer an alternative name for some commands, you may want to abbreviate a command to save keystrokes, or there may be certain parameters that you always pass to a certain command and you would like those parameters to be passed automatically.

To create an alias you must use the alias command. For example, to create an alias for ls so that the -F option is passed automatically, you would type the following command:

```
$ alias ls='ls -F'
```

Now whenever you invoke ls on the command line, ls will be expanded to the form 'ls -F' and the expanded command will be executed. The concept here is very similar to the wildcard expansion concept. The expansion of the command takes place behind the scenes in both cases and is not displayed to the user. However, the expansion occurs before the command is passed on to the operating system.

Aliases last until you log out from the current shell or until they are unaliased. The unalias command is used to kill an alias without having to log out. To remove the ls alias used in the preceding command, type the following:

```
$ unalias ls
```

Now the ls command will go back to normal and will no longer be expanded to 'ls -F'.

As you become more familiar with using bash, you will most likely start to use several aliases regularly. You can set up aliases to be created when you log in by adding them to the bash startup scripts. These scripts are covered later in this chapter. Some of the common aliases you might want to have set when you log in automatically are

- alias ll='ls -l'
- alias la='ls -a'
- alias md='mkdir'
- alias rd='rmdir'
- alias rr='rm -rf'

You can get a list of all the current aliases that are set by typing the alias command by itself, without passing any arguments.

## Command-Line Completion

One of the most useful and commonly used features of bash is known as command-line completion.

In fact, when you get used to using command-line completion on a regular basis, you won’t know how you survived without it.

The main idea behind command-line completion is that bash will try to complete your current command based on what you have typed so far and what available commands start with that. The key used to perform command-line completion is the Tab key. Press the Tab key once and bash will try to complete your command. If it is unsuccessful, you can press Tab again to get a list of all the commands that can fit into what you have typed so far.

The main reasons for using command-line completion are to save some keystrokes and to find commands when you can’t remember exactly how they are spelled. The following is a simple example of using command-line completion.

Say you would like to execute the history command in order to see all your previous commands. With command-line completion, you don’t have to type in every letter. First, just type in h and then press Tab. Nothing should happen. That means there is more than one command in your path that begins with an h. You can press Tab again at this point to get a list of those commands. If you do so, all commands that begin with the letter h should appear. Now, continue typing in the next character in the history command, i. Then press Tab twice again. Now the search has been narrowed to all commands in your path that begin with hi. A list of those commands should be displayed. Now type the s and again press Tab. This time there shouldn’t be any commands other than history that begin with his, and therefore the rest of the history command will be filled in for you automatically on the command line. You should now have a command line that looks like this:

```
$ history
```

To execute the command, press the Enter key. You should get a list of your most recent commands.

## Pipes

One of the fundamental philosophies of UNIX was that a chain of smaller processes should solve large problems. Each of the smaller processes is performed by a single utility that was built to perform a single task, and to perform that task well. It was that philosophy that saw the creation of the small, reusable utilities that UNIX users have come to depend upon—commands like sort, less, awk, and grep. The creators of UNIX needed something to tie together all those simple commands into the chain, and thus the pipe was born.

The pipe symbol is the "|" character and it basically means "Take the output from one command and send it as input to the next command." That way a bunch of simple commands can be strung together to perform some complicated tasks. A basic example of using a pipe is when you have a command whose output scrolls off the screen and you would like to have the output pause after every screen and continue only after a keypress. The ls command will scroll off the screen when run from a directory containing many files; however, you can get ls to display only a screenful of data at a time by piping the output of ls to the more command. You can try it by typing:

```
$ ls /dev | more
```

Here, the contents of the /dev directory are displayed one screen at a time. Press the Spacebar to move down through each screen.

A more complex example of using a pipe would be to print out a sorted list of usernames from the /etc/passwd file. You would need to use several commands to accomplish this: cat, awk, and sort. cat would be needed to print the file, awk would then extract all the usernames, and finally sort would sort those names. Here is the command:

```
$ cat /etc/passwd | awk -F: '{ print $1 }' | sort
```

You should get a listing of all the users who have an account on your system, with one user per line.

Hopefully, you can see the power that is available through the use of pipes. Becoming familiar with using pipes requires a different way of looking at problem solving—with time and patience you will find some very innovative solutions to problems using pipes.

## Input and Output Redirection

Other very useful features of bash are known as output redirection and input redirection. Input redirection allows you to use the contents of a file as the input for a command, whereas output redirection allows you to store the output of a command to a file.

The < operator is used for input redirection and the > operator is used for output redirection. For example, say you wanted to print out a sorted version of a list that was contained in a file. You would redirect that file to the sort command:

```
$ sort < inputfilename
```

Here the contents of the file would be sent to the sort command and the sort command would then display the result of the sort. Now, say you wanted to redirect the output of that sort to a different file instead of standard output. Here is the command:

```
$ sort < inputfilename > outputfilename
```

After running the command, you should not see any immediate output. Instead, you can view the output by listing the contents of the output file with the cat command:

```
$ cat outputfilename
```

In the case of using the > operator, anything that was previously in that file before executing the command is erased. If you would like to preserve the contents of the file and append the output onto the end of the file, you can use the >> operator instead. To append a listing of the current directory into the end of the file you just created from the sort command, type the following:

```
$ ls >> outputfilename
```

An example of using redirection to direct the output of a command to both standard output and standard error is

```
$ ls -lF &> filename
```

or

```
$ ls -lF >& filename
```

Executing either of these commands would cause the output of the ls -lF command to be put into the file specified by filename along with any error messages that the command generates.

## History

Every command that you enter into the command prompt is saved into what is called history. The list of commands in your history can be of an unlimited size; however, it is usually set to a specified limit. Under bash, the shell variable HISTSIZE is used to specify the maximum number of commands to store in the history list. You can use the history command to search through your previous commands and execute certain commands again. The history command is available to get a listing of all the commands in your history file. Type the history command at the shell prompt:

```
$ history
```
