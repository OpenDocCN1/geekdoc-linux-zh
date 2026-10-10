
## 第 20 项：避免二进制数据的序列化

将端口值从网络短整型（`short`）转换为原生字节序；这是通过调用 `ntohs(3)` 完成的，你可以在 `DumpAddr()` 函数中看到这一点：

```cpp
cout << "saddr.sin_port is " << ntohs(saddr->sin_port) 
      << "\n";
```

就像 `htons()` 在大端系统上是空操作一样，`ntohs()` 也是如此。

接下来，我们考虑存储在 `sin_addr` 中的 IP 地址。按照惯例，IP 地址的值被排列为字节序列，从左到右排序。`inet_pton(3)` 函数负责处理从人类可读的字符到网络字节序字节序列的转换，并且在读取时，我们可以使用 `inet_ntop(3)` 从 `sin_addr` 字段获取一个可以打印到控制台的可打印字符串。

上述对端口和 IP 地址字段的处理暗示了一种使二进制数据能够抵抗平台差异（具有韧性）的通用策略：

- 同意存储此类值时使用的字节数。
- 同意字节序转换（即小端与大端转换），并确保写入者在写入之前将其转换为该格式，读取者在将结果作为值使用之前也进行转换。

显然，对端口和地址的处理虽然是正确的，但不足以解决我们的问题。其原因是：文件的前两个字节将 `sin_family` 字段作为 `short` 存储，而在 Mac OS X 上，前两个字节被用于存储一个 `sin_len` 值，紧随之后是一个 1 字节的 `long` 类型的 `sin_family` 字段。因此，在 Linux 上读取 Mac OS X 的文件会将值 `0x0020` 放入 `sin_family` 字段中，该值为 512，且不会被 `DumpAddr()` 函数识别为合法值。同样，`inet_ntop(3)` 无法转换 `sin_addr()` 字段，因为它的第一个参数也不是合法值。在 Mac OS X 上读取 Linux 生成的文件时也会发生类似的问题；此时，第一个字符 `0x02` 被加载到 `sin_len` 字段中，值 `0` 被加载到 `sin_family` 中，`DumpAddr()` 生成了类似的结果。

解决这个问题办法两种方法：

- 提出一种平台中性的写入 `sin_family` 字段的方法。
- 编写元数据来告知数据的格式是什么。

这两个选项中的第二个可以通过要求写入者在文件开头输出一个令牌（`token`），该令牌可用于识别文件中数据的格式。图像文件格式经常这样做，用以帮助读取者识别正在读取的文件格式；例如，PNG 文件始终以 8 字节的字符序列开头，标识该文件包含 PNG 图像数据。然后我们将该值读取到一个具有相应布局的结构体中，然后将字段从结构体拷贝到原生的 `sockaddr_in` 结构体中。

- 写入者在文件开头输出一个 1 个或多个字节的序列（具有约定的长度和值）以标识格式，随后是原生数据。
- 读取者从文件开始读取标识字节，并根据这些字节将数据从文件读取到与识别出的格式对应的结构体中，然后将结果中的每个字段拷贝到原生结构体中。

这两个选项中的第一个选项（生成一种平台中性的格式）几乎相同，但实现起来更简单，因为它具有优势：不需要在文件开头生成标识字节，且读取者不需要感知可能需要支持的所有可能的格式。所有需要的仅仅是让写入者从原生表示拷贝到约定的平台中性格式，而让读取者在使用数据之前，从平台中性格式拷贝到原生表示即可。

以下函数 `XPBinaryRead()` 和 `XPBinaryWrite()` 实现了支持 `sockaddr_in` 跨平台版本所需的更改。

## 第 6 章 杂项移植性主题

范围。我们如何知道 `short` 到底有多大？一种方法是计算 `short` 的位数：

```cpp
int shortSizeInBits = sizeof(short) * 8;
printf("size of short in bits is %d\n", shortSizeInBits);
```

当由 GCC 编译并运行在我基于 G4 芯片的 Mac OS X 系统上时，它输出如下：

```
size of short in bits is 16
```

利用这个结果，我们可能会推断在该系统上，`short` 的补码范围正好是 `[-32768, 32767]`。然而，这并不是保证的。为什么呢？这里我们依赖于 `sizeof` 运算符返回类型以字符（`char`）为单位的大小，我们假设字符的大小是 8 位。使用 `sizeof` 是一个好主意，但这个假设（像很多假设一样）是危险的，因为 8 位只是 `char` 的最小大小保证，而不是绝对要求。这意味着，事实上，我们的 `short` 大小可能是 16 位、32 位，甚至是 64 位。为了确定整数类型的实际范围，我们需要更可靠的方法，而为此，我们需要去别处查看。

头文件 `limits.h`（C++ 中为 `climits`）就是那个地方。该文件包含了宏，列出了 `short`、`int`、`long` 和 `long long`（以及它们的无符号对应类型）可以取的极值。定义的宏格式均为 `T_MAX` 和 `T_MIN`，其中 `T` 是 `CHAR`、`SHRT`、`INT`、`LONG` 和 `LLONG` 之一。通过在上述名称后加一个 `U`（例如 `CHAR` 和 `USHRT`），还提供了 `T_MAX` 的无符号版本。（无符号类型不需要 `T_MIN`，最小值始终为 0。）

以下是 Darwin/Mac OS X 上 `limits.h` 的核心内容：

```cpp
#define CHAR_MAX    127      /* 有符号 char 的最大值 */
#define CHAR_MIN   (-128)   /* 有符号 char 的最小值 */
#define UCHAR_MAX   255      /* 无符号 char 的最大值 */
#define CHAR_MAX    127      /* char 的最大值 */
#define CHAR_MIN   (-128)   /* char 的最小值 */
#define USHRT_MAX   65535    /* 无符号 short 的最大值 */
#define SHRT_MAX    32767    /* short 的最大值 */
#define SHRT_MIN   (-32768) /* short 的最小值 */
```

### 项目 2：避免与类型大小和组织相关的问题

```cpp
#define UINT_MAX 0xffffffff /* 无符号 int 的最大值 */
#define INT_MAX 2147483647 /* int 的最大值 */
#define INT_MIN (-2147483647-1) /* int 的最小值 */
```

```cpp
#ifdef __LP64__
#define ULONG_MAX 0xffffffffffffffff /* 无符号 long 的最大值 */
#define LONG_MAX 0x7fffffffffffffff /* 有符号 long 的最大值 */
#define LONG_MIN (-0x7fffffffffffffff-1) /* 有符号 long 的最小值 */
#else // 如果 !__LP64__
#define ULONG_MAX 0xffffffff /* 无符号 long 的最大值 */
#define LONG_MAX 2147483647 /* 有符号 long 的最大值 */
#define LONG_MIN (-2147483647-1) /* 有符号 long 的最小值 */
#endif // __LP64__
```
