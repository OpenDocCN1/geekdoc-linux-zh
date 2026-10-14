


## Networking

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_93_0.png)

### Strange things can happen when clocks aren't synchronised!

WINS，微软对 NetBIOS 名称服务的实现，它为 NetBIOS 名称提供与 DNS 为域名提供的类似服务（将主机名映射到网络地址）。没有 WINS 服务器也能解析名称，但仅限于本地子网——如果客户端无法通过 WINS 服务器解析 NetBIOS 名称，则会退而在网络上广播“你在吗？”消息。这就是系统管理员讨厌 NetBIOS 的原因之一，也是除非你真的需要它否则应将其禁用的原因。你也可以在互联网上读到大量关于 NetBIOS 不安全的内容。

> “你可以在互联网上读到大量关于 NetBIOS 不安全的内容。”

### Password management

这是 Active Directory 设置与经典设置不同的第一个领域。经典 Samba 使用自己的密码数据库，其中包含加密的密码，但由于文件权限与 Unix 用户和组相关，因此这些与服务器上的用户直接相关。Active Directory 用户与 Unix 用户无关（稍后会详细介绍）。要向经典 Samba 添加用户：

```
smbpasswd -a myuser
New SMB password:
```

### Quick tip

升级用户应注意 **smbpasswd** 文件在内部已更改，因此在 Samba 3.x 和 Samba 4 之间不可移植。

```
Retype new SMB password:
Forcing Primary Group to 'Domain Users' for myuser
Forcing Primary Group to 'Domain Users' for myuser
Added user myuser.
```

请注意，一旦用户已添加到 Samba，Windows 将要求输入其密码——即使是访客共享。添加用户特定的共享，例如主目录，可以通过在 **smb.conf** 中添加条目来实现：

```
[myuser]
    comment = %U home directory
    writable = yes
    valid users = myuser
    path = %H
```

或者，更普遍地使用特殊的 **[homes]** 共享，它为每个用户创建主目录共享。当用户尝试连接共享时，Samba 会查找像上面那样的显式共享定义。如果未找到，但存在 **[homes]** 共享，则该共享将像模板一样使用以创建用户请求的共享。下面显示了一个合适的示例；browsable 条目可防止在浏览共享时出现 **[homes]**。

```
[homes]
    comment = %U home directory
    writable = yes
    browsable = no
```

另一种特殊类型的共享是 **[printers]**。顾名思义，这允许 Windows 客户端使用连接到 Samba 服务器的打印机。它使用 CUPS 来排队原始打印作业，这意味着客户端需要安装适当的打印机驱动程序。它将转换为打印机可以处理的原始数据。打印需要设置了粘滞位的 **spool** 目录：

### Windows 7 test client

需要一台运行 Windows 的计算机来完全评估 Samba 4 的 Active Directory 功能。我们安装了 Windows 7 Ultimate Service Pack 1 以及远程服务器管理工具。

从这些工具中，你需要的是 Active Directory 用户和计算机（可执行文件名是 **dsa.msc**）。请参考相关的 Microsoft 网页以获取有关安装这些工具的更多信息：

- **Windows 7 Service Pack 1:** www.microsoft.com/en-us/download/details.aspx?id=5842
- **Windows 7 RSAT:** www.microsoft.com/en-gb/download/details.aspx?id=7887

如果你希望 Windows 机器响应 ICMP Ping 请求，你需要向 Windows 防火墙添加适当的规则（或完全禁用防火墙）。

要添加规则，请转到“开始 > 控制面板 > 系统和安全 > Windows 防火墙 > 高级设置 > 入站规则 > 新建规则”。为 ICMPv4 协议创建自定义规则。请记住，Windows 的家庭版和入门版无法加入域。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_93_1.png)

对于 Active Directory 用户和计算机，搜索“dsa.msc”并以管理员身份运行。


