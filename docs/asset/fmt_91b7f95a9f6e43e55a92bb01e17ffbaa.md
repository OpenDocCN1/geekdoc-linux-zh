
如果你在外出时没有打印机，但需要硬拷贝输出，有一些替代方案。首先，你随时可以光顾当地的打印或复印中心，将你的文档放在软盘上进行复制，或者付费使用打印机。另一个替代方案，尽管不是分辨率最好的，是将你的文档传真到传真机上。Linux 支持使用多种软件包（如 `efax`、`mgotty+sendfax`，或针对 SuSE Linux 用户的 `HylaFax`）发送和接收传真。

> **iBook 支持**
>
> 为了使用 iBook 的内部调制解调器，你必须使用 Apple 的 OpenFirmware 启动提示和 `Yaboot` 启动工具启动 Yellow Dog Linux。然后你可以使用调制解调器通过 Linux 传真软件发送或接收传真。

如果你拥有拨号互联网访问权限，你可以尝试互联网全球传真服务。访问 `http://linux.codema.com/tc/csmtp.html` 并阅读有关如何发送传真的详细信息。使用此服务，你可以通过电子邮件将传真文档发送到世界几乎任何地方的传真机。发送传真非常简单：

```
remote-printer.recipients_name@faxnumber.odd.tpc.int
```

在此示例中，收件人名称是你希望接收传真的那人的名字。传真号码必须是完整的 10 位数字。并非所有美国区号都受支持。例如，如果你想给一位名叫 Joe Piccolo 的人发送传真，并且你知道他在华盛顿特区的传真号码，请编写你的电子邮件文档，然后将消息发送到

```
remote-printer,Joe_Piccolo1@2025551212;1664.tpc.int
```

你的收件人的传真机将收到一张封面页，连同你的电子邮件消息。要获取当前支持此免费服务的世界区号列表（以及你可以用于发送图形和文本的 Linux 客户端链接），请访问 `http://www-usa.tpc.int/fax_cover_auto.html`。

### 打印到远程 Linux 打印机

打印到网络打印机是另一种替代方案，配置远程 Linux 打印机非常容易。首先，连接打印机的远程计算机应具有配置正确的 `/etc/hosts.lpd` 文件。此文件包含允许本地打印的远程计算机的主机名（或 IP 地址）。例如，如果你家庭办公室的局域网中有一台名为 `lp.service.org` 的计算机，请编辑该计算机的 `/etc/hosts.lpd` 文件并添加你想授予打印权限的计算机的 IP 地址或主机名，如下所示：

```
192.168.2.32
apltiva.service.org
green.service.org
laptop3.service.org
...
```

然后，你应该像这样重启 `lp.service.org` 上的 `lpd` 守护进程：

```
# /etc/rc.d/init.d/lpd restart
```

如果你的笔记本电脑主机名是 `laptop3.service.org`，你将被允许打印到连接在 `lp.service.org` 上的打印机。为了打印到 `lp.service.org` 上的打印机，你需要知道打印机的名称，例如 `green`（其下会有 `/var/spool/lpd/green` 目录下的暂存目录），并且知道 `green` 例如是一台 HP 400。在你的笔记本上运行 Red Hat `printtool` 客户端，然后单击“添加”按钮。你会看到图 14.1 中所示的对话框。单击“远程 UNIX (lpd) 队列”按钮，然后单击“确定”。你会看到如图 14.4 所示的“编辑远程 UNIX (lpd) 队列条目”对话框。

输入你想为远程 HP 400 打印机使用的名称，例如 `remoteHP400`。接下来，输入远程主机的名称，例如 `lp.service.org`，以及远程主机上远程打印机的名称，例如 `green`。完成后，单击“选择”按钮，并配置远程条目以匹配远程主机上名为 `green` 的打印机。例如，如果远程打印机是使用黑白墨盒的 HP 400，请为你的过滤器配置单色 HP 400。完成后，单击“确定”。然后再次单击“确定”以退出配置和打印机条目对话框。你应该使用 `printtool` 的 `lpd` 菜单来重启 `lpd`。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_351_0.png)

> 图 14.4 使用 `printtool` 的“编辑远程 Unix 打印机”对话框为你的笔记本创建一个远程打印机条目，并选择额外的输入过滤器选项。

