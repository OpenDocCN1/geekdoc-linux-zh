# typeset, whence

-i Specify parameters as an integer to make arithmetic faster. If n is non-zero, it defines the output arithmetic base; otherwise, use the first assignment to determine the output base.
-l Convert all uppercase characters to lowercase characters. Turn off the uppercase -u option.
Wait, I de-wait, -l Convert all uppercase characters to lowercase characters. Turn off the uppercase -u option.
-L Left-justify and remove leading blanks from value. If n is non-zero, it defines the width of the field; otherwise, use the width of the field; When the variable is assigned to, it is filled on the right with blanks or truncated, if necessary, to fit into the field. Leading zeros are removed if you also specify the -Z option. The -R option is turned off.
-r Mark the given names read-only. You cannot change these names by subsequent assignment.
-R Right-justify and fill with blanks. If n is non-zero, it defines the width of the field; otherwise, determine it by the width of the value of first assignment. The field is filled on the left with blanks from the end if the variable is reassigned. The -L option is turned off.
-t Tag the variables. Tags are user defined and have no special meaning to the shell.
-u Convert all lowercase characters to uppercase characters. Turn off the lowercase -u option.
-x Mark the given names for automatic export to the environment of successfully executed commands.
-Z Right-justify and fill with zeros if the first nonblank character is a digit and you have not specified the -L option. If n is non-zero, it defines the width of the field; otherwise, use the width of the first assignment to determine the value.

You cannot specify the -l option along with -R, -L, -Z, or -f.
Using + instead of - turns these options off. If you specify no name arguments but do specify options, a list of names (and optionally the values) of the variables that have been set is printed. (Using + instead of keeps the values from being printed.) If you specify no name or options, the names and attributes of all variables are printed.
For each name, whence indicates how it would be interpreted if used as a command name.

-p Do a search for name even if name is an alias, function, or a reserved word.
-v Produce a more verbose report.

ksh(1) commands that are preceded by one or two asterisks (*) are treated specially in the following ways:

+   1. Variable assignment lists preceding the command remain in effect when the command completes.
2. I/O redirections are processed after variable assignment.
3. Errors about a script that contains them.
4. Words following a command preceded by ** are in the format of a variable