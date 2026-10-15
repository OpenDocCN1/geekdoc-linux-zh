
# 2.6.7 who 的第三个版本

前面版本的 `who` 使用 `read()` 系统调用从 `utmp` 文件读取数据，一次读取一个 `utmp` 结构体。访问文件中数据的一种替代方法是利用 API 提供的抽象数据层。当我们为 `utmp` 文件相关的 man 页面进行 man 页面搜索时，我们忽略了在名为 `getutent` 的页面上找到的函数：

- `endutent [getutent] (3)` - access utmp file entries
- `getutent (3)` - access utmp file entries
- `getutid [getutent] (3)` - access utmp file entries
- `getutline [getutent] (3)` - access utmp file entries
- `pututline [getutent] (3)` - access utmp file entries
- `setutent [getutent] (3)` - access utmp file entries
- `utmpxname [getutent] (3)` - access utmp file entries

我们现在来看看该页面提供了什么。该页面的开头包含以下内容（取决于你的系统）：

```
SYNOPSIS
    #include <utmpx.h>
    struct utmp *getutent(void);
    struct utmp *getutid(struct utmp *ut);
    struct utmp *getutline(struct utmp *ut);
    struct utmp *pututline(struct utmp *ut);
    void setutent(void);
    void endutent(void);
    int utmpxname(const char *file);
```

```
DESCRIPTION
    New applications should use the POSIX.1-specified "utmpx" versions of these functions; see CONFORMING TO.
```

该 man 页面的第一句话告诉我们这些函数不是 POSIX.1 兼容的，并且这些函数有 `utmpX` 版本。我们暂时忽略此警告，看看如何使用这些非 POSIX 函数，仅仅因为需要解释 POSIX.1 兼容接口的一些内容，我们稍后会回到这个问题。

man 页面基本上告诉我们，有一种简单的方法可以读取 `utmp` 文件中的记录，只需要四个步骤：

- 1. 使用 `utmpxname()` 选择应由其他函数访问的文件。
- 2. 调用 `setutent()` 将文件指针回绕到文件开头。
- 3. 反复调用 `getutent()` 获取文件中的下一个 `utmp` 记录；`getutent()` 在读取完文件中的最后一记录后将返回 `NULL` 指针。
- 4. 读取完所有记录后调用 `endutent()`。

换句话说，此接口为 `utmp` 文件提供了一个隐藏的迭代器：`setutent()` 初始化它，`getutent()` 依次推进它，而 `endutent()` 发送一个信号表示它不再需要。此外，`utmpxname()` 函数只需被告知文件的路径名，它就会负责打开它。

man 页面还提到 `_PATH_UTMP` 是一个宏，其值为 `utmp` 文件的路径。我们已经知道 `UTMP_FILE` 包含该路径，但如果我们深入一点，实际阅读头文件，我们会发现 `<paths.h>` 头文件定义了 `_PATH_UTMP` 和 `_PATH_WTMP`，而 `<utmp.h>` 将 `UTMP_FILE` 定义为 `_PATH_UTMP` 的另一个名称。

我们可以把所有这些结合起来创建一个更简单的 `who` 版本，命名为 `who3`。在此版本中，我们增加了额外的功能，即用户可以在命令行上可选地提供单词 `"wtmp"`，如果她想查看 `wtmp` 文件中的记录的话。`show_info()` 和 `show_time()` 函数保持不变，因此我们只显示主程序的列表。

## 1 列出 who3.c

```
31 void show_info( struct utmp *utbufp )
32 // displays the contents of the utmp struct only if a user
33 // login, with time in human readable form, and host if
34 // not null
35 {
36     if ( utbufp->ut_type != USER_PROCESS )
37         return;
38
39     printf("% -8s", utbufp->ut_name); /* the logname */
40     printf("_");
41     printf("% -8s", utbufp->ut_line); /* the tty     */
42     printf("_");
43     show_time( utbufp->ut_time );      /* login time  */
44     printf("_");
45     if ( utbufp->ut_host[0] != '\0' ) /* the host    */
46         printf("_(%)s", utbufp->ut_host);
47     printf("\n");
48 }
49
50 void show_time( long timeval )
51 // displays time in a format fit for human consumption
52 // uses ctime to build a string then picks parts out of it
53 // Note: %12.2s prints a string 12 chars wide and LIMITS
54 // it to 12 chars.
55 {
56     char* timestr = ctime(&timeval);
57     // string looks like "Sat Sep  3 16:43:29 EDT 2011"
58
59     // print 12 chars starting at char 4
60     printf("%12.12s", timestr + 4 );
61 }
```

```
2 #include <stdio.h>
3 #include <stdlib.h>
4 #include <unistd.h>
5 #include <utmp.h>
6 #include <fcntl.h>
7 #include <time.h>

int main(int argc, char* argv[])
{
    struct utmp *utbufp;
    if ( (argc > 1) &&( strcmp(argv[1], "wtmp") == 0 ) )
        utmpname(_PATH_WTMP);
    else
        utmpname(_PATH_UTMP);
    setutent();
    while( (utbufp = getutent()) != NULL )
        show_info( utbufp );
    endutent();
    return 0;
}
```

这个程序不是线程安全的。各个 UNIX 库中的许多函数使用静态变量来存储结果。这些变量在调用这些函数的程序内部充当全局变量。如果程序是多线程的，这些线程如果重叠使用不安全的函数调用，就可能破坏彼此的数据。线程安全函数则没有这个问题。`who3` 程序的线程安全版本可以使用 `getutent_r()`，它是 `getutent()` 的 GNU 线程安全版本。

手册页告诉我们，要使用 `getutent_r()` 函数，必须在包含头文件 `<utmp.h>` 之前定义一个宏，即 `_GNU_SOURCE` 宏。这就是手册页中以下几行的用途：

```
The above functions are not thread-safe. Glibc adds reentrant versions
#define _GNU_SOURCE    /* or _SVID_SOURCE or _BSD_SOURCE */
#include <utmp.h>
int getutent_r(struct utmp *ubuf, struct utmp **ubufp);
```
