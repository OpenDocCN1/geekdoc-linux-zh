```
function mycp () {
case $# in
    0)       # Zero arguments
             # File descriptor 3 duplicates standard input
             # File descriptor 4 duplicates standard output
             exec 3<&0 4>&1
             ;;
    1)       # One argument
             # Open the file named by the argument for input
             # and associate it with file descriptor 3
             # File descriptor 4 duplicates standard output
             exec 3< $1 4>&1
             ;;
    2)       # Two arguments
             # Open the file named by the first argument for input
             # and associate it with file descriptor 3
             # Open the file named by the second argument for output
             # and associate it with file descriptor 4
             exec 3< $1 4> $2
             ;;
    *)       echo "Usage: mycp [source [dest]]"
             return 1
             ;;
esac
# Call cat with input coming from file descriptor 3
# and output going to file descriptor 4
cat <&3 >&4
# Close file descriptors 3 and 4
exec 3<&- 4<&-
}
```

The real work of this function is done in the line that begins with cat. The rest of the script arranges for file descriptors 3 and 4, which are the input and output of the cat command, respectively, to be associated with the appropriate files.

![](bbox=[0.08, 0.71, 0.96, 0.93])

```
$ cat sortmerg
#!/bin/bash
usage () {
if [ $# -ne 2 ]; then
echo "Usage: $0 filel file2" 2>&1
exit 1
fi
}
# Default temporary directory
: ${TMPDIR:=/tmp}
```