

大多数 Linux 发行版中使用的标准 DHCP 软件包是由互联网软件联盟 (ISC) 提供的。尽管该软件包因其广泛使用且包含客户端和服务端而看似适合用于嵌入式 Linux 系统，但实际上它并不适合，因为其*Makefile*和*配置*脚本很难适应交叉编译。

不过，还有另一个开源软件包同时提供 DHCP 服务器和 DHCP 客户端，并且可以用于嵌入式 Linux 系统：*udhcp*。*udhcp* 项目是 BusyBox 项目的一部分，其网站位于 *http://udhcp.busybox.net/*。该软件包可在该网站上获取，并根据 GPL 许可进行分发。*udhcp* 仅依赖于 C 库，并且可以使用 *glibc* 和 *uClibc* 进行编译。

首先，在你的 `${$PRJROOT}`/sysapps 目录中下载并解压 *udhcp* 软件包。例如，对于我们的 SYSM 模块，我们使用了 *udhcp* 0.9.8。在后续操作中，请进入该软件包的目录：

```
$ cd ${$PRJROOT}/sysapps/udhcp-0.9.8
```

该软件包无需配置。唯一重要的选项是 *CROSS_COMPILE*，它应包含交叉工具链的前缀，例如，如果在 ARM 上使用 *uClibc*，则为 *arm-uclibc*-（你需要保留末尾的连字符），如果偏好 *glibc*，则为 *arm-linux*-。

编译并链接该软件包：

```
$ make CROSS_COMPILE=arm-uclibc-
```

编译时间很短。当针对 *glibc* 进行链接并删除符号表 (stripped) 后，† 服务器和客户端的大小约为 16 KB。当针对 *uClibc* 进行链接并删除符号表后，服务器和客户端的大小约为 15 KB。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_325_0.png)

本章中提供的所有文件大小对应于一位作者的配置环境，你很可能获得略有不同的结果。此处提供的数字仅供参考。例如，ARM 代码，以及通常的 RISC 代码，通常比 x86 代码更大。

如果你在系统中使用服务器，请将其复制到目标机的 */usr/sbin* 目录：

```
$ cp udhcp ${$PRJROOT}/rootfs/usr/sbin
```

如果你使用的是客户端，请将其复制到目标机的 */sbin* 目录：

```
$ cp udhcpc ${$PRJROOT}/rootfs/sbin
```

服务器和客户端都需要配置文件和运行时文件来存储租约状态相关信息。如本节中的命令所示，服务器（守护进程）名为 *udhcpd*，客户端名为 *udhcpc*。

> † *udhcp* 的 *Makefile* 在构建完成后会自动删除二进制的符号表。

对于服务器，请创建 `/var/lib/misc` 目录和一个租约文件，并将示例配置文件复制到目标机的根文件系统：

```
$ mkdir -p ${PRJROOT}/rootfs/var/lib/misc
$ touch ${PRJROOT}/rootfs/var/lib/misc/udhcpd.leases
$ cp samples/udhcpd.conf ${PRJROOT}/rootfs/etc
```

如果你忘记创建租约文件，服务器将拒绝启动。

对于客户端，请创建 `/etc/udhcpc` 目录和 `/usr/share/udhcpc` 目录，并将其中一个示例配置文件复制到 `/usr/share/udhcpc/default.script`：

```
$ mkdir -p ${PRJROOT}/rootfs/etc/udhcpc
$ mkdir -p ${PRJROOT}/rootfs/usr/share/udhcpc
$ cp samples/sample.renew \
> ${PRJROOT}/rootfs/usr/share/udhcpc/default.script
```

此外，编辑目标机的 `/etc/inittab` 文件以启动所需的守护进程。例如，以下是我们的 SYSM 模块中用于 DHCP 服务器的行：

```
::respawn:/usr/sbin/udhcpd
```

要完整了解 `udhcpd` 和 `udhcpc` 的配置和使用，请阅读软件包附带的手册页 (manpages) 并查看项目网站。

## Internet 超级服务器

与大多数 Unix 系统一样，在 Linux 中，网络服务是以守护进程的形式实现的。每个网络守护进程响应特定端口的请求。例如，Telnet 服务在端口 23 上运行，而更安全的 SSH 服务使用端口 22。为了让网络服务正常工作，必须有一个进程处于活动状态并在每个相应的端口上进行监听。然而，并非启动所有网络守护进程让每个守护进程监听其自己的端口，一些系统使用了一个 Internet“超级服务器”。这个超级服务器是一个特殊的守护进程，它监听所有启用的网络服务的端口。当来自特定端口的请求进来时，相应的网络守护进程被启动，并且请求被传递给它进行处理。

这种方案有两个主要优点。首先，始终只有最小的一组所需守护进程处于活动状态，因此不会浪费系统资源。其次，它提供了一种集中管理网络服务的机制。

虽然许多网络服务可以由 Internet 超级服务器管理，但某些服务——如 HTTP 服务器或 SNMP 代理——几乎总是设置为由其直接控制端口，出于可扩展性和可靠性的原因。

