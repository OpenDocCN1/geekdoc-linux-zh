
Cygwin 支持 SysV IPC 的移植版。

注意：这没有经过广泛测试。特别是 `d_semct1_semun` 是未定义的，因为它未通过 Configure 测试，并且在 Win9x 上 `shm*()` 函数似乎会挂起。它还创建了在未来编译 CPAN 模块时目前不支持！

- `lutil`

标准 Cygwin 发布版包含 `lutil`。

## Cygwin 上 Perl 的配置时选项

`INSTALL` 文档描述了若干配置时选项。其中某些选项可以在 Cygwin 上工作，另一些尚未可行。此外，某些是实验性的。你可以在 `Configure` 提示时选择选项，也可以在命令行上定义（未定义的）符号。

- `Uusedl`
此符号强制静态编译 Perl。
- `Dusemymalloc`
默认不使用源码自带的 `malloc()`，因为它速度较慢且不是线程安全的。如果你想通过 `-Dusemymalloc` 强制 Perl 使用这种方式，请定义此符号。
- `Useperlio`
此符号禁用 PerlIO 抽象。PerlIO 现在是默认值；不建议禁用 PerlIO。
- `Dusemultiplicity`
在 C 程序中嵌入 Perl 并使用多个实例时需要此项。这仅在你使用 `-Uethreads` 构建非线程时需要。
- `Use64bitint`
Perl 默认使用 64 位整数。如果你想使用较小的 32 位整数，使用此符号。
- 
`g`支持长 double（12字节）。然而，在 Perl 中需要若干长双精度函数（`atan2`, `cos`, `exp`, `floor`, `fmod`, `frexp`, `isnan`, `log`, `modf`, `pow`, `sin`, `sqrt()`, `strtol`）。这些在 newlib 即 Cygwin 库中尚未可用。
- `Useithreads`
如果你想要更快的非线程 Perl，定义此符号。
- `Dulargefiles`

Cygwin 使用 64 位整数进行内部尺寸和位置计算，这将由 `Configure` 正确检测并定义。

- `Dymlinks`

使用此在源码树之外构建 perl。详情可以在 `INSTALL` 文档中找到。这是从源码构建的推荐方法。

## Cygwin 可疑警告

在 `Configure` 期间可能会看到看起来可疑的消息。

Win9x 和 `d_eofnblk`

Win9x 在非阻塞读取关闭管道时无法正确报告 EOF。你会看到它返回以下消息：

但它也返回 -1 信号 EOF，请小心！警告：你无法区分 EOF 和无数据！*** 哇！！！***在此机器上 `$d_eofnblk` 的推荐值为 "define"！保留推荐值吗？[y]

至少与 WinNT 保持一致，你应该保留推荐值。

编译器/预处理器定义

由于 Cygwin 对 `_LONG_DOUBLE` 的 `#define`，发生了以下错误：

猜测你的 C 编译器和预处理器定义了哪些符号...`try.c`:
`<line>`: missing binary operator

此失败似乎没有引起任何问题。对于旧版本的 gcc，报告的是“parse error”而不是 "missing binary operator"。

# 编译 CYGWIN

只需运行 `make` 并等待即可：

```bash
make 2>&1 | tee log.make
```

# 在 CYGWIN 上测试

运行测试套件有两个步骤：

```bash
make test 2>&1 | tee log.make-test
cd t; ./perl harness 2>&1 | tee ./log.harness
```

两次运行的都是相同的测试，但通过 `./perl harness` 运行时会提供更多信息。

测试结果取决于你的宿主机系统和你的 Cygwin 配置。在某些 Cygwin 设置下测试可能会通过，但始终会尝试进行测试，并记录了可以解释的测试失败。Perl 可能会通过所有测试，但更有可能的是某些测试会由于下面列出的原因之一而失败。

## Cygwin 上的文件权限

