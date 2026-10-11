8.4 Moving Around in the File Hierarchy

259

```
/* ch08-getcwd.c --- demonstrate getcwd().
Error checking omitted for brevity */

#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>

int main(void)
{
    char buf[PATH_MAX];
    char *cp;

    cp = getcwd(buf, sizeof(buf));
    printf("Current dir: %s\n", buf);

    printf("Changing to ..\n");
    chdir("..");                /* "cd .." */

    cp = getcwd(buf, sizeof(buf));
    printf("Current dir is now: %s\n", buf);

    return 0;
}
```

This simple program prints the current directory, changes to the parent directory, and then prints the new current directory. (*cp* isn't really needed here, but in a real program it would be used for error checking.) When run, it produces the following output:

```
$ ch08-getcwd
Current dir: /home/arnold/work/prehall/progex/code/ch08
Changing to ..
Current dir is now: /home/arnold/work/prehall/progex/code
```

Formally, if the *buf* argument is *NULL*, the behavior of *getcwd*() is undefined. In this case, the GLIBC version of *getcwd*() will call *malloc*() for you, allocating a buffer of *size* size. Going even further out of your way to be helpful, if *size* is 0, then the buffer it allocates will be “big enough” to hold the returned pathname. In either case, you should call *free*() on the returned pointer when you're done with the buffer.

The GLIBC behavior is helpful, but it's not portable. For code that has to work across platforms, you can write a replacement function that provides the same functionality while having your replacement function call *getcwd*() directly if on a GLIBC system.