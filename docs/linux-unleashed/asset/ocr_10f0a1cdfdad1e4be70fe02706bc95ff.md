be counting and a prompt then appears on the command line asking for more information. Because the prompt is sometimes not easily identifiable, it may not be obvious what is happening. (It may even appear as though bash has died because, although everything you type shows up onscreen, nothing else appears to be happening.)

What is actually occurring is that the `wc` command is collecting input for itself. If you press **Ctrl+D**, the results of the `wc` command are written to the screen. If you enter the `wc` command with a filename as an argument as shown in the following example, `wc` returns the number of characters, words, and lines contained in that file:

```
```
wc test
11 2 1
```
```

Another way to pass the contents of the `test` file to `wc` is to redirect the input of the `wc` command from the terminal to the `test` file. This results in the same output. The `<` symbol is used by bash to mean “redirect the input to the current command from the specified file.” So, redirecting `wc`’s input from the terminal to the `test` file can be done by entering the following command:

```
```
wc < test
11 2 1
```
```

Input redirection is not used all that often because most commands that require input from a file have the option to specify a filename on the command line. There are times, however, when you come across a program that does not accept a filename as an input parameter, and yet the input that you want to give exists in a file. Whenever this situation occurs, you can use input redirection to get around the problem.

# ## Output Redirection

Output redirection is more commonly used than input redirection. *Output redirection* enables you to redirect the output from a command into a file, as opposed to having the output displayed onscreen.

There are many situations in which this can be useful. For example, if the output of a command is quite large and does not fit on the screen, you may want to redirect it to a file so that you can view it later using a text editor. There also may be cases where you want to keep the output of a command to show to someone else or to print the results. Finally, output redirection is also useful if you want to use the output from one command as input for another. (There is an easier way to use the output of one command as input to a second command. This is shown in the “Pipes” section.)

Output redirection is done in much the same way as input redirection. Instead of using the `<` symbol, the `>` symbol is used.