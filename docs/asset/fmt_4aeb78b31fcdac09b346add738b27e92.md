
除了通过直接编辑配置文件来配置 Samba，你还可以使用多种 GUI 工具。例如，`Webmin` 包含 Samba 配置选项，如图 12.3 所示。Samba 还包括一个名为 `Samba Web Administration Tool` 的工具，其功能与 `Webmin` 类似，但它是一个专门针对 Samba 的工具。要使用它，请输入 `http://servername:901` 作为 URL，其中 `servername` 是服务器的名称或 IP 地址。（不过，你必须首先启用 `SWAT`，这通常是通过在 `/etc/inetd.conf` 或 `/etc/xinetd.conf` 中添加条目来完成的，这两者在本章后面都有简要描述。）

![](img/10371fe30b7fdac23ef2ef30d5ffe738_321_0.png)

Samba 通常从 `/etc/rc.d` 目录树中的启动脚本运行。如果尚未存在，你应在 `/etc/rc.d/rc3.d` 和 `/etc/rc.d/rc5.d` 目录中创建适当的链接。在 Red Hat 系统上，以下命令应该有效，但你可能需要根据其他发行版调整这些路径名和文件名：

```bash
# ln -s /etc/rc.d/init.d/smb /etc/rc.d/rc[35].d/S91smb
```

如果你刚刚以这种方式配置了 Samba，你需要手动启动它，或者在修改其配置后重启它。分别可以通过输入 `/etc/rc.d/init.d/smb start` 或 `/etc/rc.d/init.d/smb restart` 来实现。

## 设置全局选项

Samba 包含许多全局选项（即出现在 `smb.conf` 文件中 `[global]` 部分的选项）。此处列出了其中一些最重要的选项：

```text
[global]
    workgroup = ARBORETUM
    netbios name = GINKGO
    server string = Big Server
    encrypt passwords = Yes
    os level = 1
    preferred master = No
    domain master = No
    hosts allow = 192.168.34.
```

这些选项的含义如下：

- `workgroup`（工作组）：Windows 网络按工作组组织，工作组是共享相同工作组名称的计算机集合。该名称由 `workgroup` 参数指定。如果你不将此参数设置为匹配你网络的工作组，可能无法访问 Samba 服务器。（许多 Windows 网络使用域而非工作组。域也有名称，同样使用 `workgroup` 参数进行设置。）

- `netbios name`（NetBIOS 名称）：计算机的 NetBIOS 名称是其他计算机识别它的名称，而 `netbios name` 参数用于设置此功能。如果未设置此参数，Samba 将采用计算机机器名的默认值；例如，`ginkgo.threeromco.com` 变为 `GINKGO`。

- `server string`（服务器字符串）：此参数设置了一个注释，当你使用 Windows 网络邻居工具浏览工作组时可以看到该注释。这是 Windows 网络的一个纯外观功能。

- `encrypt passwords`（加密密码）：此参数至关重要，且常常给新的 Samba 管理员带来很多麻烦。默认情况下，Samba 仅接受明文密码，这些密码未经加密传输。这种特性可能存在安全风险；然而，以加密形式传输密码更好，这使得破解截获的密码变得困难或不可能。但是，在 Samba 上使用加密密码需要维护一个单独的仅用于 Samba 的密码列表。（Samba 会将明文密码与 Linux 常规密码数据库进行比对。）早期版本的 Windows 95 和 Windows NT 4.0 使用明文密码，但 Windows 95 OSR 2、Windows 4.0 SP 3 以及所有后续版本的 Windows 均使用加密密码。“设置密码选项”部分更详细地描述了 Samba 的加密密码处理机制。

- `os level`（OS 级别）：`os level` 参数控制 Samba 如何在主浏览器选举中宣告自身。这些选举决定哪台计算机维护本地计算机列表，以方便其他系统。除非你是经验丰富的 Samba 管理员并理解承担主浏览器职责的后果，否则应将此值设置得较低（例如设为 1）。

