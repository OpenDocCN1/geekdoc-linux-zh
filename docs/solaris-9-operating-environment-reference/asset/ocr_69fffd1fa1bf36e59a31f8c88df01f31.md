intr    User-defined interrupt character (usually ^C). Abort the current
command, and print a new prompt.

kill    User-defined kill character (usually ^U). Kill the entire current
command line.

quit    User-defined quit character (usually \^). Quit the debugger.

suspend User-defined suspend character (usually ^Z). Suspend the debugger.

On keyboards that support an extended keypad with arrow keys, mdb interprets
t following keystrokes as editing commands.

+   - up-arrow Fetch the previous command from the history (same as ^P).

+   - down-arrow Fetch the next command from the history (same as ^N).

+   - left-arrow Move cursor backward one character (same as ^B).

+   - right-arrow Move cursor forward one character (same as ^F).

# Output Pager

mdb provides a built-in output pager. The output pager is enabled when the debugger’s
standard output is a terminal device. Each time a command is executed, mdb pauses
after one screenful of output and displays a pager prompt, mdb as shown below.

```
> More <space>, <cr>, q, n, c, a ?
```

The following sequences are recognized by the pager.

+   - Space Display the next screenful of output.

+   - a, A Abort the top-level command, and return to the prompt.

+   - c, C Continue displaying output without pausing at each screenful until the
current top-level command is complete.

+   - n, N, Newline, Return Display the next line of output.

+   - q, Q, ^C, \^ Quit (abort) only the current demd.

# Formatting demcds

The /, \, ?, and = metacters are used to denote the special output-formatting
dcmds. Each of these demcds accepts an argument list containing one or more format
characters, repeat counts, or quoted strings. A format character is used to read and format data from the
target shown below. A repeat count is a positive integer preceding the format character that is always
interpreted in base 10 (decimal). You can also specify a repeat count as an expression
enclosed in square brackets preceded by a dollar sign ($ }). A string argument must be
enclosed in double quotes (" *"). No blanks are allowed between format arguments.
with