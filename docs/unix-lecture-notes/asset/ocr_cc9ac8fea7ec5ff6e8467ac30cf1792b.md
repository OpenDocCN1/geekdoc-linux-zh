# 3.9  Implementing ls

The first attempt at writing ls will handle multiple command line arguments and not much more. For each argument, if it is a directory, it will display its contents, in no particular order. One problem is solved for us by the opendir() call; the call will fail, returning a -1 if the argument is not a directory. This will be our test for whether or not a filename is that of a directory.

```
```c
Listing: ls.c Version 1
#include <stdio.h>
#include <sys/types.h>
#include <dirent.h>

#define HERE "."
void ls(char []);

int main(int argc, char *argv[])
{
    int i = 1;

    if (1 == argc)    // no arguments; use .
        ls(HERE);
    else
        // for each command line argument, display contents
        while (i < argc) {
            printf("%s\n", argv[i]);
            ls(argv[i]);
            i++;
        }
}

// List the contents of the directory named dirname
// Uses opendir to check whether argument is a directory
// Doesn't check if argument is or "." or ".."
void ls(char dirname[])
{
    DIR        *dir_ptr;    // directory stream
    struct dirent *direntp; // hold one entry

    if ((dir_ptr = opendir(dirname)) == NULL)
        // Could not open — maybe it was not a directory
        fprintf(stderr,"Cannot open %s\n", dirname);
    else
    {
        while ((direntp = readdir(dir_ptr)) != NULL)
            printf("%s\n", direntp->d_name);
        closedir(dir_ptr);
    }
}
```
```