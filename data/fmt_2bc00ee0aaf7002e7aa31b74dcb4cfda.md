
```
EXTRA_CFLAGS=
EXTRA_LDFLAGS=
EXTRA_LIBS=
EXTRA_INCLUDES=
EXTRA_DEPS=

#CC=		gcc
#CPP=
#OPTIM=

#RANLIB=

TARGET=htpssd

#
# SSL Related stuff. N.B. This is set up to use the SSLsay
source, NOT an
# installed version.
#
#KEYNOTE_BASE=/home/ben/work/KeyNote
SSL_BASE=/usr/local/etc/openssl-1.0.9.6
SSL_INCLUDE= -I$(SSL_BASE)/include
SSL_CFLAGS= -DAPACHE_SSL

SSL_LIB_DIR= $(SSL_BASE)
SSL_LIBS= -L$(SSL_LIB_DIR) -lssl -lcrypto
SSL_APP_DIR= $(SSL_BASE)/apps
SSL_APP=/usr/local/etc/openssl-1.0.9.6/apps/openssl
```

10. 运行 `./Configure` 例程。

11. 输入 `make`。

12. 在 `make` 命令执行后，你应该将二进制文件复制到之前复制 `httpd` 文件相同的位置。输入 `cp htpssd ../`

### 编辑 htpssd.conf 配置

就像之前设置并用于配置常规 apache Web 守护进程的 `httpd.conf` 文件一样，应该有另一个 `htpssd.conf` 文件，它确定安全 Web 守护进程的运行方式。在 `htpssd.conf` 文件中，你必须指定一个特定的端口号。与运行在端口 80 下的常规 `httpd` 守护进程不同，安全 Web 事务通过端口 443 运行。你可以在此文件中进行这些特定修改。

以下列表解释了如何正确安装安全 Web 守护进程配置。

1. 从示例 OpenSSL/`httpd.conf` 文件中复制选定的行（如下所示），并将它们添加到 `/usr/local/etc/apache-ssl/conf/` 中列出的 `htpssd.conf` 文件中。

2. 将这些行添加到文件末尾，因为 Apache 从开头读到结尾，后面的设置会覆盖前面的设置：

```
SSLEnable
SSLCacheServerPath        src/modules/ssl/gcache
SSLCacheServerPort        logs/gcache_port

SSLCertificateFile        /usr/local/ssl/certs/thawte_test.cert
SSLCertificateKeyFile     /usr/local/ssl/private/quasi.
                          gnuware.com.key

SSLVerifyClient    0
SSLVerifyDepth     2

SSLSessionCacheTimeout   300
```

3. 检查工作服务器上的 `httpd.conf` 文件，确定你需要更改什么。你可能需要将端口号更改为 443，而不是端口 80。

4. 通过发出以下命令启动安全服务器：

   `/usr/local/etc/apache-ssl/httpd -f /usr/local/etc/apache-ssl/conf/httpsd.conf`。

5. 在提示时输入你的 PEM 短语。

如果你完成这些步骤后一切看起来正常，你将能够编码 Web 页面并安全地向你自己或他人传输信息进行处理。

### 结论

既然你现在可以设置网络连接，你会迫切地想使用你的调制解调器、电缆调制解调器或任何其他连接到 ISP 或提供互联网连接的另一个 Linux 箱子的设备创建类似的拨号连接。下一章还将查看用于连接到 Internet 的各种 Linux 程序。就像提供给 Windows 用户的众多免费软件一样，大量的 Linux 应用程序为 Linux 用户提供了相同的功能，无论是在 X 会话中还是在控制台上。

### 互联网连接

前一章讨论了如何配置局域网互联网连接。设置有效的 IP 地址需要资金投入和特定用途，并非所有 Linux 用户都能负担得起一个可用的静态 IP 地址。在这些情况下，必须有一些其他方法来提供有效地址，以便连接到互联网或其他网络。本章将探讨如何设置调制解调器连接以及建立家庭与办公使用之间的链接。在这里，学习如何以有限带宽将单独机器相互连接是一个先例，同时还包括优化当前可用的 Linux 软件，以建立从小型网络到大型网络的连接。

本章将处理以下主题。

- 在 Linux 下设置调制解调器
- 创建独立的 PPP 服务器
- 允许多台机器使用 `ipchains` 优化一个连接
- 选定的防火墙问题
- 为互联网使用配置浏览器
- 使用基本 FTP 命令和远程获取信息

