
# Advanced Bash-Scripting Guide

```
echo Major: $major, minor: $minor  # Major: 3, minor: 4
```

# Example 15-12. Using eval to select among variables

```bash
#!/bin/bash
# arr-choice.sh

# Passing arguments to a function to select
# one particular variable out of a group.
arr0=(10 11 12 13 14 15 )
arr1=(20 21 22 23 24 25 )
arr2=(30 31 32 33 34 35 )
#      0 1 2 3 4 5       Element number (zero-indexed)

choose_array() {
  eval array_member=\${arr\$array_number}[$element_number]
  # Using eval to construct the name of a variable,
  # in this particular case, an array name.
  echo "Element $element_number of array $array_number is $array_member"
}
# Function can be rewritten to take parameters.

array_number=0      # First array.
element_number=3
choose_array        # 13

array_number=2      # Third array.
element_number=4
choose_array        # 34

array_number=3      # Null array (arr3 not allocated).
element_number=4
choose_array        # (null)

# Thank you, Antonio Macchi, for pointing this out.
```

# Example 15-13. Echoing the command-line parameters

Chapter 15. Internal Commands and Builtins

# Advanced Bash-Scripting Guide

```bash
echo -n ""      # so it echoes literally,
# and $param dereferences "$param"
# #-                   as expected.
eval echo \$param
# Gives the *value* of variable.
# The "eval" forces the *evaluation*
# # of \$
# as an indirect variable reference.

(( param ++ ))
done

exit $?

==================================================
```

```bash
$ sh echo-params.sh first second third fourth fifth
Command-line parameter $1 = first
Command-line parameter $2 = second
Command-line parameter $3 = third
Command-line parameter $4 = fourth
Command-line parameter $5 = fifth
```

# Example 15-14. Forcing a log-off

```bash
#!/bin/bash
# Killing ppp to force a log-off.
# For dialup connection, of course.

# Script should be run as root user.

SERPORT=tty3
# Depending on the hardware and even the kernel version,
+# the modem port on your machine may be different
+# /dev/ttyS1 /dev/ttyS2.

killpp="kill -9 \$ps aux | awk '/ppp/ { print \$1 }'"
# ------ process ID of ppp
```

```bash
$killpp      # This variable is now a command.
```

The following operations must be done as root user.

chmod 666 /dev/$SERPORT # Restore r/w permissions, or else?
# Since doing a on ppp changes the permissions on the serial port,
+# we restore permissions to previous state.

rm /var/lock/LOCK.$SERPORT # Remove the serial port lock file. Why?
exit $?

# Example 15. Internal Commands and Builtins

# Advanced Bash-Scripting Guide

# Example 15-15. A version of rot13

```bash
#!/bin/bash
# A version of "rot13" using 'eval'.
# Compare to "rot13.sh" example.

setvar_rot_13() {      # "rot13" scrambling
{
  local varname=$1 value=$2
  eval $varname='$(echo \$value | tr a-z n-a-m)'
}

setvar_rot_13 "foobar"      # Run "foobar" through rot13.
echo $var

setvar_rot_13 var "$var"    # Run "sbbone" through rot13.
# Back to original variable.
echo $var
}
```

# This example by Stephane Chelas. Modified by document author.

```bash
exit 0
```

Here is another example using eval to evaluate a complex expression, this one from an earlier version of Yong's Tetris game.

```bash
eval ${1+="\x${y}}"
```

# Example-53 uses eval to convert array elements into a command.

The eval command occurs in the older version of indirect deferencing.

The eval command can be used to parameterize brace expansion.

The eval command can be risky, and normally should be avoided when there exists a reasonable alternative.

An eval \$COMMAND executes the contents, which may contain such surprises as living code. The set command changes the value of internal variables. One is to toggle flags which help determine the behavior of script. Another application for it is to reset positional parameters that a script sees as a command.

# Example 15-16. Using set with positional parameters

```bash
#!/bin/bash
# set-test.sh
# Invoke this script with three command-line parameters, for example, "set.sh one three".
```

