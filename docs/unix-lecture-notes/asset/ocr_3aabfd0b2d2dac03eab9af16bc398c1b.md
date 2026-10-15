the O_CREAT flag. Instead it is opened with the current position pointer pointing to the start of the file. The current position pointer is a member of the open file structure, the data structure that is created by the kernel when a file is opened. It points to the position of the next byte to read or write in the file.

For example, to open the file whose path is stored in the C-string file_to_open, one could write

```
if ( ( fd = open(file_to_open, O_RDWR)) == -1 ) {
    perror(file_to_open);
    // handle error here
}
```

# 2.7.2 Logout Records

When a user logs out of a UNIX system, the kernel does some bookkeeping tasks. One of the tasks is to update the utmp file to indicate that the user logged out. In particular, it has to change the utmp record for the login session by changing the ut_type member from USER_PROCESS to DEAD_PROCESS. It also has to change the ut_time member to the current time and zero out the ut_user and ut_host members.

In short, the logout process has to do the following:

+   1. Open the utmp file for reading and writing
+   2. Read the utmp file until it finds the record for the terminal from which the logout took place.
+   3. Modify a copy of the utmp record in the process's memory, and replace the utmp record in the file with the modified one, i.e., modify the utmp file.
+   4. Close the utmp file.

The first and last steps need no discussion. The second step requires being able to identify which utmp record in the file corresponds to the one logout is trying to modify. It cannot use the ut_user member because a single user might have several lines open at a time. The piece of information that is unique is stored in the ut_line. The ut_line member stores the name of the pseudo-terminal as a string such as "pts/4". Only one person can be using a given terminal at the same time, so it is sufficient to match the line.

The more interesting part of this task is how to replace the utmp record in the file. The record may be in the middle of the file, so this operation involves replacing a fixed-size sequence of bytes starting at some specific position in a file with a sequence of the exact same size.

# 2.7.3 Using lseek to Move the File Pointer

As noted above, when a file is opened and a file descriptor is returned for it, a data structure is created by the kernel. This data structure represents the connection to the file. The current position pointer of the data structure is the position of the next byte to read or write in the file. If the file is open for reading, a read of N bytes starts at this position, and then the current position pointer is advanced N bytes. If it is open for writing and writes N bytes, it writes starting at the current