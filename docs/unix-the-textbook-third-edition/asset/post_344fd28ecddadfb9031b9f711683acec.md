
break;
/* handle other errors */
default:
}

We address this issue for network-related system calls, particularly, the select() system call, in Chapter 20.

## 18.11 SYSTEM CALLS FOR MANIPULATING DIRECTORIES

UNIX provides a set of system calls for creating, deleting, and changing directories. Table 18.14 lists these calls along with their purpose. We will not discuss these calls any further. However, you will get to practice them in a programming exercise given at the end of the chapter.

As a system programmer, you do not need to know the details of the kernel data structures for directories. However, such knowledge enhances your understanding of the UNIX operating system and your skills as a programmer. The most important directory data structure is defined in the <sys/dirent.h> file. Here is the definition of the directory entry in Solaris that is independent of the file system.

```
struct dirent {
    ino_t       d_ino;      /* "inode number" of entry */
    off_t       d_off;      /* offset of disk directory entry */
    unsigned short d_reclen; /* length of this record */
    char        d_name[1];  /* name of file */
};
```

In FreeBSD, it the directory entry is defined as

```
struct dirent {
    __uint32_t d_fileno;    /* file number of entry */
    __uint16_t d_reclen;    /* length of this record */
    __uint8_t  d_type;      /* file type, see below */
```

| TABLE 18.14 UNIX System Calls Related to Directories |
| System Call | Purpose |
| chdir() | Change directory |
| mkdir() | Create directory |
| rmdir() | Remove directory |
| remove() | Remove an empty directory; equivalent to rmdir() |
| rename() | Rename a directory |

```
__uint8_t d_namlen;    /* length of string in d_name */
char    d_name[255 + 1]; /* name must be no longer than this */
};
```

Definitions in both systems have three common fields: the inode number for the file (called the file number under FreeBSD), the file name, and the length of the directory entry. The BSD definition contains two additional fields: the length of the string in the name field and the type of the file the entry represents. The type field is not strictly required here because the inode contains this information, as discussed in Section 18.9. The Solaris definition contains the additional field of offset of the disk directory entry.

You can use several C library functions to manipulate directories, including opendir(), closedir(), readdir(), telldir(), seekdir(), and rewinddir().

## EXERCISE 18.17

Browse through the man pages for the previously stated calls to manipulate directories in order to understand their syntax and semantics. Then write small programs to use them in order to enhance your understanding of these calls.

## 18.12 IMPORTANT WEB RESOURCES

Table 18.15 lists useful websites for UNIX system programming and related topics.

| TABLE 18.15 Web Resources for the UNIX System Programming and Related Topics |
| https://www.freebsd.org/ | Home page for FreeBSD. Contains a lot of useful material, including FreeBSD source, manual pages, support, SVN repository, forums, user groups, etc. |
| http://www.oracle.com/technetwork/server-storage/solaris11/documentation/index.html | Webpage for Oracle Solaris 11 product documentation. |
| http://www.gnu.org/ | Homepage for the free operating system GNU by the Free Software Foundation. Work on GNU's kernel, The Hurd, started in 1990 (before work on Linux had started). |
| http://www.tutorialspoint.com/index.htm | An excellent site for tutorials on almost all known programming languages, including C, and development environments. |
| http://www.tutorialspoint.com/c_standard_library/index.htm | The C standard library. |
| www.compileonline.com (http://www.tutorialspoint.com/codingground.htm) | A great free site for online editing, compiling, and running programs in almost any language from assembly language to Python and from Algol-68 to Ruby. |

## SUMMARY

UNIX provides two APIs for software development: the language libraries and the system call interface. Application programmers typically use the interface provided by the language libraries and system programmers primarily use the system call interface. We described the UNIX system calls and their use in small programs for the I/O of file data and attributes. Our focus was on regular files.

Before discussing the system calls, we explained that four types of events cause the control to be transferred to the kernel code. They are interrupt, trap, signal, and system call, with the first two caused by the system hardware and the last two primarily caused by software. We also discussed the details of events that happen in order to execute a system call. We discussed briefly the C Standard Library and the difference between Standard I/O and low-level I/O through system calls.

We discussed the system calls for data I/O for regular files and I/O of file attributes using the open(), creat(), read(), write(), close(), truncate(), and stat() system calls. For random I/O, we used the lseek() system call to set the file pointer to the byte where the next read or write operation should be performed. We showed the use of the lseek() and write() system calls to illustrate how holes can be created in a regular file under UNIX. We showed the holes created in a file by displaying its octal dump using the od command.

We discussed briefly several system calls and C library functions for accessing and manipulating file attributes and directories. These calls are: access(), chdir(), chmod(), chown(), closedir(), mkdir(), opendir(), read(), readdir(), rename(), rewinddir(), seekdir(), telldir(), umask(), utime().

We also showed the kernel data structures for the stat structure and a directory entry, as described in the <sys/stat.h>, <limits.h>, and <sys/limits.h> files.

Finally, we showed how you can use a small piece of code to restart a system call if it is interrupted in the middle of execution and the underlying OS kernel does not automatically restart it. Such interruption may occur when blocking I/O is done on slow devices, keyboards, and files such as pipes, FIFOs, and sockets.

## QUESTIONS AND PROBLEMS

- 1. What is a system call? List names of three system calls in each of the following categories:
- a. Process control
- b. File management
- c. Device management
- d. Information maintenance
- e. Communications
