
```
30
$ let "CNT=5"
$ let "PRODUCT=CNT++*5"
$ printf "%d\n" "$PRODUCT"
25
$ printf "%d\n" "$CNT"
6
```

In general, it’s a good idea to avoid expressions with this kind of “side-effect,” because it makes your script harder to maintain. Instead, perform increments and decrements on a separate line to make the results clear to read.

The self-referential operators cannot be used with integer variables without the `let` statement.

```
$ COST+=5
bash: COST+=5: command not found
```

## Other `let` Features

Parentheses are allowed in the expressions.

```
$ let "RESULT=(5+3)*2"
$ printf "The expression is %d" "$RESULT"
The expression is 16
```

Assignment in the `let` command is an operator that returns the value being assigned. As a result, multiple variables can be assigned at once.

```
$ let "TEST=TEST2=5"
$ printf "The results are %d and %d\n" "$TEST" "$TEST2"
The results are 5 and 5
```

`let` can evaluate more than one expression at a time. Several, small assignments can be combined on one line.

```
$ let "SUM=5+5" "SUM2=10+5"
```

Excessive numbers of assignments in a single `let` command will lead to readability problems in a script. When each `let` is on a single line, it’s easier to look through the script for a specific assignment.

The conditional expression operator (?) is shorthand for an `if` statement when one of two different expression are evaluated based on the left condition. Because this is a feature of the `let` command, it works only with numeric expressions, not strings. The following example constrains a truth value to a 1 or a 0.

```
$ VALUE=5
$ let "RESULT=VALUE > 1 ? 1 : 0"
$ printf "%d\n" "$VALUE"
1
```

More than one conditional expression operator can be chained together.

```
$ FILE_COUNT='ls -1 | wc -1'
$ let "RESULT=FILE_COUNT=0? 0: (FILE_COUNT%2 == 0 ? \"$FILE_COUNT/2 : FILE_COUNT/2+1)"
$ printf "The files will fit in a report with 2 columns %d high\n" "$RESULT"
The files will fit in a report with 2 columns 11 high
$ printf "%d" "$FILE_COUNT"
22
```

Double parentheses are an alias for *let*. They are used to embed *let* expressions as parameters in another command. The shell replaces the double parentheses with the value of the expression.

```
declare -i X=5;
while (( X > 0 )) ; do
        printf "%d\n" "$X"
done
```

This script fragment prints a list of numbers from four to zero. The embedded *let* reduces X by one each time through the loop and checks to see when the value of X reaches zero.

### temperature.bash: Converting Fahrenheit to Celsius

To review *let* arithmetic, the script *temperature.bash*, shown in Listing 6.2, converts a temperature from Fahrenheit to Celsius.

**Listing 6.2 temperature.bash**

```
#!/bin/bash
#
# temperature.bash: Convert Fahrenheit to Celsius
#
# Ken O. Burch
# CVS $Header$

short -s -o nouse

declare -i FTEMP  # Fahrenheit temperature
declare -i CTEMP  # Celsius temperature

# Title

printf "%s\n" "Fahrenheit-Celsius Conversion"
printf "\n"

# Get the value to convert

read -p "Enter a Fahrenheit temperature: " FTEMP

# Do the conversion

CTEMP="`(${'$'}FTEMP-32) /9`"
printf "The Celsius temperature is %d\n" "CTEMP"

exit 0
```

### Arithmetic Tests

The `test` command can compare numeric values, but it uses different operators than the ones used to compare string values. Because all shell variables are stored as strings, variables can either be compared as numbers or strings depending on the choice of operator. Perl programmers will find this similar to Perl. Bash will not report an error if string operators are used with integer variables.

- `n1 -eq n2` — (*equal*) True if n1 is equal to n2
- `n1 -ne n2` — (*not equal*) True if n1 is not equal to n2
- `n1 -lt n2` — (*less than*) True if n1 is less than n2
- `n1 -le n2` — (*less than or equal*) True if n1 is less than or equal to n2
- `n1 -gt n2` — (*greater than*) True if n1 is greater than n2
- `n1 -ge n2` — (*greater than or equal*) True if n1 is greater than or equal to n2

