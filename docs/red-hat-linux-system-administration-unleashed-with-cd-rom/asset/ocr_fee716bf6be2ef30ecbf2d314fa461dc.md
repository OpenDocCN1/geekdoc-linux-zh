Several shell variables help customize the spelling correction feature, including the correct variable and the autocorrect variable. The correctshell variable can either be set to the value of cmd, which tells tsch to correct spelling mistakes in only the command name, or to all, which tells tsch to correct spelling mistakes in the entire line. If the autocorrect shell variable is set, tsch will attempt to correct spelling mistakes during command-line completion before each completion attempt.

# Pipes

Pipes is another feature found in both bash and tsch, and again, both shells treat pipes the same for the most part.

# Input and Output Redirection

Another very useful feature of tsch, which is also found in bash, is known as output and input redirection. Input redirection allows you to redirect where the input for a command is coming from and output redirection allows you to redirect where the output for a command is going.

The < character is used for performing input redirection. Here is an example of using input redirection to direct the input of a file to a command:

```
```
$ command < inputfilename
```
```

In the preceding case, whatever content the file inputfilename contains will be sent to command as input. The command would receive the data from the file just as it would receive data from the keyboard.

The > character is used for performing output redirection. Output redirection is often used to store the results of a command to a file. If you wanted to store the results of the preceding command to a file, you could use the following:

```
```
$ command < inputfilename > outputfilename
```
```

After running the command you should not see any immediate output. Instead, open the output file and all the output should be inside that file.

With the output redirection operator, all data within any file you direct output to is erased. There is an operator you can use instead if you want to append the output from a command to a file. It is represented by the >> character. Here is an example of using it:

```
```
$ command >> outputfilename
```
```

The output from the command would be added onto the end of the file outputfilename. The append operator is useful for writing log files.