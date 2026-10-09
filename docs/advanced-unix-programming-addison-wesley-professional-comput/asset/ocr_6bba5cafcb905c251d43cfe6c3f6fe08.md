```
**ftok**—generate System V IPC key

#include <sys/ipc.h>

key_t ftok(
    const char *path,      /* pathname of existing file */
    int id                 /* desired key number */
);
/* Returns key on success or -1 on error (sets errno) */
```

Actually, ftok can generate lots of keys from the same path; the desired key is specified by the id argument, which could be a character, as only its lowest 8 bits are used. It can't be zero, either. For example, if you need four keys for your application (one message queue, one semaphore set, and two shared memory segments), you can use a single path name (e.g., /tmp/myappkeys) and call ftok four times with the second argument taking on the values q, s, m, and n (or whatever four values you like). The pathname must already exist—ftok will not create it.

Recall that I said that System V IPC objects are not files and do not have i-nodes. The file whose name is passed to ftok exists only to provide a global name for key generation. The contents of the file don't matter. It's not guaranteed that if the file is unlinked and re-created the same keys will be generated even though the name stays the same, so you should create the file when the application is installed or run for the first time and leave it around until the application is uninstalled.

Two different paths are guaranteed to generate two different keys only if the paths are in the same file system (Section 3.2.4). If you're worried about different applications accidentally using the same key, you can use the special key IPC_PRIVATE in an Xget call (explained further in Section 7.5.1), which guarantees you a unique IPC object without using ftok or specific keys at all. You have to somehow publish the resulting identifier so all the processes that need it can get it; one way to do that is to write it to a file whose name is known to those processes. But, for most purposes, including all the examples in this book, we're going to assume that ftok conflicts won't occur.

To summarize:

+   * You access a System V IPC object with an identifier. How you get the identifier doesn't matter—it can be an argument to an exec, passed with a message, read from a file, returned from a system call like msgget, or whatever.