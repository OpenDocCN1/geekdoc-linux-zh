
这告诉我们，readdir()需要一个DIR*类型的参数，并返回一个指向dirent结构的指针。手册页的其余部分可能包含这个dirent结构的定义，但可能不包含，具体取决于系统。如果确实没有，那么你需要使用前面描述的策略来查找它。它不会解释什么是DIR*或它在哪里定义。这几乎肯定需要进一步研究。需要说明的是，如果手册页中没有dirent定义，你应该在SEE ALSO部分查找可能提供更多信息的手册页；该列表可能如下所示：

```
SEE ALSO
    read(2), closedir(3), dirfd(3), ftw(3), opendir(3),
    rewinddir(3), scandir(3), seekdir(3), telldir(3),
    feature_test_macros(7)
```

在上面列出的手册页中，最可能的候选者是opendir()的手册页；这个函数很可能是在进行任何目录处理时第一个调用的函数。如果该页面也没有定义，那么我们就必须阅读<dirent.h>的手册页，或者直接阅读头文件本身。

无论如何，你都会发现dirent结构的定义如下：

```
struct dirent {
    ino_t       d_ino;        /* inode number */
    off_t       d_off;        /* offset to the next dirent */
    unsigned short d_reclen;  /* length of this record */
    unsigned char  d_type;    /* type of file; not supported
                               by all system types */
    char        d_name[256];  /* filename */
};
```

但无论你是在readdir()的第3节或3P节手册页中，还是在<dirent.h>头文件的页面中，都会发现如下这样的警告：

> 根据POSIX，dirent结构包含一个字段char d_name[]，其大小未指定，在终止的空字节之前最多有NAME_MAX个字符。POSIX.1-2001还将字段ino_t d_ino记录为XSI扩展。使用其他字段将损害程序的可移植性。

也就是说：dirent结构中唯一保证存在的两个成员是d_ino和d_name，并且d_name成员不一定是固定长度的字符串；POSIX只保证它是一个以NULL结尾的字符串，其长度最多为NAME_MAX个字符。因此，无论如何，我们都不应该使用那些其他成员，并且我们应该确保任何存储名称的变量都足够大，能够存储NAME_MAX个字符。我们将在后面回到如何在程序中使用NAME_MAX这个问题。

我们需要弄清楚如何使用readdir()，什么是DIR，以及我们如何获得一个DIR*来用于readdir()。readdir()的手册页基本上是说，使用同一个目录流指针连续调用readdir()会返回所指目录中的连续条目，并且

当所有条目都被访问后，会返回一个NULL指针。这与getutent()函数处理utmp结构的方式非常相似，该函数需要通过调用setutent()来初始化库。我们有理由猜测，SEE ALSO部分列出的opendir()函数为readdir()执行了这种初始化。

opendir()的手册页内容如下：

## 概要

```
#include <sys/types.h>
#include <dirent.h>

DIR *opendir(const char *name);
```

## 描述

opendir()函数打开与目录名称对应的目录流，并返回指向该目录流的指针。流被定位在目录的第一个条目处。

## 返回值

opendir()函数返回指向目录流的指针。出错时，返回NULL，并适当地设置errno。

换句话说，给定一个目录的路径名字符串，opendir()会返回一个指向被称为DIR的某种东西的指针，文档将其称为目录流。大写字母的名称通常是宏，在头文件中用“#define”指令定义，DIR类型可能是一个宏。它也可能是一个typedef。为了打开目录并从中读取，我们不需要知道DIR是什么，所以现在我们继续。

正如正确使用getutent()需要我们在访问完所有utmp记录后调用endutent()进行清理一样，正确使用readdir()也要求我们在之后进行清理。SEE ALSO部分包含对closedir()函数的引用。如果我们查看它的手册页，我们会看到，closedir()在给定一个指向DIR的指针时，会关闭与目录的连接，这正是当readdir()返回NULL指针时我们必须做的事情。

通过阅读readdir()（第3节和3P节）、opendir()和dirent.h的手册页，我们可以梳理出目录读取接口的工作原理。当使用opendir()打开目录时，一个静态变量指向目录中的第一个条目。readdir()调用会读取这个隐藏变量所指向的条目，并递增指针，使其指向下一个条目。因此，连续调用会遍历整个目录。如果程序在任何时候需要知道它将读取哪个条目，telldir()：

```
#include <dirent.h>
long telldir(DIR *dirp);
```

会返回其索引，这是一个从目录流开头算起的整数偏移量。如果程序需要在不关闭目录的情况下重新开始，rewinddir()可以做到这一点，而seekdir()会将指针移动到指定的索引：
