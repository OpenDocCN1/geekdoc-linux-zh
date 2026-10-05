# 1018 CHAPTER 27 PROGRAMMING THE BOURNE SHELL

To see how conditional expressions works, replace the line that tests age in the age2 script with the following conditional expression. You must surround the [[ and ]] tokens with whitespace or a command terminator, and place dollar signs before the variables:

```
if [[ 30 < $age $age < 60 ]]; then
```

You can also use test's relational operators -gt, -ge, -lt, -le, -eq, and -ne:

```
if [[ 30 -lt $age $age -lt 60 ]]; then
```

The test builtin tests whether strings are equal. The [[ expression ]] syntax adds comparison tests for string operators. The > and < operators compare strings for order, "aa" = "bbbb". The operator tests for pattern match, not just equality; [[ string = pattern ]] is true matches. This operator is not symmetrical; the pattern must appear on right side of the sign. For example, [[ artist = a ]] is true (=0), whereas [[ a*= artist ]] is false (=1):

```
$ [[ artist = a ]]
$ echo $$
$ [[ a*= artist ]]
$ echo $?

```

The next example uses a command line that starts with a compound condition. The condition tests that the directory bin and the file src/myscript.bash exists. If this is true, cp copies src/myscript.bash to bin/myscript. If the copy succeeds, chmod makes myscript executable. If any of these steps fails, echo displays a message.

```
$ [[ -d bin -f src/myscript.bash ]] && cp src/myscript.bash \
/myscript && chmod +x bin/myscript || echo "Cannot make \
executable version of 'myscript'
```

# STRING PATTERN MATCHING

The Bourne Again Shell provides string pattern-matching operators that can manipulate patterns and other strings. These operators can delete from string prefixes or suffixes that match patterns. Table 27-7 lists the four operators.

Table 27-7 String operators

| Operator | Function |
| --- | --- |
| # | Removes minimal matching prefixes |
| ## | Removes maximal matching prefixes |
| % | Removes minimal matching suffixes |
| %% | Removes maximal matching suffixes |

The syntax for these operators is

```
${varname pattern}
```