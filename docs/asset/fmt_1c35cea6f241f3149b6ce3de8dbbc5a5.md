
## 5.1.2. 目录内容

`inode` (`ino_t`) 在 V7 `<sys/types.h>` 中定义为 `'typedef unsigned int ino_t'`。由于 PDP-11 是 16 位的，`inode` 号也是。这种组织使得直接读取目录变得容易；因为项的大小是固定的，代码非常简单。（唯一需要注意的是，完整的 14 字符 `d_name` 没有符号终止。）

目录内容的管理对系统也很容易。当文件从目录中删除时，系统会将 `inode` 号替换为二进制零，表示目录中的“槽位”未占用。新文件可以重新使用该空槽。这有助于保持目录文件的大小合理。（按照惯例，`inode` 号 1 不使用；`inode` 号 2 始终是第一个可用 `inode`。更多细节见第 8.1 节。）

现代系统提供长文件名。每个目录项都是可变长度的，文件名部分的常见限制为 255 字节。稍后，我们将展示如何在现代系统上读取目录内容。现代系统还提供 32 位（甚至是 64 位！）`inode` 号。

### 5.1.3 硬链接 (Hard Links)

当使用 `open()` 或 `creat()` 创建文件时，系统会找到一个未使用的 `inode` 并将其分配给新文件。它会为文件创建一个目录条目，其中包含文件名和 `inode` 号。`ls` 的 `-i` 选项显示 `inode` 号：

```bash
$ echo hello, world > message
$ ls -il message
22786-rw-r-- 2 arnold devel 13 May 4 15:43 message
```

由于目录条目将文件名与 `inode` 关联，因此一个文件可以有多个名称。每个指向同一个 `inode` 的目录条目被称为该文件的链接，或`硬链接`。链接通过 `ln` 命令创建。`ln oldfile newfile` 的用法如下：

```bash
$ ln message msg
$ ls -il message msg
22786-rw-r-- 2 arnold devel 13 May 4 15:43 message
22786-rw-r-- 2 arnold devel 13 May 4 15:43 msg
```

输出显示两个文件的 `inode` 号是相同的，长格式输出中的第三字段现在为 2。这是`链接计数`，报告了该文件有多少个链接（指向该 `inode` 的目录条目）。

这一点再强调也不为过：硬链接都指向同一个文件。如果你修改了其中一个，你就修改了所有其他：

```bash
$ echo "Hi, how ya doin?" > msg
$ cat msg
Hi, how ya doin? 
$ ls -il message msg
22786-rw-r-- 2 arnold devel 19 May 4 15:43 message
22786-rw-r-- 2 arnold devel 19 May 4 15:43 msg
```

尽管我们在同一个目录中创建了指向同一文件的两个链接，但硬链接并不限于同一个目录；它们可以位于同一文件系统上的任何其他目录。（这将在第 5.1.6 节“符号链接”第 128 页中进行更多讨论。）

此外，只要你对创建链接的目录具有写权限，就可以为文件创建链接。（该文件保留了原始文件的所有属性：所有者、权限等。这是因为它是原始文件；它只是获得了一个额外的名称。）用户级无法为目录创建硬链接。

## 5.1 考虑目录内容

一旦文件被删除，用与原相同的相同的创建新文件将创建一个新文件：

```bash
$ rm message
$ echo "What's happenin?" > message
$ ls -il msg message
228794-rw-r--r-- 1 arnold devel 17 May 4 15:58 message
228756-rw-r--r-- 1 arnold devel 19 May 4 15:51 msg
```

注意，现在两个文件的链接计数都等于 1。

在 C 语言级别，链接通过 `link()` 系统调用创建：

```c
#include <unistd.h>
int link(const char *oldpath, const char *newpath);
```

如果链接创建成功，返回值为 0，否则返回 -1，此时 `errno` 返回错误代码。一个重要的失败情况是 `newpath` 已经存在。系统不会为你删除它，因为尝试这样做会导致文件系统的不一致。

### 5.1.3.1 GNU link 程序

`link` 程序非常复杂且巨大。然而，GNU Coreutils 包含一个简单的 `link` 程序，它只是对前两个参数调用了 `link()`。以下示例显示了 `link.c` 中的代码，并删除了一些无关部分。行号对应实际文件。

```c
20 /* 实现概述：
21
22   简单地调用系统 'link' 函数 */
23
      ...为了起见省略了包含语句 ...
34
35 /* 此程序的正式名称（例如，没有 `ln` 前缀）。 */
36   #define PROGRAM_NAME "link"
37
38   #define AUTHORS "Michael Stone"
39
40   /* 运行此程序时的名称。 */
41   char *program_name;
42
43 void
44   usage (int status)
45   {
62     ...为了起见省略了内容 ...
63 }
64
64 int
65 main(int argc, char **argv)
66 {
67   program_name = argv[0];
68   setlocale(LC_ALL, "*");
69   bindtextdomain(PACKAGE, LOCALEDIR);
70   textdomain(PACKAGE);
71
72   atexit(close_stdout);
73
74   parse_long_options(argc, argv, PROGRAM_NAME, GNU_PACKAGE, VERSION,
75   USERS, usage);
76
77   /* 以上处理了 --help 和 --version。*/
78   /* 由于没有其他 getopt 的调用，在这里处理 `--help'。*/
79   if (1 < argc && STREQ(argv[1], "--"))
80   {
81     --argc;
82     ++argv;
83   }
84
85   if (argc < 3)
86   {
87     error(0, 0, _("参数太少"));
88     usage(EXIT_FAILURE);
89   }
90
91   if (3 < argc)
92   {
93     error(0, 0, _("参数过多"));
94     usage(EXIT_FAILURE);
95   }
96
97   if (link(argv[1], argv[2]) != 0)
98     error(EXIT_FAILURE, errno, _("无法创建 %s 到 %s"),
99            quote_n(0, argv[2]), quote_n(1, argv[1]));
100  
101  exit(EXIT_SUCCESS);
102 }
```
