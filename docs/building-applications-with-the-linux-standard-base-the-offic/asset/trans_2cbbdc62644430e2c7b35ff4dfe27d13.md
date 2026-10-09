

| 目标 | .DEFAULT, .IGNORE, .PRECIOUS, .SILENT, .SUFFIX |
|---|---|
| 内部宏 | $*, $§, $?, $<, $@, $$, $(), $(D) |
| 预定义宏 | ar, as, cc, ld, lex, lint, m2c, pc, rm -f, yacc |
| 环境变量 | MAKEFLAGS |
| 变量 | CC, CFLAGS, CPPFLAGS, FC, FFLAGS, LEX, LFLAGS, YACC, YFLAGS, LD, LDLFLAGS |

- C 用户指南⁶
- C++ 用户指南⁷

当应用程序编译为适用于 Solaris 环境后，必须在运行于 SPARC 硬件上的 Linux 版本上重复该过程。由于该应用程序已经符合 GNU 工具链的要求，因此可能出现的唯一问题将源于运行时应用程序编程接口（API）。为了实现完全兼容的应用程序，需要修正这些 API 之间的差异。以下是 Linux 和 Solaris 之间的一些主要差异。

### 系统调用

在提供逻辑卷支持、文件访问控制列表以及系统审计日志支持的 API 方面，Solaris 和 Linux 之间存在命名差异。STREAMS 支持（对于编写基于流的网络驱动程序非常有用）在 Linux 上不可用，但在 Solaris 上可用。因此，解决此类问题的方法是获取第三方独立开发的解决方案，或者重写应用程序以使用相关技术。在这种情况下，可以使用 POSIX 套接字代替 STREAMS 进行网络通信。

### 库差异

Linux 上可用的标准 C++ 库包括对大多数功能的支持。Solaris 具有一些额外的库，例如 *compat=4*、经典 *iostreams* 以及支持 ASCII 编码十进制转换的 *math* 库。如果待移植的应用程序使用了其中任何这些额外库，则必须将其修改为使用标准 C++ 库。

**线程差异** Solaris 进程基于称为 *轻量级* *进程*（*LWP*）的线程。在当前 Linux 实现中，线程基于 *进程*。Solaris 中有两种类型的线程可用：POSIX 线程和原生线程模型。Linux 支持 POSIX 线程，因此所有使用原生线程的应用程序都应修改为使用 POSIX 线程。

### 5.1.4 步骤 4：在目标平台上构建 Linux 上的应用程序

在目标平台上安装 Linux，并重新构建前一步骤中修改后的应用程序。

## 5.2 移植中的问题

将应用程序从 Solaris 平台移植到 Linux 平台可能被视为一项简单的任务，这是因为 Linux 平台的 GNU C 库提供了应用程序级别的便携性。在大多数情况下，只需重新编译程序即可移植应用程序。但如果代码包含任何依赖于系统或硬件的结构，则需要一些修改以完成完整的移植。此类移植工作的复杂度与系统和硬件依赖代码的数量成正比。如果应用程序仅使用标准语言结构且不考虑平台因素，则此类应用程序的移植相对简单。如果应用程序使用非 POSIX 结构或平台特定的优化，则移植难度较大。通常，Java 应用程序属于第一类，而非 POSIX C 程序属于第二类。与移植相关的部分问题在下述章节中进行了说明。

### 5.2.1 字节序

字节序，或 *端序*（*endianness*），是数据元素的一种属性，指的是其字节在内存中存储或寻址的方式。该属性由平台的 CPU 架构决定。端序有两种可能的值：*大端*（*big endian*）和*小端*（*little endian*）。

#### 5.2.1.1 大端

在这种字节序类型中，最高有效字节存储在最低存储地址——例如，最高有效字节存储在最左侧位置。Sun SPARC、HP Precision 和 IBM PPC 使用这种排序方式（例 5.1）。

> 例 5.1：大端排序
> 数据：0x33445566
> 存储：
>
> | 字节 0 | 字节 1 | 字节 2 | 字节 3 |
> | --- | --- | --- | --- |
> | 33 (最高有效) | 44 | 55 | 66 |

#### 5.2.1.2 小端

在这种字节序类型中，最低有效字节存储在最低存储地址——例如，最低有效字节存储在最左侧位置。Intel 和 DEC 架构使用此排序方式（例 5.2）。

