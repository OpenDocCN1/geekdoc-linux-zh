# ## Using Redirection and Pipes

Several of the preceding examples have used *redirection* and *pipes* (aka *pipelines*). These are mechanisms that you can use to redirect the input to a process or the output from a process. Redirection passes input to or from a file, and a pipe enables you to tie two or more programs together so that one uses the output of another as input.

Normally, the standard output of a program goes to the display you used to launch it. The output redirection operator, `>`, changes this, sending standard output to a file that you specify. For instance, suppose you want to capture the output of *ifconfig* in a file called *iface.txt*. You could use the following command to do this:

```
`$ ifconfig > iface.txt`
```

This operator wipes out the current *iface.txt* file, if it exists. If you want to append information rather than overwrite it, you can use the `>>` operator instead of `>`.

Many programs produce a second type of text-mode output, known as *standard error* (sometimes abbreviated *stderr*). This type of output carries error messages that should not be ignored, and so it’s redirected separately from standard output. You use `2>` to redirect standard error, or `2>>` to append standard error to a file rather than replace that file. You can redirect both standard error and standard output by using `&>`.

You can replace standard input by using the input redirection operator, `<`. This is most useful when you must routinely provide the same information to a program time after time. You can create a file with that information and pass it to the program with the input redirection operator; thus:

```
`$ superscript < script-input.txt`
```

To have one program take another’s output as input, you use a pipe, which is represented by a vertical bar (|). An earlier example illustrated this process: the output of *ps* may contain too much information to be easily parsed, so you can pass its output through *grep* to locate just the information you want; thus:

```
`# ps ax | grep xterm`
```

This command searches for the string *xterm* in the *ps* output and displays all the lines that match. The output of *ps* goes into *grep*, and *grep’s* output appears on your screen. (You could use another pipe or redirect *grep’s* output, if you prefer.)

In addition to these basic redirection operators, you can use the *tee* command to create multiple copies of a program’s output. It’s typically used to send output both to standard output and to a file. To use it, pipe a program’s output through *tee*, and give *tee* an output filename:

```
`$ ps ax | tee processes.txt`
```

This example displays the output of the *ps ax* command on the screen *and* stores it in the *processes.txt* file.