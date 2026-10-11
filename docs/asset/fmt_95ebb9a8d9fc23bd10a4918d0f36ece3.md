
微软实际上从 3.5 版本开始就包含了在 Unix 服务器上打印的支持。NT 包含一个名为 `Microsoft TCP/IP Printing` 的工具，你可以在控制面板中进行操作：选择网络，然后是服务，最后点击添加。（你可以在《Mastering Windows NT Server》第 14 章中阅读更多相关信息。）但不用担心需要学习新技能——我打赌你以前已经做过了。你是否在网络上连接了带有 HP JetDirect 硬件的惠尔-惠普（Hewlett-Packard）激光打印机？（再次，如果没有，请参阅《Mastering Windows NT Server》第 14 章。）NT 只需指定其 IP 地址即可连接到任何服务器。一旦你这样做，你就可以像打印机通过并行线连接到服务器一样，在网络上共享打印机。因此，要将 Linux 打印机作为共享打印机，只需在 NT 服务器上添加 `Microsoft TCP/IP Printing` 模块，然后它就会告诉 NT 你有一台新打印机。当服务器询问它在哪个端口上（并行、串口或或其他）时，告诉它它是通过 TCP/IP 端口连接的，并填写 Linux 打印服务器的 IP 地址。此后，任何 Microsoft 网络客户端都可以共享该打印机。

## Samba：适用于 Linux 的微软网络

在我使用的所有软件中，使用频率最高的无疑是文件服务器（尽管电子邮件和 Web 协议竞争者）。Linux 有它自己的文件服务器系统，但如果没有交流对象，拥有出色的文件服务器协议也毫无价值；正如某人观察到的，“你知道我最佩服哪位推销员吗？就是那个发明第一个电话的人！”

如果 Linux 要与世界上其他地区的文件服务器共存，那么它需要能够与文件领域的巨头对话。当然，最大的巨头是微软——而 Linux 已经应对了这一挑战。通过运行名为 `Samba` 的工具，你可以将 Linux 机器直接置于微软网络的中心，所有其他系统都会认为 Linux 机器只是另一个微软文件服务器。此外，Linux 还包含了一些软件，让你的 Linux 不仅可以作为服务器，还可以作为客户端：Linux 包含两个工具，让你的 Linux 工作站在涉及微软文件服务器时表现得像 Windows 机器，让这些机器能够从微软文件服务器读取和写入文件。

（文件和打印）服务器各使用各自的协议，这些协议旨在快速运行，同时具有足够的安全性。Novel 世界多年来一直使用 `NetWare Core Protocol`（`NCP`），正如你已经读过的，大部分 Linux/Unix 世界使用网络文件系统（`NFS`）。自从 1985 年年中微软点对点网络最早出现以来，微软网络一直使用一种名为 `Server Message Block`（`SMB`）的协议。虽然它在多年间发生了一些变化，但每个版本都具有良好的向后兼容性，因此你基本上可以使用文件服务器客户端相同的语言与所有这些微软网络产品通信：

- Windows XP 和 .NET Server
- Windows 2000 Server 和 Professional
- Windows NT Server 和 Workstation
- Windows 9x
- Windows for Workgroups 3.11 和 3.1
- 适用于 DOS 6.x 的 Microsoft Workgroup Add-On
- Lantastic
- OS/2 LAN Server
- Microsoft LAN Manager

如你所见，许多服务器产品是使用或围绕 `SMB` 构建的。因此，Linux 社区中有人整合出一个可以作为 `SMB` 服务器或客户端的工具是理所当然的。这看起来没那么容易，很大是因为 `SMB` 并不是一个记录完善的协议——噢，是的，有书面文档和规范，但微软实际的客户端和服务器程序并没有遵循这些文档和规范。

