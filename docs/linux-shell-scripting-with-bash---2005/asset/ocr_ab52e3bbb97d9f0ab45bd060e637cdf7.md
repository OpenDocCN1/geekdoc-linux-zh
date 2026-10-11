```
if test -f "$TMP" -a ! -w "$TMP" ; then
printf "${SCRIPT}:${LINE}: the temp file $TMP exists and cannot\" "be overwritten — aborting" >&2
exit 192
fi
```

This is not exactly the same as

```
if test -f "$TMP" && test ! -w "$TMP" ; then
printf "${SCRIPT}:${LINE}: the temp file $TMP exists and cannot\" "be overwritten — aborting" >&2
exit 192
fi
```

The version using && executes the test command twice and can run slower than the version using the -a switch, so the -a switch is preferred over using && in an if expression.

Parentheses can also be used as long as they are escaped with backslashes. Parentheses have special meaning to the shell. In certain cases, they are required.

One situation that tends to confuse shell programmers is when mixing the not operator with -a or -o switch. In most computer languages, not takes precedence as a unary operator and executes first. In Bash, -a and -o take precedence over the not operator, causing the following test to always be false:

```
if test ! -f "$TMP" -o -f "$TMP" ; then
```

Bash interprets this command as “if the file neither exists nor exists.” This odd behavior is in accordance with the POSIX standard. To get the expected result, you must use parentheses.

```
if test \( ! -f "$TMP" \) -o -f "$TMP" ; then
```

Square brackets are an alternative form of the test command. Using square brackets makes your if commands easier to read.

```
if [ -f "$TMP" -a ! -w "$TMP" ] ; then
printf "${SCRIPT}:${LINE}: the temp file $TMP exists and cannot\" "be overwritten — aborting" >&2
exit 192
fi
```

The square brackets version is in all ways identical to the normal test command. The Korn shell introduced a variation of the test command that used double square brackets. This variation is supported by Bash for compatibility. The Korn shell test will not perform word splitting or pathname expansion between the brackets, making double quotes unnecessary around variable substitutions.

```
if [ [ -f $FILE ] ] ; then
printf "%s\n" "The file exists"
fi
```