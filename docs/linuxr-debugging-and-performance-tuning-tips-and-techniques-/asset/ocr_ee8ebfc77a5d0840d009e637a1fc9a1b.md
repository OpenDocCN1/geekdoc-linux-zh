```
```POSIX
#include <sys/types.h>
#include <sys/stat.h>

mode_t umask (mode_t mask);
```
```

The return value is the old umask. Thus, to determine the current mask, you must set it to a value and then reset it (or change it, as desired):

```
```
mode_t mask = umask(0);	/* retrieve current mask */
(void) umask(mask);		/* restore it */
```
```

Here is an example of the umask in action, at the shell level:

+   $ umask *Show the current mask*  
+   0022  
+   $ touch newfile *Create a file*  
+   $ ls -l newfile *Show permissions of new file*  
+   -rw-r--r-- 1 arnold devel 0 Mar 24 15:43 newfile  
+   $ umask 0 *Set mask to empty*  
+   $ touch newfile2 *Create a second file*  
+   $ ls -l newfile2 *Show permissions of new file*  
+   -rw-rw-rw- 1 arnold devel 0 Mar 24 15:44 newfile2

# 4.6.2 Creating Files with creat()

The creat()⁴ system call creates new files. It is declared as follows:

```
```POSIX
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

int creat (const char *pathname, mode_t mode);
```
```

The mode argument represents the permissions for the new file (as discussed in the previous section). The file named by pathname is created, with the given permission as modified by the umask. It is opened for writing (only), and the return value is the file descriptor for the new file or -1 if there was a problem. In this case, errno indicates the error. If the file already exists, it will be truncated when opened.

In all other respects, file descriptors returned by creat() are the same as those returned by open(); they're used for writing and seeking and must be closed with close().