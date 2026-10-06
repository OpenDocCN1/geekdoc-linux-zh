# Advanced Bash–Scripting Guide

```
#!/bin/bash

# script "set-test"

# Invoke this script with three command line parameters,
# for example, \./set-test one two three".

echo
echo "Positional parameters before set uname -a\ : :"
echo "Command-line argument $1 = $1"
echo "Command-line argument $2 = $2"
echo "Command-line argument $3 = $3"

echo
set unname -a' # Sets the positional parameters to the output
# of the command uname -a'

echo "Positional parameters after set uname -a\ : :"
# $1, $2, $3, etc. reinitialized to result of uname -a'
echo "Field #1 of 'uname -a = $1'
echo "Field #2 of 'uname -a = $2'
echo "Field #3 of 'uname -a = $3'
echo

exit 0
```

See also Example 10–2.

The unset command deletes a shell variable, effectively setting it to null. Note that this command does not affect positional parameters.

```
bash$ unset PATH
bash$ echo $PATH
bash$
```

Example 11–11. "unsetting" a variable

```
#!/bin/bash
# unset.sh: Unsetting a variable.

variable=hello # Initialized.
echo "variable = $variable"
\unset variable # Unset.
# Same effect as variable=
echo "$(unset) variable = $variable" # $variable is null.

exit 0
```

The export command makes available variables to all child processes of the running script or shell. Unfortunately, there is no way to export variables back to the parent process, to the process that called or invoked the script or shell. One important use of export command is in startup files, to

Chapter 11. Internal Commands and Builtins