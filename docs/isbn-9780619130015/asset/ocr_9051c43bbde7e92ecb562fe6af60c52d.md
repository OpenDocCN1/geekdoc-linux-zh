# 500 appendix B

| Command | Purpose | Useful Options |
| :--- | :--- | :--- |
| **top** | Display a list of the most CPU-intensive tasks, such as the processor state, in real time | -c displays the command line that initiated each process. -l ignores any idle processes. -q displays output continually, with no delay between outputs. -s causes the top command to run in secure mode, disabling its interactive commands. -S runs top in cumulative mode, which displays the cumulative CPU time used by a process. |
| **touch** | Change a file's time and date stamp | -a updates access time only. -c prevents touch from creating a file that it does not exist. -m updates the modification time only. |
| **tput** | Format screen text | clear clears the screen. cols prints the number of columns on the current terminal. cup moves the screen cursor to a specified row and column. rmso disables boldface output. smso enables boldface output. |
| **tr** | Translate characters | -d deletes input characters found in string 1 from the output. -s checks for sequences of string 1 repeated consecutive times. |
| **trap** | Executes a command when a specified signal is received from the operating system | |
| **umount** | Disconnect the file system partitions from the directory tree | |
| **uniq** | Select unique lines or rows | -d outputs one copy of each line that has a duplicate. -u outputs only the lines of the source file that are not duplicated. |
| **wc** | Count the number of lines, bytes, or words in a file | -c counts the number of bytes or characters. |

Table B-1
(continued)