# Chapter 15. Internal Commands and Builtins

# Advanced Bash-Scripting Guide

```bash
echo "Positional parameters before set:"
echo -a
echo "Command-line argument #1 = $1"
echo "Command-line argument #2 = $2"
echo "Command-line argument #3 = $3"
```

```bash
set -a # Sets the positional parameters to the output of the command
echo -a
```

```bash
echo
echo +++++
# Flags set in script. anomalous behavior?
```

```bash
echo "Positional parameters after set:"
echo -a
echo "Field #1 of set = $1"
echo "Field #2 of set = $2"
echo "Field #3 of set = $3"
```

exit 0
```

# Example 15-17. Reversing the positional parameters

```bash
#!/bin/bash
# reverseposparams.sh: Reverse positional parameters.
# Script by Dan Jacobson, with stylistic revisions by document author.
```

```bash
set a b c d e; # Spaces escaped, Spaces not escaped
OLDIFS=$IFS; IFS=$-; # Saving old IFS and setting new one.
```

```bash
echountil [ $# -eq 0 ];
do # Step through positional parameters.
echo "\$k" # Before
k=$1;$k # Append each param to loop variable.
echo "\$k" # After
shift
done
```

```bash
set $k # Set new positional parameters.
echo
echo $* # Count of positional parameters.
echo
```

# 15. Internal Commands and Builtins

# Advanced Bash-Scripting Guide

```bash
echo
for i # Omitting the "in list" sets the variable -- i to the positional parameters.
do
    echo $i # Display new positional parameters.
done
IFS=$OLDIFS # Restore IFS.
```

# Question:
# Is it necessary to set a new IFS, internal field separator, in order for this script to work properly?
# What happens if you don't? Try it.
# And, why use the new IFS -- a colon -- in line 17, to append to the loop variable?
# What is the purpose of this?
exit 0

$ ./revposparams.sh
k0 = a
k = b

k0 = a b
k = c b

k0 = c a b
k = d e c b

Invoking set without any options or arguments simply lists all the environmental and other variables that have been initialized.

```bash
bash$ set
AUTHORCOPY=/home/bozo/posts
BASH=/bin/bash
BASH_VERSION='2.05.8 (1)-release'
...
XAUTHORITY=/home/bozo/.Xauthority
./etc/bashrc
variable22=abc
variable23=xzy
```

Using set with the -- option explicitly sets the contents of a variable to the positional parameters. If no variable follows the -- it unsets the positional parameters.

# Example 15-18. Reassigning the positional parameters

```bash
#!/bin/bash
```

Chapter 15. Internal Commands and Builtins 200

# Advanced Bash-Scripting Guide

```bash
variable="one two three four five"

set $variable
# Sets positional parameters to the contents of "$variable"

first_param=$1
second_param=$2
shift; shift; # Shift first two positional params. also works.
remaining_params="$*"

echo "first parameter = $first_param"    # one
echo "second parameter = $second_param"    # two
echo "remaining parameters = $remaining_params"  # three four five

echo;

# Again.
set --$variable
first_param=$1
second_param=$2
echo "first parameter = $first_param"    # one
echo "second parameter = $second_param"    # two
echo "remaining parameters = $remaining_params"  # three four five
```

```bash
set - # Unsets positional parameters if variable specified.

first_param=$1
second_param=$2
echo "first parameter = $first_param"    # (null value)
echo "second parameter = $second_param"    # (null value)
```

exit 0
# ====================================

The unset command deletes a shell variable, effectively setting it to null. Note that this command does not affect positional parameters.

| bash$ unset PATH
| bash$ echo $PATH
| bash$ |

# Example 15-19. "Unsetting" a variable

```bash
#!/bin/bash
# unset.sh: Unsetting a variable.

variable=hello                        # Initialized.
echo "variable = $variable"

unset variable                         # Unset.
# In this particular context,
# same effect as: variable=
echo "$(unset variable) = $variable"  # variable is null.
```