#### 使用拨号连接

尽管家庭带宽的增加越来越受欢迎，更多普通用户正在设置 DSL（Dedicated Server Line，专用服务器线路）、电缆调制解调器和 ISDN 线路，但仍有许多普通用户只能负担得起拨号调制解调器连接。正如免费托管服务和依赖家用电脑和标准调制解调器来连接到其服务的商业 ISP（Internet Service Providers，互联网服务提供商）的流行度所证明的那样，调制解调器仍然构成了用户连接到互联网的大部分方式。

随着 Linux 日益流行，更多人用自己的 Linux 版本替换默认操作系统，对 Linux 下易于的调制解调器配置的需求将会增加。此外，一旦这些机器连接好，它们就可以通过 IP 伪装（IP masquerading）使用一个简单的调制解调器连接来建立其他联网机器到互联网的访问。这种优势并非没有危险。随着越来越多的人从家里使用他们的机器连接到互联网，并且他们的连接时间增加，有些人会利用任何安全漏洞并危及无辜机器。本章还将讨论如何防止最侵入性的攻击，针对那些 24/7 连接的用户。有关增强 Linux 安全的更多信息，请参见第 19 章。

##### 确定 Linux 调制解调器

现在你已经安装了 Linux 并体验了系统包含的各种功能，你很可能想要收集更多信息并开始分享你学到的东西。除了与本地用户进行网络交流外，与他人联系的最佳方式之一是使用调制解调器连接到互联网。这意味着你可以访问电子邮件、阅读和发布新闻组、使用 Telnet 和 FTP 与其他服务器通信，并且对许多 Linux 用户来说最重要的是浏览互联网网站。

为了消除由竞争者延续的一些神话，Linux 提供的互联网访问资源与其他操作系统一样多，甚至更多。事实上，最新的统计将 Linux 列为首选的网站提供商。其余使用 Solaris，另一个 UNIX 分支，以及微软的 IIS 服务器。

对于大多数目的来说，普通的标准调制解调器就可以工作得很好，但你应该为 Linux 采取一些预防措施。目前，建议你不要购买或使用 WinModem。WinModem 是为 Windows 使用而设计的，这些特定类型的调制解调器需要一个专有操作系统来访问正常运行所需的驱动程序。

有两种不同类型的调制解调器：硬件驱动调制解调器和软件使能调制解调器。WinModem 属于后者。由于大多数 WinModem 制造商没有发布运行其特定调制解调器所需的代码，Linux 开发人员无法将特定调制解调器驱动程序写入内核。目前正在努力将这些软件驱动的调制解调器移植到 Linux，但目前建议用户避免在 Linux 机器上安装任何专为仅在 Windows 下运行而设计的硬件。

> 注意
>
> PCTel 为 WinModem 特定的芯片组编写了软件驱动程序，特别是 HSP 仿真器。Lucent 也为其 WinModem 发布了驱动程序，但根据其文档，它仅适用于 Red Hat Linux，不适用于其他 Linux 发行版。这两家公司目前构成了将 WinModem 导出到 Linux 的研究主体。

##### 比较外置和内置调制解调器

购买硬件驱动调制解调器要容易得多，它内置了系统所需的所有驱动程序。Linux 查询调制解调器，发送必要的命令，然后建立握手和连接。你可以选择两种类型的硬件驱动调制解调器：外置和内置。每种都有优缺点。大多数人似乎更喜欢外置调制解调器，因为它易于访问，可以开和关，并且释放了主板上的 ISA 或 PCI 插槽。如果插槽有限且有几个其他外设设备，后者的优点可能至关重要。内置调制解调器对某些人有吸引力，因为它不需要外部输入或电源来开启或关闭，释放了一个 COM 端口，而且通常比外置调制解调器便宜。

Linux 似乎与内置调制解调器更兼容，并且更容易在机器之间传输这些调制解调器。（后者问题在你了解 IP 伪装以及一个 Linux 调制解调器如何与几台计算机共享后，变得无关紧要。）内置调制解调器工作得同样好。在某些情况下，重要的是你能够手动或在 BIOS 设置中配置 IRQ 和 COM 端口。尽管 Linux 现在支持有限版本的“即插即用”，但能够在卡上切换设置总是很好的，如果需要的话。然而，大多数调制解调器已经预留了内存地址和 IRQ 号码的范围专供其使用。
