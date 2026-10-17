
可以在 UNIX 系统上创建 tarball 或 `.tar` 文件，并使用 Windows 版本的 `mkhsoff` 或 `mkhbryd` (http://www.ps.ucl.ac.uk/~jecourse/mkhbryd.html) 创建带有 Rock Ridge 扩展的 CD-R，以保留 UNIX 的所有权和权限信息。如果你想从 FTP 站点为 UNIX 系统创建 CD 但但在 Windows 机器上刻录 CD，这种功能将非常有用——你可以利用许多 FTP 服务器发送 `.tar` 格式数据的能力，然后从 `.tar` 文件创建 CD。

要了解更多关于 Rock Ridge 扩展的信息，请参见“ISO-9660 的 Rock 扩展”，第 324 页。

表 15.3 和 15.4 总结了 `tar` 的一些最有用的选项。你必须精确使用表 15.3 列出的其中一个参数，可以使用表 15.4 列出的任意数量的参数。你可以在字符串中组合两个或多个单字符 `tar` 参数，例如使用 `tar -cv` 创建一个启用详细模式（verbose）的 `.tar` 文件。如果你需要使用多个需要其自身参数的选项，你可能需要使用该选项的长格式；但仅对于单个参数，你可以使用短格式，例如 `tar -cvf test.tar`。在 GNU 版本的 `tar` 中，你可以省略单字符中的横杠 `-`。

### 注意

`tar` 的选项对大小写敏感！某些字母具有双重作用，大写和小小写不同可能会导致意外的结果。

表 15.3 必需参数

| 参数 | 含义 |
|---|---|
| `-A` | 将一个 tar 文件连接到另一个文件 |
| `-c` | 创建归档 |
| `-d` | 从归档中删除文件 |
| `-r` | 向现有归档添加文件 |
| `-t` | 列出归档内容 |
| `-u` | 添加比归档文件中新的磁盘文件 |
| `-x` | 从归档中提取文件 |

表 15.4 可选参数

| 参数 | 含义 |
|---|---|
| `-f` | 使用文件名 |
| `-h` | 将符号链接存储为指向的文件 |
| `-i` | 即使文件无法读取也继续 |
| `-k` | 不覆盖现有文件 |
| `-l` | 仅从单个文件系统创建归档 |
| `-M` | 操作多卷归档 |
| `-p` | 保留所有 UNIX 权限 |
| `-P` | 不去除路径开头的 / |
| `-T` | 从文件名获取文件列表 |
| `-v` | 列出处理的所有文件 |
| `-W` | 执行操作后验证文件 |
| `--exclude` | 从操作中排除文件 |
| `-X` | 排除文件名列出的文件 |
| `-Z` | 将 UNIX compress 程序应用于归档 |
| `-z` | 将 GNU gzip 程序应用于归档 |

## 跨平台工具

在 Windows 风格的操作系统上，你可能会发现使用 Windows GUI 工具处理 tarball 非常方便。许多创建和操作 zip 归档的工具也可以处理 tarball，因此对于这些使用非常有帮助。

# 使用 GNU 编译器和调试器开发软件

FSF 的最早项目之一是开发 C 编译器，后来被称为 GNU C 编译器或 GNU 编译集合 `GCC`，http://www.fsf.org/software/gcc/gcc.html。该编译器已一直用作其他编译器的模型，包括 GNU Pascal (https://agnes.dida.physik.uni-essen.de/-gnu-pascal/)、FORTRAN（现包含在 GCC 中）以及其他。由于 C 和 C++ 是许多程序员的首选语言，我重点关注这些语言，而你可能为了特定的跨平台目的使用其他的 GNU 编译器。

# GNU 工具集

注意：我在这书中甚至无法开始教授编程。对于 C 语言编程入门，Sams 出版的 Stephen Prata 为 White Group 编写的《C 语言入门》（第三版）是一个很好的起点。C 语言最初是在 Brian W. Kernighhan 由 Prentice-Hall 出版的《C 语言》中定义的。

为你的操作系统获取 GCC

Linux 和 BSD 等开源 UNIX 变体极度依赖 GCC。这些开源软件（OSS）通常包含 GCC 以及相关工具，如 `gdb` (http://www.fsf.org/software/gdb/gdb.html)，即 GNU 调试器。对于其他平台，你可能需要去其他处寻找：

- DOS—有一个名为 `DJGCC` (http://www.delorie.com/djgcc/) 的 GCC DOS 移植版可供。由于 GCC 是为 32 位或更宽的系统设计的，该移植版创建的 32 位二进制文件需要 DOS 扩展器（包含在软件包中）才能运行。
- Windows—Cygnus 公司 (http://www.cygnus.com) 已将 GCC 移植到 Windows。该移植版本包含了本书附带光盘中的自解压归档文件。
- OS/2—Eberhart Matthe 将 GCC 移植到 OS/2，并以自己的名字命名该包（EMX）。该 GCC 移植版也可以用于创建 32 位 DOS 可执行文件；对于非 GUI 程序，它们可以在 DOS 和 OS/2 下同时运行。EMX 可以从 http://ftp-os2.msnu.edu/pub/os2/dev_emx/ 以及其他 OS/2 FTP 提示处获取。
- BeOS—Geek Gadgets 项目 (http://www.ninemonths.com/index.html) 为 BeOS 提供了包括 GCC 在内的许多 GNU 组件。BeOS 的 x86 版本包含了 GCC 的二进制版本。（事实上，BeOS 是用 GCC 编译的）。
- GCC 扩展—多年来涌出了各种项目以各种方式扩展 GCC。其中影响最大的是 EGCS，它是 GCC 开发团队的一个分支，用以添加更多新功能。许多 Linux 发行版使用 EGCS 代替 GCC 或额外使用它。另一个流行的 GCC 扩展是 PGCC，它提供了比 GCC 更好的奔腾处理器优化。关于各种 GCC 扩展的信息可以在 http://egcs.cygnus.com/extensions.html 找到。

许多这些 GCC 及相关工具出现在本书附带的光盘上，因此你可以立即使用这些工具。

# GCC 前端

GCC 是一个命令行编译器。也就是说，要编译程序，你使用：

```bash
gcc -o myprog myprog.c
```

此命令将源代码 `myprog.c` 编译为可执行文件 `myprog`。（在 DOS、Windows 和 OS/2 平台上，你可能会调用可执行文件 `myprog.exe`）。共享多个源文件的复杂程序的开发者通常使用 `make` 工具来简化程序构建过程。`make` 使用一个特殊文件（通常称为 `Makefile`）来告诉系统哪些文件需要编译成最终的可执行文件，以及哪些文件依赖于哪些文件。这样，如果你只更改了一个源代码文件，`make` 就能确定哪些文件需要重新编译。下次运行 `make` 时，它会重新编译那些需要重新编译的文件以及你修改的文件。

许多商业开发环境（特别是针对 Windows 的）为这一过程提供了 GUI 前端。该前端通常称为集成开发环境（IDE，注意不要与硬盘类型混淆）接管了 `make` 的功能，并为开发过程提供用户友好的界面。有多种适用于 GCC 的 IDE 可用：图 15.2 显示了来自 CoderCaser 的示例。

# 图 15.2

IDE 提供了面向编程的编辑器、项目文件列表以及其他对专业程序员有帮助的功能。

![](img/a1fdd83cd6e78ae8289e5a9f74e5d320_411_0.png)

编辑器窗口根据编程语言规则提供颜色编码；项目控制提供包含的源文件列表

UNIX 系统有许多可用 IDE。这些 IDE 包括：

- Metroworks CodeWarrior GNU Linux 版 (http://www.metroworks.com/desktop/linux/))—Metroworks 生产自己的 Windows 和 MacOS 编译器，它进入了 Linux 领域。其初始版本是在 GCC 外围封装了 Metroworks 的 IDE。Metroworks CodeWarrior 是商业软件。另一个版本使用了相同的 IDE 连同 Metroworks C 编译器。
- Code Crusader (http://www.planetsoftware.com/jcc/)—这是一个松散基于 CodeWarrior 的类 UNIX OSS 开源 IDE。
- Cygnus Code Fusion (http://www.cygnus.com/codefusion/index.html)—这是另一个围绕 GNU 工具构建的 Linux 商业 IDE。

使用跨平台库
