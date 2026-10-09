```
$ who | grep sam
sam       tty1    2013-03-24 05:00
```

less and more  Another way of handling output that is too long to fit on the screen, such as a list of files in a crowded directory, is to use a pipeline to send the output through less or more (both on page 220).

```
$ ls | less
```

The less utility displays text one screen at a time. To view another screen of text, press the SPACE bar. To view one more line, press RETURN. Press h for help and q to quit.

> optional  The pipeline symbol (|) implies continuation. Thus the following command line
> $ who | grep 'sam'
> sam       tty1    2013-03-24 05:00
> is the same as these command lines
> $ who |
> > grep 'sam'
> sam       tty1    2013-03-24 05:00

When the shell parses a line that ends with a pipeline symbol, it requires more input before it can execute the command line. In an interactive environment, it issues a secondary prompt (>; page 362) as shown above. Within a shell script, it processes the next line as a continuation of the line that ends with the pipeline symbol. See page 1063 for information about control operators and implicit command-line continuation.

# LpI  FILTERS

A filter is a command that processes an input stream of data to produce an output stream of data. A command line that includes a filter uses a pipeline symbol to connect standard output of one command to standard input of the filter. Another pipeline symbol connects standard output of the filter to standard input of another command. Not all utilities can be used as filters.

In the following example, sort is a filter, taking standard input from standard output of who and using a pipeline symbol to redirect standard output to standard input of lpr. This command line sends the sorted output of who to the printer:

```
$ who | sort | lpr
```

The preceding example demonstrates the power of the shell combined with the versatility of Linux utilities. The three utilities who, sort, and lpr were not designed to work with one another, but they all use standard input and standard output in the conventional way. By using the shell to handle input and output, you can piece standard utilities together on the command line to achieve the results you want.