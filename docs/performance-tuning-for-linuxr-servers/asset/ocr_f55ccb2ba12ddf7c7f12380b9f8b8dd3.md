# ## Using Function Calls

You can choose to write to buffer/page cache as usual and call functions explicitly when you want the program to flush the buffer to disk. For instance, you may want to use the buffer/page cache when a significant amount of I/O is occurring and call these functions when activity slows down. Two functions are available:

| Function | Description |
|---|---|
| fdatasync | Flushes all data buffers, providing operation completion with data integrity. |
| fsync | Flushes all data and file control information from the buffers, providing operation completion with file integrity. |

For a complete description of these functions, refer to the man pages for `fdatasync` and `fsync`.

# ## Using File Descriptors

If you want to write data to disk in all cases automatically, you can set file status flags to force this behavior instead of making explicit calls to `fdatasync` or `fsync`.

To set this behavior, use these flags with the `open` function:

| Flag | Description |
|---|---|
| O_DSYNC | Forces data synchronization for each write operation. For **example:** `fd = open("filea", O_RDWR|O_CREAT|O_DSYNC, 0666);` |
| O_SYNC | Forces file and data synchronization for each write operation. For **example:** `fd = open("filea", O_RDWR|O_CREAT|O_SYNC, 0666);` |