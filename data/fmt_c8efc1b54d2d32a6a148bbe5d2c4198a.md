
> **重要** 在继续之前，请注意工作平台的名称，通常称为目标三元组（`target triplet`）。确定目标三元组名称的简单方法是运行许多软件包源码随附的 `config.guess` 脚本。解压 Binutils 并运行：`./config.guess`。例如，对于现代 32 位 Intel 处理器，输出将是 `i686-pc-linux-gnu`。

> 同样请注意平台动态链接器的名称，通常称为动态链接器（`dynamic linker`）（不要与作为 Binutils 一的静态链接器 `ld` 混淆）。Glibc 提供的动态链接器加载程序所需的共享库，准备程序运行，然后运行它。32 位 Intel 机器的动态链接器名称将是 `ld-linux.so.2`。确定动态链接器名称的一种万无一失的方法是通过运行命令检查主机系统中的一个随机二进制文件：`readelf -l <name of binary> | grep interpreter` 并注意输出。涵盖所有平台的权威参考位于源码根目录下的 `shlib-versions` 文件中。

第 5 章构建方法工作的一些关键点：

- 通过更改 LFS 目标三元组中的“vendor”字段来微调工作平台的名称。
- 使用此工具链构建其他基本工具。
- 在章中编译的文件将安装在 `$LFS/tools` 目录下，以将它们与下一章安装的文件以及主机生产目录中的文件隔离开。
- 目标 LFS 系统的构建过程。
- 由于在此处编译的软件包是临时的，我们不希望污染即将建立的 LFS 系统。
- 目标 LFS 系统的清洁、无故障构建。

# Linux From Scratch - 版本 7.1

在 Binutils 的第二次模糊测试中，我们能够利用 `--with-lib-path` 参数来控制 `ld` 的库搜索路径。从现在起，核心工具链是自给自足且自托管的。第 5 章的其余软件包都将针对新的 Glibc `/tools` 进行构建。

在第 6 章进入 chroot 环境后，第一个要安装的主要软件包是 Glibc，这是由于上述的自给自足特性。一旦将 Glibc 安装到 `/usr`，我们将对工具链的默认设置进行快速切换，然后继续构建目标 LFS 系统的其余部分。

## 5.3. 通用编译指令

在构建软件包时，存在以下几个假设：

- 某些软件包在编译前进行了补丁，但仅在需要通过补丁规避某个问题时才进行。在本章和下一章中通常需要补丁，但有时在其中某章需要。因此，如果下载的补丁说明缺失，请不要担心。在应用补丁时，可能会遇到关于偏移（offset）或模糊（fuzz）的警告信息。不要担心这些警告，补丁已成功应用。
- 在大多数软件包的编译期间，屏幕上会有几条警告不断滚动。这些是正常的，可以安全地忽略。这些警告正如它们显示所示——是关于 C 或 C++ 语法过时（而非无效）使用的警告。C 标准经常变化，某些软件包仍在使用旧标准。这并不是一个问题，但它会阻止某些功能的实现。
- 检查 LFS 环境变量是否设置正确：

```
echo $LFS
```

确保输出显示了 LFS 分区挂载点的路径，使用我们的示例，该路径为 `/mnt/lfs`。
- 最后，必须强调最后两个重要事项：

> 重要

构建指令假设正在使用 `bash` 壳。

> 重要

再次强调构建过程：

1. 将所有源码和软件包放在从 chroot 环境可以访问的目录中，例如 `/mnt/lfs/sources/`。不要将源码放在 `/mnt/lfs/tools/` 中。
2. 切换源码目录。
3. 对于每个软件包：
   a. 使用 `tar` 程序提取要构建的软件包。在第 5 章中，确保在提取软件包时你是 `lfs` 用户。
   b. 切换到提取软件包时创建的目录。
   c. 按照书籍指令构建软件包。
   d. 返回源码目录。
   e. 除非另有说明，否则删除提取的源码目录以及构建过程中创建的任何 `<package>-build` 目录。

## 5.4. Binutils-2.22 - 第一轮

Binutils 软件包包含一个链接器、一个汇器器以及处理目标文件的其他工具。

预计构建时间：1 SBU

所需磁盘空间：350 MB

### 5.4.1. 安装交叉编译 Binutils

> 注意

回去并重读上一节中的注释。理解标记为“重要（important）”的注释将为你以后避免很多问题。

让 Binutils 成为第一个编译的软件包是非常重要的，因为 Glibc 和 GCC 都会对可用的链接器和汇器器进行各种测试，以决定启用自身的哪些功能。

Binutils 文档建议在源码目录之外的专用构建目录中构建 Binutils：

```
mkdir -v ../binutils-build
cd ../binutils-build
```

> 注意

为了使书中列出的 SBU 值具有参考价值，请测量从配置到包括首次安装在构建该软件包的时间。为了方便实现这一点，可以使用 `time` 命令将这三个命令封装起来，如下：`time { ./configure .. make && make install; }`

现在准备编译 Binutils：

```bash
./binutils-2.22/configure \
  --target=$LFS_TARGET --prefix=/tools \
  --disable-nls --disable-werror
```

