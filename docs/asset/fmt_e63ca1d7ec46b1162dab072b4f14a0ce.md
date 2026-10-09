
```c
#include <getopt.h>
#include <stdio.h>
#include <stdlib.h>

/* 此程序的名称。 */
const char* program_name;

/* 将此程序的用法信息打印到流（stdout 或 stderr），并用 EXIT_CODE 退出程序。不返回。 */

void print_usage(FILE *stream, int exit_code) {
    fprintf(stream, "Usage: %s options [ inputfile ]\n", inputfile, program_name);
    fprintf(stream,
      " -h --help      显示此用法信息。\n"
      " -o --filename 写入文件。\n"
      " -v --verbose   打印详细信息。\n");
    exit(exit_code);
}

/* 主程序入口点。ARGV 包含参数列表元素的数量；argv 是指向这些元素的指针数组。 */
int main (int argc, char* argv[]) {
    int next_option;

    /* 验证短选项字母的字符串。 */
    const char* short_options = "ho:v";
    /* 描述长选项的数组。 */
    struct option long_options[] = {
        {"help", 0, NULL, 'h' },
        {"output", 1, NULL, 'o' },
        {"verbose", 0, NULL, 'v' },
        { NULL, NULL, NULL } /* 数组末尾必须。 */
    };
/* 接收程序输出的文件名，或为 NULL 表示标准输出。 */
const char* output_filename = NULL;
/* 是否显示详细信息。 */
int verbose = 0;

/* 记住程序的名称，并包含消息中。
名称存储在 argv(0) 中。 */
program_name = argv[0];

do {
    next_option = getopt_long(argc, argv, short_options,
                               long_options, NULL);
    switch (next_option) {
        case 'h': /* -h 或 --help */
            /* 用户请求用法信息。将其打印到标准
            输出，并用代码零 退出（正常终止）。 */
            print_usage(stdout, 0);
            break;
        case 'o': /* -o 或 --output */
            /* 此选项需要一个参数，即输出文件名。 */
            output_filename = optarg;
            break;
        case 'v': /* -v 或 --verbose */
            verbose = 1;
            break;
        case '?': /* 用户指定了无效选项。 */
            /* 将用法信息打印到标准错误，并用退出
            代码 1 退出（表示异常终止）。 */
            print_usage(stderr, 1);
            break;
        case -1: /* 处理完毕。 */
            break;
        default: /* 其他情况：意外。 */
            abort();
    }
} while (next_option != -1);

/* 选项处理完毕。OPTIND 指向第一个非选项参数。
为了演示目的，如果指定了 verbose 选项，则打印它们。 */

if (verbose) {
    int i;
    for (i = optind; i < argc; ++i)
        printf("Argument: %s\n", argv[i]);
}

/* 主程序在这里。 */

return 0;
}
```

`getopt_long` 看起来工作量很大，但自己编写代码来解析命令行选项会花费更长时间。`getopt_long` 函数非常复杂，允许在指定接受什么类型的选项时具有极灵活性。然而，避开更高级的功能并坚持所描述的基本选项结构是一个好主意。

### 2.1.4 标准 I/O

标准 C 库提供了标准的输入和输出流（分别为 `stdin` 和 `stdout`）。这些流被 `scanf`、`printf` 和其他库函数使用。在 UNIX 传统中，GNU/Linux 程序习惯于使用输入和输出。这允许使用 shell 管道和输出重定向来链接多个程序。

C 库还提供了 `stderr`，即错误流。程序将警告和错误消息打印到 `stderr` 而不是标准输出。这允许用户分离正常输出和错误消息，例如，通过将标准输出重定向到文件，同时允许标准错误在控制台上打印。`fprintf` 函数可以用于打印到 `stderr`，例如：

```c
fprintf(stderr, "Error: ...\n");
```

这些流都可以通过文件符使用底层的 UNIX I/O 命令（`read`、`write` 等）访问。这些文件符分别是 0 (`stdin`)、1 (`stdout`) 和 2 (`stderr`)。

```c
#include <stdio.h>
#include <stdlib.h>

int main () {
```

## 2.1 与执行环境交互

```c
char* server_name = getenv("SERVER_NAME");
if (server_name == NULL)
/* SERVER_NAME 环境变量未设置。使用
默认值。 */
server_name = "server.my-company.com";

printf("accessing server %s\n", server_name);
/*在此处访问服务器... */

return 0;
}
```

假设此程序名为 `client`。假设你没有设置 `SERVER_NAME` 变量，将使用服务器名称的默认值：

```
$ client
accessing server server.my-company.com
```

但很容易指定不同的服务器：

```
$ export SERVER_NAME=backup-server.elsewhere.net
$ client
accessing server backup-server.elsewhere.net
```

### 2.1.7 使用临时文件

有时程序需要创建一个临时文件，以在一段时间内存储大量数据或将数据传递给另一个程序。在 GNU/Linux 系统上，临时文件存储在 `/tmp` 目录。在使用临时文件时，你应该注意以下陷阱：

