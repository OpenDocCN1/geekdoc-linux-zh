
`configure` 选项的含义：

`--prefix=/tools`
这告诉配置脚本将 Binutils 程序准备在 `/tools` 目录。

`--with-sysroot=$LFS`
对于交叉编译，这告诉构建系统在需要时从 LFS 查找目标系统库。

`--with-lib-path=/tools/lib`
指定链接器配置使用的库路径。

# 从零开始构建 Linux - 版本 8

`--target=$LFS_TGT`

由于 `LFS_TGT` 变量中的机器描述与 `config.guess` 脚本返回的值略有不同，此开关将告诉 `configure` 脚本调整 Binutils 的构建系统，以构建交叉链接器。

`--disable-nls`

这将禁用国际化，因为临时工具不需要 i18n。

`--disable-werror`

这可以防止在宿主机编译器出现警告时停止构建。

继续编译软件包：

```bash
# make
```

编译现在已完成。通常情况下，我们现在会运行测试套件，但在此早期阶段，测试框架（Tcl、Expect 和 DejaGNU）尚未就绪。在此时阶段运行测试的益处微乎其微，因为第一遍编译的程序很快就会被第二遍编译的程序所取代。

如果在 x86_64 上构建，请创建一个符号链接以确保工具链的完整性：

```
case $(uname -m) in
x86_64) mkdir -v /tools/lib && ln -sv lib /tools/lib64 ;;
esac
```

安装软件包：

```bash
# make install
```

此软件包的详情见第 6.16.2 节，“Binutils 的内容”。

## 5.5. GCC-7.3.0 - 第一阶段

`GCC` 软件包包含 GNU 编译器集合，包括 C 和 C++ 编译器。
估计构建时间：8.8 SBU
所需磁盘空间：2.2 GB

### 5.5.1. 交叉 GCC 的安装

`GCC` 现在需要 `GMP`、`MPFR` 和 `MPC` 软件包。由于这些包可能未包含在宿主机发行版中，它们将与 `GCC` 一起构建。将每个包解压到 `GCC` 源码目录并重命名生成的目录，以便 `GCC` 构建时自动使用它们：

> 人们对本章存在常见的误解。操作与稍后解释的所有其他章节相同（软件包构建说明）。首先从源码目录提取 `gcc` tar 包，然后进入新创建的目录。只有在此之后，再按照说明进行操作。

```bash
tar - xf ../mpfr-4.0.1.tar.xz
mv -v mpfr-4.0.1 mpfr
tar -xf ../gmp-6.1.2.tar.xz
mv -v gmp-6.1.2 gmp
tar -xf ../mpc-1.1.0.tar.xz
mv -v mpc-1.1.0 mpc
```

以下命令将更改 `GCC` 默认动态链接器的位置，以使用安装在 `/tools` 中的链接器。它从 `GCC` 的搜索路径中移除了 `/usr/include`。执行：

```bash
for file in gcc/config/{linux,i386/linux,{64}}.h
do
  cp -uv $file,{.}
  sed -e 's@/lib/(64)\/\@ld@/tools&@'
      -e 's@/usr@/tools@' $file.orig > $file
echo ""
#undef STANDARD_STARTFILE_PREFIX_1
#undef STANDARD_STARTFILE_PREFIX_2
#define STANDARD_STARTFILE_PREFIX_1 "/tools/lib/"
#define STANDARD_STARTFILE_PREFIX_2 "/tools/lib/" >> $file
touch $file.orig
done
```

上面的内容似乎难以理解，让我们稍微拆解一下。首先，我们将 `gcc/config/linux.h` 和 `gcc/config/i386/linux64.h` 复制到同名但带有 "orig" 后缀的文件中。第一个 `sed` 替换了 "tools/lib","lib64/lib" 或 "lib32/lib"，而第二个 `sed` 则替换了硬编码的 "usr"。接下来，我们在文件末尾添加了定义语句，以更改默认的定义前缀。注意 "tools/lib/" 尾尾的 "/" 是必须的。配合 `cp -u` 使用时，这可以防止在无意中运行命令时原始文件发生意外更改。

最后，在 x86_64 宿主机上，将 64 位库的默认目录名为 "lib"：

```bash
case $(uname -m) in
x86_64)
sed -e '/m64=/s/lib64/lib/lib/' \
  -i.orig gcc/config/i386/t-linux64
esac
```

`GCC` 文档建议在专用的构建目录中构建 `GCC`：

```bash
mkdir -v build
cd build
```

准备 `GCC` 编译：

```bash
./configure \
--target=$LFS_TGT \
--prefix=/tools \
--with-glibc-version=2.11 \
--with-sysroot=$LFS \
--with-newlib \
--without-headers \
--with-local-prefix=/tools/include \
--with-native-system-header-dir=nls \
--disable-shared \
--disable-multilib \
--disable-decimal-float \
--disable-threads \
--disable-libatomic \
--disable-libgomp \
--disable-libmpx \
--disable-libquadmath \
--disable-libsssp \
--disable-libvtv \
--disable-libstdcxx \
--enable-languages=c,c++
```

以下选项的含义：

- `--with-newlib`: 由于还没有可用的 C 库，此选项确保在构建 `libgcc` 时定义了 `inhibit_lib_constant`。这防止了任何需要 lib 支持的代码编译。
- `--without-headers`: 在创建完整的交叉编译器时，`GCC` 需要与目标系统兼容的标准头。对于我们的目的，不需要头文件。此选项防止 `GCC` 查找查找它们。
- `--with-local-prefix=/tools`: 本地前缀是 `GCC` 搜索本地安装文件的系统位置。默认值是 `/usr/local`。将其设置为 `/tools` 有助于将宿主机的 `/usr/local` 排除在 `GCC` 的搜索路径之外。
- `--with-native-system-header-dir=/tools/include`: 默认，`GCC` 在 `/usr/include` 中搜索系统头文件。结合 `sysroot`（通常会映射到 `LFS/usr/include`），在后续章节中安装的头文件将进入 `LFS/tools`。此开关确保 `gcc` 能够正确找到它们。在 `GCC` 的第二遍编译中，此开关将确保不会找到宿主机系统的头文件。
- `--disable-shared`: 此开关强制 `GCC` 静态链接其内部库。我们这样做是为了避免与宿主机系统可能出现的问题。
- `--disable-decimal-float` `--disable-threads`, `--disable-libatomic`, `--disable-libgomp`, `--disable-libmpx`, `--disable-libquadmath`, `--disable-libsssp`, `--disable-libvtv`, `--disable-libstdcxx`: 这些开关分别禁用对小数扩展、线程、`libatomic`、`libomp`、`mpx`、`quadmath`、`vtv` 以及 C++ 标准库的支持。这些功能在构建交叉编译器时会失败，且对于交叉编译 `libc` 的任务来说是不必要的。
- `--disable-multilib`: 在 x86_64 上，LFS 尚不支持 `multilib`。此开关是无害的。
- `--enable-languages=c,c++`: 此选项仅启用 C 和 C++ 语言。

以下命令将继续编译软件包：

```bash
# make
```

编译现在已完成。通常情况下，我们现在会运行测试套件，但在此早期阶段，测试框架（Tcl、Expect 和 DejaGNU）尚未就绪。在此时阶段运行测试的益处微乎其微，因为第一遍编译的程序很快就会被第二遍编译的程序所取代。

如果在 x86_64 上构建，请创建一个符号链接以确保工具链的完整性：

```
case $(uname -m) in
x86_64) mkdir -v /tools/lib && ln -sv lib /tools/lib64 ;;
esac
```

安装软件包：

```bash
# make install
```
