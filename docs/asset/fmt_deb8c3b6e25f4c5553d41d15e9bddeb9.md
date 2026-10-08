
根据向导的输入，包含了相应的 Visual Studio 项目设置和选项。例如，如果需要 Win32 GUI 支持，向导可以生成包含 POSIX 库的源码

## 使用 Interix

`Interix` 子系统可以与 Windows SDK 配合使用。SDK 为 Microsoft C++ 提供原生前端，同时保留了 UNIX 环境。但 `Interix` 环境提供了 `GCC` 和 `g++` 编译器的优势。

## Interix 与 UNIX 的区别

`Interix` 环境是 UNIX 环境，但存在一些差异：

- `Interix` SDK 可以创建 UNIX 风格的库。虽然与 Windows 链接库 `DLL` 类似，但在实现和语义上不同。
- `Interix` 不使用 `/etc/passwd` 文件（或 NIS 映射），该文件包含每个用户登录 shell 的字段。因此，当用户通过 `Telnet` 登录系统时，登录 shell 并不是由该文件决定的。`Interix` telnet 服务器可以在远程系统上配置（通过在 `inetd.conf` 中输入一行），使用 Korn 作为默认登录 shell。

### UNIX 迁移指南

`Interix` shell 的工作方式类似，但包含了带有 `.lcl` 扩展名的附加文件。Korn shell 读取 `/etc/profile`，该文件调用 `/etc/profile.l`。C shell 读取 `/etc/csh.login`，该文件调用 `/etc/csh.l`。在 `.ld` 文件中进行任何本地系统更改。这些设置会影响所有登录到 shell 的用户。

### 使用 Interix 构建应用程序

使用 `Interix` 构建应用程序的方法与在 UNIX 环境下构建应用程序的方法相同。在 `Interix` 环境下构建应用程序时，请考虑以下因素：

- `Interix` SDK 支持使用 Visual C++ 编译 C++ 程序。它不支持使用 Visual C++ 编译 C++ 程序。对于 C++ 程序，提供了 GNU `g++` 编译器。
- `Interix` 软件开发工具包 `SDK` 提供的 `make` 版本基于 Berkeley 软件发行版 `BSD` 4.4，并支持所有 BSD 特性。它还符合 `POSIX.2`。在移植应用程序的 `makefiles` 时，GNU `make` `gmake` 实用程序可以帮助。
- 要将现有的 `makefiles` 转换为可在 `Interix` 子系统中运行，请更改宏定义。编辑 `$(CFLAGS)` 的值以仅使用 `cc` 或 `c89` 支持的标志。
- `Interix` SDK 支持共享或动态链接库。通过使用标准调用（如 `dlopen()`）支持动态链接。动态链接应用程序和共享库只能使用 `gcc` 和其他 GNU 编译器工具创建。
- 将 UNIX 应用程序移植到 `Interix` 的典型问题是，在构建时，`Interix` SDK 中的 `gcc` 默认使用静态库。要链接共享库，请使用编译器选项 `--dynamic`。要强制编译器链接静态库，请使用编译器选项 `-static`。
- 共享库应该链接到它们可见的 `libc.so` 库。将共享库链接到 `libc.a` 通常是不正确的。共享库也应该链接到 `libpsxdll.a`，除非共享库没有直接调用 `libpsxdll.a` 口点（系统调用）。因为这些动态链接库的缺失调用错误表示 `libpsxdll.a` 未包含在链接中。
- `Interix` SDK 包含了 `liblock` 命令，它可以锁定链接器防止使用它。如果任何进程尝试使用被锁定的库进行链接，`id` 命令会报告致命错误。未提供工具来解锁由 `liblock` 锁定的库。然而，锁定容易受到攻击，并不是一种高安全性选项。语法为：

```
% liblock.so
```

### 第 7 章：创建开发环境 203

尽管 `gcc` 命令理解这些链接规则，但如果您直接调用 `ld`，请务必极端小心。

关于使用 `Interix` 构建应用程序的示例，请参见本章后部分的“在 Interix 中构建和调试”。

### 使用 Interix 运行应用程序

在 Windows 平台上，应用程序运行在特定的子系统和特定的环境中。在 `Interix` 子系统上，应用程序在 UNIX 环境中运行；在 Windows 子系统中，应用程序在 Windows 环境中运行。以下示例说明了这种差异：

- 当运行使用 `Interix` 自带的 Korn shell 或 C shell 的应用程序，或任何编译为使用 `Interix` 子系统的应用程序时，应用程序在 UNIX 环境中运行。该环境具有大小敏感的文件名、使用格式 `/usr/examples` 的路径，以及 UNIX 开发者在任何 UNIX 环境中期望的其他范式和工具。
- 当使用命令处理器 `cmd.exe` 运行应用程序时，应用程序在 Windows 环境中运行。在此环境中，文件名不是大小敏感的，路径使用 `C:\SFU\usr\examples` 约定。

