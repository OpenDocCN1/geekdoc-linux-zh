Therefore, the main use of **mknod** is to make the special files, usually in the `/dev` directory, that are used to access devices. As this is generally done only when a new device driver is installed, the **mknod** command is used, which executes the system call.

The **perms** argument uses the same bits and macros as were defined for the **stat** structure in Section 3.5.1, and **dev** is the device-ID as defined there. If you’ve installed a new device driver, you’ll know what the device-ID is.

# ### 3.8.3 fcntl System Call

In Section 2.2.3, which you may want to reread before continuing, I explained that several **open file descriptors** can share the same **open file description**, which holds the file offset, the status flags (e.g., **O_APPEND**), and access modes (e.g., **O_RDONLY**). Normally, you set the status flags and access modes when a file is opened, but you can also get and set the status flags at any time with the **fcntl** system call. You can also use it to get, but not set, the access modes.

```
```
#include <unistd.h>
#include <fcntl.h>

int fcntl(
    int fd,            /* file descriptor */
    int op,            /* operation */
    ...               /* optional argument depending on op */
);
/* Returns result depending on op or -1 on error (sets errno) */
```
```

There are ten operations in all, but I’m only going to discuss four of them right here. The others will be discussed elsewhere, as indicated in **Table 3.4**.

| Operation | Purpose | Where |
|:----------|:--------|:------|
| F_DUPFD   | Duplicate file descriptor | Section 6.3 |
| F_GETFD   | Get file-descriptor flags | Here |
| F_SETFD   | Set file-descriptor flags (uses third `int` argument) | Here |
| F_GETFL   | Get file-description status flags and access modes | Here |