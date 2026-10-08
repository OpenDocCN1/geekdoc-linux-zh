
# Appendix B

### Table B-1: Common UNIX commands (Options)

| Command | Purpose | Useful Options |
| :--- | :--- | :--- |
| rm | Remove a file | -i requests confirmation before deleting a file.<br>-r deletes a specified directory and its contents. |
| rmdir | Remove a directory | -i requests confirmation before deleting a file.<br>-r deletes a specified directory and its contents. |
| sed | Specify an editing command or a script file containing sed commands | -a appends text after a line.<br>-d deletes specified text.<br>-e specifies multiple commands on one line.<br>-n indicates line numbers.<br>-p displays lines.<br>-s substitutes specified text. |
| set -o noclobber | | Prevents files from being overwritten by the > operator |
| sh | Execute a shell script | -n reads commands without executing them. |
| sort | Sort and merge multiple files | + designates the position that follows an offset (+) as a character position, not a field position.<br>+n sorts on the field specified by n.<br>-b ignores leading blank characters.<br>-d sorts in dictionary order.<br>-f indicates that a specified character separates the fields.<br>-m merges files before sorting.<br>-n sorts numbers arithmetically.<br>-o directs the sorted output to a specified file. |
| tail | Display the last few lines of a file | -n n displays the last n lines of the specified file. |
| test | Compare values and validate file existence | ! logical negation<br>-a logical AND<br>-b tests if a file exists and is a lock special file (which is a block-oriented device, such as a disk or tape drive).<br>-c tests if a file exists and is a character special file (that is, a character-oriented device, such as a terminal or printer).<br>-d true if a file exists and is a directory.<br>-e true if a file exists.<br>-eq equals to.<br>-f tests if a file exists and is a regular file.<br>-ge greater than or equal to<br>-gt greater than<br>-le less than or equal to<br>-lt less than<br>-n tests for a non-zero string length.<br>-ne not equal to<br>-o logical OR<br>-r true if a file exists and is readable.<br>-s true if a file exists and its size is greater than zero.<br>string tests for a non-zero string length.<br>string1 = string2 tests two strings for equality.<br>string1 != string2 tests two strings for inequality.<br>-w true if a file exists and is writeable<br>-x true if a file exists and is executable<br>-z tests for a zero-length string. |
| top | Display a list of the most CPU-intensive tasks, such as the processor state, in real time | -c displays the command line that initiated each process. -l ignores any idle processes. -q displays output continually, with no delay between outputs. -s causes the top command to run in secure mode, disabling its interactive commands. -S runs top in cumulative mode, which displays the cumulative CPU time used by a process. |
| touch | Change a file's time and date stamp | -a updates access time only. -c prevents touch from creating a file that it does not exist. -m updates the modification time only. |
| tput | Format screen text | clear clears the screen. cols prints the number of columns on the current terminal. cup moves the screen cursor to a specified row and column. rmso disables boldface output. smso enables boldface output. |
| tr | Translate characters | -d deletes input characters found in string 1 from the output. -s checks for sequences of string 1 repeated consecutive times. |
| trap | Executes a command when a specified signal is received from the operating system | |
| umount | Disconnect the file system partitions from the directory tree | |
| uniq | Select unique lines or rows | -d outputs one copy of each line that has a duplicate. -u outputs only the lines of the source file that are not duplicated. |
| wc | Count the number of lines, bytes, or words in a file | -c counts the number of bytes or characters. |
| whatis | Display a brief description of a command | -l counts the number of lines.<br>-w counts the number of words. |
| who | See who is logged on to UNIX | -H displays column headings.<br>-i displays session idle times.<br>-q displays a quick list of users. |

### Table B-2: UNIX utilities by category

