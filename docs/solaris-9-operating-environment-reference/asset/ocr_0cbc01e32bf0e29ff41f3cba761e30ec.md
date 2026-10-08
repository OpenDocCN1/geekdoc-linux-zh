# ksh, rsh 601

MAILCHECK Specify how often (in seconds) the shell checks for changes in the modification time of any of the files specified by the MAILPATH variables. The default value is 600 seconds. When the time has elapsed, the shell checks before issuing the next prompt.

MAILPATH Colon-separated list of file names. If this variable is set, then inform the user of any modifications to the specified files that have occurred within the last MAILCHECK seconds. Each file name can be followed by a ? and a message that is printed. The message undergoes substitution with the variable $ defined as the name of the file that has changed. The default message you have mail in $_

NLSPATH Determine the location of message catalogs for the processing of LC_MESSAGES.

PATH Specify the path for commands. The user cannot change PATH if executing under rsh (except in .profile).

PPID Set by the decimal process ID of the process that invoked the shell. In a subshell, PPID is set to the same value as that of the parent of the current shell. For example, echo PPID and (echo PPID) would produce the same value.

PS1 Expand the value of this variable for parameter substitution to define the primary prompt string, by default, $. Replace the character ! in the prompt string by the command number. Two successive occurrences of ! produce a signal ! when the prompt is printed.

PS2 Specify the secondary prompt string, by default, >.

PS3 Specify the selection prompt string used within a select loop, by default, #.

PS4 Expand the value of this variable for parameter substitution and use value to precede each line of an execution trace. If omitted, the execution trace prompt is -.

SHELL Store the path name of the shell in the environment. At invocation, if the basename of this is rsh, rksh, or krsh, then the shell becomes restricted.

TIMEOUT If set to a value greater than 0, terminate a command is not entered in the prescribed number of seconds after the PS1 prompt is issued. (Note that the shell can be compiled with a maximum bound for this value which cannot be exceeded.)

VISUAL If the value of this variable ends in emacs, gmacs, or vi, then turn on the corresponding option.

# Blank Interpretation

After parameter and command substitution, the results of substitutions are scanned for the field separator characters (those found in IFS) and split into distinct arguments when such characters are found. Explicit null arguments (\") or ('') are retained. Implicit null arguments (those resulting from parameters that have no values) are removed."