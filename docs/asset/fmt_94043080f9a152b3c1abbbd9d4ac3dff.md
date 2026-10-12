
此时，我们关注的是 `libsimple_math.so.1.0`。注意它是如何匹配 `Makefile` 中的 `SOVERSION` 变量的。同样注意我们是如何选择符号链接的。仅仅因为我们选择符号链接的方式，我们实际上让 `mytest` 使用任何未来的 `libsimple_math.so.1.0.7`（其中我们的简单数学库被升级到新版本）。然而，它不会链接到任何类似 `simple_math.so.1.1` 的库。作为 `libsimple_math` 的开发者，我们决定在这个例子中，不同次版本（minor version）的库被认为命名为 `libname.major.minor.patch` 的版本号是不兼容的，而不同级别（level）的库则将不兼容。

我们可以将 `SOVERSION` 改为 `libsimple_math.so.1`。这实际上意味着未来不同级别的库将是兼容。

### 23.3 安装 DLL .so 文件

考虑一个过时或有 Bug 的 DLL：仅用更新后的文件覆盖 DLL 文件将影响所有使用它的应用程序。如果这些应用程序依赖于 DLL 代码的某些行为，那么它们在使用新的 DLL 时可能会崩溃。UNIX 通过允许同时存在多个版本的 DLL 优雅地解决了这个问题。程序本身已经将它们所需的版本号构建在内部。

## 第 24 章 源码与二进制包

### 24.1 构建源码包

遵循标准也意味着软件包可以通过以下命令进行安装：

```
./configure
make
make install
```

这通常意味着软件包可以在任何 UNIX 系统上编译。因此，本节是让 Linux 软件在非 Linux 机器上运行的良好指南。一个示例将说明这些步骤。通过从 `/pub/Linux/apps/X/` 下载 `cooledit`。创建一个 `/opt/src` 目录构建此类包。现在运行

```bash
cd /opt/src
tar -xzvf cooledit-3.17.2.tar.gz
cd cooledit-3.17.2
```

你会注意到大多数源码名为 `包-minor.patch.tar.gz`。主版本在开发者进行重大功能更新或引入不兼容性时更改。次版本在添加小功能时更新。补丁号（也称为补丁级别）在发布新版本时更新，通常表示 Bug 修复。

此时你可以应用任何可能的补丁。参见第 20.7.3。

现在你可以对软件包进行 `./configure`。`./configure` 脚本由 `autoconf` 生成——这是一个开发者用于创建可以在任何类型的 UNIX 系统上编译的 C 源码的包。`autoconf` 软件包包含了所有软件应遵循的 GNU 编码规范。`autoconf` 是 David Mackenzie 的杰作。我经常听到 UNIX 系统已经分化，不再兼容。像 `cooledit`（以及无数其他软件）可以在任何 UNIX 机器上编译这一事实应该消除这种荒谬。简而言之，所有 Linux 软件都运行在所有 UNIX 上。唯一的例外是少数使用 Linux 内核特性的包

```
./configure --prefix=/opt/cooledit
```

在这里，`--prefix` 指向软件包安装的顶层目录（参见第 17.2）。始终尝试

```
./configure --help
```

来查看软件包特定的选项。`LD_LIBRARY_PATH` 告诉链接器去哪里查找库。`ldconfig` 命令更新共享库缓存。这是管理库的一种非常方便的方法。最后，运行你的程序，

```bash
ldconfig
```

`LD_LIBRARY_PATH` 环境变量告诉链接器去哪里查找库。`ldconfig` 命令更新共享库缓存。这是管理库的一种非常方便的方法。最后，运行你的程序，

### 24. 源码包与二进制包

#### 24.1. 编译 GNU 源码包

另一个技巧是设置编译选项：

```bash
CFLAGS='-O2 -fomit-frame-pointer -s -pipe' ./configure --prefix=/opt/cooledit
```

- `-O2` 将编译器优化设置为“尽可能快且不增加二进制文件体积”。（`-O3` 几乎不会提供任何优势。）
- `-fomit-frame-pointer` 允许编译器使用一个通常用于调试的寄存器。只有当你绝对确定对分析该软件包运行过程中的任何问题不感兴趣时，才使用此选项。
- `-s` 剥除目标代码。通过消除调试数据来减小目标代码的。
- `-pipe` 指示不使用临时文件。而是使用管道将代码输送到编译的不同阶段。这通常会加快编译速度。

编译软件包。根据代码量和你的 CPU 性能，这可能需要几个小时。在本文编写时，`cooledit` 在任何入门级机器上仅需 10 分钟即可完成。

```bash
make
```

如果你决定最终仍然倾向于带有调试支持进行编译，也可以运行：

```bash
make CFLAGS='-O0 -g'
```

使用以下命令安装软件包：

```bash
make install
```

安装到不同子目录的一个巧妙技巧并不总是支持的：

```bash
mkdir /tmp/cooledit
make install prefix=/tmp/cooledit
```

你可以使用这些命令将完成的构建包打包，以便解压到不同的系统。但是，你永远不要尝试从与安装前缀不同的目录运行软件包，因为大多数软件包在当前位置编译，然后从该位置访问已安装的数据。

当你希望软件包按照开发者的意图运行时时，使用源码包是最好的方法。当供应商忽略未包含某些文件时，你通常也能找到更多的文档。

### 24.2 RedHat 和 Debian 二进制包

在本节中，我们将 Debian 示例放在括号内，( ... )。由于这些是来自实际系统的示例，它们并不总是对应。

#### 24.2.1 软件包版本控制

RedHat 和 Debian 软件包的编号通常如下（尽管这并非规则）：

```
<package-name>--source-version>-<package-version>.<hardware-platform>.rpm
<package-name>..<source-version>-<package-version>.deb
```

例如，

```bash
bash-1.14.7-22.i386.rpm
( bash-2.03-6.deb )
```

这是你正在使用的 Bourne Shell，主版本 1，次要版本 14，补丁 7，软件包版本 22，为 Intel 386 处理器编译。有时，Debian 会将架构附加到版本号后面，在上面的例子中，可能是 `bash-2.03-6.i386.deb`。

`<source-version>` 是原始 `.tar` 文件上的版本（如上所述）。`<package-version>`（也称为发布版本 `release`）指的是 `.rpm` 文件本身；在此例中，`bash-1.14.7-22.i386.rpm` 已经打包了第 8 次，每个新数字可能对安装方式进行了细微改进。`i386` 被称为架构，也可以是 `sparc`（用于 Sun Microsystems 工作站的 SPARC 类型处理器）、`machine`、`pc`（用于 PowerPC 的其他非 Intel 工作站）、`alpha`（用于 DEC Alpha 高端 64 位服务器/工作站机器）或其他等。

#### 24.2.2 安装、升级和删除

要安装软件包，请对 `.rpm` `.deb` 文件运行以下命令：

```bash
rpm -i mirrordir-0.10.48-1.i386.rpm
( dpkg -i mirrordir_0.10.48-2.deb )
```

升级（如果软件包已存在，Debian 会自动选择升级）可以使用以下命令：

```bash
rpm -U mirrordir_0.10.49-1.i386.rpm
( dpkg -i mirrordir_0.10.49-1.deb )
```

然后使用以下命令完全卸载：

```bash
rpm -e mirrordir
( dpkg --purge mirrordir )
```

在 Debian® 中，移除软件包不会删除配置文件，因此允许你以后稍后决定重新安装时，恢复到其当前的设置：

```bash
rpm -r mirrordir
```

如果你需要重新安装软件包（可能是因为文件损坏），

```bash
rpm -i --force python-1.6-2.i1386.rpm
```
