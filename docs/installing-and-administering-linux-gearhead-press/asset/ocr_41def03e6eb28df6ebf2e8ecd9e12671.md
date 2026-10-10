# Tapes and Floppy Diskettes, Continued

| COMMAND | DESCRIPTION |
| :--- | :--- |
| (empty) | -v Verbose\n-d Create needed directory for relative path names\n-u Unconditional to override last modification date\n\nExample:\n$ cpio -o > /dev/fd0\n\nfilename1\n\nfilename2\n\n<Ctrl>-d\n\nOr $ cpio -iv filename1 < /dev/fd0 |
| tar | Alternative utility to back up and restore files |


# Transmitting

| COMMAND | DESCRIPTION |
| :--- | :--- |
| mail | Send and receive mail. With username argument, send mail to that user. Without username argument, display your mail. When processing your mail, at the ? prompt for each mail item, you can use the following subcommands, too:\n\nd Delete\n\ns Append\n\nq Quit\n\n<Enter> Skip\n\nm Forward |
| uucp | Copy file to other UNIX system (UNIX-to-UNIX copy) |
| uux | Execute on a remote system (UNIX-to-UNIX execute) |