
进入`/usr/include`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

- `--with-tclinclude=/usr/include`：这显式告诉 Expect 去哪里寻找 Tcl 的头文件。

构建软件包：

```bash
make
```

要测试结果，执行：

```bash
make test
```

安装软件包：

```bash
make install
ln -svf expect5.45.4/libexpect5.45.4.so /usr/lib
```

### 8.17.2. DejaGNU 的内容

- 安装的程序：`expect`

- 安装的库：`libexpect-5.45.so`

#### 简描述（此处无具体描述）

## 8.18. Binutils-2.37

`Binutils`包包含链接器、汇编器和其他工具。

预计编译时间：6.3 SBU

所需磁盘空间：4.5 MB

### 8.18.1. 安装 Binutils

为编译准备 Binutils：

```bash
SRCDIR=$(pwd)
cd unix
./configure --prefix=/usr \
--mandir=/usr/share/man \
$ [ "$(uname -m)" = x86_64 ] && echo --enable-64bit
```

`configure`选项的含义：

```
$ [ "$(uname -m)" = x86_64 ] && echo --enable-64bit
```

构造部分（`<shell command>`）被 shell 命令的输出所替换。如果在 32 位机器上运行，该输出为空；如果在 64 位机器上运行，则输出为 `--enable-64bit`。

构建软件包：

```bash
make
```

```bash
sed -e "s|$$SRCDIR/unix/usr/lib|" \
-e "s|$$SRCDIR/unix/usr/include|" \
-i tclConfig.sh
```

```bash
sed -e "s|$$SRCDIR/unix/pkgs/tdbcl.1.2/|/usr/lib/tdbcl.1.2/" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/generic/|/usr/include|" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/library/|/usr/lib/tcl8.6|" \
-e "s|$$SRCDIR/pkgs/tdbcl.1.2/|/usr/include|" \
-i pkgs/tdbcl.1.2/tdbConfig.sh
```

```bash
sed -e "s|$$SRCDIR/unix/pk/itcl4.2.1/|/usr/lib/itcl4.2.1/" \
-e "s|$$SRCDIR/pkgs/itcl4.2.1/generic/|/usr/include|" \
-e "s|$$SRCDIR/pkgs/itcl4.2.1/|/usr/include|" \
-i pkgs/itcl4.2.1/itclConfig.sh
```

```bash
unset SRCDIR
```

- **`tclsh8.6`**：Tcl 命令 shell

- **`tclsh`**：指向 `tclsh8.6`

- **`libtcl8.6.so`**：Tcl 库

- **`libtclstub8.6.a`**：Tcl Stub 库

### 8.18.2. Binutils 的内容

- 安装的程序：`expect`

- 安装的库：`libexpect-5.45.so`

# Linux From Scratch - 版本 11

- `ar`: 创建、修改、从归档中提取

- `as`: 汇编器，将 gcc 的输出汇编为对象文件

- `c++filt`: 链接器用于去符号 C++ 和 Java 符号，并防止重载函数冲突

- `dwp`: DWARF 封装工具

- `elfedit`: 更新 ELF 文件的 ELF 头部

- `gprof`: 显示调用分析数据

- `ld`: 链接器，将多个对象文件和归档文件合并为一个文件，重定位其数据并绑定符号引用

- `ld.gold`: `ld`的精简版本，仅支持 elf 文件格式

- `ld.bfd`: `ld`的硬链接

- `nm`: 列出给定对象文件中出现的符号

- `objcopy`: 将其中一种对象文件转换为另一种对象文件，可以通过选项控制特定的显示信息；其显示的信息对正在开发编译工具的程序员有用

- `objdump`: 显示给定对象文件的信息，可以通过选项控制特定的显示信息；其显示的信息对正在开发编译工具的程序员有用

- `ranlib`: 生成归档内容的索引并将其存储在归档中；该索引列出了所有由归档成员（可重定位对象文件）定义的符号

- `readelf`: 显示 ELF 类型二进制文件的信息

- `size`: 列出给定对象文件的段大小和总大小

- `strings`: 输出每个给定文件中长度至少为指定长度的可打印字符序列（默认为四）；对于对象文件，默认只打印初始化和加载部分的字符串，而对于其他类型的文件，它会扫描整个文件

- `strip`: 丢弃对象文件中的符号

- `libbfd`: 二进制文件描述符库

- `libctf`: 兼容 ANSI-C 类型格式调试支持库

- `libctf-nobfd`: `libctf`的变体，不使用 `libbfd`功能

- `libopcodes`: 用于处理操作码的库——即处理器指令的“可读文本”；用于构建如 `objdump`等工具

## 8.19. GMP-6.2.1

`GMP`软件包包含数学库。这些用于任意精度算术的函数非常用用。

预估的编译时间：1.0 SBU

所需的磁盘空间：52 MB

### 8.19.1. 安装 GMP

> 注意