一位名叫 Andrew Trigdell 的澳大利亚人需要一个适用于 Unix 的 `SMB` 兼容工具，并通过观察一个名为 `PathWorks` 的类似工具（它不是为 Unix 而是为 Digital 的 V 操作系统构建）来研究 `SMB` 是如何工作的。`PathWorks` 并没有告诉 Trigdell 他需要的所有信息，因此他在网络上放置了一个嗅探器，观察 Windows 机器与 NT 服务器通信时通过的数据包。凭借这些信息，他构建了后来成为 `Samba` 的早期版本。不久后，在 Sun 工作的 Jeremy Allison 也有类似的需求，于是 Trigdell 和 Allison 开始合作。从那以后，其他几个人加入了他们，组成了 `Samba` 开源项目。你可以在 `www.samba.org` 找到 `Samba` 的最新源代码，我看到的每个 Linux 发行版都带有某个版本的 `Samba`。

我提到可以从 `www.samba.org` 获取最新 `Samba` 是出于特定原因。`Samba` 的人员正努力保持与微软 `SMB` 协议的兼容，而该协议经常更改，即使在服务补丁包和热修复中也是如此。每当微软修复一个安全漏洞时，他们就可能会“破坏” `Samba`。有时你可以通过新版本的 `Samba` 来修复这种“损坏”，这意味着（这里是坏消息）学习如何编译和安装最新版本的 `Samba` 可能对你最有利。这与大多数 Linux 子系统形成对比，我认为，那些子系统提供了功能，但并没有新到让我无法等待我最喜爱的发行版提供带有新 Linux 子系统的新版本。

> **注意** Red Hat 7.3 包含了一个相当新的 `Samba` 版本，版本 2.2.3a。但你始终可以从 Red Hat 的 `http://www.redhat.com/apps/download/` 获取最新的 RPM。滚动到页面底部，你可以在那里搜索 RPM。

然而，即使是最新版本，你有时也会发现无法建立连接。（注：原始 OCR 文本似乎变得碎片化或重复）。

## SMB 客户端

正如你在第 5 章所读，Linux 喜欢组织所有的存储空间以便通过单树结构呈现。

## 使用 smbfs 挂载

正如你在第 5 章挂载光驱或软盘时看到的那样，我需要在 Linux 机器上创建一个目录作为挂载点。假设我为此目的创建了一个目录 `/ntshare`。

### Samba：Linux 上的微软网络连接

在那些类型正确的情况下，我可能只会得到一个 Linux 提示符并进入；`mount` 命令不会提供很多信息。与其使用 `%` 符号来指示密码，我也可以使用 `password=` 参数，如下面的另一种命令格式所示：

```
mount -t smbfs -o username=mminasi,password=swordfish
//ourserver/goodies/ntshare
```

现在，在上述两种情况下，我使用的 `mminasi` 账户是 `\SERVER` 的本地账户，`mminasi` 账户位于 `\SERVER` 的本地 SAM 文件中。但如果我想使用域帐户进行身份验证，我只需要一个正斜杠和域名——无论是新的类似 DNS 的活动目录（Active Directory）名称，还是旧式的 BIOS 名称——`neither` 还是 `smbfs` 都不知道如何找到我的账户。假设 `mminasi` 是名为 `acme.com` 的活动目录域上的账户，其 NetBIOS 名称为 `acme`，那么该命令的任何变体都将有效：

```
mount -t smbfs -o username=mminasi/acme,password=swordfish
//ourserver/goodies/ntshare
```

```
mount -t smbfs -o username=mminasi/acme.com,password=swordfish
//ourserver/goodies/ntshare
```

```
mount -t smbfs -o username=mminasi/acme.com%//ourserver/goodies
//ntshare
```

```
mount -t smbfs -o username=mminasi/acme.com%swordfish
//ourserver/goodies/ntshare
```

注意，至少在我看来，你不能使用 UPN 类型的登录名称，如 `mark@acme.com`，`smbfs` 似乎可以在挂载时通过。

注意，你不能在逗号后放置任何空格（例如 `username=mminasi` 和 `password=swordfish` 之间的那个），否则命令将无法工作，你会收到一条错误消息，告诉你你显然是一个不会使用 `mount` 的白痴。一旦执行了 `mount` 命令，当输入 `ls /ntshare` 时就会显示共享的内容。注意，与大多数 Linux 命令不同，服务器和共享名称是不区分大小写的。`-o` 指的是逗号分隔的选项，表 9.1 列出了这些选项，其中一个特别重要：
