Since the read and write system calls do not contain disk offset addresses, large-device interfacing was possible by the addition of an interface to seek to a 64-bit address. The new interface added was 11seek, appropriately named as a long 11seek. Note the use of the new offset type, offset_t, rather than the old off_t.

```
typedef longlong_t      offset_t;
offset_t 11seek(int fdes, offset_t off, int sbase)
```

# Header File <sys/unistd.h>

The 11seek interface allowed a process to seek across a 64-bit file offset in any device that supports large access. Only raw disk devices permit large access. Since the 11seek interface was added primarily for database vendors, and since many database vendors take advantage of asynchronous I/O, two new interfaces were created for asynchronous I/O (greater than 2 Gbyte) files.

```
typedef longlong_t      offset_t;
iadore64(int fd, caddr_t *buf, int bufsz, offset_t offset,
 whence, ai_result_t *result)
owrite64(int fd, caddr_t *buf, int bufsz, offset_t offset,
 whence, ai_result_t *resultp)
```

# Header File <sys/asynch.h>

Note that all of the Solaris 2.51 large-device interfaces require application changes.

# 11.6.3 Solaris 2.6: The Large-File OS

Solaris 2.6 was the first Solaris release to provide support for files greater than 2 gigabytes. The file systems were enhanced to deal with files crossing the 2-gigabyte boundary, and a 64-bit API was introduced to allow applications to access large files.

Since the existing API had using 32-bit offsets in all of the file interfaces, the existing APIs could not change without breaking Unix 95, POSIX, and binary compatibility. For this reason, a transitional large-file interface was provided in Solaris 2.6.

# 11.6.3.1 The Large-File Summit

Sun was not the only vendor to address the large-file compatibility issues, and an industry summit was called to specify a common set of large-file application interfaces for 32-bit environments (see the large-file summit documentation at http://www.sas.com/standard/large.file/). The large-file summit specified a new set of interfaces, similar to the Unix 95/POSIX interfaces, but with an extension of 64 added to the name of the interface. For example, the 32-bit