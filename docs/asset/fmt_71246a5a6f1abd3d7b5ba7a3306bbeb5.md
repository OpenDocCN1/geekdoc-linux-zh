
从示例 13.10 中显示的经过编辑的 `configure` 输出中，我们可以看到 `configure` 脚本已正确检测到 `mallinfo()` 不属于 LSB，因此未使用它。尽管 `libresolv` 和 `libpopt` 也不在 LSB 编写规范中，但 `lsbCC` 已检测到存在库的静态版本，因此可以使用。

接下来，我们尝试编译 `rsync` 二进制文件（示例 13.11）。由于我们告诉 `configure` 脚本使用 `lsbCC` 作为编译器，因此在调用 `make` 时不需要设置 `CC` 环境变量。

### 示例 13.10：运行 configure 脚本

```bash
$ tar xrfz rsync-2.5.5.tar.gz
$ cd rsync-2.5.5/
$ CC=lsbcc ./configure
configure: Configuring rsync 2.5.5
checking build system type... i686-pc-linux-gnu
checking host system type... i686-pc-linux-gnu
checking target system type... i686-pc-linux-gnu
checking for gcc... lsbcc
checking for C compiler default output... a.out
checking whether the C compiler works... yes
...
checking for connect... yes
checking for inet_ntop in -lresolv... yes
checking for inet_ntop... yes
...
checking for mtrace... no
checking for mallinfo... no
checking for setgroups... yes
...
config.status: creating popt/dummy
config.status: creating shconfig
config.status: creating config.h

rsync 2.5.5 configuration successful
```

### 示例 13.11：编译 rsync 二进制文件

```bash
$ make
...
lsbcc -I. -I. -g -O2 -DHAIVE_CONFIG_H -Wall -W -c clientname.c \
-0 clientname.o
clientname.c: In function 'client_sockaddr':
clientname.c:120: warning: implicit declaration of function \
'IN6_IS_ADDR_V4MAPPED'
clientname.c:120: dereferencing pointer to incomplete type
clientname.c:127: storage size of 'sin6' isn't known
clientname.c:127: warning: unused variable 'sin6'
clientname.c: In function 'compare_addrinfo_sockaddr':
clientname.c:213: dereferencing pointer to incomplete type
```

在编译 `clientname.c` 时发生了一个错误。示例 13.12 展示了 `clientname.c` 第 120 行附近的代码。

![](img/d75cffbcb54aabfb0f9854162061d394_214_0.png)

```
...
#define INET6
if (get_sockaddr_family(ss) == AF_INET6 &&
    IN6_IS_ADDR_V4MAPPED(&((struct sockaddr_in6 *)ss)->sin6_addr)) {
/* OK, so ss is in the IPv6 family, but it is really
 * an IPv4 address; something like
...
```

这里我们看到代码试图使用 IPv6 例程。LSB 1.3 不支持 IPv6，因此头文件中不包含此代码片段所需的宏定义。不幸的是，`configure` 脚本没有检测到这个问题，因为它假设如果安装了特定版本（或更高版本）的 `glibc`，则开发系统支持 IPv6。更好的做法是直接测试某些 IPv6 宏和接口是否存在。

幸运的是，可以通过向 `configure` 脚本传递参数手动禁用 IPv6 支持。因此，我们重新配置并再次调用 `make`（示例 13.13）。

![](img/d75cffbcb54aabfb0f9854162061d394_214_1.png)

现在发生了一个链接错误——链接器无法找到 `getpass()` 函数。`getpass()` 不在 LSB 编写规范中（Linux 上的 man 页将其标记为废弃），因此 LSB C 桩库中不包含它的桩代码。`glibc` 的信息页建议了一种替代方法，因此我们用建议的代码片段修补了 `rsync` 源代码。之后，`make` 成功并生成了一个 `rsync` 二进制文件。

### 示例 13.13：在不支持 IPv6 的情况下运行 configure

```
$ ./configure --disable-ipv6
configure: Configuring rsync 2.5.5
...
$ make
....
lsbccc -g -02 -DHAVE_CONFIG_H -Wall -W -0 rsync rsvnc.o \
generator.o receiver.o cleanup.o sender.o exclude.o util.o \
main.o checksum.o match.o syscall.o log.o backup.o options.o \
flist.o iio.o compat.o hlink.o token.o udidlist.o socket.o \
fileio.o batch.o clientname.o params.o loadparm.o \
clientserver.o access.o connection.o authenticate.o \
lib/fmtmatch.o lib/compat.o lib/snprintf.o lib/mdfour.o \
lib/pfstring.o zlib/deflate.o zlib/inblock.o zlib/infcodes.o \
zlib/infast.o zlib/inflate.o zlib/inftrees.o zlib/inftil.o \
zlib/trees.o zlib/zutil.o zlib/adler32.o -ipopt -iresolv
authenticate.c:278: undefined reference to `auth_client':
authenticate.c:278: undefined reference to `getpass'
collect2: ld returned 1 exit status
make: *** [rsync] Error 1
```

