# Advanced Bash-Scripting Guide

```
echo `username0 = $(username0-`whoami`)'
# Will not echo.

echo

echo username has not been declared.
echo `username = $(username-`whoami`)'
# Will echo2

username2=
echo `username2 has been declared, but is set to null.`
echo `username2 = $(username2-`whoami`)'
#
# Will echo because of :- rather than just - in condition test.
# Compare to first instance, above.


# Once again:

variable=
# variable has been declared, but is set to null.

echo "${variable-0}" # (no output)
echo "${variable-1}" # 1
#
\unset variable
echo "${variable-2}" # 2
echo "${variable-3}" # 3

exit
```

The default parameter construct finds use in providing "missing" command-line arguments in scripts.

```
DEFAULT_FILENAME=generic,data
filename=${1:-DEFAULT_FILENAME}
# If not otherwise specified, the command block block operates
+# on the file "generic.data".
# Begin-Command-Block
#
#
#
# End-Command-Block
```

```
# From hanoi2.bash example:
DISKS=${1:-E_NOPARAM} # Must specify how many disks.
# Set DISKS to $1 command-line-parameter,
# or to $E_NOPARAM if it is unset.
See also Example 3-4, and Example A-6.
```

Compare this method using an and to list to supply a default command-line argument.
$ {parameter=default}. $ {parameter:=default}

If parameter not set, set it to default.

Chapter 10. Manipulating Variables

129