| Command | Purpose |
| :--- | :--- |
| **File Processing Utility** | |
| afo | Create an archive or restore files from archive |
| awk | Process files |
| cat | Display or join files |
| cmp | Compare two files |
| comm | Compare sorted files and show differences |
| cp | Copy files |
| cpio | Copy and back up files to an archive |
| cut | Select characters or fields from input lines |
| dd | Copy and convert input records |
| diff | Compare two text files and show differences |
| fdformat | Format a floppy disk at a low level |
| find | Find files within file tree |
| fmt | Format text very simply |
| grep | Match patterns in a file |
| groff | Process embedded text-formatting codes |
| gzip | Compress or decompress files |
| head | Display the first part of a file |
| ispell | Check one or more files for spelling errors |
| less | Display text files (pause when screen is full) |
| ln | Create a link to a file |
| lpr | Print file (hard copy) |
| ls | List file and directory names and attributes |
| man | Display documentation for commands |
| mkdir | Create a new directory |
| mkfs | Build a UNIX file system |
| mv | Rename and move files and directories |
| od | Dump formatted file |
| paste | Horizontally concatenate files |
| pr | Display and format files |
| rdev | Query or set the root image device |
| rm | Remove files |
| rmdir | Remove directory |
| sed | Edit streams (non-interactive) |
| sort | Sort or merge files |
| tail | Display the last lines of files |
| tar | Copy and back up files to a tape archive |
| touch | Change file modification dates |
| uniq | Display unique lines of sorted file |
| wc | Count lines, words, and bytes |
| **System Status Utility** | |
| chgrp | Change the group associated with a file |
| chmod | Change the access permissions of a file |
| chown | Change the owner of a file |
| date | Set and display date and time |
| df | Display the amount of free space remaining on disk |
| du | Summarize file space usage |
| file | Determine file type (e.g., shell script, executable, ASCII text, and others) |
| finger | Display detailed information about users who are logged on |
| free | Display amount of free and used memory in the system |
| kill | Terminate a running process |
| ps | Display process status by process identification number and name |
| sleep | Suspend execution for a specified time |
| top | Dynamically display process status, like ps, but in real time |
| w | Display detailed information about users who are logged on |
| who | Display brief information about users who are logged on |
| **Network Utility** | |
| ftp | Transfer files over a network |
| rcp | Remotely copy a file from network computer |
| rlogin | Log on to a remote computer |
| rsh | Execute commands on a remote computer |
| rwho | Display the names of users attached to a network |
| telnet | Connect to remote computer on a network |
| **Communication Utility** | |
| mail | Send electronic mail messages |
| mesg | Deny (mesg n) or accept (mesg y) messages |
| pine | Send and receive electronic mail and news |
| talk | Let users simultaneously type messages to each other |
| write | Send a message to another user |
| **Programming Utility** | |
| configure | Automatically configure program source code |
| gcc | Compile C and C++ programs |
| make | Maintain program source code |
| patch | Update source code |
| **Source Code Utility** | |
| ci | Create changes in Revision Control Systems (RCS) |
| co | Retrieve an unencoded revision of an RCS file |
| cvs | Manage concurrent access to files in a hierarchy |
| rcs | Create or change attributes of an RCS file |
| rlog | Print a summary of the history of an RCS file |
| **Miscellaneous Utility** | |
| at | Execute a shell script at a specified time |
| cal | Display a calendar for a month or year |
| crontab | Schedule a command to run at a preset time |
| expr | Evaluate expressions (used for arithmetic and string manipulations) |
| fsck | Check and fix problems on a file system (repairs damages) |
| tee | Clone output stream to one or more files |
| tr | Replace specified characters, like a translation filter |
| tty | Display terminal pathname, like the built-in command, pwd |
| xargs | Convert standard output of one command into arguments for another |

### Table B-3: vi Commands

| Command | Purpose |
| :--- | :--- |
| ! | Leave vi temporarily |
| . (repeat) | Repeat your most recent change |
| / | Search forward for a pattern of characters |
| d$ or D | Delete from the cursor to the end of the line |
| d0 | Delete from the cursor to the start of the line |
