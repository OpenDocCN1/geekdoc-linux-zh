The linked list exists within the process’s address space, not in the kernel. `sem_head` points to the first `semaddr` structure on the list, and `sad_next` provides the pointer for support of a singly linked list. The character array `sad_name[]` holds the object name (file name), `sad_addr` points to the actual semaphore, and `sad_inode` contains the inode number of the file that was passed in the `sem_open(3R)` call. Here is the sequence of events.

+   - When entered, `sem_open(3R)` obtains a file lock on the passed file argument, using the `pos4obj_lock()` internal interface.
+   - Once the lock is acquired, `pos4obj_open()` and underlying routines open the file and return a file descriptor.

+     - If this is a new semaphore, the file is truncated with `ftruncate(3C)` to the size of a `sem_t` structure (it does not need to be any larger than that).
+     - If it’s not a new semaphore and the process is opening an existing semaphore, then the linked list is searched, beginning at `semheadp`, until the inode number of the file argument to `sem_open(3R)` matches the `sad_inode` field of one of the `semaddr` structures, which means the code found the desired semaphore.

Once the semaphore is found, the code returns `sad_addr`, a pointer to the semaphore, to the calling program.

The POSIX semaphore code uses the `/tmp` file system for the creation and storage of the files that the code memory maps based on the name argument passed in the `sem_open(3R)` call. For each semaphore, a lock file and a data file are created in `/tmp`, with the file name prefix of `.SEML` for the lock file, and `.SEMD` for the data file. The full file name is prefix plus the strings passed as an argument to `sem_open(3R)`, without the leading slash character. For example, if a `sem_open(3R)` call was issued with `"/sem1"` and the first argument, the resulting file names in `/tmp` would be `.SEMLsem1` and `.SEMDsem1`. This file name convention is used in the message queue code as well, as we’ll see shortly.

If a new semaphore is being created, the following events occur.

+   - Memory for a `semaddr` structure is `malloc`’d, the passed file descriptor is `mmap`’d, the semaphore (`sem_t`) fields and `semaddr` fields are initialized, and the file descriptor is closed.

Part of the initialization process is done with the jump table and a call to `sema_init()`. (`sema_init()` is used for semaphore calls from the Solaris threads library, libthread, and also used for POSIX unnamed semaphores.) `sema_init()` is passed a pointer to a `sem_t` (either from the user code or when invoked from `sem_open(3R)`, as is the case here), an initial semaphore value, and a type.

+   - The fields in `sem_t` are set according to the passed arguments, and the code returns. If a type is not specified, the type is set to `USYNC_PROCESS`.