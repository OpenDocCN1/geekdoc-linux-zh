
```c
        exit(1);

    }

    inbytesleft = 0;             /* 已转换字节数 */

    for ( ; ; ) {

        /* 翻译字符 */

        /* 如果有剩余字节，它们会在缓冲区开头 */

        ret_val = iconv(cd, &inchar, &inbytesleft, &outchar, &outbytesleft);

        if (ret_val == -1) {

            if (inbytesleft == 0) {

                break;

            }

            if (errno == EINVAL) {

                printf("iconv open failed: %d\n", errno);

                exit(1);

            }

        }

        /* 将数据拷贝到输出 */

        memcpy(outbuf, outchar, outbytesleft);

        outchar += outbytesleft;

        outbytesleft -= outbytesleft;

        inchar += bytesread;

        inbytesleft -= bytesread;

    }

}
```

### 3.10 国际化 (I18N) 与本地化

```
"Language-Team: LANGUAGE <LL00li.org\n"
"MIME-Version: 1.0\n"
"Content-Type: text/plain; charset=ISO-8859-2\n"
"Content-Transfer-Encoding: 8bit\n"
#: hello.c13
msgid "Linux Porting Guide"
msgstr "Guia de Migracion a Linux"
#: hello.c14
msgid "Author: Mendoza, Skrawatanananond, Walker"
msgstr "Author: Mendoza, Skrawatanananond, Walker"
```

编辑 `message.po` 文件，并为*每一个*需要翻译的消息修改 `msgstr`。如果在运行 `xgettext` 之前没有设置字符集，请编辑字符集。然后针对 `messages.po` 运行 `msgfmt` 命令。名为 `my_messages.mo` 的文件指的是通过 `bindtextdomain` 设置的域，并带有 `.mo` 扩展名。

```
$ msgfmt -v -o my_message.mo messages.po
```

在此示例中，我们在本地目录中为西班牙语（哥斯黎加）创建一个目录（默认目录 `/usr/lib/local`，因为我们没有 root 权限）：

```
$ mkdir -p locale/es_CR/LC_MESSAGES
```

然后将 `my_messages.mo` 移动到正确的目录：

```
$ mv my_message.mo locale/es_CR/LC_MESSAGES
```

导出正确的 LC_MESSAGES 值并运行程序：

```
$ export LC_MESSAGES=es_CR
$ ./hello
```

Guia de Migracion a Linux
Autor: Mendoza, Skrawatanananond, Walker

我们刚刚在 Linux 上成功创建了一个消息目录文件。

## 大端/小端环境

尽管 Linux 是在 Intel 平台上开发的，该平台主要是一个小端环境，但它已被移植到其他几个支持大端环境的硬件平台。端序（Endianness）或字节序，指的是数据元素及其各个字节的存储方式。在大端（BE）环境中，最低地址与多字节值的最位字节或最左侧字节相关联。在小端（LE）环境中，最低地址与多字节值的次位字节或最右侧字节相关联。通常，对于 BE 来说，位 0 与最高位（MSB）相关，而对于 LE 来说则与最低位相关。

示例 3-6 显示了一个示例程序，该程序在 BE 或 LE 环境下编译和运行时，打印数据的方式有所不同。

### 示例 3-6

在 Intel 服务器（LE 环境）上编译并运行时，将打印以下内容：
`x in hex: aabbcccd`
`x by bytes: dd cc bb aa`

在 IBM Power 服务器（BE 环境）上编译并运行时，将打印以下内容：
`x in hex: aabbcccd`
`x by bytes: aa bb cc dd`

## 3.12 从 32 位到 64 位迁移

注意，前面的示例是使用 `gcc` 编译的，它默认创建一个 32 位可执行文件。

大多数基于 RISC 的计算机（包括 IBM PowerPC 服务器）以及互联网协议（IP）使用大端布局，而 Intel 和 Alpha 架构利用小端（LE）布局。在移植软件时，建议注意端序问题，因为如果不注意，这些问题可能无法被发现，导致在发生时出现难以发现的问题。

移植软件中的问题包括：

- 非均匀数据引用²⁰
- 跨 BE 和 LE 平台的数据共享
- 网络设备之间的数据交换（例如，IP 和 PCI）²¹

非均匀数据引用在用户空间应用程序中发生得更频繁，而后两类是在较低的代码级别（例如，设备驱动程序）上遇到的困难。非均匀数据引用源于对端序的不当数据类型引用，通常涉及联合（unions）或指针。端序友好型代码应该包含定义，以判断平台是 LE 还是 BE。从不将指针强制转换为 `int` 并在转换期间显式引用数据类型和字节值，被认为是一种良好的编程习惯。

64 位 Linux 平台正在逐渐取代旧的 32 位服务器。64 位应用程序环境可以极大提高处理大数据的内存寻址性能和吞吐量。示例 3-6 显示了使用指针的非均匀数据引用。PCI 设备使用 LE 格式，如果将设备驱动程序移植到 BE 平台，则需要考虑到。

IBM 的 PowerPC 和 AMD 的 64 位架构上的 Linux 提供了一个独特的平台，因为 32 位和 64 位应用程序可以同时运行而没有任何性能损失。这种优势可以通过使用 `gcc` 编译 64 位应用程序来实现，使用 `-m64` 标志生成 64 位对象文件，如下例：

```
$ gcc -m64 sample.c -o sample.o
```

在某些平台（如 IBM PowerPC）上，即使 Linux 平台是 64 位的，`gcc` 编译器也会产生 32 位对象。32 位和 64 位编译环境的数据类型模型是不同的。32 位应用程序的 C 数据类型模型是 IL32 模型。`int` (I) 和 `long` (L) 以及指针 (P) 的字母表示这些数据类型都是 32 位类型。64 位的数据类型模型是 LP64 模型。除了 `int` 之外，`long` (L) 和指针 (P) 都会增长到 64 位。其余的整数类型和浮点类型也是如此。

64 位 Linux 平台正在顺利取代老老的 32 位服务器。64 位应用程序环境可以大幅提高处理大数据的应用程序的内存寻址性能和吞吐量。示例 3-6 显示了使用指针的非均匀数据引用。PCI 设备使用 LE 格式，如果将设备驱动程序移植到 BE 平台，则需要考虑到。

IBM 的 PowerPC 和 AMD 的 64 位架构上的 Linux 提供了一个独特的平台，因为 32 位和 64 位应用程序可以同时运行而没有任何性能损失。这种优势可以通过使用 `gcc` 编译 64 位应用程序来实现，使用 `-m64` 标志生成 64 位对象文件，如下例：

```
$ gcc -m64 sample.c -o sample.o
```
