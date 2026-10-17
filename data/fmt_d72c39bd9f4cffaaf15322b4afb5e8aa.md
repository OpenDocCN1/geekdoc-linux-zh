
```bash
gcc -dumpspec | sed -e '@/tools@$g' \
-e '@startfile_prefix_spec;/(n;s@.**/usr/lib/@' \
-e '@cpp:/n;s@@@-system /usr/include/@' \
-dinarame $(gcc --print-libgcc-file-name)`/specs
```

检查 `spec` 文件以验证预期更改已生效是一个好主意。

确保调整后的工具链的基本功能（编译和链接）按预期工作至关重要。为了做到，执行以下健全检查：

```bash
echo 'int main() {} > dummy.c
cc dummy.c -v -Wl,--verbose &> dummy.log
readelf -l a out | grep ':lib'
```

不应该有错误，且最后一个命令的输出将是（考虑到动态链接器名称的平台特定差异）：

> [Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]

关于 64 位系统的说明：`/lib` 是我们动态链接器的位置，但它是通过 `lib64` 中的符号链接访问的。

> 注意
> 在 32 位系统上，解释器应为 `/lib/ld-linux.so.2`。

现在确保你已准备好使用启动文件：

```bash
grep -o '/usr/lib.*/crt[lin].*s' dummy.c
```

上一个命令的输出应该是：

```
/usr/lib/../../crt1.o succeeded
/usr/lib/../../crt.o succeeded
/usr/lib/../../crtn.o succeeded
```

验证编译器正在搜索正确的头文件：

```bash
grep -B1 '^ /usr/include' dummy.log
```

此命令应返回以下输出：

```
#include <...> search starts here:
/usr/include
```

接下来，验证链接器是否使用了正确的搜索路径：

```bash
grep 'SEARCH.*/usr/lib' dummy.log | sed 's|;\n|g'
```

包含 `-linux-gnu` 组件的路径引用应该被忽略，否则上一个命令的输出应该是：

```
SEARCH_DIR("/usr/lib")
SEARCH_DIR("/lib")
```

接下来确保我们使用的是正确的 `libc`：

```bash
grep "/lib*/libc.so.6 " dummy.log
```

上一个命令的输出应该是：

```
attempt to open /lib/libc.so.6
```

最后，确保我们使用的是正确的动态链接器：

```bash
grep "/lib*/libc.so.6 " dummy.log
```

最后一个命令的输出应该是：

```
attempt to open /lib/libc.so.6
```

## make 参数的含义

`tooldir=/usr`

通常情况下，`tooldir`（可执行文件最终将所在的目录）被设置为 `$(exec_prefix)/$(target_alias)`。例如，`x86_64` 机器会将其扩展为 `/usr/x86_64-unknown-linux-gnu`。由于这是一个自定义系统，不需要 `/usr` 下这个特定于目标的目录。`$(exec_prefix) / $(target_alias)` 将用于交叉编译（例如，在 Intel 机器上编译一个包，并生成一个可以在 PowerPC 机器上执行的代码）。

> 重要提示
> 本节中 Binutils 的测试套件被认为是至关重要的。在任何情况下都请勿跳过它。

测试结果：

```bash
make -k check
```

安装包：

```bash
make tooldir=/usr install
```

## 6.13.2. Binutils 目录

- **已安装的程序：** `addr2line`, `ar`, `as`, `c++filt`, `elfedit`, `gprof`, `ld`, `bfd`, `nm`, `objdump`, `ranlib`, `size`, `strings` 和 `strip`
- **已安装的库：** `libbfd.{a,so}` 和 `libcodes.{a,so}`
- **已安装的目录：** `/usr/lib/ldscripts`

## 概要说明

- **addr2line** 将地址转换为文件名和行号；给定一个地址和一个可执行文件的名称，它使用可执行文件中的调试信息来确定与地址相关的源文件和行号
- **ar** 创建、修改和从归档中提取内容
- **as** 汇编器，将 `gcc` 的输出汇编成目标文件
- **c++filt** 链接器用于反修饰 C++ 和 Java 符号，并防止重载函数导致崩溃
- **elfedit** 更新 ELF 文件的 ELF 头部
- **gprof** 显示调用图剖析数据
- **ld** 链接器，将多个目标文件和归档文件合并成单个文件，重定位它们的数据并连接符号引用
- **bfd** 将 `ld` 硬链接到 `ld`
- **nm** 列出给定目标文件中出现的符号
- **objcopy** 将一种类型的目标文件转换为另一种
- **objdump** 显示有关给定目标文件的信息，可以通过选项控制要显示的特定信息；显示的信息对于开发编译工具的程序员非常有用
- **ranlib** 生成归档内容的索引并将其存储在归档中；该索引列出了由归档成员（可重定位目标文件）定义的所有符号
- **readelf** 显示有关 ELF 类型二进制文件的信息
- **size** 列出给定目标文件的段大小和总大小
- **strings** 对于每个给定文件，输出至少达到指定长度（默认为四）的可打印字符序列；对于目标文件，默认只打印初始化和加载部分中的字符串，而对于其他类型的文件，它会扫描整个文件
- **strip** 丢弃目标文件中的符号
- **libbfd** 二进制文件描述符库
- **libopcodes** 一个用于操作码的库——即处理器指令的“可读文本”版本；它用于构建如 `objdump` 类的工具

## 6.14. GMP-6.1.2

GMP 包包含数学库。这些实用的函数为任意精度算术运算提供了支持。

**估算编译时间：** 1.3 SBU
**所需磁盘空间：** 59 MB

### 6.14.1. GMP 的安装

> 注意
> 如果你为 32 位 `x86` 编译，但你的 CPU 能够运行 64 位代码且你在环境中指定了 `CFLAGS`，则配置脚本将尝试为 64 位配置并失败。通过以下调用 `configure` 命令可以避免这种情况：
```
ABI=32 ./configure ...
```

为编译准备 GMP：

```
./configure --prefix=/usr \
    --enable-cxx \
    --disable-static \
    --docdir=/usr/share/doc/gmp-6.1.2
```

新配置选项的含义：

- `--enable-cxx` 此参数启用 C++ 支持
- `--docdir=/usr/share/doc/gmp-6.1.2` 此变量指定文档的正确位置。

编译包并生成 HTML 文档：

```
make
make html
```

> 重要提示
> 本节中 GMP 的测试套件被认为是至关重要的。在任何情况下都请勿跳过它。

测试结果：

```
make check 2>&1 | tee gmp-check-log
```

> 注意
> `gmp` 中的代码针对构建它的处理器进行了高度优化。偶尔，该代码会误判系统能力，导致测试或其他使用 `gmp` 库的应用程序中出现错误，并提示“Illegal instruction”（非法指令）。在这种情况下，应该使用 `--build=x86_64-unknown-linux-gnu` 选项重新配置 `gmp` 并重新构建。

确保测试套件中的所有 190 项测试均通过。通过执行以下命令检查结果：

```
awk '/# PASS:/{total+3} ; END{print total}' gmp-check-log
```

安装包及其文档：

```
make install
make install-html
```

### 6.14.2. GMP 目录

**已安装的库：** `libgmp.so` `libgmpxx.so`
**已安装的目录：** `/usr/share/doc/gmp-6.1.2`

## 概要说明

- `libgmp` 包含精度函数
- `libgmpxx` 包含 C++ 函数

## 6.15. MPFR-3.1.2

MPFR 包包含多精度函数。

**估算编译时间：** 0.8 SBU
**所需磁盘空间：** 45 MB

### 6.15.1. MPFR 的安装

为编译准备 MPFR：
