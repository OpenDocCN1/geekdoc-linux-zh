
`-rw-r-r- 1 rstevens other1 0 Oct 23 17:08 /tmp/.1234.tmp`

`solaris % mqcreate -e /tmp.1234` second create with `-e` fail

`mq_open` error for `/tmp.1234`: File exists

## `mq_getattr` 和 `mq_setattr` 函数

（我们把这个版本的程序称为 `mq_create1`，因为我们在描述属性后在图 5.5 节中对其进行了增强。）第三个文件具有我们通过 `FILE_MODE` 常量指定的权限（用户读写，组和其他和其他只读），其他文件具有不同的权限。我们假设文件名 `D` 包含数据，文件名 `L` 是某种锁，而文件名 `P` 指定权限。

在 Unix 4.0B 下，我们可以看到创建的实际路径。

```
alpha % mq_create /tmp/mq_1234

alpha % -l /tmp/mq_1234

rwr-r-- -1 reverse-system 11976 Oct 23 17:04 /tmp/mq_1234

alpha % mq_open /tmp/mq_1234: File exists
```

## 示例：`mqunlink` 程序

图 5.3 是我们的 `mqunlink` 程序，它从系统中移除消息队列。

```c
#include "unipipe.h"

2 int
3 main(int argc
4 {
5   if (argc < 2)
6     err_quit("usage: mqunlink <name>");
7   mq_unlink(argv[1]);
8   exit(0);
9 }
```

> 图 5.3 移除消息队列。

我们可以移除由程序创建的消息队列。目录中的所有文件都被移除。

## `mq_getattr` 和 `mq_setattr` 函数

每个消息队列有四个属性，由 `mq_getattr` 返回，一个由 `mq_setattr` 设置。

```c
#include <mqueue.h>
int mq_getattr(mqd_t mqdes, struct mq_attr *attr);
int mq_setattr(mqd_t mqdes, const struct mq_attr *oldattr, struct mq_attr *newattr);
如果成功则返回 0，出错时返回 -1
```

结构包含了这些属性。这些属性的指针传递给 `mq_open`，允许我们设置队列的最大消息数每条消息的大小。我们不能只指定一个而不另一个；两者必须指定（见练习 5.1）。图 5.5 是新程序。

```c
#1 #include <sys/ipc.h>
2 struct mq_attr attr;
3 int
4 main(int argc, char **argv)
5 {
6 int c, flags;
7 mq_t mq;
8 flags = O_RDWR | O_CREATE;
9 while (c = getopt(argc, argv, "emz")) != -1) {
10 switch (c) {
11 case 'e':
12 break;
13 flags |= O_EXCL;
14 break;
15 case 'm':
16 attr.mq_maxmsgs = atol(optarg)
17 break;
18 case 'z':
19 attr.mq_msgsize = atol(optarg)
20 break;
21 }
22 if (optind - argc == 1)
23 err_quit("usage: mqcreate [-e] [-m max msgs] [-z msgsize] <name>");
24 if (attr.mq_maxmsgs == 0 || attr.mq_msgsize == 0) ||
25 (attr.mq_maxmsgs != 0 && attr.mq_msgsize != 0)
26 err_quit("must specify both -m max msgs and -z msgsize");
27
28 mq = mq_open(argv[1], flags, FILE_MODE,
29 (attr.mq_maxmsgs != 0) ? &attr : NULL);
30 mq_close(mq)
31 exit(0);
32 }
```

> 图 5.5 允许指定属性的图 5.2 的修改。

# Posix 消息队列

要指定命令行选项需要一个参数，我们在调用 `getopt` 时在 `m` 和 `z` 选项后面指定一个冒号。在处理该选项时，`optarg` 指向该参数。

我们的 `getopt` 封装函数调用了标准库的 `getopt` 函数，并在 `getopt` 检测到错误时终止进程：未包含在第三个参数中的选项，或者缺少必需参数的选项（由选项字母后跟冒号表示）。在任何情况下，`getopt` 都会写入错误消息并返回错误，这导致我们的 `getopt` 封装函数终止。例如，`getopt` 会检测到以下两个错误：

```
solaris mqcreate -e
mqcreate: requires an argument -- z
mqcreate: illegal option --n
mqcreate: illegal option --q
```

我们的程序检测到以下错误（未指定必需参数）：

```
solaris mqcreate
usage: mqcreate [-e] | [-n maxsize -m filesize]
solaris mqcreate -n 1024 -m 8192 /foobar
-rw-rw-rw- 1 /tmp/foobar 1 rsteams 839736 Oct 25 11:29 /tmp/foobar
-rw-rw-rw- 1 rsteams 0 Oct 25 11:29 /tmp/foobar
-rw-rw-rw- 1 rsteams 0 Oct 25 11:29 /tmp/foobar
```

如果两个选项都没有指定，我们必须传递一个空指针作为 `mq_open` 的最后一个参数，否则我们传递指向我们的 `attr` 结构的指针。

我们现在运行此版本的程序，指定最大 1024 条消息，每条消息最多 8192 字节。

该队列包含的数据的大小考虑了最大尺寸消息的总和（1024 * 8192 = 8,388,608），剩余的 8728 字节开销允许每条消息占用 8 字节（8 * 1024）加上额外的 1536 字节。

如果我们在 Digital Unix 4.0B 下执行该程序，我们得到：

```
solaris alpha -m 256 -m 2048 /tmp/bbq
alpha is -l1 /tmp/bbq
-rw-rw-rw- 1 rsteams 537288 Oct 25 15:38 /tmp/bbq
```

此实现允许我们留出最大数量的最大尺寸消息（256x2048 = 524,288），剩余的 13000 字节开销允许每条消息占用 8 字节（48 x 25）加上额外的 712 字节。

## 5.4 `mq_send` 和 `mq_receive` 函数

这两个函数分别向队列放入消息和从队列中取出消息。每条消息都有一个优先级，这是一个小于 `MQ_PRIO_MAX` 的无符号。Posix 要求该限制至少为 32。

Solaris 2.6 的上限是 32，但在 Digital Unix 4.0 中此限制为 256。我们通过图 5.8 展示了如何获取这些值。

`mq_receive` 从指定的队列返回优先级最高的旧消息，除了消息的实际内容和长度外，还可以返回优先级。

`mq_receive` 的此操作与 System V 的 `msgrcv`（第 6.4 节）不同。System V 消息有一个类型字段，类似于优先级，但通过 `msgrcv`，我们指定了三种不同的场景来返回哪种消息：队列中最旧的消息、特定类型的旧消息，或者类型小于等于某个值的旧消息。

```c
#include <mqueue.h>
int mq_send(mqd_t mqdes, const char *ptr, size_t len, unsigned int prio); // 返回：OK 或错误时返回 -1
size_t mq_receive(mqd_t mqdes, char *ptr, size_t len, unsigned int *prio); // 返回：OK 时返回消息字节数，错误时返回 -1
```
