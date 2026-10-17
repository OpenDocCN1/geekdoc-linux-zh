
以下命令将找到 `gcc/config` 中命名为 `linux.h`、`linux.64` 或 `sysv.h` 的所有文件。对于每个文件，我们将其复制到带有后缀 `.orig` 的同名文件中。

```bash
for file in gcc/config/{linux.h,linux.64,sysv.h}; do
  cp -uv $file $file.orig
  sed -e 's|/lib|/tools|' \
      -i.orig $file
  echo
  #undef START_FILE_1
  #undef START_FILE_2
  #define START_FILE_PREFIX "/tools/lib/" >> $file
  touch $file.orig
done
```

`--with-native-system-header-dir=/tools/include`

默认情况下，GCC 在 `/usr/include` 中搜索系统头文件。结合 sysroot 切换，这将映射到 LFS`/usr/include`。然而，在接下来的两个节中安装的头文件将存放在 LFS`/tools/include`。此切换确保了 gcc 能够正确找到它们。在 GCC 的第二次编译中，此切换将确保不会找到任何宿主系统的头文件。

`--disable-shared`

`--disable-threads` `--disable-libatomic`, `--disable-libgomp`, `--disable-libmpx`, `--disable-libquadmath`, `--disable-libssp`, `--disable-libvtv`, `--disable-libstdcxx` `--disable-decimal-float`, `--disable-multilib`

这些切换分别禁用了对十进制扩展、线程、`libatomic`、`libgomp`、`libmpx`、`libquadmath`、`libvtv` 以及 C++ 标准库的支持。在构建交叉编译器时，这些功能将导致编译失败，而且对于交叉编译 libc 的任务来说并不是必需。

`--disable-multilib`

在 x86_64 上，LFS 尚未支持 multilib 配置。此切换对 x86 是无害的。

`--enable-languages=c,c++`

此选项确保只构建 C 和 C++ 编译器。这些是目前需要的唯一语言。

运行以下命令编译 GCC：

```bash
# make
```

编译现在已完成。在此时，通常会运行测试套件，但如前所述，测试套件框架尚未就绪。在此时阶段运行测试的好处微乎其微，因为来自第一轮编译的程序很快就会被替换。

安装软件包：

```bash
# make install
```

关于此软件包的详细信息请参阅第 6.17.2 节，“GCC 的内容”。

## 5.6. Linux-4.9.9 API 头文件

Linux API 头文件（在 `linux-4.9.9.tar.xz` 中）暴露了内核的 API 供 Glibc 使用。

预计编译时间：少于 0.1 SBU

所需的磁盘空间：771 MB

### 5.6.1. 安装 Linux API 头文件

Linux 内核需要为系统的 C 语言库（LFS 中的 Glibc）暴露一个应用程序编程接口 (API)。这是通过对 Linux 内核源码压缩包中提供的各种 C 头文件进行清理来实现的。确保软件包中没有嵌入过期文件：

```bash
make mrproper
```

现在从源码中提取用户可见的内核头文件。它们被放置在一个中间本地目录，并复制到所需的位置。`HDR_PATH=dest` 会移除目标目录中的任何现有文件。

```bash
make INSTALL_HDR_PATH=dest headers_install
cp -rv dest/include/* /tools/include
```

关于此软件包的详细信息请参阅第 6.7.2 节，“Linux API 头文件的内容”。

## 5.7. Glibc-2.25

Glibc 软件包包含了主 C 库。该库提供了内存分配、目录搜索、打开和关闭文件、读和写文件、字符串处理、模式匹配、算术等基本例程。

**预计编译时间：**4.1 SBU

**所需的磁盘空间：**753 MB

### 5.7.1. 安装 Glibc

Glibc 文档建议在专用构建目录中构建 Glibc：

```bash
mkdir -v build
cd build
```

接下来，为编译 Glibc 准备：

```bash
../configure \
  --prefix=/tools \
  --host=$LFS_TGT \
  --build=$(../scripts/config.guess \
  --enable-kernel=2.6.32 \
  --with-headers=/tools/include \
  libc_cv_forced_unwind=yes \
  libc_cv_c_cleanup=yes
```

以下选项的含义如下：

```bash
--prefix=/tools \
--host=$LFS_TGT \
--build=$(../scripts/config.guess \
--enable-kernel=2.6.32 \
--with-headers=/tools/include \
libc_cv_forced_unwind=yes \
libc_cv_c_cleanup=yes
```

这些切换组合的效果是 Glibc 交叉编译，使用我们刚刚构建的交叉编译器而不是 `/usr/bin` 中的。

```bash
host=$LFS_TGT
--build=$(../scripts/config.guess \
--enable-kernel=2.6.32
--with-headers=/tools/include
```

此切换告诉 Glibc 针对 2.6.32 之后的内核进行。

```bash
--enable-kernel=2.6.32
```

此切换告诉 Glibc 在 tools 目录安装后进行编译。

```bash
--with-headers=/tools/include
```

此变量传递给 configure 脚本以告知 force-unwind 支持是有效的。

```bash
libc_cv_forced_unwind=yes
```

同样，我们通过 configure 向已安装的 header 传递 C cleanup 支持。

```bash
libc_cv_c_cleanup=yes
```

在此阶段可能会出现以下警告：

```bash
configure: WARNING:
*** These auxiliary programs are missing or
*** incompatible versions: msgfmt
*** some features will be disabled.
*** Check the host system.
```

`msgfmt` 缺失通常没事。如果发生这种情况，使用 `-j1` 重新运行命令。

编译软件包：

```bash
make
```

安装软件包：

```bash
make install
```

如果输出如上方所示，说明一切正常。调查并回溯找到问题所在并修复它。

关于此软件包的详细信息请参阅第 6.9.3 节，“Glibc 的内容”。

## 5.8. Libstdc++-6.3.0

Libstdc++ 是标准 C++ 库。它是 `g++` 编译器正常运行所需的

预计编译时间：0.4 SBU

所需的磁盘空间：898 MB

### 5.8.1. 安装目标 Libstdc++

Libstdc++ 是 GCC 源码的一部分。你首先应该解压 GCC 压缩包并进入 `gcc-6.3.0` 目录。

为 Libstdc++ 创建并进入独立的构建目录：

```bash
mkdir -v build
cd build
```

为编译 Libstdc++ 准备：

```bash
./libstdc++-v3/configure \
--host=$LFS_TGT \
--prefix=$tools \
--disable-multilib \
--disable-nls \
--disable-libstdccxx-threads \
--disable-libstdccxx-pch \
--with-gxx-include-dir=/tools/$LFS_TGT/include/c++/6.3.0
```

configure 选项的含义：

- `--host=...`指示使用我们刚刚构建的交叉编译器，而不是 `/usr/bin` 中的。

- `--disable-libstdccxx-threads`由于我们尚未构建 C 线程库，C++ 库也无法构建。

- `--disable-libstdccxx-pch`此切换阻止安装预编译包含文件，这些在在此阶段是不需要的。
