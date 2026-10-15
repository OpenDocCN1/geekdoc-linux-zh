# 12.6.10 The exec Command and Loops

The exec command can be used to close standard input or output without creating a sub-shell.

# EXAMPLE 12.48

(The File)

```
1  cat tmp
apples
pears
bananas
peaches
plums
```

(The Script)

```
#!/bin/ksh
# Scriptname: spellerr
# Purpose: Check and fix spelling errors in a file

2  exec < tmp      # Opens the tmp file
3  while read line  # Read from the tmp file
do
4    print $line
5    print -n "Is this word correct? [Y/N] "
6    read answer </dev/tty  # Read from the terminal
    case $answer in
    [Yy]*)
        continue
        ;;
    *)
        print "New word? "
7      read word </dev/tty
        sed "s/$line/$word/" tmp > error
        mv error tmp
8
        print $word has been changed.
        ;;
    esac
done
```

# EXPLANATION

+   1 The contents of the tmp file are displayed.
+   2 The exec command changes standard input (file descriptor 0), so that instead of input coming from the keyboard, it is coming from the tmp file.
+   3 The while loop starts. The read command gets a line of input from the tmp file.