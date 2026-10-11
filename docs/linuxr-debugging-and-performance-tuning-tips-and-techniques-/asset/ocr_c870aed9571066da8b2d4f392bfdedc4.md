Each process has a current working directory. Each new process inherits its current directory from the process that started it (its parent). Two functions let you change to another directory:

```
```c
#include <unistd.h>

int chdir(const char *path);        POSIX
int fchdir(int fd);                 XSI
```
```

The chdir() function takes a string naming a directory, whereas fchdir() expects a file descriptor that was opened on a directory with open().$^{6}$ Both return 0 on success and –1 on error (with errno set appropriately). Typically, if open() on a directory succeeded, then fchdir() will also succeed, unless someone changed the permissions on the directory between the calls. (fchdir() is a relatively new function; older Unix systems won’t have it.)

These functions are almost trivial to use. The following program, ch08-chdir.c, demonstrates both functions. It also demonstrates that fchdir() can fail if the permissions on the open directory don’t include search (execute) permission:

```
```c
1 /* ch08-chdir.c -- demonstrate chdir() and fchdir(). */
2 /* Error checking omitted for brevity */
3
4 #include <stdio.h>
5 #include <fcntl.h>
6 #include <unistd.h>
7 #include <sys/types.h>
8 #include <sys/stat.h>
9
10 int main(void)
11 {
12     int fd;
13     struct stat sbuf;
14
15     fd = open(".", O_RDONLY);   /* open directory for reading */
16     fstat(fd, & sbuf);          /* obtain info, need original permissions */
17     chdir("..");               /* cd .. */
18     fchmod(fd, 0);             /* zap permissions on original directory */
19
20     if (fchdir(fd) < 0)        /* try to `cd' back, should fail */
21         perror("fchdir back");
22 }
```
```

> $^{6}$ On GNU/Linux and BSD systems, you can apply the dirfd() function to a DIR \* pointer to obtain the underlying file descriptor; see the GNU/Linux dirfd(3) manpage.