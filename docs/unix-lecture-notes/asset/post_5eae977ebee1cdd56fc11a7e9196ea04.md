
Listing cp1.c
// First attempt at cp command, based on a program
// by Bruce Molay in Understanding Unix/Linux Programming, p.53

#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>

#define BUFFERSIZE 4096
#define COPYMODE 0644

void die(char* string1, char* string2); // print error and quit

int main(int argc, char *argv[])
{
    int source_fd, target_fd, n_chars;
    char buf[BUFFERSIZE];

    if ( argc != 3 ){
        fprintf( stderr, "usage: %s source destination\n", *argv);
        exit(1);
    }

    // try to open files
    if ( ( source_fd = open(argv[1], O_RDONLY)) == -1 )
        die("Cannot_open_", argv[1]);
    if ( ( target_fd = creat( argv[2], COPYMODE)) == -1 )
        die( "Cannot_creat", argv[2]);

    // copy from source to target
    while ( ( n_chars = read( source_fd , buf, BUFFERSIZE) )
        > 0 ) {
        if ( n_chars != write( target_fd , buf, n_chars ) )
            die("Write_error_to_", argv[2]);
    }
    if ( -1 == n_chars )
        die("Read_error_from_", argv[1]);

    // close both files
    if ( close(source_fd) == -1 || close(target_fd) == -1 )
        die("Error_closing_files", "");

    return 0;
}

void die(char *string1, char *string2)
{
fprintf(stderr,"Error:%s.", string1);
perror(string2);
exit(1);
}

## Comments

- The buffer is declared as an array of BUFFERSIZE chars, which is equal to the maximum number read in a read() call.
- The die() function encapsulates the error handling logic and calls the perror() function.
- Every call to a function in the API is checked for a possible error.
- The main work is in the while loop (lines 32-36). The entry condition is that the read() call transferred one or more bytes. The body is the call to write the bytes just read to the output file. The return value of write() is checked to see if the number of bytes transferred equals the number requested by the call.

If you compile and run this program you will see that it works correctly. But does it run fast? How long will it take to copy a very large file? How does one time programs in UNIX?

## 2.8.4 Timing Programs

The time command is a means of measuring the amount of time (and other resources) that a command uses. The time command has many options, but its simplest form is

```
$ time -p command
```

where command is the command that you wish to know about. The '-p' option tells time to display the traditional POSIX output, which consists of three values, each measured in seconds to two decimal places:

- Elapsed clock time, denoted "real"
- User time, denoted "user"
- System time, denoted "sys"

Elapsed time is the number of seconds from when the command was invoked until it completed. User time is the total amount of time that the process, and any children executing on its behalf, spent running in user mode. System time is the total amount of time spent on the process's behalf running within the kernel, i.e., in privileged mode, including such time spent by its children as well. Non-POSIX output may be more voluminous; you can read the man page for further details. Also, shells such as bash typically define their own version of the time command, so it is best to type the full path name when using it, if you want the non-bash version.

I created a file named bigfile containing about 30 MB of data. When I ran

```
$ time -p cp1 bigfile copy_of_bigfile
```

I got the following output on one of the UNIX systems at Hunter College:

```
real  4.05
user  0.01
sys   0.02
```

What accounts for the difference between the sum of user and system times and the elapsed time? It is the time that the process spent waiting for I/O to complete. When a process issues a request for I/O, it is blocked until the I/O is complete. The time that it spends in this blocked, or waiting, state is part of the elapsed (real) time. cp1 spent about 4 seconds waiting for I/O. Although the amount of time that a process spends waiting for I/O depends heavily on what else the system is doing, the more calls it makes, the longer it will take, on average. The reason for this will be explained below.

As we use cp1 on larger and larger files, we will see worse performance. To create a spreadsheet with the results of the time command I used a different option to it:

/usr/bin/time -f "\t%re\t%U\t%S"

The -f option expects a format string, which I supplied as a tab-separated string of real-time, user-time, and system-time format symbols. This allowed me to open the output with a spreadsheet program for analysis:

| File Size (bytes) | Real | User | Sys |
|---|---|---|---|
| 19,004,256 | 17.28 | 0.00 | 0.05 |
| 38,008,512 | 39.17 | 0.01 | 0.11 |
| 76,017,024 | 73.69 | 0.00 | 0.21 |

Notice that the real and system times increase roughly in proportion to the size of the file over this small sample.

## 2.8.5 Buffering and its Impact on Performance

Consider the cp1 program above. Suppose that N is the size of the file to be copied, measured in bytes. Then the while loop in lines 32 through 36 iterates ⌈N/BUFFERSIZE⌉ times, since each iteration copies BUFFERSIZE bytes. It follows that as BUFFERSIZE is increased the number of iterations decreases inversely, i.e., if we double the buffer size, we halve the number of calls to both read() and write(). The question is, how is the total running time affected as the buffer size increases, in general? Is the amount of time to make a single call to read() proportional to the number of bytes to be read, or are there other components of its running time that are not related to the size of the read?

To answer this question, we will first perform a little experiment. We will revise the cp program so that the buffer size is an input parameter, and run the program on a very large input file with
