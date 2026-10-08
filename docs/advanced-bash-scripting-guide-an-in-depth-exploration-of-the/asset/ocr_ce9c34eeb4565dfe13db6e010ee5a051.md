# Advanced Bash-Scripting Guide

```
# The length of an array, measured in defined elements,
# including null content elements.
echo
echo 'Defined content count: ${#ArrayVar[@]}' elements'.
# That is NOT the maximum subscript (4).
# That is NOT the range of the subscripts (1 .. 4 inclusive).
# It IS the length of the linked list.
###
```

```
# Both the maximum subscript and the range of the subscripts
# be found with additional scripting programming.
###
```

```
# The length of a string, measured in non-null elements (characters):
echo
echo '- Quoted, Glob-Pattern references -'
echo 'Non-Null character count: "${#VarSomething}"'.
```

```
# The length of an array, measured in defined elements,
# including null-content elements.
echo
echo 'Defined element count: "${#ArrayVar[@]}"'.
```

```
# Interpretation: Substitution does not affect the ${ ... } operation.
# Suggestion:
# Always use the All-Elements-Of character
# + if that is what is intended (independence from IFS).
```

```
# Define a simple function.
# I include an underscore in the name
# to make it distinctive in the examples below.
###
# Bash separates variable names and function names
# in different namespaces.
# The Mark-One eyeball isn't that advanced.
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
($simplesimple # Gives an error message:
# line 436: SimpleFunc: command not found
```