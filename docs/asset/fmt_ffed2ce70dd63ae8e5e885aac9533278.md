
# Linux 编程：反逆向工程技术

# 序言

## 为什么要读这本书？

有很多文章和书籍讨论了反逆向工程技术以及如何破解它们。然而，这些内容通常局限于短小的代码片段或 IDA 中的汇编截图。这本书尝试与众不同，从一个简单的程序开始，随着你阅读的深入，你将用反逆向技术来更新它。这让读者有机会自己去编译和分析二进制文件。我相信，对“概念证明”（proof of concept）的强调使得这本书独一无二。

这本书的另一个独特之处在于对 Linux 反逆向工程的强调。黑客们自 90 年代末以来就开始编写这些技术了，但大部分内容散落在互联网各地。这本书尝试整合大多数技术，并将它们作为一个整体呈现给读者。

最后，目前互联网上存在的很多概念证明代码都很糟糕。这并不是要评判，但有些代码无法编译，有些会直接崩溃，还有的编写方式非常奇怪。书中提供的代码尝试保持整洁、有用且易于维护。

## 未涵盖的话题

书中刻意遗留了一些话题。我想提前告知读者以便他们知道将得到什么。

- 虚拟机检测：虚拟机检测技术随着双方的博弈而不断变化。上周有效的技术下周可能被破解。因此，我完全避开了这个主题。
- 隐藏网络通信：理解二进制的网络通信对逆向工程有巨大的帮助。然而，这个话题太深，在这些书中无法详述。
- Rootkit 主题：隐藏和持久化不在讨论范围内。
- 任何与内核的内容：本书仅关注用户态二进制文件。

# 第 1 章：引言

## 介绍“Trouble”

本书围绕一个名为 Trouble 的绑定 shell（bind shell）的混淆展开。

### 什么是绑定 shell？

绑定 shell 是一种 shell 类型，目标机器在受害者机器上打开一个通信端口或监听器，并等待传入的连接。攻击者连接到受害者机器的监听器，从而在服务器上执行代码或命令¹。

Trouble 绑定 shell 被用作示例，并不是因为它的独特或有趣，而是因为它短小且简单。它还具有一个让逆向工程工程师可能感兴趣的属性：访问 shell 需要密码。书中的所有活动都试图隐藏或恢复该 shell 的密码。

## 使用 CMake

你将使用 `CMake`² 来编译 Trouble。`CMake` 是一个开源的 Makefile 生成工具。它对于依赖检查非常有用，并支持简单的语法。如果你不熟悉 `CMake`，不要担心，随着书籍进展，你将会学会的。

`CMake` 依赖“`CMakeList.txt`”来生成 Makefiles。对于第一章，你将在 `chapter_1_introduction/trouble` 目录下找到 Trouble 的“`CMakeList.txt`”。

> ¹http://resources.infosecinststitute.com/icmp-reverse-shell/
> ²https://cmake.org/

### `chap_1_introduction/trouble/CMakeLists.txt`

```
project(trouble C)
cmake_minimum_required(VERSION 3.0)
```

```
### 这将为绑定 shell 创建一个 32 字节的“密码”。该命令
### 仅在运行 "cmake" 时执行，所以如果你想生成新密码，
### 应该从命令行运行 "cmake ..; make"
exec_program("/bin/sh")
$(CMAKE_CURRENT_SOURCE_DIR)
ARGS -c 'cat /dev/urandom | tr -dc a-zA-Z0-9 | head -c 32'
OUTPUT_VARIABLE random_password
```

```cmake
### 将随机密码作为宏传递给 ${PROJECT_NAME}
add_definitions("-password="${random_password}")
```

```cmake
set(CMAKE_C_FLAGS "-Wall" -Wextra -Wshadow -g -std=gnu11)
add_executable(${PROJECT_NAME} src/trouble.c)
```

```cmake
### 构建成功后，向用户显示随机密码
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
COMMAND ${CMAKE_COMMAND} -E echo "The bind shell password is: ${random_password}")
```

此文件不仅会生成 Trouble 的 Makefile，而且每次执行时都会生成 shell 的 32 字节密码。密码是通过以下命令使用 urandom 创建的：

```
cat /dev/urandom | tr -dc a-zA-Z0-9 | head -c 32
```

