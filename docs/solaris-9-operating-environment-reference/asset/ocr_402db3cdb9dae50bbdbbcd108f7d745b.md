```
awk '/\/\/' { print "quote:", $0 }
```

The rest of the examples show simple awk programs.
The following example writes to the standard output all input lines for which field 3
is greater than 5.

```
$3 > 5
```

The following example writes every tenth line.
(NR % 10) == 0

The following example writes any line with a substring matching the regular
expression.
/ (G|D) [2-9] ([[:alpha:]]*)/

The following example prints any line with a substring containing a G or D, followed
by a sequence of digits and characters. It uses character classes digit and alpha to
match language-independent digit and alphabetic characters.
/ (G|D) ([[:digit:]][[:alpha:]]*)/

The following example writes any line in which the second field matches the regular
expression and the fourth field does not.
$2 /xyz/ && $4 ~ /xyz/

The following example writes any line in which the second field contains a backslash.
$2 - \\\

The following example writes any line in which the second field contains a backslash.
Note that backslash escapes are interpreted twice, once in lexical processing of the
string and once in processing the regular expression.
$2 - "\\\\\""

The following example writes the penultimate and the last field in each line with
fields separated by colons.
OFS=":";print $(NF-1), $NF

The following example writes the line number and number of fields in each line.
The three strings representing the line number, the colon, and the number of fields are
catenated and that string is written to standard output.
(print NR ":" NF)

The following example writes lines longer than 72 characters.
(length($0) > 72)

The following example writes the first two fields in opposite order, separated by the
OFS.
( print $2, $1 )