# Advanced Bash-Scripting Guide

Does:
as the right-hand-side of an assignment, preserves the hard quotes protecting the contents of the literal during assignment.

Notes:
The strange names (\*) are used to avoid trampling on the user's chosen names when this is sourced as a library.

```
_Protect_Literal_String_Doc
# The 'for illustration' function form
_protect_literal_str() {
# Pick an unused, non-printing character as local IFS.
# Not required, but that shows that we are ignoring it.
  local IFS=$'x1B' # ESC character
# Enclose the All-Elements-Of in hard quotes during assignment.
  local tmp=$'x27$\\\\'x27'
  local tmp=$'x27$\\\\''' # Even uglier.
  local len=$($tmp) # Info only.
  echo $tmp is len. # Output and information.
}
```

```
# This is the short-named version.
is() {
  local IFS=$'x1B' # ESC character (not required)
  echo=$'x27$\\\\'x27' # Hard quoted parameter glob
}
```

```
# <<:'_Protect_Literal_String_Test'
# # Remove the above to disable this. # # #
```

![](bbox=[0.0, 0.0, 0.1, 0.1])

```
See how that looks when printed.
echo " - Test One - "
_protect_literal_str 'Hello ${user}'
_protect_literal_str 'Hello ${username}'
echo
```

```
Which yields:
# - Test One
# 'Hello ${user}' is 13 long.
# 'Hello ${username}' is 21 long.
```

```
# Looks as expected, but why all of the trouble?
# The difference is hidden inside the Bash internal order
++ of operations.
# Which shows when you use it on the RHS of an assignment.
```

```
# Declare an array for test values.
declare -a array2
```

```
# Assign elements with various types of quotes and escapes.
array2=$(_pls ${Me})' 'Hello ${You}'\'Pass: ${pw}\' )
```

```
# Now list that array and see what is there.
echo " - Test Two - -
```

# Appendix A. Contributed Scripts

628