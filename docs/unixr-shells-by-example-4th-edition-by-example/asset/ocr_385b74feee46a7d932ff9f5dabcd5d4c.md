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

+   1 The statement reads: If the number of arguments is not equal to 2, print the error message and send it to standard error, then exit the script with an exit status of 1. Either the built-in test command or the `let` command can be used to test numeric expressions.
+   2 The fi marks the end of the block of statements after then.
+   3 The statement reads: If the value of the first positional parameter passed in from the command line is less than 0 or greater than 30, then print the message and exit with a status of 2. See Table 14.4 on page 884 for numeric operators.
+   4 The fi ends the if block.
+   5 The statement reads: If the value of the second positional parameter passed in at the command line is less than or equal to 20 (512-byte blocks), then print the message and exit with a status of 3.
+   6 The fi ends the if block.
+   7 The find command starts its search in the root directory. The -xdev option prevents find from searching other partitions. The -mtime option takes a number argument, which is the number of days since the file was modified, and the -size option takes a number argument, which is the size of the file in 512-byte blocks.