现在，你可以使用 `lpr` 命令的 `-P` 选项，配合打印机名称（如 `remoteHP400`），从你的笔记本打印到计算机 `lp.service.org` 上名为 `green` 的打印机，如下所示：

```
# lpr -PremoteHP400 mydocument.txt
```

只要 `lp.service.org` 正确连接到互联网，就可以通过局域网或从世界任何地方实现此操作。

### 打印到共享 Windows 打印机

你还可以使用 Red Hat `printtool` 客户端为连接到运行 Windows 的远程计算机上的共享打印机创建一个本地打印机条目。你需要知道计算机的 IP 地址或主机名，知道远程打印机的名称，拥有远程计算机的有效用户名和密码，并知道远程计算机的工作组名称或域名称。之后，配置方法与远程 Linux 计算机相同，你可以轻松地使用 `lpr` 命令及其 `-P` 选项，后跟你的远程打印机条目名称，打印到远程计算机。

#### 资源信息

`http://www.astart.com/lprng/LPRng.html`

Linux 替代打印队列系统 `LPRng` 的主页。

#### 打印 HOWTO

Grant Taylor 关于如何配置和使用 Linux 打印的信息。通常可以在 `/usr/doc/HOWTO` 目录下找到，不过最新的副本（与几乎所有章节型文档一样）可以在 `http://www.linuxdoc.org` 上找到。

#### IR（红外）HOWTO

`http://home.sndf.de/wehe/ir_misc.html`

一个详尽的设备表格，列出了包括笔记本电脑在内的可以使用 Linux 和 IrDA 的设备。

Werner Heuser 对 Linux IrDA 项目的总结，其中包含在 Linux 下使用 IrDA 的技巧和应用。可以在最新 Linux 发行版的 `/usr/doc/HOWTO` 目录下或 `http://www.linuxdoc.org` 上找到。

`http://www.creative-it.com/linux/irda/toshiba_irda_howto.html`

Guenther Wieser 针对东芝笔记本用户关于使用 IrDA 和 Linux 的具体说明。

`http://www.physiol.usyd.edu.au/daved/linux/bjc-80.html`

对于希望使用 IrDA 进行打印的 CanonBJC-50 和 BJC-80 移动 Linux 用户来说，这是最佳的入门起点。

`http://www.linuxworld.com/linuxworld/lw-1999-06/lw-06-hylafax_p.html`

一篇关于使用 `HylaFax` 的文章，附带有关互联网传真侧边栏信息。

## 第 15 章：在路上建立连接

- 拨号连接
- DSL 连接
- 无线连接
- 网络连接策略
- 免费服务
- 资源信息

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_354_0.png)

本章向你介绍各种技术和软件，使作为移动 Linux 用户的你能够在旅途中连接到你的互联网服务提供商（ISP）和互联网。你还将了解沿途可用的不同技术以提供帮助。本章首先展示一些通常随 Linux 提供的常见互联网连接工具，以及常见的互联网连接方式。然后，它指引你找到其他新技术和技术的来源，这些技术可以在你穿梭于办公室、家中、仓库或乡村时提供帮助。

### 拨号连接

调制解调器是连接互联网最常用的工具。随着其他技术（如数字用户线路服务 `DSL` 和蜂窝电话公司）在市场上争夺连接份额，这一状况将维持多久尚待观察。然而，目前内置、外置或 PC 卡调制解调器仍然是移动 Linux 用户的首选标准连接硬件。本节向你展示使用 Linux 软件连接 ISP 的三种方法。

拨号互联网连接使用点对点协议 `PPP` 通过串行线路提供网络服务和信息。一种先行的协议，串行线路接口协议 `SLIP`，曾经很流行，但现在似乎已失宠。`PPP` 在 Linux 下得到很好的支持。当你通过调制解调器与你的 ISP 连接时，Linux 会创建一个名为 `ppp0`（针对第一个 PPP 设备）的接口，几乎每个 Linux 网络实用程序或互联网程序都通过这个新接口进行通信。当你结束连接时，Linux 从内存中移除 `ppp0` 接口。

#### 配置

你的第一项工作是确定你的 PC 卡或内置调制解调器在笔记本上连接到哪个串行端口。如果你使用外置调制解调器，你可能需要一个调制解调器电缆，一端是 `DB-25` 连接器，另一端是母 `DB-9` 插头（适合大多数笔记本电脑上的公 `DB-9` 串行连接器）。