- `preferred master, domain master`（首选主浏览器、域主浏览器）：这两个参数也影响 Samba 是否承担主浏览器职责。如果设置为 `Yes`，`preferred master` 会使 Samba 尝试承担此角色，如果服务器未配置为赢得选举，这可能非常有害。因此，除非你理解选举过程，否则我们建议将此值设置为 `No`。同样，`domain master` 决定 Samba 是否试图成为域主浏览器（这与本地主浏览器略有不同）。

- `hosts allow`（允许主机）：此参数是一个重要的安全功能。如果使用，它会阻止 Samba 访问除指定计算机以外的所有设备。你可以按主机名（如果与 NetBIOS 名称不同，则不使用 NetBIOS 名称）或 IP 地址列出计算机。如果主机名以句点开头，或者由少于四个元素组成的 IP 地址以句点结尾，则表示整个计算机网络。例如，在前面的示例中，允许 `192.168.34.0/24` 网络上的所有计算机访问。虽然此参数并非必需，但使用它是一个好主意，特别是当服务器连接到整个互联网时。

这些参数中最关键的是 `workgroup` 和 `encrypt passwords`。当你首次安装 Samba 时，它不太可能已配置为在你的工作组中运行，因此你必须设置 `workgroup` 参数才能使用该服务器。同样，除非你使用的是相当旧的客户端，否则你通常必须配置 Samba 使用加密密码，或者重新配置客户端使用明文密码。

## 设置密码选项

如果你设置了 `encrypt passwords = Yes`，必须在 Linux 上设置加密密码文件。为此，你可以使用 `smbpasswd` 程序，该程序向加密密码文件（在 Red Hat 7.3 系统中为 `/etc/samba/smbpasswd`）添加用户名和密码，或编辑这些信息。对于系统上的每个用户，你都应该发出命令 `smbpasswd -a`。该程序会要求你两次输入密码。首次运行此程序时，它可能会通知你找不到 `smbpasswd` 文件，因此正在创建它。

如果你更喜欢使用明文密码和常规 Linux 密码数据库，可以通过更改较新的 Windows 客户端以发送明文密码来实现。在 Red Hat 7.3 系统中，目录 `/usr/share/doc/samba-2.2.3a/docs/Registry` 包含几个 `.reg` 文件，可用于对 Windows 系统进行相应的更改。将文件名与你运行的操作系统版本匹配的文件（例如，对于 Windows 98，使用 `Win98_PlainPassword.reg`）复制到软盘，将该软盘移至目标 Windows 系统，并双击文件以调整客户端配置。在更改生效之前，你需要重启 Windows。

## 配置文件共享

文件共享构成了大多数 `smb.conf` 文件的主要部分，尤其是在拥有许多共享的服务器上。此共享演示了最常见的文件共享选项：

```ini
[bigshare]
    comment = Shared Program Directory
    path = /home/samba/bigshare
    read only = No
    browseable = Yes
    create mask = 0666
    directory mask = 0777
```

此共享参数的含义如下：

- `comment`（注释）：`comment` 参数的作用与 `server string` 参数类似，只是 `comment` 设置的是与特定共享相关联的注释。

- `path`（路径）：`path` 参数设置要共享的目录。这可以是计算机上的任何目录，当然，出于安全原因，共享某些目录（如 `/etc`）是不明智的。

- `read only`（只读）：默认情况下，Samba 不授予写入它所共享目录的权限。你可以通过包含 `read only = No` 参数来允许用户写入 Samba 共享。`writeable` 和 `writable` 是 `read only` 的反义词，因此 `writeable = Yes` 等同于 `read only = No`。

- `browseable`（可浏览）：如果此参数设置为 `Yes`，共享将出现在 Windows 下的网络邻居浏览列表中。通常最好将此参数设置为 `Yes`。