> 例 5.2：小端排序
> 数据：0x33445566
> 存储：
>
> | 字节 0 | 字节 1 | 字节 2 | 字节 3 |
> | --- | --- | --- | --- |
> | 66 (最低有效) | 55 | 44 | 33 |

#### 5.2.1.3 字节序与 Union 数据结构

如果代码使用 *union*（联合体）数据结构，前几节讨论的字节序将成为移植中的一个问题。*Union* 是一种用于在同一存储区域中操作不同类型数据的数据结构。管理该存储区域中存储数据的大小和对齐完全是编译器的职责。例如，考虑例 5.3 中所示的联合体。

```
Example 5.3: Union Data Structure

union char_int {
    char a[4];
    int i;
};
char_int;
```

考虑例 5.4 中使用上述联合体的代码。

```
Example 5.4: Wrong Use of a Union

// define an instance variable of the union
union char_int cint;
// define a variable to hold the computation result
int result;
// assign a value to the union using the integer variable
cint.i = 0x10394500;
// divide the constant 100 with the union’s MSB,
// that is, its first byte
result = 100/a[0];
```

此示例利用字节序知识检索整数数据的最高有效字节。虽然此代码在大端架构上能正常工作，但当它移植到小端机器时，由于除以零错误，代码将失败。为了使其具有可移植性，代码内部不应使用字节序信息，或者必须通过编译参数有条件地定义字节信息（例 5.5）。

字节序也可能导致网络数据传输问题。大多数现代网络协议都考虑了端序。这些协议使用外部数据表示（XDR）排序来传输数据。来自不同源环境的数据在开始传输之前会转换为此表示。传输结束时，数据将转换回目标环境的本地表示。进行原始数据传输的分布式应用程序也应考虑端序。

```
Example 5.5: Correct Use of a Union

// Portability code added
#ifdef BIGENDIAN
const int MSBBYTE=0;
#else
const int MSBBYTE=3;
#endif

// define an instance variable of the union
union char_int cint;
// define a variable to hold the computation result
int result;
// assign a value to the union using the integer variable
cint.i = 0x10394500;
// divide the constant 100 with the union’s MSB.
// that is, its first byte
result = 100/a[MSBBYTE];
```

标准 C 库提供了许多例程来执行此转换。诸如以下这样的 API 提供了一种在执行网络传输时确保平台独立性的方法。

- ntohl() 将无符号 int 从 XDR 转换为本地格式。
- ntohs() 将无符号 short 从 XDR 转换为本地格式。
- htonl() 将无符号 int 从本地格式转换为 XDR。
- htons() 将无符号 short 从本地格式转换为 XDR。

## 5.3 信号处理

信号是通知进程或线程事件发生的手段。在此领域中，Linux 支持大多数 UNIX 系统（如 SVR4 和 BSD 实现）支持的信号。然而，有一些例外需要考虑。

- SIGEMT，表示硬件故障，不受支持。
- SIGINFO，表示键盘信息请求，受支持。
- SIGSYS，表示无效的系统调用，不受支持。
- SIGABRT 和 SIGIOT 是相同的。
- SIGIO、SIGPOLL 和 SIGURG 是相同的。
- SIGBUS 定义为 SIGUNUSED，因为 Linux 中没有“总线错误”。

表 5.2 列出了各种信号及其在 Solaris 和 Linux 环境中的含义。此表可用于验证代码中使用的信号在 Linux 中是否具有不同的语义。

表 5.2：Solaris 和 Linux 中信号的语义

| 信号 | Solaris | Linux |
| :--- | :--- | :--- |
| SIGHUP | 终止 | 忽略 |
| SIGINT | 终止 | 忽略 |
| SIGQUIT | 终止，核心 | 终止，核心 |
| SIGILL | 终止，核心 | 终止，核心 |
| SIGTRAP | 终止，核心 | 忽略 |
| SIGABRT | 终止，核心 | 终止，核心 |
| SIGEMT | 终止，核心 | 在 Linux 上不受支持 |
| SIGFPE | 终止，核心 | 终止，核心 |
| SIGKILL | 终止 | 终止 |
| SIGBUS | 终止，核心 | 终止，核心 |
| SIGSEGV | 终止，核心 | 终止，核心 |
| SIGSYS | 终止，核心 | 在 Linux 上不受支持 |
| SIGPIPE | 终止 | 忽略 |

