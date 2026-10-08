# Advanced Bash-Scripting Guide

File data-file for Example 15-22, above. Must be present in same directory.

```
# This is a data file loaded by a script.
# Files of this type may contain variables, functions, etc.
# It loads with a 'source' or '.' command from a shell script.

# Let's initialize some variables.

variable1=23
variable2=474
variable3=5
variable4=97

message1="Greetings from *** LINENO *** of the data file!"
message2="Enough for now. Goodbye."

print_message () {
  # Echoes any message passed to it.

  if [ -z "$1" ];
    then
      return 1 # Error, if argument missing.
    fi

  echo

  until [ -z "$1" ];
    do
      # Step through arguments passed to function.
      echo -n "$1" # Echo args one time, suppressing line feeds.
      echo -n " " # Insert spaces between words.
      shift
      # Next one.
    done
  echo
  return 0
}
```

If the sourced file is itself an executable script, then it will run, then return control to the script that called it. A sourced script may use a return for this purpose.

Arguments may be (optionally) passed to the sourced file as positional parameters.

```
source $filename arg1 arg2
It is possible for a script to source itself, though this does not seem to have any practical applications.
```

# Example 15-23, A (useless) script that sources itself

```
#!/bin/bash
# self-source.sh: a script sourcing itself "recursively."
# From "Stupid Tricks," Volume II.

MAXPASSCOUNT=100 # Maximum number of execution passes.

echo -n "pass_count"
# At first execution pass, this just echoes two blank spaces.
```

Chapter 15. Internal Commands and Builtins