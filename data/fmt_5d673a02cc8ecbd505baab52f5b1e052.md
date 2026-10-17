
本节解释了整体构建方法背后的某些原理和技术细节。不需要立即理解本节中的所有内容。在执行实际构建后，大部分信息将变得更加清晰。在过程中可以随时参考本节。

第 5 章的总体目标是产生一个临时区域，其中包含一组已良好的工具，这些工具可以与宿主系统隔离开。通过使用 `chroot`，后续章节中的命令将包含在该环境中，确保 LFS 系统进行清洁、无故障的构建。构建过程的设计旨在最大限度地减少新读者的风险，同时提供最大的教育价值。

> 注意
>
> 在继续之前，请注意工作平台的性质，通常称为目标三元组（target triplet）。确定目标三元组名称的简单方法是运行许多包源码附带的 `config.guess` 脚本。解压 Binutils 源码并运行脚本：`./config.guess` 并注意输出。例如，对于 32 位 Intel 处理器，输出为 `x86-pc-linux-gnu`。对于 64 位 Intel 处理器，输出为 `x86_64-pc-linux-gnu`。

# Linux From Scratch - 版本 8.0

在第6章进入 `chroot` 环境后，第一个要安装的主要软件包是 Glibc，这是由于上述提到的它具有足够的默认设置。一旦 Glibc 安装到 `/usr`，我们将对工具链进行快速切换，然后继续构建目标 LFS 系统的其余部分。

## 5.3. 通用编译说明

在构建软件包时，说明中包含了几个假设：

- 有几个软件包使用了补丁后编译，但仅在需要通过补丁来规避问题时才这样做。在本章和下一章中都需要补丁，但有时只在其中一个章节中需要。因此，如果下载的补丁说明似乎缺失，请不要担心。应用补丁时也可能会遇到关于偏移（offset）或模糊（fuzz）的警告信息。不要担心这些警告，因为补丁已成功应用。
- 在大多数软件包的编译过程中，会有几个警告在屏幕滚动。这是正常现象，可以安全地忽略。这些警告正如它们出现时的那样——关于对 C 或 C++ 标准的过时但并非无效使用的警告。C 语言的变化频繁，某些软件包仍然在使用旧标准。这并不是问题，但会引起警告的产生。
- 最后检查一次 LFS 环境变量是否正确设置：

```
echo $LFS
```

确保输出显示了 LFS 分区挂载点的路径，在我们的示例中应为 `/mnt/lfs`。
- 最后，必须强调最后两个重要事项：

> **重要**
>
> 构建说明假设宿主机系统要求（包括符号链接）已正确设置：
>
> - `bash` 是正在使用的 shell。
> - `sh` 是指向 `bash` 的符号链接。
> - `/usr/bin/awk` 是指向 `gawk` 的符号链接。
> - `/usr/bin/yacc` 是指向 `bison` 的符号链接，或执行 `bison` 的小型脚本。

> **重要**
>
> 为了强调构建过程：
>
> 1. 将所有源代码和软件包放置在 `chroot` 环境可以访问的目录中，例如 `/mnt/lfs/sources/`。不要将源代码放在 `/mnt/lfs/tools/` 中。
> 2. 切换到源代码目录。
> 3. 对于每个软件包：
>   a. 使用 `tar` 程序解压要构建的软件包。在第 5 章中，确保在解压软件包时你是 LFS 用户。
>   b. 切换到解压软件包时创建目录。
>   c. 按照书籍说明构建软件包。
>   d. 除非另有说明，否则删除解压后的源代码目录。

## 5.4. Binutils-2.27 - 第一阶段

`Binutils` 软件包包含一个链接器、一个汇器以及处理目标文件的其他工具。

近似编译时间：1 SBU

所需的磁盘空间：519 MB

### 5.4.1. 安装 Binutils

> 注意：返回并重新阅读上一节中的注释。理解标记为“重要”的注释将帮助你以后避免很多问题。

让 `Binutils` 第一个编译的软件包是非常关重要的，因为 `Glibc` 和 `GCC` 都会对可用的链接器和汇器进行各种测试，以确定启用它们自己的功能。

