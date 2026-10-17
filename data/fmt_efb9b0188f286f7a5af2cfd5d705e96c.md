
`grep 'SEARCH.**/usr/lib' dummy.log | sed 's; |\n|'`

包含 `-linux-gnu` 组件的路径引用应该被忽略，否则上一个命令的输出应为：

```
SEARCH_DIR("/usr/x86_64-pc-linux-gnu/lib/lib64")
SEARCH_DIR("/usr/local/lib64")
SEARCH_DIR("/usr/lib64")
SEARCH_DIR("/usr/lib64")
SEARCH_DIR("/usr/x86_64-pc-linux-gnu/lib")
SEARCH_DIR("/usr/local/lib")
SEARCH_DIR("/usr/lib")
SEARCH_DIR("/usr/lib")
```

32 位系统可能会看到一些不同的目录。例如，这里是 i86 机器的输出：

接下来确保我们使用的是正确的库：

```
grep "/lib.**/libc.so.6 " dummy.log
```

上一个命令的输出应该是：

```
attempt to open /lib/libc.so.6 succeeded
```

最后，确保 GCC 使用正确的动态链接器：

```
grep found dummy.log
```

上一个命令的输出应该是（考虑到动态链接器的平台差异）：

```
found ld-linux-x86-64.so.2 at /lib/ld-linux-x86-64.so.2
```

如果输出如所示或完全没有输出，则说明出现了严重错误。请调查并回溯步骤以找出问题所在并进行修正。最可能的原因是规范文件（spec file）调整出现问题。任何问题将在继续后续流程之前得到解决。

如果一切运行正常，清理测试文件：

```
rm -v dummy.c a.out dummy.log
```

最后，移动放置错误的文件：

```
mkdir -pv /usr/share/gdb/auto-load/usr/lib
mv -v /usr/lib/*gdb.py /usr/share/gdb/auto-load/usr/lib
```

## 62.20. GCC 内容

- **已安装程序：** `c++`, `cc` 链接到 `gcc`, `cpp`, `g+`, `gcc`, `gcc-ar`, `gcc-nm`, `gcc-ranlib`, 以及 `gcov`
- **已安装库：** `libasan.{so}`, `libatomic.{so}`, `libgcca.{so}`, `libgcc_eh.a`, `libgcc_s.so`, `libgcov.a,{so}`, `liberty.a`, `libitm.{so}`, `libplto.so`, `libquadmath.{so}`, `libpss.{so}`, `libmsp_nshared`, `libstdc++.{so}`, `libstdcpc++,{so}`, 以及 `libans.{so}`
- **已安装目录：** `/usr/include/c++`, `/usr/lib/gcc`, `/usr/libexec/gcc`, 以及 `/usr/share/gcc-7.3.0`

### 简要描述

- **`c++`** C++ 编译器
- **`cc`** C 编译器
- **`cpp`** 预处理器；它被编译器用于展开源文件中的 `#include`、`#define` 和类似的语句
- **`g++`** C++ 编译器
- **`gcc`** C 编译器。它是 `ar` 的包装器，为命令行添加了插件。该程序仅用于添加“链接时优化”，在默认选项下并不可用
- **`gcc-nm`** `nm` 的包装器，为命令行添加了插件
- **`gcc-ranlib`** `ranlib` 的包装器，为命令行添加了插件。该程序仅用于添加“链接时优化”，在默认选项下并不可用
- **`gcov`** 覆盖率工具；用于分析哪些优化的效果最显著
- **`libasan`** 地址检测器（Address Sanitizer）运行时库
- **`libgcc`** 为 `gcc` 的运行时支持
- **`libgcov`** 当指示 `GCC` 进行性能分析（profiling）时，该库会被链接
- **`libgomp`** 用于 C/C++ 和 Fortran 多处理器编程的 OpenMP 实现
- **`liberty`** 各种程序使用的例，包括 `getopt`, `strerror` 和 `strtol`
- **`libto_plugin`** `GCC` 的链接时优化 (`LTO`) 插件允许允许跨编译单元进行优化
- **`libquadmath`** 精确数学库
- **`libsp`** 支持 `GCC` 栈溢出（stack smashing）功能
- **`libstdc++`** 标准 C++ 库
- **`libsupc++`** 为 C++ 语言的支持
- **`libtsan`** 线程检测器（Thread Sanitizer）库