UNIX 文件权限基于针对每个{用户、组、其他}的每个{读、写、执行}的模式位集。默认情况下，Cygwin 跟踪 Win32 的只读属性，该属性被表示为 UNIX 文件写位（文件始终是可读的，如果文件具有 `{.com,.bat}` 扩展名或带有 #1 则为可执行的；目录始终是可读和可执行的）。在带有 `nsec cygwin` 设置的 WinNT 上，额外的模式位是扩展文件属性。在带有默认 `nsec cygwin` 设置的 WinNT 上，权限使用标准的 WinNT 安全描述符和访问控制列表。如果没有这些选项之一，测试将失败（尚未更新）：

| 失败测试列表（失败的用例） | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| io/fs | 5,9-10 | | | | | |
| lib/anydbm.t | 2 | lib/db-btree.t | 20 | | | |
| lib/db-hash.t | 16 | lib/db-recno.t | 18 | | | |
| lib/dbdbm.t | 2 | lib/ndbm.t | 2 | lib/odbm.t | 2 | |
| lib/sdbm.t | 2 | op/stat.t | 9,20 | | | |
| (.tmp 不是执行扩展名) | | | | | | |

## NDBM_File 和 ODBC_File 在 FAT 系统上无效

不要在 FAT 文件系统上使用 `NDBM_File` 或 `ODBC_File`。它们可以在 FAT 上构建，但许多测试将失败：

| | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| ../ext/NDBM_File.t | 13 | 3328 | 59 | 83.106 | 1-2 4 16-71 | | |
| ../ext/ODBC_File/odbm.t | 255 | 65280 | ?? | % | % | % | |
| ../lib/AnyDBM/File.t | 252 | 512 | 26.16% | 1 | 4 | | |
| ...lib/Memo/t/errors.t | 0 | 139 | 15 | 54.45 | 7-11 | | |
| ../lib/Memo/t-ndbm.t | 13 | 3328 | 4 | 100.00 | 1-4 | | |
| run/fresh/perl.t | 97 | 1 | 1.03% | 91 | | | |

如果你尝试在 FAT 上运行（或在 FAT 上使用 `AnyDBM_File`），请运行 `Configure` 并带有 `-Ui_ndbm` 和 `-Ui_db` 选项，以防止构建 `NDBM_File` 和 `ODBC_File`。

使用 NTFS (`Cygwin=ntfsec`)，即使 perl 是在 FAT 上构建的，应该也没有问题。

## io_* 中的 fork() 失败

`fork()` 失败可能导致以下测试失败：

```
ext/IO/lib/IO/t/io_multihomed.t
ext/IO/lib/IO/t/io_sock.t
ext/IO/lib/IO/t/io_unix.t
```

参见下文“杂杂”中关于 fork 的注释。

# CYGWIN 移植的特定特性

## Cygwin 上的脚本移植性

Cygwin 在 Win32 系统上层提供类 UNIX 语义方面做得非常出色。然而，除了上述项目外，还有一些你应该了解的差异。这是一份关于移植性的简短指南，更多信息可以在 Cygwin 文档中找到。

### 路径名

Cygwin 路径名用斜杠 (`/`) 分隔，支持通用命名代码 (`/UNC`)。不建议使用 Cygwin-1.7 非 POSIX 路径。名称可以包含所有打印字符。

文件名不区分大小写，但保留大小写。包含反斜杠或驱动器字母的路径是 Win32 路径，不受 posix 风格路径的翻译影响，Cygwin 将占上风，因此最好将它们转换为 POSIX。

为了转换，我们有 `Cygwin::win_to_posix_path()` 和 `Cygwin::posix_to_win_path()`。

由于 cywin-1.7 路径名是 UTF-8 编码的。

### 文本/二进制

Cygwin-1.7 的文本模式已弃用并强烈不建议使用。

当文件被打开时，它处于文本模式或二进制模式。在文本模式下，文件会受到 CR/LF/Ctrl-Z 翻译。在 Cygwin 中， `open()` 的默认模式由底层文件的挂载模式决定。参见：

> "`Cygwin::is_binary()` 是一个函数，用于对将被视为文本的文件设置二进制模式。带有 `O_TEXT` 标志的 `sysopen()` 会对原本会被视为二进制的文件设置模式："

```perl
sysopen(FH, "bar", O_WRONLY|O_CREATE|O_TEXT)
```