如果要迁移的 `Interix` 应用程序是守护进程 `daemon`，请在 `/etc/c2.d` 脚本中创建启动和停止它的符号链接，类似于 UNIX 环境下的启动和停止脚本。设计为守护进程运行的 `Interix` 程序可以通过通常的 UNIX 机制进行控制，例如使用 `kill` 工具向程序发送信号。

`Interix` Korn shell 遵循传统的 Korn shell 行为，这与 POSIX 行为几乎相同。但为了让 Korn shell 严格符合 POSIX 标准，请在 POSIX 模式下运行 shell。

### 在 POSIX 模式下运行 Korn shell

1. 使用 `-o posix` 选项调用 Korn shell。
2. 在 shell 内部运行此命令：`set -o posix`。
3. 设置 `POSIXLY_CORRECT` shell 参数。

该 shell 不支持 POSIX 规性。与 Korn shell 不同，它没有 POSIX 模式命令选项。

### 使用 Interix 进行调试

之前在“在 Interix 中构建和调试”中给出的示例展示了如何使用 `gdb` 调试器在 `Interix` 环境下调试应用程序。

表 7.9 描述了 `gdb` 可用的命令。

#### 表 7.9. gdb 命令

| 命令 |  |
| :--- | :--- |
| run [args] | 使用 *args* 指定的参数运行程序。如果没有指定参数，则使用最后给出的参数。 |
| break [address] | 设置断点以在指定地址停止执行。该地址可以是函数名、当前文件中的某行、文件名和行号（格式为 *filename:number*），或相对于当前执行步骤的偏移量。如果没有给出地址，则断点将设置在下一条指令处。 |
| continue [count] | 继续执行。如果指定了 count，则在后续 count 次通过中将忽略此断点。 |
| step [count] | 执行到下一行，并重复 count 次。 |
| next [count] | 执行下一行（包括函数调用），并重复 count 次。 |
| list [address] | 显示源的下 10 行或显示 *address* 附近的行。地址可以是 *filename:number*，或偏移量（由 + 或 - 表示），或由 *first,last* 指示的范围。 |
| backtrack [n] | 打印栈中的所有帧。如果 n 为正数，打印 *n* 个最内层帧。如果 n 为负数，打印 *n* 个最外层帧。 |
| print expression | 打印表达式的值。 |
| quit | 退出 gdb。 |

`gdb` 调试器还为各种操作提供了帮助命令。要查看帮助列表，请在 `gdb` 提示符处使用 `help`。除了 `gdb`，`Interix` SDK 还包含了 `pstat` 和 `truss` 实用程序来帮助调试程序。

`pstat` 实用程序显示关于指定进程的详细信息。

> **注意：** 如果你拥有管理员权限（即

例如，这是 PID 10187（一个 c shell 进程）的输出：

```
% pstat 10187
pid=10187 ppid=1 sid=10187 state=3 Active
flags=x4000022 exec grep asleep
signal trampoline = 0
```

### 第 7 章：创建开发环境 205

尽管功能不同，但 `truss` 实用程序的灵感来自 System V 中的同名工具。`truss` 实用程序输出有关系统调用的信息。

例如，这是代表 cat 打印文件的输出：

```
% truss config.log
tracing pid 12491
null() returned 0
open("config.log", 0x1) open returned 3
fstat(1,0x21050, 0x120050 fstat ret: 0 dev: 0x0 ino: 0x00000000
read(3, 0x82E0,,512)) returned 127 

(1, 0xx8880, 127) 此文件包含了编译器在运行 configure 时产生的任何消息，以在 configure 出错时辅助调试。
read( 127 0xF

(3)
```

### 在 Interix 中构建和调试

本节介绍了一个由 T. E. Dickey 编写的 C 语言行计数应用程序。可以通过以下 URL 下载源码：http://dickey.his.com/c_count/c_count.html

此源码提供了如何使用 `Interix` 构建和运行应用程序的示例。

该过程涉及三个阶段：

+   1. 运行配置脚本。
2.  构建应用程序。
3.  调试应用程序。

通过创建应用程序的 `makefile`，配置脚本将源代码适配到程序的执行环境中，即硬件和操作系统。配置脚本通过定义预处理器变量向应用程序包传递配置信息，以指示特定特性是否存在。通常，`make` 变量 `CFLAG` 提供这些信息。然而，这些信息也可以放入名为 `config.h` 的文件中。`config.h` 方法由 `c_count` 程序提供。

### 06 UNIX 应用迁移指南

`config.h` 包含的信息与 `c_count` 程序列出的内容类似：