如果你正在为 32 位 x86 编译，但你的 CPU 能够运行 64 位代码且你在环境变量中指定了 `CFLAGS`，则配置脚本将尝试配置为 64 位并失败。通过调用下面的配置 命令可以避免这种情况：

```
ABI=32 ./configure .
```

> 注意

`GMP`的默认设置会产生针对主机处理器优化的库。如果需要处理能力低于主机 CPU 的适用于处理器的库，可以通过运行以下命令创建通用库：

```
cp -v config.sub.guess config.guess
cp -v config.sub.sub config.sub
```

为编译准备 `GMP`：

```bash
./configure --prefix=/usr \
  --enable-cxx \
  --disable-static \
  --docdir=/usr/share/doc/gmp-6.2.1
```

新配置 选项的含义：

- `--enable-cxx`: 此参数启用 C++ 支持

- `--docdir=/usr/share/doc/gmp-6.2.1`: 此变量指定文档的正确位置。

编译软件包并生成 HTML 文档：

```
make
make html
```

> 重要

本节中的 `GMP` 测试套件被认为是关键的。在任何情况下都不要跳过。

测试结果：

```
make check 2>&1 | tee gmp-check-log
```

# Linux From Scratch - 版本 11.0

> `gmp` 中的代码针对其构建时所在的处理器进行了高度优化。偶尔，检测处理器的代码会误判系统能力，导致测试或其他使用 `gmp` 库的应用程序中出现带有““Illegal instruction”（非法指令）消息的错误。在这种情况下，应使用 `--build=x86_64-pc-linux-gnu` 选项重新配置 `gmp` 并重建。

确保测试套件中的所有 197 个测试均通过。通过执行以下命令检查结果：

```
awk '/# PASS:/{total=$3} ; END(print total)' gmp-check-log
```

安装软件包及其文档：

```
make install
make install-html
```

### 8.19.2. GMP 的内容

- 安装的库：`libgmp.so` 和 `libgmpxx.so`

安装目录：`/usr/share/doc/gmp-6.2.1`

#### 简述

- `libgmp` 包含精度数学函数

- `libgmpxx`：包含 C++ 精度数学函数

## 8.20. MPFR-4.1.0

`MPFR`软件包包含多精度数学的函数。

预估的编译时间：0.8 SBU

所需的磁盘空间：38 MB

### 8.20.1. 安装 MPFR

为编译准备 `MPFR`：

```bash
./configure --prefix=/usr \
    --disable-static \
    --enable-thread-safe \
    --docdir=/usr/share/doc/mpfr-4.1.0
```

编译软件包并生成 HTML 文档：

```
make
make html
```

> **重要**

本节中的 `MPFR` 测试套件被认为是关键的。在任何情况下都不要跳过。

测试结果：

```
make check
```

安装软件包及其文档：

```
make install
make install-html
```

### 8.20.2. MPFR 的内容

- 安装的库：`libmpfr.so`

安装目录：`/usr/share/doc/mpfr-4.1.0`

#### 简述

- `libmpfr` 包含多精度数学

## 8.21. MPC-1.2.1

`MPC`软件包包含任意精度复数的库。

预估的编译时间：0.3 SBU

所需的磁盘空间：21 MB

### 8.21.1. 安装 MPC

为编译准备 `MPC`：

```bash
./configure --prefix=/usr \
    --disable-static \
    --sysconfdir=/etc \
    --docdir=/usr/share/doc/mpc-1.2.1
```

编译软件包并生成 HTML 文档：

```
make
make html
```

测试结果：

```
make check
```

安装软件包及其文档：

```
make install
install-html
```

### 8.21.2. MPC 的内容

- 安装的库：`libmpc.so`

安装目录：`/usr/share/doc/mpc-1.2.1`

#### 简述

- `libmpc` 包含精度函数

## 8.22. Attr-2.5.1

`attr`软件包包含管理文件系统扩展属性的工具。

预估的编译时间：0.1 SBU

所需的磁盘空间：4 MB

### 8.22.1. 安装 Attr

为编译准备 `Attr`：

```bash
./configure --prefix=/usr \
    --disable-static \
    --sysconfdir=/etc \
    --docdir=/usr/share/doc/attr-2.5.1
```

编译软件包并生成 HTML 文档：

```
make
make html
```

测试结果：

```
make check
```

安装软件包及其文档：

### 8.22.2. Attr 的内容

- 安装的程序：`attr`, `getattr` 和 `setattr`

- 安装的库：`libattr.so`

安装目录：`/usr/share/doc/attr-2.5.1`

#### 简述

- `attr`：扩展文件系统的扩展属性

- `getattr`：获取文件系统的扩展属性

- `setattr`：设置文件系统的扩展属性

- `libattr` 包含处理扩展属性的库

## 8.23. Acl-2.3.1

`acl`软件包包含管理访问控制列表（ACL）的工具，这些列表用于为文件和目录定义更细粒度的权限。

预估的编译时间：0.1 SBU

所需的磁盘空间：6 MB

### 8.23.1. 安装 Acl

为编译准备 `Acl`：

