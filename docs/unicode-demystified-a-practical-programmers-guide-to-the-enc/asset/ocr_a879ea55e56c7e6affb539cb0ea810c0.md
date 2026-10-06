# Chapter 15 The Z Shell and Advanced Shell Programming

sh % read MON month, day and year separated by spaces: " DAY Y
ter month, day and year separated by spaces:

After the prompt, read pauses while you type an input line. If you type three values,
they are assigned to MON, DAY, and YR. The question mark (?) is escaped to pre-
ent the Z Shell using it as a filename pattern-matching operator.

The read builtin supports other options. Table 15-15 lists some of the more
common ones.

# read options

| | |
|---|---|
| -A (array) | Breaks the input into words according to IFS and assigns the words
as an array to the first variable name in the argument list. |
| -e (echo) | Displays the words that are typed after the user presses RETURN
but does not assign them to the variables named in the argument list. |
| -E (echo) | Displays the words that are typed after the user presses RETURN. |
| -p (coprocess) | The command
read -p...
reads its input line from standard output of the coprocess. For more
information, refer to "The Coprocess" on page 806. |
| -q (query) | Reads one character and returns. If the user enters a or y, Read
sets varname to y; otherwise, varname is set to n. The
buildin sets the return value to 0 if the user enters a or Y. This
makes it easier to prompt the user for simple yes/no responses, as
in |
 -r (raw input) | Ordinarily if the input line ends in a backslash character (\),
backslash and the NEWLINE it is discarded, and the next
line is treated as a continuation of the same line of input. This op-
tion causes a trailing backslash to be treated as a regular character.
One application is for reading an input file that is itself a shell script
containing backslashes that you want to reproduce. |