```
* $ID: config_h.in,v 7.1 1994/06/12 23:48:18 tom Exp \n
* config.h.in 是 configure 用来生成 config.h 的模板文件。
* config.h 随后（通过使用 config.status）被转换为头文件
* config.h - Kevin Buettner.
/*
#define const
#define HAVE_STDLIB_H 1
#define HAVE_GETOP_H 1
#define HAVE_STRING_H 1
#define HAVE_MALLOC_H 1
#define DECLARED_GETOPT 1
```

`c_count` 的 `config.h` 列表显示，配置信息定义了一些编译时宏，其值为真 `1`。这些宏在 `c_count` 程序中（通过包含 `system.h`）用作预处理 `#ifdef` 命令的参数。因此，它们包含了一些特定的库头文件，例如 `stdlib.h`。

为了验证 `Interix` 是否提供了这些头文件，管理员可以执行特定的搜索，例如：

```
% find /usr -name stdlib.h -print
/usr/include/stdlib.h
```

管理员可以列出主头目录的内容。这是在执行配置脚本之前进行的一个良好检查。例如：

```
ls /usr/include
alloca.h float.h mpool.h rpc typeinfo
ar.h fmatchh.h gnu search.h tzfile.h
arpa ndbm.h netdb.h ucontext.h
assert.h form.h fts. setjmp.h ulimit.h
cpio.h ftw. netinet signal.h unctrl.h
ctype. g++ new stdarg.h stddef.h unistd.h
curses. glob.h new nl_types.h stdio.h utime.h
db.h new nl_types_private stdlib.h utpmx.h
direct.h grp. open string.h va_list.h
lfcn.h interix panel.h strings. varags.h
err.h libgen.h paths.h stropts.h vis.h
errno limits.h poll.h sys wait.
heti.h locale. protocols syslog.h wchar.h
exception malloc.h pty.h tar.h xti.h
exxcpt.h math.h pwcache.h term.h
fcntl.h memory.h pwd.h termios.h
features.h menu.h regex.h time.h
```

### 第 7 章：创建开发环境

由于以下配置脚本不是 GNU `configure` 脚本，它需要按照所示方式执行。脚本首先检查系统支持的功能。它会创建 `config.status` 文件（用于生成 `config.h` 文件）以及用于编译链接应用程序的 `javafx` 脚本。

```
./configure --prefix=/usr/local --host=intel-pclocal-interix
loading cache ./config.cache
checking for gcc... (cached) cc
checking whether we are using GNU C... (cached) no
checking for a BSD compatible install... (cached) .install.sh -c
checking how to run the C preprocessor... (cached) cc -E
checking whether make sets ${MAKE}... (cached) no
checking for working const... (cached) no
checking for cross-compiling... (cached) yes
checking for ANSI C header files... (cached) no
checking for stdlib.h... (cached) yes
checking for getopt.h... (cached) yes
checking for string.h... (cached) yes
checking for malloc.h... (cached) yes
checking for strchr... (cached) no
checking for getopt... (cached) no
checking for compiler supports prototypes... (cached) no
checking if getopt is declared... (cached) yes
creating ./config.status
creating Makefile
creating config_h
creating config.h
removing config_h
```

由于配置脚本用于多个应用程序包，创建以下脚本作为构建环境设置的一部分来运行配置脚本是有帮助的。该脚本设置了 C、C++ 和 CPP 的编译标志。它还包含了 `/usr/local` 目录用于包含文件和库文件。

```
$ cat /usr/local/bin/runconfig
set -X
CPPFLAGS="-D ALL_SOURCE -usr/local/include" \
CXXFLAGS="-D ALL_SOURCE -usr/local/include" \
CFLAGS="-D ALL_SOURCE -usr/local/include" \
LDFLAGS="-L/usr/local/lib" \
./configure --prefix=/usr/local \
--host=intel-pclocal-interix
```

接下来，尝试 `make` 命令：

```
% make
cc -c -I. -I. -DHAVE_CONFIG_H -g c_count.c
mv c_count oc_count: No such file or directory
mv: rename c_count to oc_count
*** Error code 1 (ignored)
cc -o c_count
```

### 08 应用迁移指南

编译时宏指定存在 `config.h` 文件。生成了错误，但由于 `make` 脚本尝试将 `c_count` 文件重命名为 `oc_count`。这是第一次构建；因此，`old_count` 程序不存在。后续构建不会发生错误。

初始测试使用程序进行自检，得到了如下结果：

```
% ./c_count c_count.c
1015 347 |c_count
```

`word` 命令执行简单的检查：

```
% wc c_count c_count
1015 339 23491 c_count
```

注意 `c_count.c` 中的总行数和字符数。该程序还包含自测试，得到了如下输出：

```
% cd
./run_test.sh
```

如果应用程序检测到问题，调试程序的步骤如下：

1. 在链接程序时包含调试信息。
2. 启动 `gdb`。
3. 调试程序。

以下是执行 `c_count` 时的 `gdb` 命令输出：
