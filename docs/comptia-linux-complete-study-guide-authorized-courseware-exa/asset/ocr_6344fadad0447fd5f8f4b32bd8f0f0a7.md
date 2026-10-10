Most of these redirections deal with output, both because there are two types of output (standard output and standard error) and because you must be concerned with what to do in case you specify a file that already exists. The most important input redirection is `\<`, which takes the specified file’s contents as standard input.

> **TIP**
> A common trick is to redirect standard output or standard error to `/dev/null`. This file is a device that is connected to nothing; it’s used when you want to get rid of data. For instance, if the `whine` program is generating too many error messages, you can type `whine 2> /dev/null` to run it and discard its error messages.

One redirection operator that requires elaboration is `<<`. This operator implements a *here document*, which takes text from the following lines as standard input. Chances are you won’t use this redirection on the command line, though; the following lines *are* standard input, so there’s no need to redirect them. Rather, you might use this command as part of a script in order to pass data to a command. Unlike most redirection operators, the text immediately following the `<<` code isn’t a filename; instead, it’s a word that’s used to mark the end of input. For instance, typing `someprog << EOF` causes `someprog` to accept input until it sees a line that contains *only* the string EOF (without even a space following it).

> **NOTE**
> Some programs that take input from the command line expect you to terminate input by pressing Ctrl+D. This keystroke corresponds to an end-of-file marker using the American Standard Code for Information Interchange (ASCII).

A final redirection tool is the `tee` command. This command splits standard input so that it’s displayed on standard output and on as many files as you specify. Typically, `tee` is used in conjunction with data pipes so that a program’s output can be both stored and viewed immediately. For instance, to view and store the output of `someprog`, you might type this:

```
$ someprog | tee output.txt
```

> **NOTE**
> The vertical bar (`|`) is the pipe character. It implements a pipe, as described in the next section.

Ordinarily, `tee` overwrites any files whose names you specify. If you want to append data to these files, pass the `-a` option to `tee`.

# # Piping Data Between Programs

Programs can frequently operate on other programs’ outputs. For instance, you might use a text-filtering command (such as the ones described shortly, in “Processing Text Using