# Commands

A simple command is a sequence of blank-separated words that can be preceded by a variable assignment list. The first word specifies the name of the command to be executed. Except as specified below, the remaining words are passed as arguments to the invoked command. The command name is passed as argument 0 (see exec(2)). The value of a simple command is its exit status if it terminates normally or (octal) 200+ if it terminates abnormally (see signal(2) for a list of status values).

A pipeline is a sequence of one or more commands separated by |. The standard output of each command is the input of the next command. Each command is run as a separate process; the shell waits for the last command to terminate. The exit status of a pipeline is the exit status of the last command.

A list is a sequence of one or more pipelines separated by ;, &&, or ||; and optionally terminated by ;, &&, or |. The symbols ;, and | have equal precedence, which is lower than that of && and || have equal precedence. A semicolon (;) sequentially executes the preceding pipeline; an ampersand (&) asynchronously executes the preceding pipeline (the shell does not wait for pipeline to finish). The symbol (&) asynchronously executes the preceding command with a two-way pipe established to the parent shell.

The standard input of the saved command can be written and read from the parent shell with the -p option of the specific command described in "Special Commands" on page 67. The symbol (;) executes the following only if the preceding returns 0 (or a non-zero value). You can use arbitrary number of newlines instead of a semicolon in a list to delimit a command.

A command is either a simple command or one of the following. Unless otherwise stated, the value returned by a command is that of the last simple command executed in the command.

```
for identifier [word...]; do; done
```

Each time a command is executed, set identifier to the next word taken from the wordlist. If you omit in word..., execute the list once for each positional parameter that is set. Execution ends when there are no more words in the list.

```
select identifier [word...]; do; done
```

Print to standard error (file descriptor 2) the set of words, each preceded by a number. If you omit in word..., use the parameters instead (see Parameter Substitution). Print the PS3 prompt, and read a line from the standard input. If this line contains the number of one for the word corresponding to this number, then set the value of the variable identifier to this word. If this line is empty, print the selection list. Otherwise, set the value of the variable identifier to null. Set the contents of the line from standard input in the shell variable REPLY. Execute the list for each selection until a break or EOF is encountered. If the REPLY variable is set to null by the execution of list, then print the selection list before displaying the PS3 prompt for the next selection.