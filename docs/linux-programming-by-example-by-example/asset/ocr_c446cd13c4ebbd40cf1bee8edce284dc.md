You can clearly see that the file has one set of permissions after its creation, and another set after the fchmod call. After creating the file, chmod uses the system function to display the file's permissions, calls fchown to change them, and then uses another system call to display the change permissions.

# ### Changing Ownership

Changing a file's ownership is analogous to changing its permissions. The chown and fchown calls accomplish this task. They are prototyped in <unistd.h> as follows:

```
int chown(const char *pathname, uid_t owner, gid_t group);
int fchown(int fd, uid_t owner, gid_t group);
```

These two calls change the owner and group of the file specified by the nullterminated string in pathname or the file descriptor fd to owner and group. As with all the functions discussed in this chapter, these two return 0 on success; upon failure, they return -1 and set errno to an appropriate value. The decision whether to use chown or fchown depends on several factors. If you know the file's name, you would probably want to use chown. If you have opened or created the file using open or creat, which return file descriptors, you would probably want to use fchown because you know the file descriptor. If you know both the filename and the file descriptor, which one to use is a coin toss. In this situation, I would prefer to use fchown because it requires less typing.

# ### Example

![](bbox=[0.03, 0.44, 0.17, 0.5])

# ### Example

This program creates a file, and then changes its ownership. Note that in order for it to work correctly, it must be run by the root user. In addition, you must replace the values assigned to owner and group with values that make sense for your system. The easiest way to accomplish this is to use the id command to obtain your UID and GID, and then substitute those values into the source code.

```
/*
 * chgown.c - Create a file and change its mode
 */
#include <stdlib.h>
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <fcntl.h>
```