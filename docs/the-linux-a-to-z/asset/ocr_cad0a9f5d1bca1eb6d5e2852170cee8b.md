```
#include <unistd.h>

int truncate(char *pathname, size_t len);
int ftruncate(int fd, size_t len);
```

If the file referred to in these calls is longer than len bytes in length, then it will be truncated to the specified size and the extra bytes will be lost.

In order for ftruncate() to operate successfully fd must be associated with an open file description that is open for writing (i.e either O_WRONLY or O_RDWR).

# 15.6 File Hierarchy

In order to create, modify and maintain the Linux file and directory hierarchy it is necessary to be able to create and remove directories, and create and remove links in directories to files. All of these things are easy to achieve, especially since they all have their own system calls.

# 15.6.1 mkdir and rmdir System Calls

A Linux process can create a directory with the mkdir() system call. The prototype for the call is:

```
#include <sys/types.h>
#include <fcntl.h>
#include <unistd.h>

int mkdir(char *pathname, mode_t mode);
```

assuming your process has appropriate permissions, a call to mkdir() will create a new directory named pathname with its permission bits set to mode. The value of the mode parameter is modified by the current umask value in the usual way. The new directory will be owned by the effective user ID of the calling process and it will automatically be initialized to contain the dot and dot-dot entries.

If a directory is empty (apart from the dot and dot-dot entries) then it can be removed from the directory hierarchy with the rmdir() system call:

```
#include <unistd.h>

int rmdir(char *pathname);
```