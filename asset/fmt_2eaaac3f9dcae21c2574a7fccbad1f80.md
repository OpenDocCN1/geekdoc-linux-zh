
```cpp
havea = true;
}

optind++;

break;

case 'p':

if (optind < argc) {
    port = atoi(argv[optind]);
    havep = true;
}
optind++;
break;

}
}

argc -= optind;
v += optind;
if (!havei && !haveo)
    usage();
if (haveo && (!havep || !havea))
    usage();
if (haveo) {
    bzero(&saddr, sizeof(saddr));
    saddr.sin_family = AF_INET;
    saddr.sin_port = htons(port);
    inet_pton(AF_INET, addr.c_str(), &saddr.sin_addr);
    DumpAddr(&saddr);
    if (BinaryWrite(&saddr, ofile.c_str())) {
        cerr << "Problem writing " << ofile
             << "\n";
    }
}
if (havei) {
    bzero(&saddr, sizeof(saddr));
    if (BinaryRead(&saddr, ifile.c_str())) {
        cerr << "Problem reading " << ifile
             << "\n";
    }
    DumpAddr(&saddr);
}
exit(0);
}
```

```cpp
void
usage() {
  cerr << "usage: rswockaddr -o file | -i file |\n  -a addr -p port\n";
  exit(1);
}
```

在描述描述源代码之前，让我们看看在 Linux 和 Mac OS X 上使用该程序生成二进制文件会发生什么：

```bash
./rswockaddr -a 192.168.1.123 -p 30 -o linuxbin.out
```

```
saddr.sin_family is AF_INET
saddr.sin_port is 30
saddr.sin_addr is 192.168.1.123
```

查看结果，通过 `od` 看到如下（文件中的每个字符以十六进制显示）：

```bash
$ od -x linuxbin.out
00000000 0200001e c0a8017b 00000000
```

前两个字节 `0200` 是 `sin_family` 字段。接下来的两个字节 `001e` 是端口（十进制）。后面是四个字节 `c0a8017b` 表示 IP 地址 `192.168.1.123`。文件中剩下的八个字节是 `sin_zero` 字段的值。

在 Mac OS 上，我们得到了类似的输出，但文件中的前两个字节不同：

```bash
$ od -x macosbin.out
00000000 0000001e c0a8017b 00000000
```

前两个字节 `0000` 是 `sin_family` 字段。接下来的两个字节 `001e` 是端口（十进制）。后面是四个字节 `c0a8017b` 表示 IP 地址 `192.168.1.123`。文件中剩下的八个字节是 `sin_zero` 字段的值。

## 288 第6 章 杂项移植性主题

显然，对端口和地址的处理虽然正确，但不足以解决我们的问题。这个问题的原因是：文件的前两个字节以 `short` 类型存储 `sin_family` 字段，而在 Mac OS 上，前两个字节被用于存储 `sin_len` 值，随后是一个 1 字节的 `sin_family` 字段。因此，在 Linux 读取 Mac OS 文件时，会将 `0x0020` 放入 `sin_family` 字段，其值为 32，`DumpAddr()` 函数无法识别为合法值。同样，`inet_ntop(3)` 也无法转换 `sin_addr()` 字段，因为它的第一个参数也不是合法值。在 Mac OS X 上读取 Linux 生成的文件也会出现类似的问题；这次，第一个字符 `0x02` 被加载到 `sin_family` 字段中，而值 0 被加载到 `sin_family`，`DumpAddr()` 生成了类似的结果。

处理这个问题有两种方法：

- 想出一种与平台无关的写入 `sin_family` 字段的方法。
- 写入元数据以告知数据的格式。

这两种方法中的后可以通过要求写入者在文件开头输出一个用于识别的标记来处理。

文件中的数据格式。图像文件格式通过这种方式帮助读者识别正在读取的文件格式；例如，PNG 文件始终以 8 字节的字符序列开头，标识该文件包含 PNG 图像数据。我们将该值读入具有适当布局的结构体中，然后将字段从该结构体拷贝到原生的 `sockaddr_in` 结构体中。简而言之：

- 写入者在文件开头输出 1 个或多个字节（具有约定的长度和值）以标识格式，随后是原生数据。
- 读取者从文件开头读取标识字节，并根据这些字节将数据从文件读取到与识别出的格式对应的结构体中，然后将结果中的每个字段拷贝到原生结构体中。

