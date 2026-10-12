
# `perl /Configure`

```
Usage: Configure [-Dxxx] [-Lxxx] [-lxxx] os/compiler
pick os/compiler from:

* BC-16 BC-32 FreeBSD NetBSD-sparc
* NetBSD-x86 SIX-N VC-MSDOS VC-NT
* VC-W31-16 VC-W31-32 VC-WIN16 VC-WIN32
* aix-cc aix-gcc alpha-cc alpha-gcc
* alpha400-cc bsdi-gcc cc debug
* debug-irix-cc debug-linux-elf dxux-R4-gcc
* dxux-R4-x86-gcc dist gcc hpx-cc
* hpx-gcc hpx-kr-cc irix-gcc irix-gcc
* linux-out elf nextstep purify
* sc05-cc solaris-sparc-cc solaris-sparc-gcc solaris-sparc-sc4
* solaris-usparc-sc4 solaris-x86-gcc sunos-cc sunos-gcc
* unixware-2.0 unixware-2.0-pentium
```

注意，除了架构和二进制目标外，你还可以在 `Configure` 命令行中设置其他选项，包括：

- `DES_PTR`—使用此选项指定在构建期间，你想在 `crypto/des/des_loc1.h` 中的 DES 使用指针而不是默认的数组查找。
- `DES_RISC`—使用此选项指定不同的 `DES_ENCRYPT` 宏以帮助注册依赖关系（RISC 架构的良好选择）。这在 RISC 处理器上通常产生更快的性能。
- `DNO_BF`—使用此选项构建没有 Blowfish 支持的 SSLeay。
- `DNO_DES`—使用此选项构建没有 DES/3DES 支持的 SSLeay。
- `DNO_IDEA`—使用此选项构建没有 IDEA 支持的 SSleay。
- `DNO_MD2`—使用此选项构建带有 MD2 支持的 SSleay。
- `DNO_RC2`—使用此选项构建没有 RC2 支持的 SSleay。
- `DNO_RC4`—使用此选项构建没有 RC4 支持的 SSleay。
- `OSAref`—使用此选项构建使用 RSAref 的 SSleay。

# 安全网络协议

## 注意

还存在其他更晦涩的选项。例如，如果需要，你可以指定在 DES 中使用 `int` 代替 `10ng`。查看 SSleay 文档获取更多信息。

在定义了架构和选项后，运行 `Configure`。作为响应，它将打印出你的预配置摘要。这是一个示例：

```
[root@linux SSleay-0.8.1b]# perl Configure linux-elf
CC =gcc
CFLAG=-DLENDIAN -DTERMIUM -O3 -fomit-frame-pointer -m486 -Winitialized
EN_LIBS=
BN_ASM=asm/x86-elf.o
DES_ENC=asm/x86-elf.o
BF_ENC=asm/x86-elf.o
DES_PTR used
DES_RISC used
BN_LONG used
RC4 mode
BF_PTR used
```

我建议将这些值剪切并粘贴到临时文件中。某些系统会导致错误的 make，你可能以后更改它们，所以准备好它们很好。

接下来，运行 `make`：

```
make
```

`make` 将花费几分钟，如果你安装了 ANSI 支持，就不会有问题。当你看到这条消息时，你就知道 `make` 成功了：

NOTE： OpenSSL 头文件已从 `include/*` 移动到 `include/openssl/*`。包含 OpenSSL 头文件应使用形式为 `#include <openssl/foo.h>` 而不是 `<foo.h>`。新的位置允许在 `/usr/local/include/openssl/` 安装 OpenSSL 头文件，并避免与其他库冲突。对于使用旧 `<foo.h>` 的程序，通常一个额外的编译器选项就足够了：例如，在你要编译程序的 Makefile 中添加 `-I/usr/local/include/openssl`（保留原始）。请确保没有旧的头文件：`include` 目录除了 `openssl` 之外应该是空的。

验证 `make` 成功后，运行此命令：

```
make test
```

根据你的系统配置，相关行可能是第 59 行或第 60 行，取决于被注释：

```
CFLAG=-DLENDIAN -DTERMIUM -O3 -fomit-frame-pointer -m486 -Winitialized
```

这是要移除的优化标记：

```
-O3
```

移除优化标记后，再次启动 (`make clean; make`)，一切应该是正常的。

警告：在 Caldera OpenLinux 1.2 上，即使你更改了 `-O3` 优化标记，`make test` 也会失败。显然，SSleay 不喜欢 1.2 的随机性。我在 OpenLinux 上尝试编译不同版本的 SSleay，没有成功。但在 Red Hat 5.1 上干净编译且没有错误。我只能得出问题出在 OpenLinux 1.2 而不是 SSleay。解决方案是获取更新版本的 OpenLinux。

当 `make test` 成功时，你会看到这条消息：

```
Signed certificate is in newcert.pem
newcert.pem: OK
make[1]: Leaving directory '/SSLeay-0.9.0b/test'
SSleay 0.9.0b 29-Jun-1998
built on Wed 30 01:20:01 PDT 1999
options:bn(64,32) md2(int) rc4(idx,int) des(ptr,risc1,16,long) idea(int)
blowfish(ptr2)
c flags:gcc -DLENDIAN -DTERMIUM -DBN_ASM -O3 -fomit-frame-pointer -m486 -Winitialized -DSHA1_ASM -MD5_ASM -DRMD160_ASM
```

一旦验证测试成功，如下所示安装包：

```
make install
```

# 解压、补丁和安装 Apache

接下来，将 `apache_1_2_6_tar.gz`（或更高版本）拷贝到 `/usr/src` 并解压：

```
cp apache_1_2_6_tar.gz /usr/src
cd /usr/src
gunzip apache_1_2_6_tar.gz
tar -xvf apache_1_2_6_tar.gz
```

Apache 将解压到 `/usr/src/apache-1.2.6/`。验证已正确解压后，将 `apache_1_2_6_ssl_1_17_tar.gz` 拷贝到 `/usr/src/apache-1.2.6` 并解压：

```
cp apache_1_2_6_ssl_1_17_tar.gz /usr/src/apache-1.2.6
cd /usr/src/apache-1.2.6
gunzip apache_1_2_6_ssl_1_17_tar.gz
tar -xvf apache_1_2_6+ssl_1_17_tar
```

这应该解压出以下文件：

- `ben.pgp.key.asc`—作者的 PGP 公钥。
- `EXTRAS.SSL`—额外功能的文档。
- `LICENCE.SSL`—Apache SSL 许可证。
- `md5sums`—这些文件的 MD5 校验和（使用 `md5sum`）。
- `md5sums.asc`—作者对 `md5sums` 的离线签名。
- `README.SSL`—概述。
- `SECURITY`—对 SSL 和安全的思考。
- `src/apache_ssl.c`—Apache 的额外模块。
- `SSLconf/conf/access.conf`—空的 Apache 访问配置文件。
- `SSLconf/conf/httpd.conf`—一个示例 `httpd.conf`。

## Linux 网络安全

第四部分

- `SSLconf/conf/mime.types`—一个示例的 `mime.types` 配置文件。
- `SSLconf/conf/srm.conf`—一个示例的 Apache `srm` 配置文件。
- `SSLpatch`—一个关重要的补丁（我们稍后会用到它）。

在确认文件已正确解压后，在编译 Apache 之前，按照如下方式应用提供的补丁：

```
patch -p1 < SSLpatch
```
