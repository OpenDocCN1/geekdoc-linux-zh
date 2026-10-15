

break;
/* handle other errors */
default:
}

我们在第 20 章中针对网络相关的系统调用，特别是 select() 系统调用，解决了这个问题。

## 18.11 用于操作目录的系统调用

UNIX 提供了一组用于创建、删除和更改目录的系统调用。表 18.14 列出了这些调用及其用途。我们将不再进一步讨论这些调用。但是，你将在本章末尾的编程练习中练习它们。

作为系统程序员，你不需要了解目录的内核数据结构的细节。然而，这种知识增强了你对 UNIX 操作系统的理解以及作为程序员的技能。最重要的目录数据结构在 <sys/dirent.h> 文件中定义。以下是 Solaris 中与文件系统无关的目录条目的定义。

```
struct dirent {
    ino_t       d_ino;      /* "inode number" of entry */
    off_t       d_off;      /* offset of disk directory entry */
    unsigned short d_reclen; /* length of this record */
    char        d_name[1];  /* name of file */
};
```

在 FreeBSD 中，目录条目定义为

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

两个系统中的定义都有三个共同字段：文件的 inode 号（在 FreeBSD 下称为文件号）、文件名以及目录条目的长度。BSD 定义包含两个额外字段：名称字段中字符串的长度以及条目所代表的文件类型。类型字段在这里并非严格必需，因为 inode 包含此信息，如第 18.9 节所述。Solaris 定义包含磁盘目录条目偏移量的额外字段。

你可以使用多个 C 库函数来操作目录，包括 opendir()、closedir()、readdir()、telldir()、seekdir() 和 rewinddir()。

## EXERCISE 18.17

浏览前面提到的用于操作目录的调用的手册页，以了解它们的语法和语义。然后编写小型程序使用它们，以增强你对这些调用的理解。

## 18.12 重要网络资源

表 18.15 列出了 UNIX 系统编程及相关主题的有用网站。

| TABLE 18.15 Web Resources for the UNIX System Programming and Related Topics |
| https://www.freebsd.org/ | Home page for FreeBSD. Contains a lot of useful material, including FreeBSD source, manual pages, support, SVN repository, forums, user groups, etc. |
| http://www.oracle.com/technetwork/server-storage/solaris11/documentation/index.html | Webpage for Oracle Solaris 11 product documentation. |
| http://www.gnu.org/ | Homepage for the free operating system GNU by the Free Software Foundation. Work on GNU's kernel, The Hurd, started in 1990 (before work on Linux had started). |
| http://www.tutorialspoint.com/index.htm | An excellent site for tutorials on almost all known programming languages, including C, and development environments. |
| http://www.tutorialspoint.com/c_standard_library/index.htm | The C standard library. |
| www.compileonline.com (http://www.tutorialspoint.com/codingground.htm) | A great free site for online editing, compiling, and running programs in almost any language from assembly language to Python and from Algol-68 to Ruby. |

## SUMMARY

UNIX 为软件开发提供了两种 API：语言库和系统调用接口。应用程序程序员通常使用语言库提供的接口，而系统程序员主要使用系统调用接口。我们描述了 UNIX 系统调用及其在文件数据和属性 I/O 的小型程序中的使用。我们的重点是常规文件。

在讨论系统调用之前，我们解释了四种导致控制转移到内核代码的事件。它们是中断、陷阱、信号和系统调用，其中前两种由系统硬件引起，后两种主要由软件引起。我们还讨论了执行系统调用时发生的事件的细节。我们简要讨论了 C 标准库以及标准 I/O 与通过系统调用的低级 I/O 之间的区别。

我们讨论了用于常规文件数据 I/O 和文件属性 I/O 的系统调用，使用 open()、creat()、read()、write()、close()、truncate() 和 stat() 系统调用。对于随机 I/O，我们使用 lseek() 系统调用将文件指针设置为下一个读或写操作应执行的字节。我们展示了 lseek() 和 write() 系统调用的使用，以说明如何在 UNIX 下的常规文件中创建空洞。我们通过使用 od 命令显示其八进制转储来展示文件中创建的空洞。

我们简要讨论了几个用于访问和操作文件属性和目录的系统调用和 C 库函数。这些调用是：access()、chdir()、chmod()、chown()、closedir()、mkdir()、opendir()、read()、readdir()、rename()、rewinddir()、seekdir()、telldir()、umask()、utime()。

我们还展示了 stat 结构和目录条目的内核数据结构，如 <sys/stat.h>、<limits.h> 和 <sys/limits.h> 文件所述。

最后，我们展示了如何使用一小段代码在系统调用在执行中间被中断且底层操作系统内核未自动重启它时重启系统调用。这种中断可能发生在对慢速设备、键盘以及管道、FIFO 和套接字等文件进行阻塞 I/O 时发生。

## QUESTIONS AND PROBLEMS

- 1. What is a system call? List names of three system calls in each of the following categories:
- a. Process control
- b. File management
- c. Device management
- d. Information maintenance
- e. Communications

