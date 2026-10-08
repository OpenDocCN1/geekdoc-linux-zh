# Advanced Bash-Scripting Guide

```
# Pass all options to getopt_simple().
getopt_simple "$@"
echo test is '$test'
echo test2 is '$test2'
\exit 0 # See also, UseGetOpt.sh, a modified version of this script.
---
```

```
sh getopt_example.sh /test=value1 /test2=value2

Parameters are '/test=value1 /test2=value2'
Processing parameter of: '/test=value1'
Parameter: 'test', value: 'value1'
Processing parameter of: '/test2=value2'
Parameter: 'test2', value: 'value2'
test is 'value1'
test2 is 'value2'
```

# Substring Replacement

$${string/substring/replacement}
Replace first match of $substring with $replacement. [50]
${string/substring/replacement}
Replace all matches of $substring with $replacement.

```
stringZ=abc123ABCabc      # xyzABC123ABCabc
echo ${stringZ/xyz}       # Replaces first match of 'abc' with 'xyz'.

echo ${stringZ//xyz}       # xyzABC123ABCxyz
# Replaces all matches of 'abc' with '#'.

echo
echo "$stringZ"         # abc123ABCabc
echo                      # The string itself is not altered!

# Can the match and replacement strings be parameterized?
match=abc
repl=000
echo ${string}/$match/${repl} # 000ABC123ABCabc
echo ${string}//$match/${repl} # 000ABC123ABC000
# Yes!
echo
nn What happens if no replacement string is supplied?
echo ${string/abc}         # ABC123ABC
echo ${string//abc}        # ABC123ABC
```

$${string/substring/replacement}
If $substring matches front end of $string, substitute $replacement for $substring.
${string%substring/replacement}
If $substring matches back end of $string, substitute $replacement for $substring.

# Chapter 10. Manipulating Variables

126