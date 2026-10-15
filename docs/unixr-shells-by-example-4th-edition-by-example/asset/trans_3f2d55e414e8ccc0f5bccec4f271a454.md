

# FORMAT

```
if command
then
    command
    command
fi
```

(Using test for numbers and strings -- old format)

```
if test expression
then
    command
fi
```

or

```
if [ string/numeric expression ] then
    command
fi
```

(Using test for strings -- new format)

```
if [[ string expression ]] then
    command
fi
```

(Using let for numbers -- new format)

```
if (( numeric expression ))
```

# EXAMPLE 14.19

```
1 if grep "$name" /etc/passwd > /dev/null 2>&1
2 then
3     echo Found $name!
fi
```

# EXPLANATION

1 The grep command searches for its argument, name, in the /etc/passwd database. Standard output and standard error are redirected to /dev/null, the UNIX bit bucket.

# EXPLANATION (CONTINUED)

3 The fi terminates the if on line 2.

4 The test command fails if more than one word appears before the = operator. For example, if the user entered yes, you betcha, the answer variable would evaluate to three words, causing the test to fail. $answer is enclosed in double quotes to prevent the resulting error message shown here.

5 The compound command operators [[ ]] allow the expansion of shell metacharacters in a string expression. The variable does not need quotes surrounding it, even if it contains more than one word, as it did with the old test command. (The double equal sign can be used to replace the single equal sign.)

6 The shopt built-in, if set to extglob, allows expanded parameter expansion. See Table 14.11 on page 955.

7 The answer variable is set to the string "not really".

8 Extended pattern matching is used here. The expression reads: If the value of the answer variable matches a string starting with no or No and if followed by zero or one occurrences of the expression in the parentheses, the expression is true. The expression could be evaluated to no, No, no way, No way, not really, or Not really.

# The exit Command and the ? Variable.

The exit command is used to terminate the script and return to the command line. You may want the script to exit if some condition occurs. The argument given to the exit command is a number ranging from 0 to 255. If the program exits with 0 as an argument, the program exited with success. A non-zero argument indicates some kind of failure. The argument given to the exit command is stored in the shells ? variable.

# EXAMPLE 14.21

```
(The Script)
$ cat bigfiles
# Name: bigfiles
# Purpose: Use the find command to find any files in the root
# partition that have not been modified within the past n (any
# number within 30 days) days and are larger than 20 blocks
# (512-byte blocks)

1 if (( $# != 2 ))   # [ $# -ne 2 ]
then
    echo "Usage: $0 mdays size" 1>&2
    exit 1
2 fi
3 if (( $1 < 0 || $1 > 30 ))   # [ $1 -lt 0 -o $1 -gt 30 ]
then
    echo "mdays is out of range"
    exit 2
4 fi
```

# EXAMPLE 14.21 (CONTINUED)

```
5  if (( $2 <= 20 ))   # [ $2 -le 20 ]
    then
        echo "size is out of range"
        exit 3
6  fi
7  find / -xdev -mtime $1 -size +$2
```

(The Command Line)

```
$ bigfiles mdays size
Usage: bigfiles mdays size
```

```
$ echo $?
1
$ bigfiles 400 80
mdays is out of range
$ echo $?
2
$ bigfiles 25 2
size is out of range
$ echo $?
3
$ bigfiles 2 25
(Output of find prints here)
```

a. Not implemented on versions prior to bash 2.x. On older versions could also be written if let (( $# != 2 )).

b. Same as above. On older versions could also be written if let (( $1 < 0 || $1 > 30 )).

# EXPLANATION

- 1 The statement reads: If the number of arguments is not equal to 2, print the error message and send it to standard error, then exit the script with an exit status of 1. Either the built-in test command or the `let` command can be used to test numeric expressions.
- 2 The fi marks the end of the block of statements after then.
- 3 The statement reads: If the value of the first positional parameter passed in from the command line is less than 0 or greater than 30, then print the message and exit with a status of 2. See Table 14.4 on page 884 for numeric operators.
- 4 The fi ends the if block.
- 5 The statement reads: If the value of the second positional parameter passed in at the command line is less than or equal to 20 (512-byte blocks), then print the message and exit with a status of 3.
- 6 The fi ends the if block.
- 7 The find command starts its search in the root directory. The -xdev option prevents find from searching other partitions. The -mtime option takes a number argument, which is the number of days since the file was modified, and the -size option takes a number argument, which is the size of the file in 512-byte blocks.

