# Advanced Bash–Scripting Guide

```
exit 0
${var/##patt/replacement}
```

If prefix of var matches replacement, then substitute replacement for patt.

```
${var/*#patt/replacement}
```

If suffix of var matches replacement, then substitute replacement for patt.

# Example 9–17. Matching patterns at prefix or suffix of string

```
#/bin/bash
# Pattern replacement at prefix / suffix of string.

v0=abc1234zip1234abc # Original variable.
echo v0 = $v0 # abc1234zip1234abc
echo

# Match at beginning (beginning) of string.
v1=$(v0/##ABCDEF) # abc1234zip1234abc
echo v1 = $v1 # ABCDE1234zip1234abc
||

# Match at suffix (end) of string.
v2=$(v0%#ABCDEF) # abc1234zip123abc
echo v2 = $v2 # abc1234zip1234ABCDEF
|----|

echo
echo

# Must match at beginning / end of string,
#+ otherwise no replacement results.
v3=$(v0#/12300) # Matches, but not at beginning.
echo v3 = $v3 # abc1234zip1234abc
# NO REPLACEMENT.
v4=$(v0%#12300) # Matches, but not at end.
echo v4 = $v4 # abc1234zip1234abc
# NO REPLACEMENT.
```

```
exit 0
${!varprefix*}, ${!varprefix@}
```

Matches all previously declared variables beginning with varprefix.

```
xyz23=whatever
xyz24=

a=${!xyz*} # Expands names of declared variables beginning with "xyz"
echo "a = $a@" # a = xyz23 xyz24
a=${!xyz24} # Same as above.
echo "a = $a@" # a = xyz23 xyz24
```

# 9.3. Parameter Substitution