for raw devices. While this may not have seemed like a significant addition, many database vendors use raw devices for storage for database tables. The large-device interfaces enable database vendors to address more than 2 gigabytes of space on raw devices.

Since the read and write system calls do not contain disk offset addresses, large-device interfacing was possible by the mere addition of an interface to seek to a 64-bit address. The new interface added was `llseek`, appropriately named as a long lseek. Note the use of the new offset type, `offset_t`, rather than the old `off_t`.

```
```c
typedef longlong_t    offset_t;

offset_t llseek(int fdes, offset_t off, int sbase)
```
```

**Header File** `<sys/unistd.h>`

The new `llseek` interface allowed a process to seek across a 64-bit file offset in any device that supports large access. Only raw disk devices permit large access. Since the `llseek` interface was added primarily for database vendors, and since many database vendors take advantage of asynchronous I/O, two new interfaces were created for asynchronous I/O on large (greater than 2 Gbyte) files.

```
```c
typedef longlong_t    offset_t;

int aioread64(int fd, caddr_t *buf, int bufsz, offset_t offset,
              int whence, aio_result_t *resultp)

int aiowrite64(int fd, caddr_t *buf, int bufsz, offset_t offset,
               int whence, aio_result_t *resultp)
```
```

**Header File** `<sys/asynch.h>`

Note that all of the Solaris 2.5.1 large-device interfaces require application changes.

# 11.6.3 Solaris 2.6: The Large-File OS

Solaris 2.6 was the first Solaris release to provide support for files greater than 2 gigabytes. The file systems were enhanced to deal with files crossing the 2-gigabyte boundary, and a 64-bit file API was introduced to allow applications to access large files.

Since the existing API had been using 32-bit offsets in all of the file seek interfaces, the existing API could not change without breaking Unix 95, POSIX, and binary compatibility. For this reason, a transitional large-file interface was provided in Solaris 2.6.