`configure` 的含义：

`--target=$LFS_TARGET`

由于 `LFS_TARGET` 变量中的机器描述与 `config-guess` 脚本返回的值略有不同，此开关将告诉 `configure` 脚本调整 Binutils 的构建系统，以构建交叉链接器。

`--prefix=/tools`

这告诉 `configure` 脚本准备将 Binutils 程序安装到 `/tools` 目录中。

`--disable-nls`

这禁用了国际化，因为临时工具不需要 i18n。

`--disable-werror`

这防止在宿主机编译器出现警告时停止构建。

继续编译软件包：

```
make
```

编译现在已完成。通常我们现在会运行测试套件，但在早期阶段，测试套件框架（Tcl、Expect 和 DejaGNU）尚未就绪。在此阶段运行测试的收益微乎其微，因为第一轮产生的程序很快就会被第二轮的程序取代。

如果在 x86_64 上构建，请创建一个符号链接以确保工具链的完整性：

```
case $(uname -m) in
  x86_64) mkdir -v /tools/lib && ln -sv lib /tools/lib64 ;;
esac
```

安装软件包：

```
make install
```

关于该软件包的详情见第 6.13.2 节，“Binutils 的内容”。

## 5.5. GCC-4.6.2 - 第一轮

GCC 软件包包含 GNU 编译器。

预计构建时间：5.0 SBU

所需磁盘空间：1.2 GB

### 5.5.1. 安装核心 GCC

GCC 软件包需要 GMP、MPFR 和 MPC。

> 注意

GCC 文档建议在源码目录之外的专用目录中构建 GCC：

```
mkdir -v ../gcc-build
cd ../gcc-build
```

准备编译 GCC：

```
../gcc-4.6.2/configure \
  --target=$LFS_TARGET --prefix=/tools \
  --disable-nls --disable-werror \
  --disable-shared --disable-multilib \
  --enable-languages=c \
  --without-ppl --without-cloog \
  --with-mpfr=$src/mpfr \
  --with-gmp=$src/gmp \
  --with-mpc=$src/mpc
```

`configure` 参数的含义：

`--target=$LFS_TARGET`

由于 `LFS_TARGET` 变量中的机器描述与 `config-guess` 脚本返回的值略有不同，此开关将告诉 `configure` 脚本调整 GCC 的构建系统以构建交叉链接器。

`--prefix=/tools`

这告诉 `configure` 脚本准备将 GCC 程序安装到 `/tools` 目录。

`--disable-nls`

这禁用了国际化，因为临时工具不需要 i18n。

...（以此此类推）

## 5.6. Linux-3.2.6 API Headers

Linux API 头文件（位于 `linux-3.2.6.tar.xz` 中）暴露内核 API 以供 Glibc 使用。

- **预计编译时间：** 0.1 SBU
- **所需磁盘空间：** 511 MB

### 5.6.1. 安装 Linux API Headers

Linux 内核需要为系统的 C 库（LFS 中为 Glibc）暴露一个应用程序编程接口 (API)。这是通过对 Linux 内核源码 tar 包中提供的各种 C 头文件进行清理来实现的。

确保没有从之前的活动中遗留的过旧文件或依赖项：

```
make mrproper
```

现在，从源码中测试并提取用户可见的内核头文件。它们被放置在一个中间本地目录中，并复制到所需的位置，因为提取过程会删除目标目录中的任何现有文件。

```
make headers_check
make INSTALL HDR=/dest headers_install
cp -rv dest/include/* /tools/include
```

关于此包的详细信息请见第 6.7.2 节，“Linux API 头文件的内容”。

## 5.7. glibc-2.14.1

Glibc 包包含主 C 库。该库提供了分配内存的基础例程。

- **预计编译时间：** 5.5 SBU
- **所需磁盘空间：** 501 MB

### 5.7.1. 安装 Glibc

修复一个导致 Glibc 无法用 GCC-4.6.2 构建的 bug：

```
patch -Npl -i ../glibc-2.14.1-gcc fix-1.patch
```

同时处理一个由于此处构建环境不完整导致头文件检查失败：

```
patch -Npl -i ../glibc-2.14.1-cpuid-1.patch
```

Glibc 文档建议在源码目录之外的专用目录中构建 Glibc：

```
mkdir -v ~/glibc-build
cd ~/glibc-build
```

由于 glibc 支持 i386，其开发者表示在为 x86 机器编译时，应使用编译器标志 `-march=i486`。有几种方法可以实现这一点，但测试表明将该标志放置在构建变量 "CFLAGS" 内部是最好的。与其覆盖 Glibc 内部构建系统使用的 CFLAGS，不如通过使用特殊的 `configparams` 将新标志附加到现有 CFLAGS 内容上。`-mtune=native` 也是必要的，以便为 -mtune 设置一个合理的值，该值在设置 -march 时会发生变化。

```
case $(uname -m) in
  i386) echo CFLAGS+="march=i486 -mtune=native" >> configparams;
esac
```

接下来，为编译准备 Glibc：