这两个选项中的第一种（生成与平台无关的格式）几乎相同，但实现起来更简单，因为它的优势是不需要在文件开头生成标识字节，而且读取者不需要感知所有可能需要支持的格式。写入者只需要从原生表示拷贝到约定的平台无关格式，读取者只需要使用数据从平台无关格式拷贝到原生表示即可。

以下函数 `XPBinaryRead()` 和 `XPBinaryWrite()` 实现了支持跨平台版本 `sockaddr_in` 所需的更改。事实 BSD 版本的 `sockaddr_in` 是的；我们需要保留 `sin_family` 字段，因为 BSD 支持它，而且 `sin_family` 字段不需要像在 Linux 中那样是 `short` 类型——一个 `char` 就足以容纳可能赋值的值。以下是跨平台结构体的定义：

```c
// platform sockaddr_in
struct xpsockaddr_in {
    u_char sin_len;      // BSD 特有
    u_char sin_family;   // 只需要 1 字节
    u_short sin_port;     // BSD 和 Linux 相同
    struct in_addr sin_addr; // 同样
    char sin_zero[8];    // 同样
};
```

# 第 20 项：避免二进制数据的序列化

`XPBinaryRead()` 读取存储在指定文件中 `xpsockaddr_in` 数据，并将其拷贝到原生的 `sockaddr_in` 结构体中：

```cpp
int
XPBinaryRead(struct sockaddr_in * saddr,
    const char *path)
{
    xpsockaddr_in xpsockaddr;
    bzero(&xpsockaddr, sizeof(xpsockaddr));
    ifstream file(path, ios_base::in);
    unsigned int retval = 1;
    if (file.is_open()) {
        file.read(reinterpret_cast<char *>(&xpsockaddr),
                  sizeof(struct xpsockaddr_in));
        retval = !(file.gcount() ==
                  sizeof(struct xpsockaddr_in));
        if (retval == 0) { // 已根据逻辑修正
#if defined(linux)
            saddr->sin_len = xpsockaddr.sin_len;
#endif
            saddr->sin_family = xpsockaddr.sin_family;
            saddr->sin_port = xpsockaddr.sin_port;
            memcpy(&saddr->sin_addr, &xpsockaddr.sin_addr,
                   sizeof(saddr->sin_addr));
            memcpy(&saddr->sin_zero, &xpsockaddr.sin_zero,
                   sizeof(xpsockaddr.sin_zero));
        }
        file.close();
    }
    return retval;
}
```

同样，`XPBinaryWrite()` 将字段从传入的原生 `sockaddr_in` 结构体拷贝到 `xpsockaddr_in` 结构体，并将结果写入文件：

```cpp
int
XPBinaryWrite(struct sockaddr_in * saddr,
    const char *path)
{
    xpsockaddr_in xpsaddr;
    bzero(&xpsaddr, sizeof(xpsaddr));
    // 将 saddr 拷贝到 xpsaddr
#if defined (linux)
    xpsaddr.sin_len = saddr->sin_len;
#endif
    xpsaddr.sin_family = saddr->sin_family;
    xpsaddr.sin_port = saddr->sin_port;
    memcpy(&xpsaddr.sin_addr, &saddr->sin_addr, sizeof(xpsaddr.sin_addr));
    memcpy(&xpsaddr.sin_zero, &saddr->sin_zero, sizeof(xpsaddr.sin_zero));
    ofstream ofile(path, ios_base::binary | 
                   ios_base::out | ios_base::trunc);
    unsigned int retval = 1;
    if (ofile.is_open()) {
      ofile.write(reinterpret_cast<char *>(&xpsaddr),
                 sizeof(struct xpsockaddr_in));
      retval = !ofile.good();
      ofile.close();
    }
    return retval;
}
```

注意，这两个函数在向 `sin_len` 字段拷贝或从其拷贝的代码周围都加了 `#if !defined(linux)`，因为该字段在 Linux 的 `sockaddr_in` 实现中并不存在。理想情况下，我们不应该在代码中使用大量的 `#ifdef`；请参见第 2 项中关于消除它们的策略。

最后，我们应该意识到影响程序中表示数据所需的大小或数据排列方式的编译器选项。g++ 支持的几个选项都属于这一类，包括以下项：

