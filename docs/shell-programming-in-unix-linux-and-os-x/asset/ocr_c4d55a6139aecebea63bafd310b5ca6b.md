![](bbox=[0.137, 0.115, 0.593, 0.503])

Figure 2.8 The shell's responsibilities

# # Program Execution

The shell is responsible for the execution of all programs that you request from your terminal.

Each time you type in a shell, the shell analyzes the line and determines what to do. As far as the shell is concerned, each line follows the same basic format:

```
program-name arguments
```

The line that is typed to the shell is known more formally as the command line. The shell scans this line and determines the name of the program to be executed and what arguments to pass to the program.

The shell uses special characters to determine where the program starts and ends, and where each argument starts and ends. These characters are collectively called whitespace characters, and are the space character, tab character, and the end-of-line character, known more formally as the newline character. Multiple occurrences of whitespace characters are ignored by the shell. When you type the command

```
mv tmp/mazewars games
```