# Advanced Bash-Scripting Guide

```
# Exercise:
# -----
# Modify this script to track changes in /var/log/messages at intervals
#+ of 20 minutes.
# Hint: Use the "watch" command.
```

As in find, a curly bracket serves as a placeholder for replacement text.

# Example 16-6. Copy files in current directory to another

```
#!/bin/bash
# copydir.sh

# Copy (verbose) all files in current directory ($PWD)
#+ to directory specified on command-line.
E_NOARGS=85

if [ -z "$1" ];      # Exit if no argument given.
then
    echo "Usage: basename $0 directory-to-copy"
    exit $E_NOARGS
fi

ls | xargs -i t cp ./$1
# -t is "verbose" (output command-line to stderr) option.
# -i is "replace" string.
# {} is a placeholder for output text.
# This is similar to the use of a curly-bracket pair in "find."

# List the files in current directory (ls .),
#+ pass the output of "ls" as arguments to "xargs" (-i -t options),
# then copy (cp) these arguments ({}) to new directory ($1).

# The result is the exact equivalent of
#+ cp $1
#+ unless any of the filenames has embedded "whitespace" characters.

exit 0
```

# Example 16-7. Killing processes by name

```
#!/bin/bash
# kill-byname.sh: Killing processes by name.
# Compare this script with kill-process.sh.

# For instance,
#+ try "./kill-byname.sh xterm" --n#+ watch all the xterms on your desktop disappear.

# Warning:
# -----
# This is a fairly dangerous script.
# Running it carelessly (especially as root)
```