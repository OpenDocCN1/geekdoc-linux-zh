
就像 `rpmbuild` 一样，`dpkg-buildpackage` 首先清理你的源码，构建应用程序并生成 Debian 包。注意，使用 `fakeroot` 是为了欺骗构建软件使其认为是以 root 权限运行。这样做是因为构建包时不需要写入标准系统位置，但在自包含构建过程中可能需要创建 root 用户的文件。记住，`fakeroot` 并没有提供任何 root 权限。

成功运行 `dpkg-buildpackage` 将产生输出：

```
$ dpkg-buildpackage -rfakeroot
dpkg-buildpackage: source package is hello
dpkg-buildpackage: source version is 1.0-1
dpkg-buildpackage: source changed by Jon Masters <jcm@jonmasters.org>
dpkg-buildpackage: source host architecture i386
fakeroot: debian/rules clean
h_testdir
h_testdir
rm -f build-stamp configure-stamp
/usr/bin/make clean
make[1]: Entering directory '/home/jcm/JPL/src/portability/dpkg/hello-1.0'
make[1]: *** No rule to make 'clean'. Stop.
make[1]: Leaving directory '/home/jcm/JPL/src/portability/dpkg/hello-1.0'
make: [clean] Error 2 (ignored)
h_clean
dpkg-source -b hello-1.0
dpkg-source: building hello using existing hello_1.0.orig.tar.gz
dpkg-source: building hello in hello_1.0-1.diff.gz
debian/rules build
h_testdir
touch configure-stamp
dh_testdir
/usr/bin/make
make[1]: Entering directory '/home/jcm/PLP/src/portability/dpkg/hello-1.0'
make[1]: Nothing to be done for 'all'.
make[1]: Leaving directory '/home/jcm/PLP/src/portability/dpkg/hello-1.0'
#doc-to-man debian/hello.sgml > hello.1
touch build-stamp
fakeroot debian/rules binary
dh_testdir
dh_testroot
dh_clean -k
dh_installdirs
/usr/bin/make install DESTDIR=/home/jcm/PLP/src/portability/dpkg/hello-1.0/debian
make[1]: Entering directory '/home/jcm/PLP/src/portability/dpkg/hello-1.0'
mkdir -p /home/jcm/PLP/src/portability/hello-1.0/debian
cp hello /home/jcm/PLP/src/portability/hello-1.0/debian
make[1]: Leaving directory '/home/jcm/PLP/src/portability/hello-1.0'
dh_testdir
dh_testroot
dh_installchangelogs
dh_installdocs
dh_installexamples
dh_installman
dh_link
dh_strip
dh_compress
dh_fixperms
dh_installdeb
dh_shlibdeeps
dh_gencontrol: warning: unknown substitution variable $(misc:Depends)
dh_mdsaums
dh_builddeb
dpkg-deb: building package 'hello' in `../hello-1.0-i386.deb'.
signfile hello-1.0-1.dsc
gpg: skipped Masters '<jcmjonmasters.org*': secret key not available
pg: [stdin]: clearsign failed: secret key not available
```

请注意，此构建的输出将出现在包源码上级目录中。因此，如果你将 `hello-1.0.tar.gz` 解压到主目录，请在主目录根目录下查找输出文件 `hello_1.0-i386.deb`。除了二进制包外，你还会看到创建了其他几个文件：

```
hello-1.0-1.diff.gz  hello_1.0-1.dsc  hello_1.0-dsc.asc
```

这些文件可以供其他开发者用于重新创建二进制包。

你会注意到在上一个示例中生成了几个警告。首先，GNU Make 抱怨它无法清理源码。这个问题只需通过在每个 `Makefile` 中添加一个清理目标（clean target）即可简单解决，以确保你的项目在需要时可以进行清理。

构建过程中观察到的第二个问题是，用户在构建包时没有安装（或可用）GPG。任何分发良好的 Debian 包都应该尽可能地进行 GPG (PGP) 签名，如果你选择允许的话，它将执行电子签名。

# 第 3 章：可移植性

## Debian 开发者 (DDs)

经常在 Debian Linux 发行版上工作，和/或负责官方 Debian 发行版软件包的人员被称为 Debian 开发者（Debian Developer），通常亲切地简写为“DD”。Debian 与许多其他发行版不同，这不仅体现在其使命上，也体现在其开发者社区中。成为 Debian 开发者相对困难，通常需要经过各种指导步骤和正式程序。

好消息是，你不需要成为 Debian 开发者就可以为 Debian 发行版发布软件包（你也不需要成为官方的 Ubuntu 开发者）。但由于你不太可能已经是或将来会成为官方认可的开发者，你将不得不通过自己的网站提供软件包。如果你提供了任何仓库，你生成的软件包将不会自动显示在用户的 `apt search` 软件包列表中——他们需要显式地告诉 `apt`。

## 更多信息

Debian 软件包管理工具非常复杂且不断演进，因此，你可能需要参考《Debian 新手维护者指南》（Debian New Maintainer's Guide，可在 Debian 网站 www.debian.org 获取）获取更多信息。Debian 维护着自己的一套发行标准以及关于什么是有效软件包的规则。再次强调，网站是获取最新参考资料的最佳地址。

## 可移植源码

为 Linux 编写的软件不仅应该与运行在相同硬件平台上的发行版尽可能保持二进制兼容，还应该在可用正确库和其他先决条件的大多数系统上正确构建。构建过程必须处理确定不同软件环境之间的差异。这既适用于 Linux 发行版之间，也适用于 Linux 与其他 UNIX 环境之间。

为了帮助发行版之间的源码级可移植性，创建了 GNU Autools。Autoconf、Auttool、Automake 以及许多其他脚本和工具共同工作，形成了 GNU 构建系统。每个工具将通过一系列测试，以了解用户可用的硬件和软件环境，确定是否可以在该相应的软件环境中构建应用程序。

通过一组配置合理的源码，构建你的软件将变成熟悉的“config-make, make install”序列，你可能已经对它有了一些了解。接下来的章节将作为 GNU Autools 的介绍。如需更多信息，请查看 Autools 教程，该书可以在 http://sources.redhat.com/ebook 在线免费阅读。

> 通过修改 `/etc/apt/sources` 文件来添加你的仓库（如果你提供的话）。

## GNU Autotools

使用示例可以更容易理解 GNU Autotools 如何工作。在这种情况下，一个简单的程序（`hello.c`）显示一条消息。它被修改为使用一个名为 `print_message` 的库（libhello）来执行实际的消息打印操作。此外，程序会尝试确定构建它的机器本质上是大端序（big-endian）还是小端序（little-endian），如果机器是大端序，则打印出一个可选的问候语（端序将在在本章稍后部分讨论——继续阅读以了解更多 Jonathan Swift 如何影响计算机科学）。

你可以创建 `hello.c` 示例程序：

```c
#include "hello.h"
int main() {
    print_message("Hello, World!");
    #ifdef __BIG_ENDIAN
    printf("This system is big-endian.\n");
    #endif
    return 0;
}
```

（注：原文示例中代码块不完整，此处根据上下文补全了逻辑，代码本身不翻译）

为了配合 `hello.c`，我们需要 `hello.h`：

```c
#ifndef HELLO_H
#define HELLO_H
void print_message(const char *msg);
#endif
```

以及实现 `libhello.c`：

```c
#include <stdio.h>
void print_message(const char *msg) {
    printf("%s\n", msg);
}
```

## 构建 Autools 项目

构建程序和库需要几个步骤。首先，我们需要运行 `aclocal` 来处理 `.m4` 宏文件：

```
aclocal -v
```

然后，使用 `autoconf` 处理 `configure.in` 并生成 `configure` 脚本：

```
autoconf -v
```

使用 `automtool` 准备 `config.h`：

```
automtool -v
```

使用 `automake` 生成生成 `Makefile.in` 文件：

```
automake -v
```

最后，运行新生成的 `configure` 脚本来生成 `Makefile`：

```
./configure
```

现在，可以使用 `make` 来构建并安装程序：

```
make
make install
```

这些单独的阶段看起来复杂且杂乱，但没关系，因为每个阶段很快就会解释。当你读完本章时，会有更多关于 Autools 的问题需要解答，但至少你知道这些工具的存在，以及在构建项目时去哪里寻找更多信息。这场战斗已经胜利了。

```
检查链接器 (/usr/bin/ld) 是否为 GNU ld... 是
检查 /usr/bin/ld 选项以重新加载对象文件... -r
检查兼容 BSD 的 nm... /usr/bin/nm -B
检查在 -s 是否有效... 是
检查如何运行 C 预处理器... gcc -E
检查是否存在 ANSI C 头文件... 是
检查是否存在 sys/stat.h... 是
检查是否存在 stdlib.h... 是
检查是否存在 string.h... 是
检查是否存在 memory.h... 是
检查是否存在 strings.h... 是
检查是否存在 inttypes.h... 是
检查是否存在 stdint.h... 是
检查是否存在 unistd.h... 是
检查 dlfcn 的可用性... 是
检查 dfcn 是否存在... 是
检查是否存在 dlfcn.h... 是
检查是否存在 g++... g++
检查我们是否使用 GNU C++ 编译器... 是
检查 g++ 是否接受 -g... 是
检查如何运行 C++ 预处理器... g++ -E
检查是否存在 g77... g77
检查我们是否使用 GNU Fortran 77 编译器... 是
检查 g77 是否接受 -g... 是
检查行参数的最大长度... 32768
检查用于解析 /usr/bin/nm -B 输出 gcc 对象的命令... 否
检查 objdir... .lib
检查是否存在 ar... ar
检查是否存在 ranlib... ranlib
检查 gcc 静态标记是否有效... 是
检查 gcc 是否支持 -fno-rtti -fno-exceptions... 否
检查 gcc 生成 PIC 的选项... -fPIC
检查 gcc PIC 标记 -FWPIC 是否有效... 是
检查 gcc 是否支持 -o file.o... 是
检查 gcc 链接器是否支持共享库...
lc 应显式链接在... 否
检查动态链接器特性... GNU/Linux ld.so
检查如何将库路径硬编码到程序中... 直接
检查 stripping 是否支持共享库... 是
检查 libtool 是否支持共享库... 是
检查是否构建共享库... 是
检查是否构建静态库... 是
configure: 创建 libtool
向 libtool 添加配置标签 "CXX"
检查 g++ 使用的 ld... /usr/bin/ld
检查链接器 (/usr/bin/ld) 是否为 GNU ld... 是
检查 g++ 链接器 (/usr/bin/ld) 支持共享库... 是
检查 g++ 生成 PIC 的选项... -fPIC
检查 g++ PIC 标记 -fPIC 是否有效... 是
检查 gcc 是否支持 -o file.o... 是
检查 gcc 链接器 (/usr/bin/ld) 支持共享库...
```

# 第 3 章：移植性

```
检查动态链接器特性... GNU/Linux ld.so
检查如何将库路径硬编码到程序中... 直接
检查是否可以提取库... 是
向 libtool 添加配置标签 "F77"
检查 libtool 是否支持共享库... 是
检查是否构建静态库... 是
检查 g77 生成 PIC 的选项... -fPIC
检查 g77 标记 -fPIC 是否有效... 是
检查 g77 是否支持 -c file... 是
检查 g77 链接器 (/usr/bin/ld) 支持共享库... 是
检查动态链接器特性... GNU/Linux ld.so
检查如何将库路径硬编码到程序中... 直接
检查是否可以提取库... 是
检查是否存在 gcc... (缓存) gcc
检查我们是否使用 GCC C 编译器... (缓存) gcc
检查 gcc 是否接受 g... (缓存) 是
检查 gcc 接受 ANSI C 的选项... (缓存) 无需
检查是否存在 ANSI 头文件... (缓存) 是
检查字节序是否为大端... 否
检查是否存在 unistd.h... (缓存) 是
检查是否存在 stdlib.h... (缓存) 是
检查 stdio.h 的可用性... 是
检查是否存在 stdio.h... 是
configure: 创建 ./config.status
config.status: 创建 Makefile
config.status: 创建 src/Makefile
config.status: 创建 include/config.h
config.status: 执行默认-l 命令
====================================================================================
感谢测试此示例。你可以在此处添加一些输出，并在需要引用任何 AC 环境变量。
======================================================================
```

注意 configure 如何报告它正在执行的各个测试的状况。你可以看到许多类似于检查 stdio.h 的输出，这表示正在代表你执行许多测试。运行 configure 后，你会发现项目源码的 include 目录下创建了一个 config.h 文件：

```
* include/config.h. 由 configure 生成。 *
* include/config.h.in. 由 autoconf 从 config.in 生成。 */
```

```
# 如果你有 <dlfcn.h> 头文件，则定义为 1。 /* /
#define HAVE_DLFCN_H 1
```

```
# 如果你有 <inttypes.h> 头文件，则定义为 1。 /* /
#define HAVE_INTTYPES_H 1
```

```
# 如果你有 <memory.h> 头文件，则定义为 1。 /* /
#define HAVE_MEMORY_H 1
```
