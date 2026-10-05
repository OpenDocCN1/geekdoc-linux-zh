# 480 COMMAND REFERENCE

-h after closing the system, it is halted, that is, it no longer reacts to input. The screen displays the message 'system halted'. Subsequently, the computer can be switched off.

-n carries out the shutdown particularly quickly (bypassing the Init-V processes).

-r after closing down the system, a restart is carried out.

-t seconds specifies the time between the warning message and the kill signal for the processes (default: 20 seconds).

# Example

```
root# shutdown -h -t 3 now
```

closes down the system with lightning speed. When you choose this shutdown variation, no text editors or other programs with unsaved files should be running, as a time of three seconds is not sufficient to make safety backups.

# sort [options] file

sort sorts the specified file and displays the result on screen. Foreign language special characters are not sorted lexically correctly (but by their character codes, that is, they appear after all other letters), sort can be controlled with a large number of options, of which the most important are described here.

-c checks whether the file is sorted or not.

-f treats upper and lower case letters as equivalent.

-m merges two or more presorted files into one large sorted file. This is faster than joining the files first and sorting them afterwards.

-o result.file writes the output into the specified file. This file may be the file to be sorted.

-r sorts in reverse order.

-ts specifies the separator character between two columns (the default is 'white space', that is, an arbitrary mixture of space and tab characters).

+n1 [-n2] only considers the characters between the nth (inclusive) and the n2th (exclusive) column. Column numbering starts with 0! Columns are normally separated by space or tab characters, but by -t. When n2 is not specified, all characters from n1 up to the end of line are considered.

The command sort file > file does not have the desired effect, but leads to file being deleted. When you want to redirect the result of the sort command into a file, you must either specify a different file name than the name of the file to