在后续关于编译 Trouble 的章节中，将更多地解释如何使用 `CMake`。

## 代码

Trouble shell 的代码位于“source”目录中。它由单个文件组成：

### `chap_1_introduction/trouble/trouble.c`

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>

// 登录 shell 的密码
static const char s_password[] = password;

bool check_password(const char* p_password)
{
    // 验证密码
    return memcmp(s_password, p_password, sizeof(s_password) - 1) != 0;
}
```

- 这实现了一个相当简单的绑定 shell。服务器在允许访问 shell 之前首先要求密码。服务器目前在每次运行 `'cmake ..'` 时随机生成。服务器没有关闭机制，因此它将一直运行到被杀死为止。

```c
int main(int argc, char* p_argv[])
{
    (void)argc; // 修复拼写
    (void)p_argv;

    int sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if (sock == -1)
    {
        fprintf(stderr, "Failed to create the socket.");
        return EXIT_FAILURE;
    }

    struct sockaddr_in bind_addr = {};
    bind_addr.sin_family = AF_INET;
    bind_addr.sin_addr.s_addr = htons(INADDR_ANY);
    bind_addr.sin_port = htons(12770);
```

```c
    int bind_result = bind(sock, (struct sockaddr*)&bind_addr, sizeof(bind_addr));
    if (bind_result != 0)
    {
        perror("Bind call failed");
        return EXIT_FAILURE;
    }
    int listen_result = listen(sock, 5);
    if (listen_result != 0)
    {
        perror("Listen call failed");
        return EXIT_FAILURE;
    }
    while (true)
    {
        int client_sock = accept(sock, NULL, NULL);
        if (client_sock < 0)
        {
            perror("Accept call failed");
            return EXIT_FAILURE;
        }
        int child_pid = fork();
        if (child_pid == 0)
        {
            // 子进程逻辑
        }
        // ... 逻辑省略
    }
}
```

*(注：由于原文代码片段在提供时存在部分断裂或重复，翻译已根据上下文逻辑保持结构对齐)*

- 此代码实现了一个相当简单的绑定 shell。服务器在允许访问 shell 之前首先要求密码。服务器目前在每次运行 `'cmake ..'` 时随机生成。服务器没有关闭机制，因此它将一直运行到被杀死为止。

## 访问 Shell

要连接到 *Trouble*，我建议使用 `netcat` 是最简单的选项。一旦连接，输入密码，你就可以执行 shell 命令。如果输入了错误的密码，连接将被断开。请参考下面的示例。

连接到 *Trouble*

```
albino-lobster@ubuntu:-$ nc 192.168.1.182 1270
TGOEu26TW0@k1b9ieXjUDBT1GfCR0jSnl
pwd
/home/albino-lobster/antique_book/chap_1_introduction/trouble/build
ls -l
total 48
-rw-rw-r-- 1 albino-lobster albino-lobster 10544 Oct 18 17:07 CMakeCache.txt
drwxr-xr-x 5 albino-lobster albino-lobster 4096 Oct 18 17:22 CMakeFiles
-rw-rw-r-- 1 albino-lobster albino-lobster 4986 Oct 18 17:22 Makefile
-rw-rw-r-- 1 albino-lobster albino-lobster 1437 Oct 18 17:07 cmake_install.cmake
-rwxr-xr-x 1 albino-lobster albino-lobster 17488 Oct 18 17:22 trouble
```

# 第 2 章：编译器选项

在谈论反逆向工程时，编译器选项往往被忽视。然而，理解不同选项如何更改最终二进制文件至关重要。编译器可以成为你最大的敌人，泄露你所有的秘密；也可以成为你最好的朋友，因为它剥除了不必要的信息。

![](img/fdf1e4bfff3995dc5a8580eb00fa23e5_15_0.png)

## 聚焦 GCC

书中的代码期望使用 `GCC` 作为编译器。并不是说不能使用 `Clang` 或其他编译器。完全可以。但是，使用 `GCC` 是因为它在多年来一直一直是事实上的标准。

如果你不熟悉 `CMake` 或 `GCC`，可能会奇奇我所说的编译器选项是什么。如果你查看“`CMakeLists.txt`”文件，会发现：

```
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -g -std=gnu11")
```

这些就是编译器选项。`GCC` 支持许多选项。Trouble 版本中使用的标志是可用选项子集。

在上面的编译器选项中，所有以 `-W` 开头的选项都告诉编译器检查特定类型的编程错误。`-g` 指令编译器在二进制文件中包含调试信息。最后，`-std=gnu11` 告诉编译器你使用的 C 代码期望使用 C11 标准的 GNU 方言。GNU 扩展并不是 C11 标准的一部分。

> https://gcc.gnu.org/on/gcc/Summary.html
> https://gcc.gnu.org/on/gcc/Warning.html
> https://gcc.gnu.org/on/gcc/Debugging.html
> https://gcc.gnu.org/on/gcc/C-Dialect.html

## 第 2 章：编译器选项 -g

![](img/fdf1e4bfff3995dc5a8580eb00fa23e5_16.png)

`readelf` 是一个理解可执行和可链接格式（ELF）的命令行实用。ELF 是 Linux 可执行文件、共享库和核心转储的标准格式。`readelf` 可以解析二进制文件并显示有关格式的信息。Ubuntu 预装了 `readelf`。`readelf` 有很多命令行选项。其中一个选项 `-S` 将显示二进制文件的节头。

Trouble 的节头

```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ readelf -S .
There are 36 section headers, starting at offset 0x3c8:
```

# 节头

| Nr | Name | Type | Size | Address | Offset | Align |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | NULL | 0000000000000000 | 0000000000000000 | 0 | 0 |
| 1 | .interp | PROBITS | 000000000000001c | 0000000000000238 | 00000238 | A | 1 |
| 2 | .ABI-tag | NOTE | 0000000000000020 | 0000000000000000 | 0 | 4 |
| 3 | .gnu.build-id | NOTE | 0000000000000024 | 0000000000000274 | 0 | 4 |
| 4 | .gnu.hash | GNU_HASH | 0000000000000064 | 0000000000000298 | A | 5 | 8 |
| 5 | .dynym | DY | 0000000000000038 | 0000000000000300 | A | 6 | 8 | https://en.wikipedia.org/wiki/Executable_and_Linkable_Format 第 2 章：编译器选项
| 6 | .dynstr | STRTAB | 0000000000000648 | 00000648 | 000000000000015e | A | 0 | 1 |
| 7 | .gnu.version | VERSYM | 000000000000007a | 000007a6 | 0000000000000046 | A | 5 | 2 |
| 8 | .gnu.version_r | VERNEED | 00000000000007f0 | 000007f0 | 0000000000000030 | A | 6 | 8 |
| 9 | .rela.dyn | RELA | 0000000000000820 | 00000820 | 0000000000000010 | A | 5 | 8 |
| 10 | .rela.plt | RELA | 0000000000000850 | 00000850 | 0000000000000180 | | 4 | 8 |
| 11 | .init | PROGBITS | 00000000000009d0 | 000009d0 | 000000000000000a | A | 0 | 4 |
| 12 | .plt | PROGBITS | 00000000000009f0 | 000009f0 | 0000000000000110 | A | 0 | 16 |
| 13 | .plt.got | PROGBITS | 0000000000000b00 | 00000b00 | 0000000000000000 | A | 0 | 8 |
| 14 | .text | PROGBITS | 0000000000000b10 | 00000b10 | 00000000000003c2 | A | 0 | 16 |
| 15 | .fini | PROGBITS | 0000000000000ed4 | 00000ed4 | 0000000000000000 | A | 0 | 4 |
| 16 | .rodata | PROGBITS | 0000000000000ee0 | 00000ee0 | 000000000000009d | A | 0 | 32 |
| 17 | .eh_frame_hdr | PROGBITS | 0000000000000f80 | 00000f80 | 000000000000003c | A | 0 | 4 |
| 18 | .eh_frame | PROGBITS | 0000000000000fc0 | 00000fc0 | 0000000000000114 | A | 0 | 8 |
| 19 | .init_array | INIT_ARRAY | 0000000000000610 | 00000610 | 0000000000000000 | WA | 0 | 8 |
| 20 | .fini_array | FINI_ARRAY | 0000000000000618 | 00000618 | 0000000000000008 | WA | 0 | 8 |
| 21 | .jdata | PROGBITS | 0000000000000620 | 00000620 | 0000000000000008 | WA | 0 | 8 |
