```
fsblkcnt_t f_bfree
```

The total number of free blocks in the filesystem.

```
fsblkcnt_t f_bavail
```

The number of blocks that may actually be used. Some filesystems reserve a percentage of the filesystem’s blocks for use by the superuser, in case the filesystem fills up. Modern systems reserve around 5 percent, although this number can be changed by an administrator. (See tune2fs(8) on a GNU/Linux system, and tuneefs(8) on Unix systems.)

```
fsfilcnt_t f_files
```

The total number of inodes (“file serial numbers,” in POSIX parlance) on the filesystem. This number is usually initialized and made permanent when the filesystem is created.

```
fsfilcnt_t f_ffree
```

The total number of free inodes.

```
fsfilcnt_t f_favail
```

The number of inodes that may actually be used. Some percentage of the inodes are reserved for the superuser, just as for blocks.

```
unsigned long int f_fsid
```

The filesystem ID. POSIX doesn’t specify what this represents, and it’s not used under Linux.

```
unsigned long int f_flag
```

Flags giving information about the filesystem. POSIX specifies two: ST_RDONLY, for a read-only filesystem (such as a CD-ROM), and ST_NOSUID, which disallows the use of the setuid and setgid permission bits on executables. GNU/Linux systems provide additional flags: They are listed in Table 8.2.

```
unsigned long int f_namemax
```

The maximum length of a filename. This refers to each individual component in a pathname; in other words, the maximum length for a directory entry.