For example, suppose `RESULT` contains the number of files in the current directory.

```
$ RESULT=`ls -1 | wc -1`
$ printf "4d" "$RESULT"
22
$ test "$RESULT" -gt 20 && printf "&s" "There are a lot of files."
There are a lot of files.
$ test "$RESULT" -le 20 && printf "There are few files"
$
```

These tests are not the same as the string comparison tests. Consider the following example.

```
$ test "$RESULT" \< 3 && printf "As a string, the result is less than 3"
As a string, the result is less than 3
```

In this case, the string 22 is compared with the string 3, and because the string 22 is alphabetically less than 3, the message is printed. Make sure you choose the correct operator to compare with.

### Pattern Recognition

Bash pattern recognition is called *globbing*. Globbing is used to match filenames given to a command, and it is also used by the Korn shell *test* command to match strings.

```
$ ls *.txt
notes.txt     project_notes.txt
```

The pattern-recognition feature works by supplying wildcard symbols that Bash will attempt to match to a string or a filename.

The asterisk (*) character represents zero or more characters. The Korn shell test can be used to match the value of a variable to a string with an asterisk.

```
COMPANY="Athabasca"
if [[ $COMPANY = A* ]] ; then
      printf "The company name begins with a letter a \n"
fi
if [[ $COMPANY = ?* ]] ; then
      printf "The company name begins with a letter a ?\n"
fi
```

This behavior doesn't work when quotation marks are used. Quotation marks tell the Korn shell *test* command not to interpret special characters. A test for "A*" would indicate a file named "A*".

```
COMPANY="Athabasca"
if [[ "$COMPANY" = "A*" ]] ; then
      printf "The company name is A*\n"
fi
```

The question mark (?) character is a wildcard representing any single character.

```
COMPANY="AIC"
if [[ $COMPANY = A?? ]] ; then
      printf "The company name is 3 characters beginning with A\n"
fi
```

You can specify a set of characters using square brackets. You can list individual characters or ranges.

```
if [[ $COMPANY = [ABC]* ]] ; then
      printf "The company name begins with a A, B or C\n"
fi
if [[ $COMPANY = [A-Z]* ]] ; then
      printf "The company name begins with a letter an uppercase letter\n"
fi
if [[ $COMPANY = [A-Z0-9]* ]]; then
    printf "The company name begins with a letter an uppercase letter or number\n"
fi
```

Partial ranges are allowed. If the start of the range is omitted, the range is all ASCII values up to that character. Likewise, the end of the range can be omitted to specify any ASCII characters after the range start character.

If the first character in a square bracket set is a exclamation point (!) or caret (^), characters not in the set count as a match.

If the extending globbing option is on using `shopt -s extglob`, Bash supports several additional patterns:

- `?(pattern-list)` — Matches zero or one occurrence of the given patterns
- `*(pattern-list)` — Matches zero or more occurrences of the given patterns
- `+(pattern-list)` — Matches one or more occurrences of the given patterns
- `@(pattern-list)` — Matches exactly one of the given patterns
- `!(pattern-list)` — Matches anything except one of the given patterns

```
COMPANY="AAA Ballistics Ltd"
if [[ $COMPANY = +([A]*Ltd ) ]]; then
    printf "The company name begins with one or more A's and finishes with Ltd\n"
fi
```

You can separate lists of patterns by using vertical bar characters (|).

```
COMPANY="Champion Ltd"
if [[ $COMPANY = Champion*([Ltd|Corp|Inc] ) ]]; then
    printf "The company name is Champion with a standard business ending\n"
fi
```

Bash defines short forms for common ranges called character classes:

- `[:alnum:]` — Alphanumeric
- `[:alpha:]` — Alphabetic
- `[:ascii:]` — ASCII characters
- `[:blank:]` — Space or tab
- `[:cntrl:]` — Control characters
- `[:digit:]` — Decimal digits
- `[:graph:]` — Non-blank characters
- `[:lower:]` — Lowercase characters
- `[:print:]` — Non-control characters
- `[:punct:]` — Punctuation characters