```
./glibc-2.14.1/configure --prefix=/tools \
  --host=$LFS_STAG --build=$(../../glibc/scripts/config.guess) \ \
  --disable-profile --enable-add-ons \
  --enable-kernel=2.6.25 --with-headers=/include \
  libc_cv_forced-unwind=yes libc_cv_cleanup=yes
```

`configure` 选项的含义：

```
--host=$LFS_STAG --build=$(../glibc-2.14.1/scripts/config.guess)
```

这些开关的组合效果是 Glibc 的构建系统配置自身进行交叉编译，使用 `/tools` 中的交叉链接器和交叉编译器。

```
--disable-profile
```

这在不包含性能分析信息的情况下构建库。如果需要在临时工具上进行性能分析，请省略过此项。

```
--enable-add-ons
```

这告诉 Glibc 使用 NPTL 作为其线程库。

```
--enable-kernel=2.6.25
```

这告诉 Glibc 使用支持 2.6.25 及更高版本 Linux 内核进行编译库。未启用针对旧内核的变通方案。

```
--with-headers=/tools/include
```

这告诉 Glibc 针对最近安装到 tools 目录的头文件进行编译，这样它就能确切知道内核具有哪些功能并据此进行自我优化。

`libc_cv_forced_unwind=yes`

在第 5.4 节“Binutils-2.22 - Pass 1”中安装的链接器是交叉编译的，因此在 Glibc 安装之前无法使用。这意味着针对 force-unwind 支持的 configure 测试将失败，因为它依赖于一个工作的链接器。传递 `libc_cv_forced_unwind=yes` 变量是为了告知 configure 并在无需运行测试的情况下避免 force-unwind 支持。

`libc_cv_c_cleanup=yes`

同样，我们将 `libc_cv_c_cleanup=yes` 传递给 `configure` 脚本，以便跳过测试并配置 C 清理处理。

在此阶段可能会出现以下警告：

```
configure: WARNING:

*** These auxiliary programs are missing or

*** incompatible versions: msfmt

*** some features will be disabled.

*** Check the INSTALL file for required versions.
```

缺失或不兼容的 `msfmt` 程序通常是无害的。`msfmt` 程序是 Getext 包的一部分，该包带有测试套件，并且可以在主机发行版提供的情况下进行优化。

编译此包：

```
make
```

此包确实包含一个测试套件，但现在无法运行，因为我们还没有 C 编译器。

**注意：** 测试套件还需要安装 locale 数据才能成功运行。

安装此包：

```
make
```

关于此包的详细信息请位于第 6.7 2 节，“Linux API 头文件的内容”。

## 5.8. Adjusting the C

在第 5.4 节“Binutils-2.22 - Pass 1”中安装的链接器是交叉编译的，因此在 Glibc 安装之前无法使用。这意味着针对 force-unwind 支持的 configure 测试将失败，因为它依赖于一个工作的链接器。传递 `libc_cv_forced_unwind=yes` 变量是为了告知 configure 并在无需运行测试的情况下避免 force-unwind 支持。

`libc_cv_c_cleanup=yes`

同样，我们将 `libc_cv_c_cleanup=yes` 传递给 `configure` 脚本，以便跳过测试并配置 C 清理处理。

在此阶段可能会出现以下警告：

```
configure: WARNING:

*** These auxiliary programs are missing or

*** incompatible versions: msfmt

*** some features will be disabled.

*** Check the INSTALL file for required versions.
```

缺失或不兼容的 `msfmt` 程序通常是无害的。`msfmt` 程序是 Getext 包的一部分，该包带有测试套件，并且可以在主机发行版提供的情况下进行优化。

安装此包：

```
make install
```

关于此包的详细信息请位于第 6.7 2 节，“Linux API 头文件的内容”。

关于此包的详细信息请位于第 6.7 2 节，“Linux API 头文件的内容”。

## 5.9. Binutils-2.22 - Pass 2

Binutils 包包含链接器、汇编器和其他处理文件的工具。

- **预计编译时间：** 1.1 SBU
- **所需磁盘空间：** 363 MB

### 5.9.1. 安装 Binutils

再次创建一个独立的构建目录：

```
mkdir -v ..binutils-build
cd ..binutils-build
```

为编译准备 Binutils：

```
CC="$LFS_gcc -B/tools/lib/"
AR="$LFS_gcc-ar" RANLIB="$LFS_gcc-ranlib"
../binutils-2.22/configure --prefix=/tools \
--disable-nls --with-lib-path=/tools/lib
```

新 `configure` 选项的含义：

`CC="$LFS_gcc -B/tools/lib/" AR="$LFS_gcc-ar" RANLIB="$LFS_gcc-ranlib"`

由于这是 Binutils 的原生构建，设置这些变量确保构建系统使用交叉编译器和相关工具，而不是主机上的工具。

`--with-lib-path=/tools/lib`

这告诉 `configure` 脚本在编译 Binutils 时指定库搜索路径，并将 `/tools/lib` 传递给链接器。这防止了链接器搜索主机上的库目录。

编译包：

```
make
```

安装包：

```
make install
```

现在为下一章的“重新调整”阶段准备链接器：

```
make -C bin ld clean
```
