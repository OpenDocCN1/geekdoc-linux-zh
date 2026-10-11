# # Shell Functions

Functions are a way of embedding small subscripts into a Bash script without saving them in a separate file. Because they are embedded in a script, they do not have to be loaded in order to be used. This, in turn, makes them run faster than separate scripts. Like separate scripts, functions can be used to break up a complex script into separate, named, tasks to improve readability.

Shell functions differ from functions in other programming languages in that they return a status code instead of a return value. Without a return value, they cannot be used in expressions.

Like variables, functions must be declared before they can be used. Instead of the *declare command*, functions are declared using the *function command*. Each function has a name and the statements composing the function are enclosed in curly brackets. See Listing 14.10.

# Listing 14.10 function.sh

```
```bash
#!/bin/bash
#
# function.sh - A simple function example

declare -rx SCRIPT=${0##*/}
declare -rx TMP="/tmp/temp.$$"
declare -rx TRASH_DIR="$HOME/.trash"

# $TRASH_TMP
#
# Move the TMP file to the trash directory

function trash_tmp {

  if test ! -d "$TRASH_DIR" ; then
    printf "%s\n" "$SCRIPT:$FUNCNAME:$LINENO: trash directory \\
$TRASH_DIR is missing" >&2
    exit 1
  fi
  if test -f "$TMP" ; then
    mv $TMP "$TRASH_DIR/."/
  fi
}

readonly -f trash_tmp
declare -t trash_tmp

printf "This is a function test\n" > $TMP
trash_tmp

exit 0
```
```