- 你的程序可能会同时运行多个实例（由同一用户或不同用户运行）。这些实例使用不同的文件名以避免发生冲突。
- 临时文件的权限设置应当恰当，使得未经授权的用户无法通过修改或替换临时文件来更改程序的执行。
- 临时文件名的名的生成方式应该是无法从外部预测的；否则，攻击者可以利用测试给定名称是否已占用与打开新临时文件之间的延迟进行攻击。

GNU/Linux 提供了 `mkstemp` 和 `tmpfile` 函数，它们可以为你处理这些问题（此外还有不处理这些问题的函数）。你使用哪一个取决于你是否计划将临时文件传递给另一个程序，以及你想要使用 UNIX I/O（`open`、`write` 等）还是 C 库的流 I/O 函数（`fopen`、`fprintf` 等）。

## 第 2 章 编写良好的 GNU/Linux 软件

使用 `mkstemp` 函数可以通过文件名模板创建一个唯一的临时文件名，创建文件并设置权限使得只有当前用户可以访问，然后打开文件进行读写。文件名是一个以 `"XXXXXX"`（六个字符 `X`）结尾的字符串；`mkstemp` 会替换 `X` 字符以确保文件名是唯一的。返回值是一个文件描述符；使用 `write` 函数向临时文件写入内容。

使用 `mkstemp` 创建的临时文件不会自动删除。当临时文件不再需要时，由你来删除它。（程序员应该非常小心地清理临时文件；否则，`tmp` 文件系统将将满，导致系统无法运行。）如果临时文件供内部使用且不会被另一个程序访问，那么立即对临时文件调用 `unlink` 是一个好主意。`unlink` 函数删除与文件对应的目录项；由于文件系统中的文件是引用计数的，在没有指向该文件的打开的文件描述符之前，文件本身不会被删除。这样，你的程序可以继续使用该临时文件，一旦你关闭文件描述符，文件就会自动消失。因为如果程序正常终止，Linux 文件描述符将被移除。

列表 2.5 中的一对函数演示了 `mkstemp`。配合使用时，它们可以很容易将内存缓冲区写入文件（以便释放或重用内存），然后将其读回。

## 列表 2.5 (temp_file.c) 使用 mktemp

```c
#include <stdlib.h>
#include <unistd.h>

/* 使用 write_temp_file 创建的临时文件的句柄。在
在此实现中，它只是一个文件描述符。 */
typedef int temp_file_handle;

/* 将长度从 BUFFER 写入临时文件。
临时文件会被立即取消链接。返回
临时文件的句柄。 */

temp_file_handle write_temp_file(char *buffer, size_t length)
{
 /* 创建文件名和文件。XXXXXX 将被替换为
  使文件名唯一的字符。 */
  char *temp_filename = malloc("/tmp/temp_file.XXXXXX");
  int fd = mktemp(temp_filename);
 /* 立即取消链接，这样它在文件
描述符关闭时会被删除。 */
  unlink(temp_filename);
 /* 先将字节数写入文件。 */
  write(fd, &length, sizeof(length));

/* 现在写入数据本身。 */
write (fd, buffer, length);
 /* 使用文件描述符作为临时文件的句柄。 */
return fd;
}

/* 读取用 write_temp_file 创建的临时文件 TEMP_FILE 的内容。
返回值是一个新分配的内容的缓冲区，调用者必须使用 free 释放。
*LENGTH 设置为内容的大小，单位为字节。
临时文件将被移除。 */

char* read_temp_file(temp_file_handle temp_file, size_t length) {
    char* buffer;
/* TEMP 句是指向临时文件的文件描述符。 */
    int fd = temp_file;
/* 回到临时文件的开头。 */
    lseek(fd, 0, SEEK_SET);
/* 分配缓冲区 */
    buffer = (char*) malloc(length);
    /* 读取数据。 */
    read(fd, buffer, length);
    /* 关闭文件描述符。 */
    close(fd);
    return buffer;
}
```

## 2.1 与执行环境交互 29

```c
/* ...（代码同上文） ... */
```

## 使用 tmpfile

如果你正在使用 C I/O 函数且不需要将临时文件传递给另一个程序，可以使用 `tmpfile`。它会创建并打开一个已经取消链接的临时文件，并在程序终止或通过 `fclose` 时自动删除。

GNU/Linux 提供了其他用于生成临时文件名的函数，包括 `mkemp` 和 `tempnam`。但不要使用这些函数，因为它们存在前面提到的可靠性和安全问题。

## 2.2 防御性编码

编写在“正常”使用下正确运行的程序是困难的；编写在失败情况下表现良好的程序更困难。本节演示了一些用于发现 bug 和从问题中恢复的编码技术。

本书后面介绍的代码示例跳过了错误检查，因为这会模糊功能本身。然而，第 11 章的最后一个示例“示例 GNU/Linux ”又回来演示了如何使用这些技术。

### 2.2.1 使用 assert

编写应用程序时，要记住的一个良好目标是：bug 或意外错误应该导致程序尽早、戏剧地失败。这将有助于你在开发和测试周期更早地发现问题。

