

当 ls 的参数是一个非目录文件时，它可能需要获取该文件的属性并显示它们。当参数是一个目录，比如 dir 时，ls 需要做类似下面的事情

```
open the directory dir
while not all directory entries in dir have been read
    read the entry
        optionally display information about the entry
close the directory
```

问题是，我们如何打开、读取和关闭一个目录，以及如何获取文件属性的信息。幸运的是，由于文件系统接口的简单性，这些任务都不特别困难。

## 3.8 目录接口

回想一下，对于内核而言，普通文件只是一串字节。目录与普通文件类似，只是

- 1. 它们永远不为空：
  
      目录不为空，因为每个目录都有两个唯一的条目，“.” 和 “..”，它们分别指向目录本身和父目录。这些是在目录创建时创建的。
  
- 2. 它们不能被非特权程序写入：
  
      它们只能通过非常特定的系统调用来修改，而与普通文件不同。相比之下，任何具有适当权限的人都可以读取目录的内容。一些对普通文件操作的命令也可以应用于目录，但结果会出乎意料。
  
- 3. 它们具有特定的结构：
  
      目录是一个包含一组（名称，i-号）对的文件。换句话说，目录是一张记录表。你可以把它想象成一个哈希表，因为它是用名称访问以检索 i-号。

一些读取文件的命令也会读取目录，但结果没有用。例如，在某些系统上，cat 命令和 od 命令可能会将目录的内容作为字节流显示，但由于目录不是文本文件，cat 的输出看起来会乱码。od 的输出可能看起来正常。通常，这些命令，像 more 命令，会检查其参数是否为目录，如果是，则拒绝执行，而是显示错误信息：

```
$ more projects
*** projects: Is a directory ***
```

more 命令拒绝显示 projects，因为它是一个目录，而目录作为字符序列显示是没有意义的。如果仔细检查，od 的输出可能会向你揭示目录的结构。od 的 -c 选项会将可转换为字符的字节作为字符显示。在 Linux 上，od、cat 或 more 都不会显示目录的内容。

如果你想知道哪些系统调用可能适用于目录，open()、read() 和 close() 系统调用会作用于目录，因为它们不会修改目录，但由于目录具有特定的结构，使用它们并没有多大意义。它们并非 intended 用于目录。最好使用专门设计用于打开、读取、修改和关闭目录的特定系统调用或库函数。

如果你使用 man 手册搜索来查找引用单词 "directory" 的 man 手册，你会找到很长的列表。最好过滤搜索的输出，使用类似

```
$ man -k directory | grep read
```

这将只显示少数条目。你可能会看到，其中包括

- readdir (2) - read directory entry
- readdir (3) - read a directory
- readdir (3p)- read a directory
- readdir_r [readdir] (3p)- read a directory
- seekdir (3) - set the position of the next
- readdir() call in the directory stream

不同的系统会根据它们运行的 UNIX 版本提供略有不同的 man 手册集合。所有系统都应该在第 2 节列出 readdir() 系统调用，而大多数系统应该在第 3 节或 3P 节或两者中列出一个名为 readdir() 的调用。在几乎所有系统上，如果你阅读第 2 节中 readdir() 系统调用的 man 手册，它会建议你不要使用此系统调用，而改用同名的 POSIX 库函数。它会指向 readdir() C 库函数，其 man 手册位于第 3 节或 3P 节。你可能需要在 man 命令中使用小写的 p，如

```
$man 3p readdir
```

由于不同系统之间存在很大差异，我们无法确切知道你会看到什么，但所有页面至少应包含以下内容：

```
SYNOPSIS
    #include <sys/types.h>
    #include <dirent.h>

    struct dirent *readdir(DIR *dir);
DESCRIPTION
    The readdir() function returns a pointer to a dirent structure representing the next directory entry in the directory stream pointed to by dir. It returns NULL on reaching the end-of-file or if an error occurred.
```

