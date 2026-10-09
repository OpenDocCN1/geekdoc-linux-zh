
The following code snippet demonstrates retrieving a directory inode:

```c
d = (struct dinode *)kindo_buf(fab0 * sizeof(struct dinode));
printf("\nlnumber %ld info:\n", inumber);
printf("\tmode = 0%o\n", d->di_mode);
printf("\tlinks = %d\n", d->di_nlink);
printf("\towner = %d\n", d->di_uid);
printf("\tmod. time = %s", ctime((time_t *)&d->di_mtime));
exit(EXIT_SUCCESS);
EC_CLEANUP_BGN

    exit(EXIT_FAILURE);
EC_CLEANUP_END
```

The complicated declaration for `sb_buf`:

```c
char sb_buf[((sizeof(struct fs) / DEV_BSIZE) + 1) * DEV_BSIZE];
```

is to round up its size to an even sector, as that’s a requirement for reading raw disk devices on FreeBSD.

The first `lseek` is to `SBLOCK * DEV_BSIZE`, which is the location of the superblock. `SBLOCK` happens to be 16, and `DEV_BSIZE` is the sector size, which is 512, as is true for most disks. The superblock always starts 16 sectors from the start of the file system. The first group of `printf` statements print a few fields from the very long `fs` structure. This is that output:

```text
Superblock info for /dev/ad0s1g:
last time written = Mon Oct 14 15:25:25 2002
number of blocks in fs = 1731396
number of data blocks in fs = 1704331
size of basic blocks in fs = 16384
size of frag blocks in fs = 2048
name mounted on = /usr
```

Next the program finds the i-node supplied as its argument (`argv[1]`) using some macros that are in one of the header files, as the arithmetic is very complicated on an FFS disk. I got the i-number of a file with the `-i` option on the `ls` command:

```text
$ ls -li x
383642 -rw-r--r-- 1 marc marc 11687 Sep 19 13:29 x
```

And this was the rest of the output for i-node 383642:

```text
inumber 383642 info:
mode = 0100755
links = 1
owner = 1001
mod. time = Thu Sep 19 13:29:30 2002
```

I’m not going to spend any more time on low-level disk access—all I really wanted was to illustrate how regular files and special files are related. But you might enjoy modifying the program a bit to display other information on a FreeBSD system if you have one, or even modifying it for another UNIX system that you do have.

## 3.2.3 statvfs and fstatvfs System Calls

Reading the superblock with `read` after finding it on a block or raw device is fun, but there’s a much better way to do it on SUS1-conforming systems (Section 1.5.1) using the `statvfs` or `fstatvfs` system calls:

```c
/* statvfs—get file system information by path */
#include <sys/statvfs.h>
int statvfs(
    const char *path,     /* pathname */
    struct statvfs *buf   /* returned info */
); /* Returns 0 on success or -1 on error (sets errno) */

/* fstatvfs—get file system information by file descriptor */
#include <sys/statvfs.h>
int fstatvfs(
    int fd,               /* file descriptor */
    struct statvfs *buf   /* returned info */
); /* Returns 0 on success or -1 on error (sets errno) */
```

Usually, you’ll use `statvfs`, which returns information about the file system that contains the path given by its first argument. If you have a file opened, you can use `fstatvfs` instead, which returns the same information.

The standard defines fields for the `statvfs` structure, but implementations are not required to support them all. Also, most implementations support additional fields and additional flags for the `f_fflag` field. You’ll have to check your system’s man page for the specifics. If an implementation doesn’t support a standard field, the field is still there, but it won’t contain meaningful information.

```c
/* struct statvfs—structure for statvfs and fstatvfs */
struct statvfs {
    unsigned long f_bsize;       /* block size */
    unsigned long f_fsize;       /* fundamental (fblock) size */
    fsblkcnt_t f_blocks;         /* total number of blocks */
    fsblkcnt_t f_bfree;          /* number of free blocks */
    fsblkcnt_t f_bavail;         /* number of avail. fblocks */
    fsfilcnt_t f_files;          /* total number of i-numbers */
    fsfilcnt_t f_ffree;          /* number of free i-numbers */
    fsfilcnt_t f_favail;         /* number of avail. i-numbers */
    unsigned long f_fsid;        /* file-system ID */
    unsigned long f_flag;        /* flags (see below) */
    unsigned long f_namemax;     /* max length of filename */
};
```

Some comments about this structure:

- Most file systems allocate fairly large blocks to files, given by the `f_fsize` field, to speed up access, but then finish off the file with smaller fragment blocks to avoid wasting space. The fragment-block size is called the *fundamental* block size and is given by the `f_fsize` field; we call it an *fblock* for short. The fields of type `fsblkcnt_t` are in units of blocks, so, to get the total space in bytes, you would multiply `f_blocks` by `f_fsize`.
- The types `fsblkcnt_t` and `fsfilcnt_t` are unsigned, but otherwise implementation defined. They're typically long or long long. If you need to display one and you have a C99 compiler, cast it to `uintmax_t` and use `printf` format `%ju`; otherwise, cast it to `unsigned long long` and use format `%llu`.
- The SUS standards define only two flags for the `f_flag` field that indicate how the file system was mounted:
  - `ST_RDONLY` is set if it’s read only, and
  - `ST_NOSUID` is set if the set-user-ID-on-execution and set-group-ID-on-execution bits are to be ignored on executable files (a security precaution).
- The term “available,” which applies to the `f_bavail` and `f_favail` fields, means “available to nonsuperuser processes.” It might be less that the corresponding “free” fields, so as to reserve a minimum amount of free space on systems where performance suffers when free space gets tight.

FreeBSD, being pre-SUS, doesn’t support the `statvfs` or `fstatvfs` functions, but it does have a similar function called `statfs` whose structure has a different name and mostly different fields. For the basic information, it’s possible to code in a way that works with both `statvfs` and `statfs`, as the following program illustrates.

# Disk Special Files and File Systems

```c
#if _XOPEN_SOURCE >= 4
#include <sys/statvfs.h>
#define FCN_NAME statvfs
#define STATVFS 1

#elif defined(FREEBSD)
#include <sys/param.h>
#include <sys/mount.h>
#define FCN_NAME statfs

#else
#error "Need statvfs or nonstandard substitute"
#endif

void print_statvfs(const char *path)
{
  struct FCN_NAME buf;

  if (path == NULL)
    path = ".";
  ec_neg1( FCN_NAME(path, &buf) )
#ifdef STATVFS
  printf("block size = %lu\n", buf.f_bsize);
  printf("fundamental block (fblock) size = %lu\n", buf.f_fsize);
#else
  printf("block size = %lu\n", buf.f_iosize);
  printf("fundamental block (fblock) size = %lu\n", buf.f_bsize);
#endif
  printf("total number of fblocks = %llu\n",
         (unsigned long long)buf.f_blocks);
  printf("number of free fblocks = %llu\n",
         (unsigned long long)buf.f_bfree);
  printf("number of avail. fblocks = %llu\n",
         (unsigned long long)buf.f_bavail);
  printf("total number of i-numbers = %llu\n",
         (unsigned long long)buf.f_files);
  printf("number of free i-numbers = %llu\n",
         (unsigned long long)buf.f_ffree);
#ifdef STATVFS
  printf("number of avail. i-numbers = %llu\n",
         (unsigned long long)buf.f_favail);
  printf("file-system ID = %lu\n", buf.f_fsid);
  printf("Read-only = %s\n",
         (buf.f_flag & ST_RDONLY) == ST_RDONLY ? "yes" : "no");
  printf("No setuid/setgid = %s\n",
         (buf.f_flag & ST_NOSUID) == ST_NOSUID ? "yes" : "no");
  printf("max length of filename = %lu\n", buf.f_namemax);
#else
  printf("Read-only = %s\n",
         (buf.f_flags & MNT_RDONLY) == MNT_RDONLY ? "yes" : "no");
  printf("No setuid/setgid = %s\n",
         (buf.f_flags & MNT_NOSUID) ? "yes" : "no");
#endif
  printf("\nFree space = %.0f%%\n",
         (double)buf.f_bfree * 100 / buf.f_blocks);
  return;

EC_CLEANUP_BGN
EC_FLUSH("print_statvfs");
EC_CLEANUP_END
}
```

Here’s the output we got on Solaris for the file system that contains the directory `/home/marc/aup` (Linux produces similar output):

```text
block size = 8192
fundamental block (fblock) size = 1024
total number of fblocks = 4473046
number of free fblocks = 3683675
number of avail. fblocks = 3638945
total number of i-numbers = 566912
number of free i-numbers = 565782
number of avail. i-numbers = 565782
file-system ID = 26738695
Read-only = no
No setuid/setgid = no
Max length of filename = 255

Free space = 82%
```

On FreeBSD this was the output for `/usr/home/marc/aup`:

```text
block size = 16384
fundamental block size = 2048
total number of fblocks = 1704331
number of free fblocks = 1209974
number of avail. fblocks = 1073628
total number of i-numbers = 428030
number of free i-numbers = 310266
Read-only = no
No setuid/setgid = no

Free space = 71%
```

The `statvfs` (or `statfs`) system call is the heart of the well-known `df` (“disk free”) command (see Exercise 3.2). Here’s what it reported on FreeBSD:
