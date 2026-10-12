

2. 运行 `iconfig` 命令，使用适当的**地址**、**子网掩码**和**广播地址**来配置 `eth0:0` 设备。例如，若要配置 `eth0:0` 上的 `192.168.1.42` 设备，请使用以下命令：

```bash
iconfig eth0:0 192.168.1.42 netmask 255.255.255.0 broadcast 192.168.1.255
```

3. 欺骗 ARP 表。你需要以太网卡的硬件地址来执行此操作。运行 `iconfig -a` 命令以获取此信息。假设你的以太网卡硬件地址是 `00:10:4B:CB:15:9F`，请输入以下命令：

```bash
arp -s earth 00:10:4B:CB:15:9F pub
```

在建立了虚拟 IP 地址后，你现在需要创建一个类似主站点的配置。在本示例中，我假设你将新的配置文件放在了 `/etc/vsftpd.earth.conf`。你可以决定为此创建一个新的目录结构，或者与现有配置重叠。我们将利用两个功能使这一切协同工作。第一个功能是能够在命令行上向 `vsftpd` 传递你希望其使用的 `config` 文件的名称。第二个功能是在 `xinetd.conf` 中使用 `bind` 指令将实例限制到特定的 IP 地址。

```text
service ftp
{
    disable = no
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/vsftpd
    nice = 10
    bind = 192.168.1.41
    server_args = /etc/vsftpd.main.conf
}

service ftp
{
    disable = no
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/vsftpd
    nice = 10
    bind = 192.168.1.42
    server_args = /etc/vsftpd.earth.conf
}
```

### 专家解答

**问：** 为什么在 FTP 中，每个虚拟服务器都需要一个独立的 IP 地址，而像 HTTP 这样的其他协议则不需要？

**答：** HTTP 实际上会将统一资源定位符 (URL) 作为请求的一部分进行传递。域名可以从 URL 中提取，服务器可以相应地对该信息进行处理。FTP 协议的设计不支持向服务器传递 URL；因此，服务器确定原始请求指向何处的唯一方法是基于请求到达的 IP 地址。

使用类似的配置，**xinetd** 将根据连接进入的接口，使用不同的配置文件启动 **vsftpd**。修改其配置后，别忘了重启 **xinetd**。

### 进度检查

- 1. 为什么从 20 端口连接时的默认值为 “no”？
- 2. 你如何更改日志文件写入位置的选项？

## 项目 11-1 设置你的 FTP 服务器

既然你已经掌握了基础知识，你应该没有理由无法让你的 FTP 服务器正常运行。本项目将引导你完成这一过程，但在阅读完前面几节内容后，这一切看起来应该像是一次简单的复习。

### 分步操作

- 1. 按照前面所述设置 **xinetd**。最简单的方法是使用你喜欢的文本编辑器编辑文件 `/etc/xinetd.d/vsftpd`，并将 disable 指令设置为 "no"。
- 2. 现在将你的编辑器指向 **config** 文件 `/etc/vsftpd.conf`。检查默认配置设置，看看它们是否适用于你的情况。特别注意 **anonymous_enable** 和 **local_enable**。如果你对某个特定选项不确定，请回顾前面的章节或 man 手册页。
- 3. 检查 `/etc/hosts.allow` 和 `/etc/hosts.deny` 中的设置，以确保它们适合你的配置。
- 4. 通过输入 `/etc/init.d/xinetd restart` 来重启 **xinetd**。
- 5. 通过尝试登录来测试你的服务器。最简单的方法只是在命令行上输入 **ftp localhost**，并在提示时提供适当的用户名和密码。

### 项目总结

**vsftp** 服务器非常简单，易于设置和运行。大多数配置值都具有合理的默认值。务必测试你的服务器，如果某些东西未按预期工作，请仔细检查你的配置。

### 模块总结

Very Secure FTP 守护程序 (**vsftpd**) 是一个功能强大的 FTP 服务器，提供了以安全方式运行商业 FTP 服务器所需的所有基本功能。本模块讨论了配置 **wu-ftpd** 服务器的过程。具体涵盖了以下主题：

