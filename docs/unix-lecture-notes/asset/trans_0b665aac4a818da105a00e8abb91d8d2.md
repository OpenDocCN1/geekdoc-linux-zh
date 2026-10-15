

#include <dirent.h>
void seekdir(DIR *dirp, long offset);

telldir() 返回的偏移量可以传递给 seekdir()。

虽然我们不需要知道 DIR 的结构就能使用这些调用，但好奇心驱使我们去探究。你会发现 DIR 并不是一个宏，而是一个 typedef：

```
typedef struct __dirstream DIR;
```

并且在系统的任何公开头文件中都没有 struct __dirstream 的定义。这是因为 __dirstream 是一个不完整类型。不完整类型是一种描述对象但缺乏确定其大小所需信息的类型。每个 UNIX 实现都必须定义它，并且可以自由地按其选择的方式定义它，但它不必在任何头文件中公开该实现。<dirent.h> 头文件声明了 struct __dirstream 并使 DIR 等同于它，但并未定义其成员。这使程序员能够声明 DIR* 类型的对象，但不能访问 DIR 对象的成员。

我们的好奇心得到满足后，我们将此事搁置一边，转而解决前面出现的 NAME_MAX 问题。没有 man page 搜索可以告诉你像 NAME_MAX 这样的常量可能在哪里定义，即程序需要包含哪个头文件才能访问其定义。可以对系统中所有头文件搜索该字符串，但那样你必须知道所有包含头文件的位置。这种搜索在 /usr/include 中很可能会失败，例如，因为 NAME_MAX 是一个系统相关的值，存储在某个包含实现相关头文件的位置。可以对 " NAME_MAX " 进行彻底的递归 grep 搜索（空格很重要），你会找到它：

```
$ grep -R " NAME_MAX " /usr/* 2>/dev/null
```

在 bash 中，重定向 2>/dev/null 会丢弃所有发送到标准错误的消息。此命令的输出可能看起来像

```
/usr/include/linux/limits.h:#define NAME_MAX        255
/* # chars in a file name */
/usr/include/glib-1.2/glib.h:#    define NAME_MAX 255
```

随后是来自其他文件的行，这些文件可能定义或未定义该宏。

NAME_MAX 是 UNIX 中的一个系统限制。它指定文件名中的最大字符数。因此它是 <limits.h> 头文件中定义的众多此类常量之一。这一事实不像迄今为止的其他事实那样容易发现。必须包含此头文件才能使用该常量。在下一章中，我们将介绍如何在程序中发现和使用系统限制。暂时，我们只使用其中几个。

我们现在已有足够的知识来尝试编写 ls。

> 10 如果你编写一个引用 __dirstream 对象的程序，编译器会报错其大小未知。如果你改为声明一个 __dirstream* 指针，程序将编译通过，因为指针的大小是已知的。你将无法解引用此指针并使用它指向的内容，因为你的程序没有它的实现。但它在使用的库中已实现。这是在 C 中信息隐藏的一个例子。

## 3.9 实现 ls

编写 ls 的第一次尝试将处理多个命令行参数，而不会做太多其他事情。对于每个参数，如果它是目录，它将显示其内容，顺序不定。其中一个问题由 opendir() 调用为我们解决了；如果参数不是目录，该调用将失败，返回 -1。这将是我们判断文件名是否为目录的测试。

```
```c
Listing: ls.c Version 1
#include <stdio.h>
#include <sys/types.h>
#include <dirent.h>

#define HERE "."
void ls(char []);

int main(int argc, char *argv[])
{
    int i = 1;

    if (1 == argc)    // no arguments; use .
        ls(HERE);
    else
        // for each command line argument, display contents
        while (i < argc) {
            printf("%s\n", argv[i]);
            ls(argv[i]);
            i++;
        }
}

// List the contents of the directory named dirname
// Uses opendir to check whether argument is a directory
// Doesn't check if argument is or "." or ".."
void ls(char dirname[])
{
    DIR        *dir_ptr;    // directory stream
    struct dirent *direntp; // hold one entry

    if ((dir_ptr = opendir(dirname)) == NULL)
        // Could not open — maybe it was not a directory
        fprintf(stderr,"Cannot open %s\n", dirname);
    else
    {
        while ((direntp = readdir(dir_ptr)) != NULL)
            printf("%s\n", direntp->d_name);
        closedir(dir_ptr);
    }
}
```
```
