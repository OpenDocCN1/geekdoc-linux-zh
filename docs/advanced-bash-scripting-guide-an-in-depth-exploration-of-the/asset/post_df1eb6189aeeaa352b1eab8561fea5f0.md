
# Advanced Bash-Scripting Guide

```
# + into a subscript sparse Bash-Array.
###
# Elements may be added to a Bash-Array by defining an element
# not previously defined.
##
# For these reasons, I have been calling them "Bash-Arrays".
# I'll return to the generic term "array" from now on.
# -- msz

=================================================
echo
# Lines 202 - 334 supplied by Cliff Bamford. (Thanks!)
# Demo -- Interaction with Arrays, quoting, echo, and @ ---
# ## all how things works

ArrayVar[0]='zero'      # 0 normal
ArrayVar[1]='one'       # 1 uniququed literal
ArrayVar[2]='two'      # 2 normal
ArrayVar[3]='three'     # 3 normal
ArrayVar[4]='I am four' # 4 normal with spaces
ArrayVar[5]='five'      # 5 normal
unset ArrayVar[6]        # 6 undefined
ArrayVar[7]='seven'     # 7 normal
ArrayVar[8]=''         # 8 defined but empty
ArrayVar[9]='nine'      # 9 normal

echo '--- Here is the array we are using for this test'
echo ArrayVar[0]='zero'   # 0 normal
echo ArrayVar[1]='one'     # 1 uniququed literal
echo ArrayVar[2]='two'      # 2 normal
echo ArrayVar[3]='three'     # 3 normal
echo ArrayVar[4]='I am four'  # 4 normal with spaces
echo ArrayVar[5]='five'      # 5 normal
echo unset ArrayVar[6]        # 6 undefined
echo ArrayVar[7]='seven'     # 7 normal
echo ArrayVar[8]=''         # 8 defined but empty
echo ArrayVar[9]='nine'      # 9 normal

echo '---Case0: No double-quotes, Default IFS of space,tab,newline --'
IFS=$'\x20\x09\x0A'                                     # # In exactly this order.
echo 'Here it is: printf %q ${(ArrayVar[*])'
printf %q ${(ArrayVar[*])}
echo
echo 'Here it is: printf %q ${ArrayVar[0]}'
printf %q ${ArrayVar[0]}
echo
echo 'Here it is: echo ${ArrayVar[*]}\'
echo ${ArrayVar[*]}
echo 'Here it is: echo ${ArrayVar[0]}'
echo ${ArrayVar[0]}
echo '---Case1: Within double-quotes - Default IFS of space-
line --'
IFS=$'\x20\x09\x0A'                                     # # These three bytes,
echo 'Here it is: printf %q "${ArrayVar[*]}\'
```

Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

```
printf q "${ArrayVar[*]}"
echo
echo 'Here is: printf q "${ArrayVar[@]}\'
printf q "${ArrayVar[@]}"
echo
echo 'Here is: echo "${ArrayVar[*]}"
echo "${ArrayVar[@]}"
echo 'Here is: echo "${ArrayVar[@]}\'
echo "${ArrayVar[@]}"
echo
echo '---Case2: Within double-quotes - IFS is q'
IFS=q
echo 'Here is: printf q "${ArrayVar[*]}"
printf q "${ArrayVar[*]}"
echo
echo 'Here is: printf q "${ArrayVar[@]}\'
printf q "${ArrayVar[@]}"
echo
echo 'Here is: echo "${ArrayVar[*]}"
echo "${ArrayVar[@]}"
echo 'Here is: echo "${ArrayVar[@]}"
echo "${ArrayVar[@]}"
echo
echo '---Case3: Within double-quotes - IFS is ^'
IFS=^'
echo 'Here is: printf q "${ArrayVar[*]}"
printf q "${ArrayVar[*]}"
echo
echo 'Here is: printf q "${ArrayVar[@]}\'
printf q "${ArrayVar[@]}"
echo
echo 'Here is: echo "${ArrayVar[*]}"
echo "${ArrayVar[@]}"
echo 'Here is: echo "${ArrayVar[@]}"
echo "${ArrayVar[@]}"
echo
echo '---Case4: Within double-quotes - IFS is followed by
space,tab,newline'
IFS=$'\x20\x09\x0A' 	# ^ 	 + tab newline
echo 'Here is: printf q "${ArrayVar[*]}"
printf q "${ArrayVar[*]}"
echo
echo 'Here is: printf q "${ArrayVar[@]}\'
printf q "${ArrayVar[@]}"
echo
echo 'Here is: echo "${ArrayVar[*]}"
echo "${ArrayVar[@]}"
echo 'Here is: echo "${ArrayVar[@]}"
echo "${ArrayVar[@]}"
echo
echo '---Case6: Within double-quotes - IFS is set and empty'
IFS=''
echo 'Here is: printf q "${ArrayVar[*]}"
printf q "${ArrayVar[*]}"
echo
echo 'Here is: printf q "${ArrayVar[@]}\'
printf q "${ArrayVar[@]}"
echo
```

Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