- **vsftpd** 最重要的配置选项
- FTP 协议的详细信息及其对防火墙的影响
- 建立虚拟 FTP 服务器
- 设置匿名 FTP 服务器
- 设置仅限普通用户的 FTP 服务器

这些足以让你的 FTP 服务器平稳运行很长一段时间。当然，像任何关于软件的印刷媒体一样，本文档会逐渐过时，信息最终也会变得过时。请务必不时访问 **vsftpd** 网站 (http://vsftpd.beasts.org)，以了解最新的进展和文档。

![](img/ec2066d370d3af1a767664d36aa7ddfe_380_0.png)

## 模块 11 掌握度检查

- 1. 被动传输与主动传输有何不同？
- 2. 你应该如何检查 FTP 服务器是否安全，以及为什么这很重要？
- 3. 控制谁可以访问你的服务器有两种不同的方法是什么？
- 4. 匿名登录时请求的密码是什么？
- 5. 判断正误？当客户端发出传输文件的请求并初始化数据连接时，控制连接会立即关闭。
- 6. 判断正误？`pasv_enable` 选项启用被动模式，其默认值为 “yes”。
- 7. 什么是 FTP？
- 8. Red Hat 为什么选择使用 `vsftpd`？
- 9. `vsftpd` 的文档文件在哪里？
- 10. 用于配置 FTP 服务器的 `ftpd_banner` 选项是什么？
- 11. 为什么 `anon_world_readable` 的默认值仅设置为 “yes”？
- 12. 设置配置选项 `userlist_enable` 允许服务器做什么？
- 13. 你希望明确允许或拒绝访问的主机名称应放在哪里？
- 14. 被动模式为什么很重要？
- 15. `vsftpd` 支持虚拟 FTP 服务器吗？
- 16. `vsftpd` 可以作为独立守护程序运行吗？

# 模块 12
使用 Apache 设置你的 Web 服务器

## 关键技能

- 12.1 解释 HTTP 的机制
- 12.2 设置 Apache HTTP 服务器
- 12.3 配置 Apache
- 12.4 使用 Apache 进行基本故障排除

在本模块中，我将讨论在你的 Linux 服务器上安装和配置 Apache HTTP 服务器 (http://httpd.apache.org) 的过程。Apache 是在其自己的类伯克利软件分发 (BSD) 许可证下发布的免费软件。根据网络上最受尊敬的统计数据之一（由 Netcraft Ltd. 发布，http://www.netcraft.com/survey），Apache 的市场份额超过 60%。来自互联网社区的这种尊重源于 Apache 服务器软件提供的以下好处和优势：

- 它很稳定。
- 包括 www.amazon.com 和 www.generalelectric.com 在内的几个主要网站都在使用它。
- 整个程序和相关组件都是开源的。
- 它适用于大量平台（所有流行的 UNIX 变体，一些不太流行的 UNIX 变体，甚至 Windows）。
- 它极其灵活。
- 它已被证明比大多数替代方案更安全。

在详细介绍配置 Apache 所需的步骤之前，我将回顾超文本传输协议 (HTTP) 的一些基础知识，以及 Apache 的一些内部工作原理，例如其进程所有权模型。这些信息将帮助我们理解为什么 Apache 被设置为按此方式工作。

> **注意**
> 虽然术语 "Apache" 长期以来一直被松散地用于指代 Apache 基金会的 **httpd** 服务器，但 Apache 基金会已开始拓展到其他许多编程领域。其其他程序通常以其全名称呼，例如 "Apache FOP" 或 "Apache Jakarta"。Apache 基金会的其他项目超出了本书的范围，因此每当我将某个程序称为 "Apache" 时，你可以肯定我指的是 **httpd** 服务器。有关 Apache 基金会的更多信息，请参阅 http://www.apache.org。

## 关键技能 12.1 解释 HTTP 的机制

超文本传输协议 (HTTP) 当然是万维网基础的重要组成部分，而 Apache 是 HTTP 协议的服务端实现。像 Netscape Navigator、Mozilla、Opera 和 Microsoft Internet Explorer 这样的浏览器是 HTTP 的客户端实现。