## 13.5.2 检查二进制文件

`lsbppchk` 可用于静态检查二进制文件的 LSB 合规性（示例 13.14）。静态应用程序检查器检查应用程序，确保它仅使用 LSB 指定的库、接口和运行时加载器，并验证其程序映像是否具有 ELF 格式要求的某些特征。

### 示例 13.14：运行应用程序检查器

```
$ lsbppchk rsync
lsbppchk for LSB Specification 2.0.0
Checking binary rsync
$ 
```

如果发现任何问题，它们将输出到标准错误流并记录在名为 `journal.binary_name` 的日志文件中。

### 13.5 案例研究：RSYNC

`lsbdynchk` 可用于在运行时检查二进制文件的合规性。动态应用程序检查器根据规范在运行时检查应用程序参数。

在此阶段应进行进一步的测试，例如在 LSB 示例实现中运行二进制文件，以及运行应用程序的功能验证测试。

### 13.5.3 FHS 问题

`lsbappchk` 工具无法验证应用程序是否完全符合 LSB 标准。某些方面，例如文件层级标准（FHS）合规性，目前需要手动检查。例如，默认情况下 `rsync` 使用位于 `/etc` 中的配置文件 `rsyncd.conf`。但 FHS 规定配置文件应位于 `/etc/opt/package`。这可以通过应用示例 13.15 中的补丁来实现。

> **示例 13.15：符合 FHS 要求的 `rsync` 补丁**

```
--- rsync-2.5.5/rsync.h 2002-03-25 00:29:43.000000000 -0700
+++ rsync-2.5.5.lsb/rsync.h 2003-05-13 18:25:25.000000000 -0600
@@ -26,7 +26,7 @@
 #define RSYNC_RSH_ENV "RSYNC_RSH"
 
 #define RSYNC_NAME "rsync"
-#define RSYNC_D_CONF "/etc/rsyncd.conf"
+#define RSYNC_D_CONF "/etc/opt/lsb-rsync/rsyncd.conf"
 
 #define DEFAULT_LOCK_FILE "/var/run/rsyncd.lock"
 #define URL_PREFIX "rsync://"
```

同样，可以通过向 `configure` 脚本传递 `--prefix=/opt/lsb-rsync` 参数，配置 `rsync` 安装到 `/opt/lsb-rsync` 而不是 `/usr/local`。

### 13.5.4 更多示例

构建符合 LSB 标准的应用程序版本的更多示例可以在第 14 章中描述的 LSB 应用程序测试套件中找到。

### 13.6 构建 LSB 开发环境

`lsb-build-base` 包的大部分源代码是根据图 13.1 所示从 LSB 编写规范数据库自动生成的。这样做的好处是头文件和桩库与规范保持同步。通常，人们不需要从数据库构建源代码，尽管所有脚本和数据库内容都在 LSB CVS 仓库中公开可用。

`lsb-build-base`、`lsb-build-cc` 和 `lsb-build-chroot` 的源码 tarball 和源码 RPM 包可从 LSB FTP 存档获取。tarball 包含一个说明如何构建该包的 `readme` 文件，而源码 RPM 包可以像往常一样使用 `rpm` 工具构建（示例 13.16）。

> 示例 13.16：构建 RPM 包

```
# rpm --rebuild lsb-build-base-1.3.4-1.src.rpm
```

### 13.7 扩展 LSB 开发环境

#### 13.7.1 使用 GCC 以外的编译器

LSB 开发环境的几乎所有测试和使用都是基于 GCC 作为编译器的。使用其他编译器构建符合 LSB 标准的应用程序是可能的。

使用开发环境的头文件和桩库并不是严格必要的，尽管这样做几乎肯定会更简单。使用另一种编译器所需的构建流程变更可总结如下：

- 使用符合 LSB 标准的头文件（`lsb-build-base` 包）。

![](img/d75cffbcb54aabfb0f9854162061d394_218_0.png)

图 13.1：LSB 开发环境

- 使用符合 LSB 标准的库。使用开发环境桩库的好处是，如果尝试使用非 LSB 接口，将会发生链接错误。

- 确保二进制文件使用该架构的 LSB 动态链接器，而不是标准的 Linux 链接器。例如，在 x86 机器上，应使用 `/lib/ld-lsb.so.1` 而不是 `/lib/ld-linux.so.2`。

如果你使用 `lsb-build-chroot`，前两项更改会自动完成。实现第三项更改的方式将取决于编译器；例如，对于 `gcc`，这是通过编辑 `specs` 配置文件完成的。

#### 13.7.2 与 IDE 集成

`lsb-build-cc` 与 IDE 的集成应该相当简单，因为唯一需要的变更是调用 `lsbcc` 而不是普通编译器。对于 `lsb-build-chroot`，需要在 `chroot` 内部运行编译过程。这可以使用辅助程序实现，或者通过通信正在 `chroot` 内运行的编译守护进程来实现。

#### 13.7.3 使用非 LSB 接口