### inetd

inetd 是 ftp://ftp.uk.linux.org/pub/linux/Networking/netkit 上可用的 netkit 软件包之一的一部分。Netkit 是一组提供各种网络功能的软件包。inetd 是 netkit-base 软件包的一部分（该软件包还包含其他有用的网络程序，如 ping）。与其他 netkit 软件包一样，netkit-base 根据 BSD 许可协议分发。

首先，下载 netkit-base 并将其解压到你的 $[PRJROOT]/sysapps 目录中。对于我们的 SYSM 模块，我们使用了 netkit-base 版本 0.17。现在，移动到 netkit-base 的解压目录：

```
$ cd $[PRJROOT]/sysapps/netkit-base-0.17
```

在开始配置 netkit-base 之前，你需要修改 configure 脚本，以防止它试图在你的主机上运行测试程序。因为你在指示它使用你为目标构建的编译器，所以它编译的测试程序仅适用于你的目标环境。因此，这些测试程序将在主机上运行失败，如果未修改，configure 脚本将无法完成。为了避免这些问题，请编辑 configure 脚本并注释掉所有尝试执行编译后二进制文件的行（在每行开头添加 # 符号）。configure 试图运行的实际测试程序都名为 __conf.test。以下是一个注释掉的行示例：

```
# ./conf.test || exit 1;
```

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_327_0.png)

在大多数情况下，以所述方式编辑软件包的 configure 脚本以解决构建问题或跳过测试是不明智的。configure 脚本通常使用 GNU autoconf 工具自动生成，因此以这种方式编辑它是徒劳且容易出错的。正确的做法是找到 configure 脚本的正确选项以使其正确运行，或者在缺乏适当选项的情况下，编辑自动构建 configure 文件的 configure.in 并使用 autoconf 工具重新生成 configure 脚本。

然而，在这种特定情况下，configure 脚本并非使用 GNU autoconf 工具创建，经过仔细检查后，其中一位作者已确认在此处以这种方式编辑脚本是唯一有效的选项。

inetd 可以使用 glibc 或 uClibc 构建。但是，要将其链接到 uClibc，你需要确保在 uClibc 中启用了 RPC 支持。如果 uClibc 是在 RPC 禁用的情况下构建的（这是默认设置），你必须重新安装 uClibc。

一旦 configure 脚本被正确编辑，请配置并编译 netkit-base：

```
$ CC=arm-linux-gcc ./configure --prefix=$[TARGET_PREFIX]
$ make
```

Netkit-base 构建速度相当快。使用 glibc 构建并删除符号表时，生成的二进制文件大小为 24 KB。使用 uClibc 时，删除符号表后的二进制文件大小为 23 KB。无论你选择哪种实际链接方法，生成的 inetd 二进制文件都比下一节我们将看到的 xinetd 二进制文件小得多。

与其他章节中我们构建的其他软件包不同，不要使用 make install 来安装 inetd，因为 Makefile 没有为跨平台开发正确构建。除其他事项外，它们试图使用主机的 strip 命令来删除二进制的符号表。

相反，请将 inetd 二进制文件和示例配置文件手动复制到目标机的根文件系统：

```
$ cp inetd/inetd $(PRJROOT)/rootfs/usr/sbin
$ cp etc.sample/inetd.conf $(PRJROOT)/rootfs/etc
```

根据你的设置编辑 inetd.conf 文件。除了 inetd.conf 之外，etc.sample 目录还包含可用于目标机 /etc 目录中的其他文件示例，如 resolv.conf 和 services。对于我们的 SYSM 模块，这是我们在后文“通过 Telnet 进行网络登录”中讨论的 Telnet 守护进程的 inetd.conf 条目：

```
telnet stream tcp nowait root /usr/sbin/telnetd
```

一旦 inetd 被复制并配置好，请编辑目标机的 /etc/inittab 文件以添加 inetd 的行。以下是我们的 SYSM 模块使用 BusyBox 的 init 时的示例行：

```
::respawn:/usr/sbin/inetd -i
```

-i 选项指示 inetd 不要作为守护进程启动。因此，如果 inetd 因某种意外原因停止运行，init 可以重新生成 inetd。2 由于 netkit-base 还包含 ping，你会在 ping 目录中找到一个 ping 二进制文件。但是，如果你已经在使用 BusyBox，则不需要使用这个二进制文件，因为 BusyBox 包含了 ping 命令。

要了解有关 inetd 使用的更多信息，请查看 netkit-base 软件包中 inetd 目录下的手册页。

### xinetd

在某些系统中，xinetd 比 inetd 更受青睐，因为它允许某些安全授权，提供广泛的日志记录功能，并且可以防止拒绝服务攻击等。虽然 xinetd 项目网站上的常见问题解答 (FAQ) 包含了它相对于 inetd 的优势完整列表，但简而言之，只有当你的嵌入式系统被设计为提供广泛的网络服务或处于如 Internet 这样充满敌意的网络环境中时，你才应该使用 xinetd 超级服务器。

