
# The difference between the unquoted and double-quoted versions
# above can be seen in the "protect_literal.sh" example.
# The first case above is processed as two, unquoted, Bash-Words.
# The second case above is processed as one, quoted, Bash-Word.

```bash
# Delayed replacement
# ----echo '-' Delayed replacement -'
funcVar='$(print $VarSomething') # No replacement, single Bash-Word.
eval $funcVar                               # $VarSomething replaced HERE.
echo
```

```bash
VarSomething='NewThing'
eval $funcVar                               # $VarSomething replaced HERE.
echo
```

```bash
# Restore the original setting trashed above.
VarSomething=-Literal
```

```bash
# There are a pair of functions demonstrated in the
# "protect_literal.sh" and "unprotect_literal.sh" examples.
# These are general purpose functions for delayed replacement literals
# containing variables.
```

REVIEW:
# ----

```bash
# A string can be considered a Classic-Array of elements (characters).
# A string operation applies to all elements (characters) of the string
# (in concept, anyways).
```

```bash
# The notation: $(array_name[@]) represents all elements of the
# Bash-Array: array_name.
```

```bash
# The Extended-Syntax string operations can be applied to all
# elements of an array.
```

```bash
# This may be thought of as a For-Each operation on a vector of strings.
```

```bash
# Parameters are similar to an array.
# The initialization of a parameter array for a script
# and a parameter array for a function only differ
# in the initialization of $(0), which never changes its setting.
```

```bash
# Subscript zero of the script's parameter array contains
# the name of the script.
```

```bash
# Subscript zero of a function's parameter array DOES NOT contain
# the name of the function.
# The name of the current function is accessed by the $FUNCTION variable.
```

```bash
# A quick, review list follows (quick, not short).

# Advanced Bash-Scripting Guide

```bash
echo ' - Test (but not change) - -
echo ' - null reference - ' -
echo -n $(VarNull:-NotSet)' ' # NotSet
echo $(VarNull)                  # NewLine only
echo -n $(VarNull:-NotSet)' ' # NotSet
echo $(VarNull)                  # NewLine only

echo ' - null contents - ' # Only the space
echo -n $(VarEmpty:-Empty)' ' # NewLine only
echo $(VarEmpty)                  # Empty
echo -n $(VarEmpty:-Empty)' ' # NewLine only
echo $(VarEmpty)                  # -

echo ' - contents - ' # Literal
echo $(VarSomething:-Content)' 
echo $(VarSomething:-Content)' ' # Literal

echo ' - Sparse Array - 
echo $(Array[@])'-not set' 

# ASCII-Art time
# State Y=yes, N=no
#                                   :
# Unset         Y      $( ... ) == 0
# Empty         N Y      $( ... ) == 0
# Contents      N N      $( ... ) > 0

# Either the first or the second part of the tests
# may be a command or a function invocation string.
echo
echo ' - Test 1 for undefined - '
declare -i t
_decT() {
  t=$t-1
}

# Null reference, set: t = -1 # Results in zero.
t=$(VarNull)
$(VarNull)                  # Function executes, t now -1.
echo $t

# Null contents, set: t = 0 # Results in zero.
t=$(VarEmpty)
$(VarEmpty--decT)             # _decT function NOT executed.
echo $t

# Contents, set: t = number of non-null characters
VarSomething='simple'           # Set to valid function name.
t=$(VarSomething)               # non-zero length
$(VarSomething--decT)         # Function executed.
echo $t

# Exercise: clean up that example.
unset t
unset_decT
VarSomething=Literal

echo
echo ' - Test and Change - ' -
echo ' - Assignment null reference - ' 
echo -n $(VarNull:-NotSet)' ' # NotSet NotSet
```

Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

```bash
echo $(VarNull)
unset VarNull
```

```bash
echo ' - Assignment=null reference -
echo -n $$(VarNull)='NotSet' '    # NotSet NotSet
echo $(VarNull)
unset VarNull
```

```bash
echo ' - No assignment if null contents -
echo -n $$(VarEmpty)='Empty' '    # Space only
echo $(VarEmpty)
VarEmpty=''
```

```bash
echo ' - No assignment if null contents -
echo -n $$(VarEmpty)='Empty' '    # Empty Empty
echo $(VarEmpty)
VarEmpty=''
```

```bash
echo ' - No change if already has contents -
echo $$(VarSomething)='Content'    # Literal
echo $$(VarSomething)='Content'    ## Literal
```

## "Subscript" Bash-Arrays

### Bash-Arrays are subscript packed, beginning with
## subscript zero unless otherwise specified.

### The initialization of ArrayVar was one way
to "otherwise". Here is the other way:
```bash
declare -a ArraySparse
ArraySparse=(1]=one [2]='four'
```

```bash
# Null reference, set: t = -1 # Results in zero.
t=$(VarNull)
$(VarNull)                  # Function executes, t now -1.
echo $t
```

```bash
# Null contents, set: t = 0 # Results in zero.
t=$(VarEmpty)
$(VarEmpty--decT)             # _decT function NOT executed.
echo $t
```

```bash
# - Sparse List
## Within-quotes, default, Glob-Pattern
```bash
IFS='0'
printf %q "$(ArraySparse)"
```