```
echo
echo ---Case7: With double-quotes IFS is unset
unset IFS
echo 'Here is: printf q "${ArrayVar[*]}\'
printf %q "${ArrayVar[@]}\'
echo
echo 'Here is: printf q "${ArrayVar[@]}\'
printf %q "${ArrayVar[@]}\'
echo
```

```
echo 'Here is: echo "${ArrayVar[*]}\'
echo "${ArrayVar[@]}\'
echo 'Here is: echo "${ArrayVar[@]}\'
echo "${ArrayVar[@]}\'
echo
echo ---End of Cases---
echo "==========================; echo
```
```
# Put IFS back to the default.
# Default is exactly three bytes.
IFS=$'\x20\x09\x0A' # In exactly this order.
```

```
# Interpretation of the above:
## Glob-Pattern is I/O; the setting of IFS
###
# An All-Elements-Of does not consider settings.
```
```
# Note the different output using the echo command and
# quoted format of printf command.
```
```
# Recall:
# Parameters are similar to arrays and have the similar behaviors.
###
```
```
# The examples demonstrate the possible variations.
# To retain the shape of a sparse array, additional
# programming is required.
###
```
```
# The source code of Bash has a routine to output
# subset]=value assignment.
# As of version 2.0, that routine is not used,
# might change in future releases.
```
```
# The length of a string, measured in non-null elements (characters)
echo
echo '- Non-quoted references -
echo 'Non-Null character count: ${*VarSomething} characters'.
```
```
# test=''\x00' # is a null character.
# See ${test}
IFS=$'\x20\x09\x0A'
```

Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

```
# The length of an array, measured in defined elements,
# including null elements.
echo
echo 'Defined content: ${#ArrayVar[@]} elements'.
# That is NOT the maximum subscript (4).
# It IS the range of subscripts (1 .. 4 inclusive).
###
```
```
# Both the maximum subscript and range of subscripts
# be found with additional scripting programming.
###
```
```
# The length of a string, measured in non-null elements (characters):
echo
echo '- Quoted, Glob-Pattern references -
echo 'Non-Null character count: ${#VarSomething}}'.
```
```
# The length of an array, measured in defined elements,
# including null-content elements.
echo
echo 'Defined element count: ${#ArrayVar[@]}'.
```
```
# Interpretation: Substitution does not affect the ${ ... } operation.
# Suggestion:
# Always use All-Elements-Of character
# if that is what intended (independence from IFS).
```
```
# Define a simple function.
# I include an underscore in the name
 to make it distinctive in the examples below.
###
# Bash separates variable names and function names
# in different namespaces.
# The Mark-One isn't advanced.
###
```
```
_simple() {
echo -n SimpleFunc$@ # Newlines are swallowed in
} # result returned in any case.
```
```
# The ( ...) notation invokes a command or function.
# The $( ... ) notation is pronounced: Result-Of.
```
```
# Invoke the function _simple
echo
echo '- Output of function _simple -'
s_simple # Try passing arguments.
echo
or
(_simple) # Try passing arguments.
```
```
echo '- Is there a variable of that name? -'
echo $simple not defined # No variable by that name.
```
```
# Invoke the result of function _simple (Error msg intended)
###
($simimple # Gives an error message:
# line 436: SimpleFunc: command not found
```

# Advanced Bash-Scripting Guide

```
#
echo
###
# The first word of the result of function _simple
# is neither a valid Bash command the name of a defined function.
###
# This demonstrates that the output of _simple is subject to evaluation.
###
# Interpretation:
# A function can be used to generate in-line Bash commands.
# A simple function where the first word of result IS a bash command:
###
_print() {
    echo -n 'printf %q \$@'
}
echo '-' - Outputs of function _print -'
_print parml1 parm2 # An Output NOT A Command.
echo
$(_print parml1 parm2) # Executes: printf %q parm2
# See above IFS examples for the various possibilities.
echo
$(_print $VarSomething) # The predictable result.
echo
# Function variables
###
echo
echo ' - Function variables -
# A variable may represent a signed integer, a string or an array.
# A string may be used like a function name with optional arguments.
# set -vx # Enable if desired
declare -f funcVar # in namespace of functions

funcVar=_print # Contains name of function.
$funcVar parml1 # Same as _print at this point.
echo
funcVar=$(_print ) # Contains result of function.
$funcVar # No input, No output.
$funcVar$VarSomething # The predictable result.
echo
funcVar=$(_print $VarSomething) # $VarSomething replaced HERE.
$funcVar # The expansion is part of the variable contents.
echo
funcVar="$(_print $VarSomething)" # $VarSomething replaced HERE.
$funcVar # The expansion is part of the variable contents.
echo
```