- fshort-enums—仅使用表示枚举关联值所需的字节数（最多到 `int`）。
- fshort-double—给双精度浮点数赋予与单精度相同的大小。
- fpack-struct—对内存中的成员进行打包，使其没有空隙，而不是在可能的最优边界上进行对齐。这些影响变量布局的选项，如果不努力确保其在项目所使用的所有平台和所有编译器上保持一致，将会导致问题。

# 第 21 项：避免与类型大小相关的问题

在实践中，我将在本项中要讨论的领域通常没有给我带来太多麻烦。尽管如此，我至少应该提到几个每位 C 和 C++ 程序员都应该关注的事项。在某些情况下，对 `int` 以及相关类型 `short` 和 `long`（以及它们的无符号变）的大小做出错误假设可能会引入移植性错误。整数类型在很大程度上取决于 CPU 和编译器。你通常可以认为，表示 `int` 使用的位数与编译器为之生成代码的 CPU 字长一致。例如，在 32 位系统上，`int` 将是 32 位（4 字节）。在 32 位系统上，`unsigned int` 同样预期是 32 位。在 64 位系统上，`int` 和 `unsigned int` 预期是 64 位。然而，不确定的可能是 `short`、`long`、`long long` 及其无符号类型。语言保证 `short` 至少是 16 位。如何知道 `short` 有多大？一种方法是计算 `short` 的位数：

```cpp
int shortInBits = sizeof(short) * 8;
printf("size of short in bits is %d\n", shortInBits);
```

使用这个结果，我们推断 `short` 的补码范围为 `[-32768, 32767]`。然而，这并没有保证。为什么？我们依赖 `sizeof` 运算符返回字符的大小，我们假设它是 8 位。使用 `sizeof` 是好主意，但这种假设像很多一样是危险的，因为 `char` 可能是 16 位、32 位甚至 64 位。为了确定任何整数类型的实际范围，我们需要更可靠的东西，为此我们需要查看别处。头文件 `limits.h`（C++ 中为 `climits`）。该文件包含了列出的 `short`、`int`、`long` 和 `long long`（以及相应的无符号类型）整数类型可以取的最小值和最大值。定义的宏格式均为 `T_MAX` 和 `T_MIN`，其中 `T` 是 `CHAR`、`SHRT`、`INT`、`LONG` 和 `LLONG` 之一。无符号版本的 `T_MAX` 也有定义，通过在前面加上 `U`；例如 `UCHAR` 和 `USHRT`。无符号类型不需要 `T_MIN`，因为 `T_MIN` 始终为 0。

以下是 Darwin/Mac OS X 的位数和限制：

```c
#define CHAR_MAX    127      /* 有符号 char 的最大值 */
#define CHAR_MIN   (-128)   /* 有符号 char 的最小值 */
```

```c
#define UCHAR_MAX   255      /* 无符号 char 的最大值 */
#define CHAR_MAX    127      /* 有符号 char 的最大值 */
#define CHAR_MIN   (-128)   /* 有符号 char 的最小值 */
```

```c
#define USHRT_MAX   65535    /* 无符号 short 的最大值 */
#define SHRT_MAX    32767    /* 有符号 short 的最大值 */
#define SHRT_MIN   (-32768) /* 有符号 short 的最小值 */
```

## 项目 2：避免与类型大小和组织相关的问题 295

```c
#define UINT_MAX 0xffffffff /* * 无符号 int 的最大值 */
#define INT_MAX 2147483647 /* * int 的最大值 */
#define INT_MIN (-2147483647-1) /* * int 的最小值 */
```

```c
#ifdef __LP64__
#define ULONG_MAX 0xffffffffffffffff /* * 无符号 long 最大值 */
#define LONG_MAX 0x7fffffffffffffff /* * 有符号 long 最大值 */
#define LONG_MIN (-0x7fffffffffffffffL-1) /* * 有符号 long 最小值 */
#else // !__LP64__
#define ULONG_MAX 0xffffffff /* * 无符号 int 的最大值 */
#define LONG_MAX 2147483647 /* * long 的最大值 */
#define LONG_MIN (-2147483647-1) /* * long 的最小值 */
#endif // __LP64__
```

```c
#define ULONG_MAX 0xffffffffffffffffff /* * 无符号 long 最大值 */
#define LONG_MAX 0x7fffffffffffffffffff /* * 有符号 long 最大值 */
#define LONG_MIN (-0x7fffffffffffffffffff-1) /* * 有符号 long 最小值 */
```
