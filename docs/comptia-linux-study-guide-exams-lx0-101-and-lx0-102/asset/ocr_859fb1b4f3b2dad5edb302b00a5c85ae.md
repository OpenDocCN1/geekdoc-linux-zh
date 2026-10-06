the text immediately following the << code isn't a filename; instead, it's a word's used to mark the end of input. For instance, typing someprog << EOF causes someprog to accept input until it sees a line that contains only the EOF (without a space following it).

> Some programs that take input from the command line expect you to terminate by pressing Ctrl+D. This keystroke corresponds to an end-of-file marker using the American Standard Code for Information Interchange (ASCII).

A final redirection tool is the tee command. This command splits standard input so that it's displayed on standard output and in conjunction with data pipes so that a program's output can be stored and viewed immediately. For instance, to view and see the output of someprog, you might type this:

```
$ someprog | tee output.txt
```

> The vertical bar (|) is the pipe character. It implements a pipe, as described in the next section.

Ordinarily, tee overwrites any files whose names you specify. If you want to append data to these files, pass the -a option to tee.

# Piping Data Between Programs

Programs can frequently operate on other programs' outputs. For instance, you might use a text-filtering command (such as the ones described shortly, in “Processing Text Using Filters”) to manipulate text output by another program. You can do this with the help of redirection operators; see the first program's standard output to a file, and then redirect the second program's standard input to read from that. This solution is awkward, though, and it involves the creation of a file that might easily overlook, leading to unnecessary clutter on your system.

The solution is to use data pipes (aka pipelines). A pipe redirects the first program's standard output to the second program's standard input and is denoted by a vertical bar (|):

```
$ first | second
```

For instance, suppose that first generates system statistics, such as system uptime, CPU use, number of users logged in, and so on. This output might be lengthy, so you want to trim it a bit. You might therefore use second, which could be a script or command that