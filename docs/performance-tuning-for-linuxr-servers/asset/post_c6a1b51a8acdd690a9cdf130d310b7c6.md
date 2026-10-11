
for drive /dev/hdb MaxMultSect is set to 16. Most IDE hard drives made in the past few years support 32-bit access. If your hard disk supports 32-bit access, you want this value to be 32.

The following command sets the MaxMultSect value to 32:

```
# hdparm -c 1 /dev/hdb
```

The number 1 turns MaxMultSect on; the number 0 turns MaxMultSect off. MaxMultSect is usually off by default. The default value is 16.

Test your hard drive's performance both before and after setting these various commands by typing the following:

```
# hdparm -T -t /dev/hdb
```

This command produces output like the following:

```
/dev/hdb:
Timing buffer-cache reads:  128MB in  0.97 seconds=131.96MB/sec
Timing buffered disk reads:  64MB in  3.80 seconds=16.84 MB/sec
```

The next field to look at is the drive's write caching. The command to turn on write caching is as follows:

```
# hdparm -W 1 /dev/hdb
```

The number 1 turns write caching on; the number 0 turns write caching off.

Another useful option to hdparm is using_dma. The command to turn dma on is the following:

```
# hdparm -d 1 /dev/hdb
```

This command produces output like the following:

```
/dev/hdb:
setting using_dma  to  1 (on)
     using_dma    =  1 (on)
```

The number 1 turns `using_dma` on; the number 0 turns `using_dma` off.

None of these settings is saved over a reboot. You have to add the appropriate commands to your /etc/rc.d/rc.sysinit file if you are using Red Hat to be sure they are run automatically on startup. If you are not running a Red Hat distribution, an easy way to find the file to change is to do a grep in the /etc directory, as shown in the following example:

```
# cd /etc
# grep -r hdparm . | more
```

After you find the configuration file that sets the options through hdparm, change that file to use the new parameters that were set with hdparm.

It is a good idea to run with the new settings for a while to ensure they are right for the system before they are permanently updated in a configuration file.

## Fragmenting a File System

Over time, the files on your file system can get broken into pieces so that they are not contiguous. This reduces file system performance when reading or writing data to the file. Defragmenting rearranges all the data on a volume so that files are written on consecutive sectors and tracks. This means that the disk heads have less moving to do in order to read from or write to a file. Thus, overall system throughput increases. To defragment a file system, see the sections describing each file system later in this chapter. Be aware that disk defragmentation can take quite a long time and it is the kind of operation that should be done when the system has a relatively small load running on it.

## File Synchronization

By default, Linux systems read from and write to a buffer/page cache that is kept in memory. They avoid actually transferring data to disk until the buffer is full or until the application calls a sync function to flush the buffer/page cache. This strategy increases performance by avoiding the relatively slow mechanical process of writing to disk more often than necessary.

Input and output operations are of two types:

- Asynchronous I/O, which frees the application to perform other tasks while input is written or read
- Synchronized I/O, which performs the write or read operation and verifies its completion before returning

Synchronized I/O is useful when the integrity of data and files is critical to an application. Synchronized output assures that the data that is written to a device is actually stored there. Synchronized input assures that the data that is read from a device is a current image of data on that device.

Two levels of file synchronization are available:

- Data integrity
  - Write operations: Data in the buffer is transferred to disk, along with file system information necessary to retrieve the data.
  - Read operations: Any pending write operations relevant to the data being read complete with data integrity before the read operation is performed.
- File integrity
  - Write operations: Data in the buffer and all file system information related to the operation are transferred to disk.
  - Read operations: Any pending write operations relevant to the data being read complete with file integrity before the read operation is performed.

### How to Assure Data or File Integrity

You can assure data integrity or file integrity at specific times by using function calls, or you can set file status flags to force automatic file synchronization for each `read` or `write` call associated with that file.

Note that using synchronized I/O can degrade system performance.

### Using Function Calls

You can choose to write to buffer/page cache as usual and call functions explicitly when you want the program to flush the buffer to disk. For instance, you may want to use the buffer/page cache when a significant amount of I/O is occurring and call these functions when activity slows down. Two functions are available:

| Function | Description |
| :--- | :--- |
| fdatasync | Flushes all data buffers, providing operation completion with data integrity. |
| fsync | Flushes all data and file control information from the buffers, providing operation completion with file integrity. |

For a complete description of these functions, refer to the man pages for `fdatasync` and `fsync`.

### Using File Descriptors

If you want to write data to disk in all cases automatically, you can set file status flags to force this behavior instead of making explicit calls to `fdatasync` or `fsync`.

To set this behavior, use these flags with the `open` function:

| Flag | Description |
| :--- | :--- |
| O_DSYNC | Forces data synchronization for each write operation. For **example:** `fd = open("filea", O_RDWR\|O_CREAT\|O_DSYNC, 0666);` |
| O_SYNC | Forces file and data synchronization for each write operation. For **example:** `fd = open("filea", O_RDWR\|O_CREAT\|O_SYNC, 0666);` |

## Performance Implications of sync/fsync

Forced synchronization of the contents of real memory and disk takes place in several ways:

- An application program makes an `fsync()` call for a specified file. This causes all the pages that contain modified data for that file to be written to disk. The writing is complete when the `fsync()` call returns to the program.
- An application program makes a `sync()` call. This causes all the file pages in memory that contain modified data to be scheduled for writing to disk. The writing is *not necessarily* complete when the `sync()` call returns to the program.
- A user can enter the `sync` command, which in turn issues a `sync()` call. Again, some of the writes might not be complete when the user is prompted for input (or the next command in a shell script is processed).
- The *sync* daemon, bdflush, is called at regular intervals. This ensures that the system does not accumulate large amounts of data that exists only in volatile RAM.

## bdflush Parameters

bdflush starts, flushes, or tunes the buffer-dirty-flush daemon. It is related to the operation of the kernel's virtual memory VM subsystem. bdflush can be tuned to improve file system performance. If you change some of the values from the default, as shown next, the system can be more responsive. The file /proc/sys/vm/bdflush controls the operation of the bdflush kernel daemon.

The default setup for the bdflush parameters under Red Hat and SUSE systems is

```
50 500 0 0 500 3000 60 20 0
```

To view the bdflush settings on a system, issue the following command:

```
# cat /proc/sys/vm/bdflush
```

```
50 500 0 0 500 3000 60 20 0
```

The first parameter (nfract), default 50, governs the maximum number of dirty buffers in the buffer cache. Setting this to a high value means that the kernel can delay writes for a longer time, but it also means that it needs to do so when memory becomes low. A low value spreads disk I/O more evenly.

The second parameter (ndirty), default 500, is the maximum number of dirty buffers that bdflush can write to the disk at one time. A high value means burst I/O, whereas a small value can lead to memory shortage when bdflush isn't started frequently.

The third and fourth parameters are not currently used.

The fifth parameter (interval), default 500, is the delay between kupdate flushes.

The sixth parameter (age_buffer), default 3000, is the time for a normal buffer to age before it is flushed.

The seventh parameter (nfract_sync), default 60, is the percentage of buffer cache that is dirty to activate bdflush synchronously.

The eighth parameter (nfract_stop_bdflush), default 20, is the percentage of buffer cache that is dirty to stop bdflush.

The ninth parameter is not currently used.

In the following example, nfract is increased from 50 to 100, and ndirty is increased from 500 to 1200:

```
# echo "100 1200 0 0 500 3000 60 20 0" >/proc/sys/vm/bdflush
```
