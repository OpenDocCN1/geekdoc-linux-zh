# Advanced Bash–Scripting Guide

```
echo "Two parameters passed.
func2 first second      # Called with two params
echo

echo "\*\" \"second\" passed."
func2 "" second          # Called with zero-length first parameter
echo                      # and ASCII string as a second one.

exit 0
```

![](bbox=[0.293, 0.301, 0.322, 0.319])

The shift command works on arguments passed to functions (see Example 34–6).

In contrast to certain other programming languages, shell scripts normally pass value parameters to functions. [51] Variable names (which are actually pointers), if passed as parameters to functions, will be treated as string literals and cannot be dereferenced. *Functions interpret their arguments literally.

# Exit and Return

exit status

Functions return a value, called an exit status. The exit status may be explicitly specified by a return statement, otherwise it is the status of the last command in the function (0 if successful, and a non–zero error code if not). This exit status may be used in the script by referencing it as $. This mechanism effectively permits script functions to have a "return value" similar to C functions.

# return

Terminates a function. A return command [52] optionally takes an integer argument, which is returned to the calling script as the "exit status" of the function, and which exit status is assigned to the variable $$.

# Example 23–3. Maximum of two numbers

```
#!/bin/bash
# max.sh Maximum of two integers.

E_PARAM_ERR--198      # If less than 2 params passed to function.
EQUAL==-199           # Return value if both params.

max2()               # Returns larger of two numbers.
  if [ -z "$2" ];    # Note: numbers compared must be less than 257.
  then
    return $SE_PARAM_ERR
  fi
```

# 23.1. Complex Functions and Function Complexities

257