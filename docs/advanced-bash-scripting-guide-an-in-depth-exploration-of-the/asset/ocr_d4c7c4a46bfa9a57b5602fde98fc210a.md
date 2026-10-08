# Advanced Bash-Scripting Guide

Functions return a value, called an exit status. This is analogous to the exit status returned by a command. The exit status might be explicitly specified by a return statement, otherwise it is the exit status of the last command in the function (0 if successful, and a non-zero error code not). The exit status may be used in the script by referencing it as $ This mechanism permits script functions to have a return value similar to C functions.

Termates a function. A return command [109] optionally takes an integer argument, which is returned to the calling script as the "exit status" of the function, and this exit status is assigned to the variable $?

Example 24-7. Maximum of two numbers

```
#!/bin/bash
# max.sh. Maximum of two integers.

E_PARAM_ERR=251 # If less than 2 params passed to function
EQUAL=2 # Return value if both params are equal.
# Error values out of range of any
# + params that might be fed to the function.

max2 (2) # Returns larger of two numbers.
{
 if [ -z "$2" ]
    # Note: numbers compared must be less than 250.
 then
    return $E_PARAM_ERR
 fi
 if [ "$1" -eq "$2" ]
 then
    return $EQUAL
 else
 if [ "$1" -gt "$2" ]
 then
    return $1
 else
    return $2
 fi
}

max2 33 34
return_val=$$

if [ "$return_val" -eq $E_PARAM_ERR ]
 then
    echo "Need to pass two parameters to the function."
elif [ "$return_val" -eq $EQUAL ]
 then
    echo "The two numbers are equal."
else
    echo "The larger of the two numbers is $return_val."
fi

exit 0
```

+   # Exercise (easy):

# Chapter 24. Functions