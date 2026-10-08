# Advanced Bash-Scripting Guide

```
funccl () {
  echo This is a function.
}

declare -f      # Lists the function above.
echo
declare -i var1 # var1 is an integer.
var1=2367
echo "var declared as $var1"
var1+=1        # Integer declaration eliminates eliminates the need for 'let'
echo "var incremented by 1 is $var1"
# Attempt to change variable declared as integer.
echo "Attempting to change var1 to floating point value, 2367.1"
var1=2367.1     # Results in error message, with no change to variable.
echo "var is still $var1"

declare -r var2=13.36 # 'declare' permits setting a variable property
# + and simultaneously assigning a value.
echo "var2 declared as $var2" # Attempt to change readonly variable.
var2=13.37      # Generates error message, and exit script.
echo "var2 is still $var2"  # This line will not execute.

exit 0          # Script will not exit here.
```

Using the declare builtins restricts the scope of a variable.

```
foo () {
  FOO="bar"
}

bar () {
  foo
  echo $FOO
}

bar      # Prints bar.
However...

foo () {
  declare FOO="bar"
}

bar () {
  foo
  echo $FOO
}

bar      # Prints nothing.

# Thank you, Michael Iatrou, for pointing this out.
```

Chapter 9. Another Look at Variables

106