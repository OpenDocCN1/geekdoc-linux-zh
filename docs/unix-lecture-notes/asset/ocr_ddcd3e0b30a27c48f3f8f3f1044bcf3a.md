```
#include <limits.h>
#ifndef PIPE_BUF
#define PIPE_BUF POSIX_PIPE_BUF;
#endif

char chunk[PIPE_BUF];
```

An alternative that may work on your system is to use the fpathconf() system call to determine the value of the atomic write size dynamically. The fpathconf() system call returns the value of various system dependent configuration values associated with an open file descriptor. The fpathconf() function’s synopsis and description is

```
#include <unistd.h>

long fpathconf(int filedes, int name);
long pathconf(char *path, int name);

DESCRIPTION
fpathconf() gets a value for the configuration option name
for the open file descriptor filedes.
```

The second argument to fpathconf() is a mnemonic name defined in the man page. These are names such as _PC_NAME_MAX, _PC_PATH_MAX, and _PC_PIPE_BUF. Each name has a different usage, and its validity depends upon whether the given file descriptor is that of a file, a directory, a pipe, or a terminal. If filedes is a pipe, then the constant _PC_PIPE_BUF is supposed to tell fpathconf() to return the maximum number of bytes that may be written atomically to that pipe. It may not return this value. This will be explained below.

Although it is not necessary to know the value of PIPE_BUF, it is an interesting exercise to learn its value and make sure that it has the magical properties it is supposed to have. The following program is designed to demonstrate (but not prove) that writes of up to PIPE_BUF bytes are atomic, and that larger writes may not be atomic. It also demonstrates how to create multiple writers and a single reader. The program creates two writer processes and one reader. One writer writes 'X's into the pipe, the other 'y's. They each write the same number of characters each time. The command line argument specifies the number of writes that each makes to the pipe. The idea is that if the number is large enough the scheduler will time slice them often enough so that one will write for a while, then the next, and so on. The parent is the reader. It reads the data from the pipe and stores it in a file. The parent reads smaller chunks since it does not matter.

# Listing 8.3: pipedemo2.c

```
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <stdlib.h>
#include <fcntl.h>
#include <limits.h>
#include <signal.h>
#include <sys/wait.h>
```