`Binutils` 文档建议在专用构建目录中构建 `Binutils`：

```
mkdir -v build
cd     build
```

> 注意：为了使书中其他部分使用的 SBU 值具有意义，请测量从配置到首次安装（包含首次安装）构建此软件包所需的时间。为了实现这一点，请将命令封装在 `time` 命令中，如下：`time ( ./configure ... && make install; )`。

> 注意：第 5 章中的近似编译 SBU 值和所需的磁盘空间不包含测试套件数据。

现在准备编译 `Binutils`：

```bash
../configure --prefix=/tools \
      --with-sysroot=$LFS             \
      --with-lib-path=/tools/lib     \
      --target=$LFS_TGT               \
      --disable-nls                   \
      --disable-error
```

配置选项的含义：

`--prefix=/tools`

这告诉 `configure` 脚本在 `/tools` 目录中准备 `Binutils` 程序。

`--with-sysroot=$LFS`

对于交叉编译，这告诉构建系统根据需要从 `$LFS` 查找目标系统库。

`--with-lib-path=/tools/lib`

这指定了链接器应该配置为使用的库路径。

`--LFS_TGT`

由于 `LFS_TGT` 变量中的机器描述与 `config.guess` 脚本返回的值略有不同，此开关将告诉 `configure` 脚本调整 `Binutil` 的构建系统以构建交叉链接器。

`--disable-nls`

这禁用了国际化，因为临时工具不需要 i18n。

继续编译软件包：

```bash
make
```

编译现在已完成。通常情况下我们现在会运行测试套件，但在这个早期阶段，测试套件框架（Tcl、Expect 和 DejaGNU）尚未就绪。在此阶段运行测试的益处微乎其微，因为来自第一阶段的程序很快就会被第二阶段的程序所取代。

如果在 `x86_64` 上构建，请创建一个符号链接以确保工具链的健全性（sanity de-check）：

```bash
case $(uname -m) in
x86_64) mkdir -v /tools/lib ln -sv lib /tools/lib64 ;;
esac
```

安装软件包：

```bash
make install
```

关于此软件包的详情位于第 6.13.2 节。

## 5.5. GCC-6.3.0 - 第一阶段

`GCC` 软件包包含 C 和 C++ 编译器以及其他工具。

近似编译时间：8 SBU

所需的磁盘空间：5 GB

### 5.5.1. 安装交叉 GCC

`GCC` 需要 `GMP`、`MPFR` 和 `MPC`。在构建交叉编译器时，这些软件包必须可用。

`GCC` 文档建议在专用构建目录中构建 `GCC`：

```
mkdir -v build
cd     build
```

准备编译 `GCC`：

```bash
../configure
--target=$LFS_TGT
--prefix=/tools
--with-glibc-version=2.11
--with-sysroot=$LFS
--with-newlib
--without-headers
--with-local-prefix=/tools/include
--with-native-system-header-dir=/nls
--disable-shared
--disable-multilib
--disable-decimal-float
--disable-threads
--disable-libatomic
--disable-libgomp
--disable-libmpx
--disable-libquadmath
--disable-libsssp
--disable-libvtv
--disable-libstdcxx
--enable-languages=c,c++
```

配置选项的含义：

`--with-newlib`

由于尚无工作的 C 库，这确保在构建 `libc` 时定义 `inhibit_lib_constant`。这防止了需要库支持的代码的编译。

`--without-headers`

在创建完整的交叉编译器时，`GCC` 需要与目标系统兼容的标准头文件。对于我们的目的不需要这些头文件。此开关防止 `GCC` 查找它们。

`--with-local-prefix=/tools`

本地前缀是 `GCC` 搜索本地安装文件的位置。默认是 `usr/local`。将其设置为 `/tools` 有助于防止主机的 `/usr/local` 进入此 `GCC` 的搜索路径。

最后，在 `x86_64` 宿主机上，64 位库的默认名称为“lib”：

```bash
case $(uname -m) in
  x86_64)
    sed -e '/m64=/s/lib64/lib/' \
      -i.orig gcc/i86-t-linux
esac
```
