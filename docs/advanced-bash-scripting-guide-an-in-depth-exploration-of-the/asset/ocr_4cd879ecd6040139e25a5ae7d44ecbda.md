# Advanced Bash-Scripting Guide

```
echo '- Longest prefix -'
echo ${stringZ##1*3}               # Unchanged (not a prefix)
echo ${stringZ##*A}                # abc
echo ${array[@]}##*c}             # ABCABC 123123 ABCABC

echo ${sparseZ[@]}##*c}             # Version-2.05b core dumps.
echo # Has been fixed by Chet Ramey.

echo '- Suffix sub-element removal -'
echo ' - Glob-Pattern match may include the last character. -'
echo ' - Glob-Pattern may be a literal or a function result. -'
echo
echo '- Shortest suffix -'
echo ${stringZ1*3}                   # Unchanged (not a suffix).
echo ${stringZ$*_abc}              # abcABC123ABC
echo ${array[@]}%abc}             # Applied to each element.

echo ${sparseZ[@]}%abc}            # Version-2.05b core dumps.
echo # Has been fixed by Chet Ramey.

echo - It would be nice- Last-Script-Of
echo ${#sparseZ[@]}%               # This is NOT valid Bash.
echo
echo '- Longest suffix -'
echo ${stringZ1*3}                   # Unchanged (not a suffix)
echo ${stringZ$*b*c}                # a
echo ${array[@]}%abc}             # ABCABC 123123 ABCABC A

echo ${sparseZ[@]}*abc}            # Version-2.05b core dumps.
echo # Has been fixed by Chet Ramey.

echo
echo '- Sub-element replacement -'
echo ' - Sub-element at any location in string. -'
echo ' - First specification is a Glob-Pattern -'
echo ' - Glob-Pattern may be a literal or Glob-Pattern result. -'
echo ' - Second specification may be unspecified. Pronounce that' -'
echo ' as: Replace-With-Nothing (Delete) -'
echo

echo # Function returning a simple, Literal, Glob-Pattern
_123() {
    echo -n '123'
}

echo '- Replace first occurrence -'
echo ${stringZ/$_{123}/999}         # Changed (123 is a component)
echo ${stringZ[@}/ABC/xyz}         # xyzABC123ABCabc
echo ${array[@]}/ABC/xyz}       # Applied to each element.
echo ${sparseZ[@]}/ABC/xyz}     # Works as expected.
echo
echo '- Delete first occurrence -'
echo ${stringZ$#_{123}/}
echo ${stringZ[@}/ABC/}
echo ${array[@]}/ABC/}
echo ${sparseZ[@]}/ABC/}
```

Appendix A. Contributed Scripts 781