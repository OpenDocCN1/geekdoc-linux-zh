
Stunnel是一个允许用户在SSL（安全套接字层）内部加密任意TCP连接的程序，在UNIX和Windows上均可用。Stunnel让用户通过由Stunnel提供加密而不改变守护程序代码的方式来保护非SSL感知的守护程序和协议（如POP3、IMAP、NNTP和LDAP）。Stunnel提供了inetd的相同功能，并增加了SSL加密。Stunnel还支持TCP Wrappers。

### OpenSSH/SSH

SSH（安全外壳）是一个用于登录远程机器和在远程机器上执行命令的程序。它在两个主机之间通过不安全的网络提供安全加密通信。它被描述为带有加密和RSA认证的R命令替代方案。

### GnuPG

GnuPG是PGP的替代品。由于它不使用专利的IDEA算法，因此可以无限制地使用。

# Linux 工具：日志和流量监控器

### MRTG (多路由流量绘图器)

多路由流量绘图器（MRTG）是一个用于监控网络链接上流量负载的工具。MRTG生成包含PNG图像的HTML页面，提供流量的实时视觉表示。MRTG由一个使用SNMP读取路由器流量计数器的Perl脚本和一个记录流量数据并创建代表被监控网络连接上流量的图表的快速C程序组成。

以下是MRTG的关键特性：

- 它是可移植的。
- 它附带一组使配置和设置变得非常简单的配置工具。
- 其生成的网页外观具有高度可配置性。

### Swatch

Swatch最初是为了主动监控通过UNIX syslog实用程序写入日志文件的消息而编写的。作为一个简单的演示，用户可以输入 `perl swatch --examine=FILENAME`，其中`FILENAME`是用户想要查看其内容的文件。

### Timbersee

Timbersee是一个与Swatch非常相似的程序。它使用正则表达式来监控日志文件中的重要消息，但其区别在于它可以同时监视多个日志文件，并且不会分出额外的进程。

### Logsurf

Logsurf被设计为实时监控系统上任何基于文本的日志文件。收集的大量日志信息（例如syslog守护程序处理的所有消息或信息服务的日志文件）使得手动检查日志以寻找异常活动几乎不可能。Logsurf实现了日志文件监控的自动化。

### IPLog

IPLog是一个TCP/IP流量记录器。它能够记录TCP、UDP和ICMP流量。其功能包括检测TCP端口扫描、TCP空扫描、FIN扫描、UDP和ICMP smurf攻击、虚假TCP标志（扫描器用于检测正在使用的操作系统）、TCP SYN扫描、TCP Xmas扫描、ICMP ping洪水、UDP扫描和IP碎片攻击的能力。它能够在混杂模式下运行并监控网络上所有主机的流量。它使用`libpcap`从网络读取数据，并且可以移植到任何支持`pthreads`且`libcap`能正常工作的系统。

### Ntop

Ntop是一个显示网络使用情况的网络流量探针，类似于流行的`top` UNIX命令所做的。Ntop基于`libpcap`，因此它可以在几乎每个UNIX平台以及Win32上运行。

Ntop的用户可以使用Web浏览器（例如Netscape）浏览Ntop（充当Web服务器）的流量信息，并获取网络状态转储。在后一种情况下，Ntop可以被视为一个带有嵌入式Web界面的简单RMON类代理。

### Linux安全审计工具 (LSAT)

Linux安全审计工具（LSAT）是用于Linux和UNIX的安装后安全审计员。它监控系统配置和系统上的网络设置，检查常见的安全/配置错误以及不需要的包。LSAT的所有模块都是用C编写的。LSAT软件包中的一些模块如下：

- `checkdotfiles`：此模块检查系统上的forward、exrc、rhosts和netrc文件。
- `checkfiles`：此模块检查`/usr/var`目录中的文件是否具有root所有权，除了检查`/tmp`和`/var/tmp`是否设置了粘滞位之外。
- `checkftpusers`：此模块检查`/etc/passwd`中的所有帐户是否都在`/etc/ftpusers`中。
- `checkinetd`：检查`/etc/inetd.conf`或`/etc/xinetd.d/*`。
- `checkkbd`：检查在Linux下是否禁用了Ctrl+Alt+Alt+Del功能。它还检查在Solaris下是否启用了KEYBOARD_DISABLE。
- `checklogging`：一个简单的检查，以确保auth和authpriv日志设施已开启。
- `checkmodules`：检查以确保可加载内核模块已启用。
- `checknetp`：验证没有接口处于混杂模式。
- `checkopenfiles`：使用LSOV（如果LSOV已安装）检查系统上的所有打开文件。
- `checkpasswd`：此模块检查`/etc/passwd`中不需要的帐户。它还检查只有root的UID=0。
- `checkmd5`：对所有常规文件执行系统范围的MD5校验和，仅在-use -m开关时执行。

# Linux 安全对策

### 物理安全

- 将计算机锁在安全的地方。

### 密码安全

- 不要使用容易猜到的密码。
- 不要与另一个人共享你的帐户。
- 检查具有空密码的用户。

# 网络安全

- 默认情况下拒绝来自网络的访问。
- 停止所有未使用的服务，如 sendmail 和 NFS。
- 定期查看 `/var/log` 中的系统日志，特别是 `/var/log/secure`。

# Linux 加固步骤

以下是加固 Linux 的一些步骤：

1. 选择一个广泛使用且能及时发布安全更新的 Linux 发行版。
2. 预先规划文件系统的布局。
3. 不要安装不必要的软件包。
4. 更改默认密码并创建普通用户。
5. 禁用不必要的守护进程和网络服务。
6. 禁用通过 SSH 进行远程 root 登录。
7. 设置并启用 IPTables。
8. 配置与安全相关的内核参数。
9. 安装基于主机的入侵检测系统（HIDS）。
10. 应用最新的更新。
11. 精简所有已安装的软件。
12. 提高登录和用户的安全性。
13. 增加审计和日志信息。

### 章节总结

- Linux 正逐渐流行，并迅速成为一个稳定的工业级操作系统。
- 一旦获知目标系统的 IP 地址，攻击者就可以开始端口扫描，寻找系统漏洞以获取访问权限。
- Linux 有可用的密码破解工具。
- Linux 的嗅探器以及数据包组装/分析工具赋予了攻击者在处理其他操作系统时同样的优势。
- 特洛伊木马、后门和蠕虫在 Linux 环境中也很常见。
- 与其他系统一样，应建立一套完善的、集成的流程来应对存在的威胁。

## 复习题

1. 列出 Linux 操作系统的优点。
2. Linux 操作系统有哪些缺陷？
3. 什么是 Rootkit？
4. 在 Linux 中如何编译程序？
5. 描述 chroot 监狱的功能。
6. 描述 Linux 的文件和目录结构。
7. 描述用于导航 Linux 文件系统的命令。
8. 列出 IPChains 和 IPTables 之间的区别。

![](img/0c79e6db97822eb68322dfe40d8564fe_64_0.png)

## 动手项目

- 安装、配置并编译 Linux 内核。
  - 步骤 1：
    - 以 root 身份登录。
    - 运行 `cp linux-2.4.2.tar.gz /usr/src/`。
    - 运行 `cd /usr/src/`。
    - 检查 `/usr/src/linux` 中的旧内核源码。
    - 通过运行 `mv /usr/src/linux linux-X.X.X` 将当前版本移动为备份，以便将来使用。
    - 运行 `tar -zxvf linux-2.4.2.tar.gz`。
    - 通过运行 `mv /usr/src/linux /usr/src/linux-2.4.2` 移动新的内核源码。
    - 通过运行 `ln -s /usr/src/linux-2.4.2 /usr/src/linux` 创建指向新内核源码的链接。
  - 步骤 2：
    - 配置内核。
    - 在 `/usr/src` 中运行 `cd` 进入内核源码目录。
    - 如果您更喜欢文本模式，请输入 `make menuconfig`，但推荐 `xconfig`。
  - 步骤 3：
    - 返回命令行并输入 `make dep` 以进行内核编译。
  - 步骤 4：
    - 通过输入 `make clean` 清理编译过程中创建的所有文件（.o 或对象文件）。
  - 步骤 5：
    - 通过运行 `make bzImage` 创建可启动的 Linux 映像（实际的 Linux 文件）。
    - 通过运行 `make modules` 制作用于安装的新模块。
    - 完成编译后，输入 `make modules_install`。