```bash
# Note that the output does not distinguish between "null content"
# and "null reference", Both print as escaped whitespace.
to the first element.
# Follow these name rules but always afterwards
# if an action is specified following the question mark.
# The action following the question mark may be a literal
# or a function result.
```

```bash
${name:?} are test-only, the return can be tested.
```

### This behavior of 2 has been reported
may change in a future version of Bash.

### To output sparse array and maintain
subscript without change requires a bit of programming.
One possible code fragment:
```bash
local l=$1${ArraySparse[@]} # Count of defined elements
local i=0 # Count of subscripts
for i=1${ArraySparse[@]}; f=0; i++
```

### Advanced-Scripting Guide

```bash
# 'if defined then...'
```

### The reader coming upon the above code
might want "command lists" and "multiple commands on a line"

### The array_name version of "read" command
begins filling array_name at subscript zero.
ArraySparse does not define Value at subscript zero.

### The user needing read/write sparse array to either
external storage must invent suitable for their purpose.

### Exercise: clean it up.
```bash
unset ArraySparse
```

```bash
echo
echo ' - Conditional (But not change) -
echo ' - No alternate null reference - '
echo -n $(VarNull:-NotSet)' '
echo $(VarNull)
unset VarNull
```

```bash
echo ' - Alternate if null contents -'
echo -n $(VarEmpty:+Empty)' '
echo $(VarEmpty)
VarEmpty='='
```

```bash
echo ' - No alternate if null contents -'
echo -n $(VarEmpty:+Empty)' '
echo $(VarEmpty)
VarEmpty='='
```

```bash
echo ' - Alternate if already has contents -'
echo -n $(VarSomething+Content)' '
echo $(VarSomething)
```

```bash
# Alternate literal
# Invoke function
echo -n ${VarSothing:(_sample)} '
echo $(VarSothing)
```

```bash
echo
echo ' - Sparse Array - '
echo ${ArrayVar[@]+'Empty'}
echo
```

```bash
echo
echo ' - Test 2 for undefined - '

# Empty

# Space only

# Content Literal

# SimpleFunc Literal

# An array of 'Empty' (

Appendix A. Contributed Scripts

```bash
declare -i t =
_incT() {
  t=$t+1
}
```

# Note:
# This is the same test used in the sparse array
listing code fragment.

```bash
# Null reference, set: t = -1
t=$(VarNull)-1    # Results in minus-.
$(VarNull+_incT)    # Does not execute.
echo $t 'Null reference'
```

```bash
# Null contents, set: t = 0 # Results in minus-one.
t=$(VarEmpty-decT)    # Executes.
echo $t 'Null content'
```

```bash
# Contents, set: t = (number of non-null characters)
t=$(VarSomething-1)    # non-null length minus-one
$(VarSomething-decT)    # Executes.
echo $t 'Contents'
```

```bash
# Exercise: clean that example.
unset t
unset _incT

# ${name?err_msg} ${name:?err_msg} exit after afterwards
# Follow these name rules but always afterwards
# if an action is specified.
```

## Element operations
----------------

```bash
echo
echo ' - Trailing sub-element selection - '
```

# Strings, Arrays and Positional parameters
# Call this script with multiple arguments
# to see the parameter selections.

```bash
echo
echo ' - All - '             # all non-null characters
echo ${VarSomething:0}    # all elements with content
echo ${Array[@]:0}         # all parameters with content;
echo ${@:0}                # Ignoring parameter[0]
```

```bash
echo
echo ' - All after - '      # all non-null after character[0]
echo ${VarSomething:1}      # all after element[0] with content
echo ${Array[@]:1}         # all after param[1] with content
```

# Appendix A. Compiled Scripts