## 21. Bzip2

Bzip2 包包含压缩和解压缩文件的程序。使用 `bzip2` 压缩文件的压缩率远优于使用“`Lempel-Ziv`”算法的传统压缩器。

**预计构建时间：** `1 SBU`
**所需磁盘空间：** `2 MB`

### 21.1. Bzip2 安装

应用补丁安装此包的文档：

```
patch -Np1 -i ../bzip2-0.6
```

以下命令确保符号链接是相对路径：

```
sed -i 's\(ln -s -f)\$(PREFIX)/bin/@' Makefile
```

确保 man 页安装在正确位置：

```
sed -i "s@(PREFIX)/man@$(PREFIX)/share/man@" Makefile
```

使用以下命令准备 Bzip2：

```
make -f Makefile-libbz2
```

`make` 参数的作用会导致 Bzip2 使用不同的 `Makefile`（此处为 `Makefile-libbz2`），它创建一个动态 `libbz2.so` 库并与之链接 Bzip2 工具。

```
make
```

安装程序：

```
make PREFIX=/usr install
```

将共享 `bzip2` 二进制文件到 `/bin` 目录，创建一些符号链接并清理：

```
cp -vp bzip2-shared /bin/bzip2
cp -av libbz2.so* /lib
ln -sv ../lib/libbz2.so.1 /usr/lib/libbz2.so
rm -v /usr/bin/(bzip2,bzcat,bzip2)
ln -sv bzip2 /bin/bzip2
ln -sv bzip2 /bin/bzcat
```

### 21.2. Bzip2 内容

已安装程序：`bzip2` 链接到 `bzip2`, `bzcat` 链接到 `bzip2`, `bzcmp` 链接到 `bdiff`, `bdiff`, `bzgrep` 链接到 `bgrep`, `bzzf` 链接到 `bgrep`, `bzgrep`, `bzip2`, `bzip2recover`, `bless` 链接到 `bzmore`, 以及 `bmore`

已安装库：`libbz2.[a,so]`

已安装目录：`/usr/share/doc/bzip2-1.0.6`

#### 简要描述

- **`bunzip2`**: 解压缩 bzipped 文件
- **`bzcat`**: 解压缩到标准输出
- **`bzcmp`**: 在 bzipped 文件上运行 `cmp`
- **`bzdiff`**: 在 bzipped 文件上运行 `diff`
- **`bzgrep`**: 在 bzipped 文件上运行 `egrep`
- **`bzfgrep`**: 在 bzipped 文件上运行 `fgrep`
- **`bzzgrep`**: 在 bzipped 文件上运行 `grep`
- **`bzip2`**: 使用带有 Huffman 编码的 Burrows-Wheeler 块文本算法压缩文件；其压缩率优于使用 `gzip` 等更传统的压缩器的“`Lempel-Ziv`”算法
- **`bzip2recover`**: 尝试从损坏的 bzipped 文件中恢复数据
- **`bzless`**: 在 bzipped 文件上运行 `less`
- **`bzmore`**: 在 bzipped 文件上运行 `more`

`libbz2`: 使用 Burrows-Wheeler 算法实现无损块排序数据压缩的库

## 6.22. Pkg-config-0.29.2

`Pkg-config` 包包含一个工具，用于在执行 `configure` 和 `make` 文件向构建工具传递包含路径和/或库路径。

预计构建时间：`0.3 SBU`
所需磁盘空间：`28 MB`

### 6.22.1. Pkg-config 安装

为编译 `Pkg-config` 准备：

```
./configure --prefix=/usr \
--with-internal-glib \
--disable-host-tool \
--dockdir=/usr/share/doc/pkg-config-0.29.2
```