有时，开发者无法构建完全符合 LSB 标准的应用程序，因为其程序的核心功能依赖于未包含在 LSB 编写规范中的特性。然而，出于兼容性原因，他们仍然希望尽可能符合 LSB 标准。

这方面的一个例子是依赖于不在 LSB 编写规范中的 C 库接口或系统调用。在这种情况下，不可能简单地提供共享库与应用程序，或者静态链接需求使二进制文件符合 LSB 标准。通过修改 LSB 开发环境，仍然可以使用它来构建二进制文件并获得相关好处。在上述情况下，最简单的方法是获取桩库的源代码，手动添加所需的接口，并构建新版本桩库。同样，可以将原型添加到 LSB 头文件中。

### 13.8 下载 LSB 开发环境

要获取 LSB 开发环境，请访问 LSB 下载网页。表 13.2 表示了可以通过万维网访问的信息。

- `lsb-build-base`：LSB 开发环境基础包提供桩库和头文件。这些可用于构建符合 LSB 标准的应用程序。请注意，包的版本号指的是生成桩库和头文件所针对的规范版本。

- `lsb-build-c++`：此包为 `lsb-build` 包提供临时 C++ 构建支持。它向 `lsb-build-base` 安装的文件中添加 C++ 头文件和符合 LSB 标准的静态 C++ 库构建。

## 表 13.2：开发环境下载页面

| 规范版本 | 软件包 | 版本 | 架构 |
|---|---|---|---|
| 2.0 | lsb-build-base | 2.0.0-1 | i486, IA64, PPC, PPC64, S390, S390x, x86_64, SRC |
| 2.0 | lsb-build-c++ | 2.0.0-1 | i486, IA64, PPC, PPC64, S390, S390x, x86_64, SRC |
| 2.0 | lsb-build-cc | 2.0.0-1 | i486, IA64, PPC, PPC64, S390, S390x, x86_64, SRC |
| 2.0 | lsb-build-chroot | 2.0.0-1 | i486, IA64, PPC, PPC64, S390, S390x, x86_64, SRC |

- `lsb-build-cc`：此软件包提供 `lsbcc`，它是可用于构建符合 LSB 的应用程序的多种方法之一。

- `lsb-build-chroot`：LSB 开发环境是一种工具，旨在简化生成符合 LSB 标准的二进制文件的过程。

# 第十四章

# 使用应用电池

**LSB 应用电池**是一组为符合 LSB 书面规范而构建的开源应用程序的集合。LSB 项目提供这些应用程序，作为进一步证明 Linux 发行版能够支持安装和运行符合 LSB 标准的应用程序的证据。

对 Linux 发行版进行认证需要多种方法来确保其符合 LSB 书面规范。LSB 运行时测试套件用于测试许多系统 API 的正确行为。LSB 库检查器用于验证所有由 LSB 指定的共享库及其各自的 API 是否存在于系统中。Linux 发行版合规性的第三项主要测试是 **LSB 应用电池**。

电池中应用程序的选择旨在更接近真实场景地调用所有由 LSB 指定的共享库。以这种方式使用应用电池可以补充 LSB 运行时测试套件，从而为 Linux 发行版提供更彻底的验证。

**应用电池** 还有一个有用的领域，即其如何使用 **LSB 开发环境**。通过使用开发环境来构建使用所有 LSB 共享库的应用程序，有助于识别 LSB 开发环境头文件和桩库中的任何缺陷。由于 `lsbdev` 是直接根据书面规范中使用的数据创建的，因此它也能发现规范本身存在的问题。

最后，除了用于测试 Linux 发行版和验证 `lsbdev` 之外，应用电池还可以向应用程序开发人员展示构建典型的符合 LSB 标准的应用程序需要哪些步骤。

在进一步讨论应用电池（`appbat`）是什么以及如何使用它之前，有必要说明 `appbat` 不是什么。`appbat` 中的应用不应被考虑用于生产环境。尽管构建这些应用程序以符合 LSB 标准只需从上游源代码进行最少修改，但 LSB 项目仅进行了最小限度的测试。`appbat` 的目的并不是创建可以替代 Linux 发行版中自带应用程序的现成生产级替代品。相反，电池中的应用仅应用于测试 Linux 发行版对 LSB 书面规范的遵从性。

## 14.1 理解应用电池

### 14.1.1 常见的开源应用程序

LSB 应用电池是由 LSB 开发环境构建的一组常见开源应用程序，以确保它们符合 LSB 书面规范。在某些情况下，应用程序只是重新编译，以确保使用 LSB 动态链接器而不是系统链接器。少数应用程序应用了小的补丁，以修复应用使用了非 LSB 参数类型，或者在使用 `lsbdev` 时 `configure` 脚本产生错误结果等简单问题。对于其他少数应用程序，则有一些更重大的补丁。一个例子是 `rsync` 应用程序，它使用了已弃用的 `getpass()` API。`rsync` 的补丁将 `getpass()` 的使用替换为对 `getpassword()` 的调用，这是一个专门为 LSB 版本的 `rsync` 编写的子程序，提供与从 `getpass()` 预期相同的返回值。
