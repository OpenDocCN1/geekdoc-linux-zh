# 8.6.9 The exec Command and Loops

The exec command can be used to open or close standard input or output without creating a subshell. Therefore, when starting a loop, any variables created within the body of the loop will remain when the loop completes. When using redirection in loops, any variables created within the loop are lost.

The exec command is often used to open files for reading and writing, either by name or by file descriptor number. Recall that file descriptors 0, 1, and 2 are reserved for standard input, output, and error. If a file is opened, it will receive the next available file descriptor. For example, if file descriptor 3 is the next free descriptor, the new file will be assigned file descriptor 3.

# EXAMPLE 8.45

```
(The File)
1 $ cat tmp
apples
pears
bananas
peaches
plums

(The Script)
#!/bin/sh
# Scriptname: speller
# Purpose: Check and fix spelling errors in a file
2 exec < tmp        # Opens the tmp file
3 while read line        # Read from the tmp file
do
4     echo $line
5     echo -n "Is this word correct? [Y/N] "
6     read answer < /dev/tty  # Read from the terminal
7     case "$answer" in
8     [Yy]*
9         continue;;
*)
10        echo "What is the correct spelling? "
11        read word < /dev/tty
12        sed "s/$line/$word/g" tmp > error
13        mv error tmp
        echo "$line has been changed to $word."
    esac
14 done
```