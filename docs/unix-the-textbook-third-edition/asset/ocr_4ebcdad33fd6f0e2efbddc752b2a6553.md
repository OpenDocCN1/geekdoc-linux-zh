of the file passed as a command line argument. It then displays the size of the file (in bytes) if it is a regular file. Otherwise, it displays an error message using the library call perror().

```
% cat stat.c
#include <sys/stat.h>
#include <sys/types.h>
int main(int argc, char *argv[])
{
    struct stat sv;
    if (argc != 2) {
        printf("Inappropriate number of command line arguments.\n");
        exit(0);
    }
    if (stat(argv[1], &sv) == 0 && S_ISREG(sv.st_mode))
        printf("File size is %d bytes\n", sv.st_size);
    else
        perror("stat");
}
```

```
% gcc48 -w stat.c
% ./a.out stat.c
File size is 374 bytes
% ls -l stat.c
-rw-r--r-- 1 sarwar faculty 374 Jan 29 23:52 stat.c
% ./a.out ~
stat: No such file or directory
% ./a.out /usr
stat: No such file or directory
%
```

Note that the error message for the ./a.out ~ and ./a.out /usr commands is stat: error 0 on Solaris.

# 18.9.4 Accessing and Manipulating File Attributes

UNIX provides several system calls for modifying file attributes, including file access permissions, file owner, and file access times. We do not discuss these system calls in detail. Table 18.13 contains brief descriptions of some system calls related to the manipulation of file attributes and their purpose.

# EXERCISE 18.14

Browse through the stat structure definition on Solaris. What are the differences between the definitions of this structure on FreeBSD and Solaris?