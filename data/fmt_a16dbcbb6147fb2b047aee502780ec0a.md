
网络配置需要进行定制，以确保使用了正确的 IP 地址。可以使用 DHCP 服务器，只要能保证服务器提供的 IP 地址与我们服务器上 `BOOT` 返回的相同即可。

在 SuSE 上，IP 地址设置在 `/etc/rc.config` 中：

```
IP_ADDR_0="192.168.0.77"

IPCONFIG="*192.168.0.77 broadcast 192.168.0.255 netmask 192.168.0.255 up"
```

# 第 22 章

RedHat 和 Mandrake Linux 需要对 `/etc/sysconfig/` 以及网络启动脚本 `sysconfig/network-scripts/ifcfg-eth0` 进行类似的更改。在 Slackware Linux 上，该文件是 `/etc/rc.init`。

建议编辑客户端根文件系统上的 `hosts` 文件，以包含客户端的地址和所用服务器的地址。这可以加快电子邮件等服务的名称解析速度。理想情况下，你应该在为客户端池系统制作副本之前，将所有客户端都添加到服务器的 `hosts` 文件中，这样所有客户端都拥有其他客户端的地址。

剩余工作的大部分集中在精简 Linux 启动和关机时启动与停止的服务上。所有不必要的的服务都应该从启动脚本中删除。这需要手动完成，但在 SuSE 上，只需编辑脚本并恰当地设置服务变量即可。在 RedHat 上，我们需要从 `/etc/rc.d` 目录中删除不需要的脚本。

一旦你创建了一组定制的启动脚本，你就应该能够将客户端无盘系统一直启动到多用户配置，并获得登录提示！

## 问题

根据你所使用的发行版，你可能会在启动和关闭无盘客户端时遇到某些困难。

一个需要注意的关键点是在 NFS 挂载执行之前使用位于 `/usr` 中的文件。在那个之前，你的客户端没有可用的 `usr`！过去的“违规者”包括在启动序列中使用 `linuxconf` 的 RedHat，以及在启动系统时使用 `loadkeys` 的 SuSE。这两个程序都存储在 `/usr` 中。另一个潜在问题是 `spec.locked`，它几乎恰好在 NFS 挂载执行时被使用。

纠正此问题的简单方法是在客户端根文件系统中创建一个 `usr` 目录，并在 NFS 挂载完成之前复制你发现需要的任何文件。NFS 挂载仍会发生，这将隐藏你复制的文件，但在服务器上会创建“真实”副本。

关闭 Linux 机器也可能是一个问题 - 因为问题在于顺序。Linux 会尝试在完成根文件系统处理之前挂载所有的网络文件系统。为了避免这种情况，最简单的方法是删除 `/etc/rc.d` 目录中的 NFS 停止脚本。通常你会删除 `S99` 和 `rcS`，它们是目标为在 Linux 停止或重启时执行的脚本。

你可以在以太网主页 http://etherboot.sourceforge.net 找到一些链接。还有一个针对无盘系统的 HOW 文档。位于 http://www.ltsp.org 的 Linux Terminal 项目提供了关于配置无盘客户端的信息。最后，如果你需要，http://disklessstations.com 可以提供合适的以太网。

## 客户端应用程序

一旦你有了基本的无盘系统，就可以开始配置应用程序。也许有用的是 X Window 系统。

如果你的发行版已经在 `/etc` 或 `/usr` 任何地方使用了 X 配置，应该像正常安装一样运行。然而，你必须为客户端制作服务器。

例如，如果你的服务器拥有 ATI Mach64 显卡，它可能需要 Mach4 X 服务器。如果你的客户端拥有 Mat 显卡，你需要 SVGA X 服务器。这需要安装在服务器上，并位于 `/usr/X11/bin`，以便 X 程序找到它。

我们没有在客户端上启用任何交换空间。这是因为目前使用 NFS 进行交换仍然是实验性的。目前，我们需要确保客户端有足够的内存运行我们想要运行的应用。如果内存不足，Linux 将开始关闭我们的应用程序。

假设我们要运行 X 并使用 Netscape 浏览网页；在 32Mb 内存是可能的。你可以通过选择更简单的应用程序来精简 X 安装的使用：

- 使用 `rxvt` 代替 `xterm`
- 使用 `icewm` 代替 KDE 或 Enlightenment
- 使用较小的 X 安装

另一种避免客户端内存消耗的方法是在服务器上运行应用程序，仅将客户端显示——换句话说，作为一个 X 终端。要做到这一点，你必须首先开启会话连接，然后登录服务器并使用 `DISPLAY` 环境变量启动应用程序：

```
$ xhost +
telnet server
export DISPLAY=client:0
netscape &
```

通过适当的服务器配置，单行即可远程调用 Netscape：

```
$ rsh /usr/local/bin/netscape -display client:0
```

无盘 Linux 系统可以用于许多应用程序——每天都会出现新用途。这些包括：

- 网络防火墙
- 路由器或桥器
- 工作站
- X 终端
- Java 工作站
- 机顶盒

希望我们鼓励了你探索无盘操作提供的可能性。无盘应用可能很快为你附近的一台旧 PC 注入生命！

在本章中，我们学习了如何配置服务器、创建启动镜像，并编译适用于无盘系统的 Linux 内核。最后，我们学习了如何从 X 终端使用无盘 Linux 系统，这是许多可能应用之一，包括防火墙、路由器、Java 工作站和静默浏览器。

![](img/930f7611cac03a5cd5573f4bb94fd7b9_847_0.png)

在 http://www.p2p.wrox.com 上的在线讨论

# 第 23 章

## XML 和 libxml2

XML，或者说它的全称可扩展标记语言（Extensible Markup Language），目前是一个非常热门的话题。在计算机媒体的任何地方你都能看到 XML 被提及，而且它经常与 SAX、XSLT、DOM、DTDs 等许多其他相关缩写放在一起。翻阅书目录，你还会看到大量关于 XML、SGML 以及相关主题的书籍。

当我们与 Wrox 讨论这本书的性质和内容，以及我们打算作为演示每章某些技术载体的示例应用程序时，我们需要为我们的 DVD 目录准备一些示例数据。Wrox 立即向我们发送了一些 XML 格式的示例数据（感谢 DanM！）。为了让你感受一下，这里是 `dvdcatalog.xml` 的开头（顺便说一下，价格是虚的！）

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes" ?>
<!DOCTYPE catalog [dvd+]>
<!ELEMENT dvd (title, price, director, actors, year_made)>
<!ATTLIST dvd
  id CDATA #REQUIRED>
<!ELEMENT title (#PCDATA)>
<!ELEMENT price (#PCDATA)>
<!ELEMENT director (#PCDATA)>
<!ELEMENT actors (actor+)>
<!ELEMENT actor (#PCDATA)>
<!ELEMENT year_made (#PCDATA)>
```

```xml
<dvd asin="0780020707*">
<title>Grand Illusion</title>
<price>29.99</price>
<director>Jean Renoir</director>
<actors>
<actor>Jean Gabin</actor>
</actors>
<year_made>1938</year_made>
</dvd>
<dvd asin="0780020685*">
<title>Seven Samurai</title>
<price>27.99</price>
<director>Akira Kurosawa</director>
<actors>
<actor>Takashi Shimura</actor>
<actor>Toshiro Mifune</actor>
</actors>
<year_made>1954</year_made>
</dvd>
```