```bash
./configure --prefix=/usr \
  --disable-static \
  --docdir=/usr/share/doc/acl-2.3.1
```

编译软件包并生成 HTML 文档：

```
make
make html
```

测试结果：

```
make check
```

安装软件包及其文档：

```
make install
```

### 8.23.2. Acl 的内容

- 安装的程序：`chacl`, `getfacl`, `setfacl`

- 安装的库：`libacl.so`

安装目录：`/usr/share/doc/acl-2.3.1`

#### 简述

- `chacl`：更改文件或目录的访问控制列表

- `getfacl`：获取文件访问控制列表

- `setfacl`：设置文件访问控制列表

- `libacl` 包含处理访问控制列表的库

## 2.24. Libcap-2.53

`Libcap`包实现了 Linux 内核中可用的 POSIX 1003.1le 能力（capabilities）的用户空间接口。这些能力将所有强大的 root 权限划分为一组不同的权限。

**预计编译时间：** 耗于 0.1 SBU

**所需磁盘空间：** 3.2 MB

### 2.24.1. 安装 Libcap

防止安装静态库：

```bash
sed -i '/install -m.**STA/d' libcap/Makefile
```

编译该包：

```bash
make prefix=/usr lib=lib
```

`make`选项的含义：

`lib=lib`

此参数将库目录设置为 `/usr/lib`，而不是 x86_64 架构上的 `/usr/lib64`。它对 x86 没有任何影响。

要测试结果，请执行：

```bash
make test
```

安装该包：

```bash
make prefix=/usr lib=lib install
```

调整共享库的权限：

```bash
chmod -v 755 /usr/lib/lib(cap,psx).so.2.53
```

### 2.24.2. Libcap 内容

**安装的程序：** `capsh`, `getcap`, `getpcaps` 和 `setcap`

**安装的库：** `libcap.so` 和 `libpssx`

**短期说明**

- `capsh`: 用于探索和限制能力支持的封装

- `getcap`: 检查文件能力

- `getpcaps`: 显示查询进程（进程）上的能力

- `setcap`: 设置文件能力

- `libcap`: 包含操作 POSIX 1003.1le 能力的库函数

- `libpssx`: 包含支持 pthread 库相关的系统调用 POSIX 语义的函数

## 8.25. Shadow-4.9

`Shadow`包包含了以安全方式处理密码的程序。

预计编译时间：0.2 SBU。所需磁盘空间：45 MB。

### 8.25.1. 安装 Shadow

> 注意：如果你想强制使用强密码，请参考 https://www.linuxfromscratch.org/blfs/view/11.0/postifs/cracklib.html 在构建 Shadow 之前安装 CrackLib。然后在配置命令中添加 `--with-libcrack`。

禁用 `groups`程序及其页面，因为 Coreutils 提供了更好的替代方案。同时防止安装位于 8.3 节“Man-pages-5.13”中的手册。

```bash
sed -i '/s/groups$ (EXEEXT) //' src/Makefile.in
find man -name Makefile.in -exec sed -i '/s/groups\.1 / /' {} \
find man -name Makefile.in -exec sed -i '/s/getspnam\.3 / /' {} \
find man -name Makefile.in -exec sed -i '/s/password\.5 / /' {} \
```

不要使用 crypt 方法，而是使用更安全的 SHA-512 进行密码加密，这允许密码超过 8 个字符。此外，有必要更改当前使用的过旧 `/var/spool/mail` 位置。从 PATH 中移除 `/bin` 和 `/sbin`，因为它们是指向 `/usr` 中对应文件的符号链接。

> 注意：如果由于某些原因倾向于保留 `/bin` 和 `/sbin`，请在 LTS 完成后修改 `.bashrc` 中的 PATH。

```bash
sed -e 's:ENCRYPT_METHOD DES:ENCRYPT_METHOD SHA512: ' \
-e 's:/var/spool/mail:/var/mail:' ' \
-e '/PATH={s/sbin:@;s/bin:@}' \
-i etc/login.defs
```

> 注意：如果你选择构建带有 Cracklib 支持的 Shadow，请运行以下命令：

```bash
sed -i 's:DICTPATH:*:DICTPATH\t/lib/cracklib/pw_dict: ' etc/login.defs
```

通过以下命令修改文件修复简单的编程错误：

```bash
sed -e "224s/rounds/min_rounds/" -i libmisc/salt
```

为编译准备准备 Shadow：

```bash
touch /usr/bin/passwd
./configure --sysconfdir=/ \
--with-group-name-max-length=52
```

# Linux From Scratch - 版本 11.0

`config`选项的含义：

`touch /usr/bin/passwd` 需要存在，因为它的位置在某些程序中是硬编码的，如果不存在默认值是不正确的。

### --with-group-name-max-length=32

最大用户名为 32 个字符。使最大组名也保持相同。

编译该包：

```bash
make
```

此包不带测试套件。

安装该包：

```bash
make exec_prefix=/usr install
make -C man install-man
mkdir -p /etc/default
useradd -D --gid 999
```