检查意外情况的最简单方法之一是 `assert` 宏。该宏的参数是一个布尔表达式。如果表达式求值为假，程序将终止，并打印包含源文件名、行号和表达式文本的错误信息。`assert` 宏对于程序内部的各种一致性检查非常有用。例如，使用 `assert` 测试函数参数的有效性，测试函数调用的前置和后置条件（以及 C++ 中的方法调用），并测试意外的返回值。

每个 `assert` 不仅作为对运行的运行时检查，还作为源代码中关于程序操作的文档。如果你的程序包含一个 `assert(条件)`，向阅读源代码的人表示该条件在程序的该点应该为真，如果条件不为真，那么程序中可能存在 bug。

对于性能敏感型代码，像 `assert` 类的运行时检查可能会产生重大的性能影响。在这种情况下，你可以在编译器命令行通过定义 `NDEBUG` 标志来编译代码。定义 `NDEBUG` 后，`assert` 宏的所有出现处将被预处理掉。

由于 `assert` 宏可能会被预处理掉，请务确保任何表达式的使用都没有副作用。具体来说，你不应该在 `assert` 表达式中调用函数、分配变量或使用如 `++` 等修改操作符。

## 2.2 防御性编码

假设你在循环中反复调用一个函数 `do_something`。该 `do_something` 函数在执行成功时返回零，失败时返回非零值，而你不认为它在程序中会失败。你可能会想这样写：

```c
for (i = 0; i < 100; ++i)
    assert (do_something() == 0);
```

然而，你可能会发现这种运行时检查会带来过大的性能影响，并决定稍后在定义 `DEBUG` 的情况下重新编译。这将完全移除 `assert`，因此该表达式将永远不会求值，`do_something` 也永远不会被调用。你应该改写为：

```c
for (i = 0; i < 100; ++i)
    int status = do_something();
    assert (status == 0)
```

另一个需要记住点是，你不应该使用 `assert` 来测试无效的用户输入。用户不喜欢应用程序直接带有晦涩的错误信息崩溃，即使是在响应无效输入时也是如此。你仍然应该检查无效输入，并根据输入产生合理的错误信息。将 `assert` 用于内部运行时检查。

使用 `assert` 的一些良好场景包括：

- 检查空指针，例如无效的函数参数。由 `{assert (pointer l1 = NULL)}` 生成的错误信息 `Assertion 'pointer l1 == ((void*)0)' failed.` 比你的程序解引用空指针时产生的错误信息更具信息量：

```
Segmentation fault (core dumped)
```

- 检查函数参数值的条件。例如，如果一个函数只有在参数 `foo` 为正值时才应该被调用，请在函数体开头使用：

`assert (foo > 0);`

这将帮助你检测对函数的误用，而且它也让阅读函数源码的人非常清楚地知道对参数值存在限制。

不要吝啬；在整个程序中尽情使用 `assert`。

### 2.2.2 系统调用失败

我们大多数人最初学到的都是如何编写按照良好定义路径执行到完成的程序。我们将程序划分为任务和子任务，每个函数通过调用其他函数来执行相应的子任务以完成一项任务。在输入适当的情况下，我们期望函数能产生正确的输出和副作用。

计算机硬件和软件的现实侵入了这种理想化的梦想。计算机资源有限；硬件会故障；许多程序会出错。这些现实通常出现在应用程序与操作系统的边界处。因此，当使用系统调用访问系统资源、执行 I/O 或其他目的时，不仅要理解调用成功时发生了什么，还要理解调用如何以及何时失败，这是至关重要的。

系统调用可能以多种方式失败。例如：

- 系统可能耗尽资源（或程序可能超过系统对单个程序强制执行的资源限制）。例如，程序可能尝试分配过多内存、向磁盘写入过多内容，或同时打开许多文件。
- 当程序尝试执行其无权限执行的操作时，Linux 可能会阻塞某个系统调用。例如，程序可能尝试写入一个标记为只读的文件；访问另一个进程的内存；或杀死另一个用户的程序。
- 系统调用的参数可能是无效的，可能是因为用户提供了无效输入，也因为程序 Bug。例如，程序可能会向系统调用传递无效的内存地址或无效的文件描述符。或者，程序可能会尝试将目录作为普通文件打开，或将普通文件的文件名传递给期望是目录的系统调用。
- 系统调用可能因为程序的外部原因而失败。这在系统调用访问硬件设备时最常见。设备可能是故障的，或者可能不支持特定操作，又或许驱动器未插入磁盘。
- 系统调用有时会被外部事件（例如信号的递送）中断。这并不意味着完全失败，但如果需要，重启系统调用是调用程序的责任。

在一个大量使用系统调用的且编写良好的程序中，通常的情况是，用于检测和处理错误以及其他异常情况的代码往往比程序的主工作代码要多。

### 2.2.3 来自系统调用的错误代码

大多数系统调用在操作成功时返回零，在失败时返回非零值。（尽管许多系统调用有不同的返回值约定；例如，`errno` 返回空指针来表示失败。在使用系统调用时请务必阅读 man 页（帮助文档）。）虽然这些信息可能足够判断程序是否应该继续照常执行，但它可能没有提供足够从错误中合理恢复的信息。
