
# grep_minus_n SHOW LINE_NUMBERS.ksh OUTPUT

## 执行信息
`OUTPUT`: `grep_minus_n SHOW LINE_NUMBERS.ksh,OUTPUT`

`HOW THE SCRIPT WAS EXECUTED`: `./grep_minus_n SHOW LINE_NUMBERS.ksh`

`OUTPUT` follows:

## 说明
`Comment`: This script is `.grep_minus_n SHOW LINE_NUMBERS.ksh`.

`PURPOSE`: Display the line number and contents of any record that contains your string.

`LOOKING FOR`: `_Toto_in FILE: /tmp/testfile.11268`

## METHOD 1
We're going to use a simple `grep`

to find `Toto` in `FILE: /tmp/testfile.11268`

The following lines contain `Toto`:

```
+   5:Dorothy (and little Toto, too!).
6:Toto, I have a feeling that we're not in Kansas anymore.
```

## METHOD 2: Same task, different formatting:

`NOTE`: The first method is MUCH faster.

```
print "METHOD2: Same task, different formatting:"
print "NOTE: The first method is MUCH faster.\n"
counter=0
while read - record
do
  ((counter++)) # Add 1 to the record counter.
  grep -c counts the numbers of What_to_find
  grep -i ignores case.
  if [ $(echo "$record" | grep -ci What_to_find) -gt 0 ]; then
    print "FOUND: ${what_to_find}_ in line number $counter of FILE: $testfile"
  fi
done
done < testfile
```

```
print "\nHere the testfile we used as input:"
cat -n testfile

rm testfile # Remove (delete) the testfile.
print "\nDONE. $0\n"
```

`FOUND`: `Toto` in line number `5` of `FILE: /tmp/testfile.11268`

`FOUND`: `Toto` in line number `6` of `FILE: /tmp/testfile.11268`

+ Here's the testfile we used as input:

```
1 The Wizard of Oz
2 The Tin Man
3 The Scarecrow
4 The Cowardly Lion
5 Dorothy (and little Toto, too!!)
6 Toto, I have a feeling that we're not in Kansas anymore.
```

`DONE`: `.grep_minus_n v_show_string_NOT_containing_string.ksh`

# grep_minus_v_show_lines_NOT_containing_string.ksh

```
PROGRAM: grep_minus_v_show_lines_NOT_containing_string.ksh
#!/bin/bash
# PROGRAM: grep_minus_v_show_lines_NOT_containing_string.ksh
# PURPOSE: display all Lines in a file that do NOT contain user's string.
# PROGRAMMER: Larry Smith. Revised by on __date__
# DIFFICULTY: Medium
# USAGE: See examples below. (Do a find on "USAGE").
```

`clear` Clear the user's screen

`print` `\nComment: This script is $0.`

`print` `"PURPOSE: display all lines in a file that do NOT contain user's string."`

`# "$# holds the number of arguments that the user entered on the command line.`

```
if [ "$# -ne 2 ]; then 
  print "must be 2 arguments: (1) what to find, (2) filename"
  print \nUSAGE EXAMPLE:\n"
  print "how you would print all lines that DO NOT BEGIN with 'This is line 2'\n"
  print "in the file named file.txt"
  print '/grep_minus v show lines NOT containing_string.ksh "This is line 2" file.txt'
  print ""
  exit
fi
```

`what_to_find="$1"` # `"$1"` the first argument from the command line.

`filename="$2"`

`print` `\nuser's string =_${what_to_find}_ FILENAME: $filename\n`

`# "$# contains all arguments from the command line.`

`# NOTE: WRONG: for file in "*"`

```
for file in $@; do
  # if it's a regular file with size (not empty) AND is readable, then ...
  if [ -f "$file" && -s "$file" -r "$file" ]; then
    grep -v "$what_to_find" "$file"
    # grep -vi "$what_to_find" "$file" # Use this line to ignore case.
  fi
done
```

`print` `\nDONE: $0"`

## 输出示例
`OUTPUT`: `/grep_minus v_show_NOT_containing_string.ksh.OUTPUT`

`HOW THE SCRIPT WAS EXECUTED`:

`./grep_minus show lines NOT_containing_string.ksh 'This is line 2' file.txt`

`OUTPUT` follows:

`Comment`: This is script `./grep_minus v show lines_NOT_containing_string.ksh`.

`PURPOSE`: Display all lines in a file that do NOT contain user's string.

`User's string`: `.This is line 2 FILENAME: file.txt`

This is line 1 of the file named 'file.txt'.

This is LINE 3 in the file named 'file.txt'.

And here's the final line in a boring file named 'file.txt'.

This is the final line in a boring file named 'file.txt'.

`DONE`. `./grep_minus v_show lines_NOT_containing_string.ksh`

# grep_NO_FRILLS.ksh

```
PROGRAM: /grep_NO_FRILLS.ksh
#!/bin/ksh
# PROGRAM: grep_NO_FRILLS.ksh
# PURPOSE: Show all lines that match a string or pattern.
# PROGRAMMER: Larry. Revised by __date__
# DIFFICULTY LEVEL: Easy!
# USAGE: ./grep_NO_FRILLS.ksh
```

`clear` Clear the user's screen

`print` `\nComment: This script is $0.`
