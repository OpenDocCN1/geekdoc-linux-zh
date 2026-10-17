
密码提示来自 `sudo` 程序，要求输入我的 Ubuntu 密码以便我执行特权操作。后两个提示是用于输入和验证该用户的 Samba 密码。

Samba 配置文件中的默认安全级别 `security = user` 要求 Samba 用户也必须存在于 Ubuntu 系统的密码文件中，否则你将收到错误且 `smbpasswd` 命令将执行失败。有关其他安全模型和配置的详细信息，请参阅 `samba` 包中的文件 `/usr/share/doc/samba-doc/htmldocs/ServerType.html`。

## 使用 Samba 打印机和主目录

在设置工作组并创建用户后，下一个需要考虑的是你希望让连接到你服务器的所有 Windows 系统用户使用的系统通用资源。这些资源最常见的例子是打印机和用户的主目录。

![](img/e88880e40d650bfe19d5b6927bd86568_882_0.png)

在 Samba 配置文件中与打印机和打印相关的 `[global]` 部分包含以下内容，你应该确保这些内容没有被注释（即前面不是以分号开头）：

```
printers = yes
printing = cups
printcap name = cups
```

在 Samba 配置文件中，`[printers]` 和 `[print$]` 部分提供了 Windows 系统如何与 Samba 服务器交互的信息。你不需要更改其中任何内容，但作为参考，这些条目如下：

```
[printers]
comment = All Printers
browseable = no
path = /tmp
printable = yes
public = no
writable = no
create mode = 0700

[print$]
comment = Printer Drivers
path = /var/lib/samba/printers
browseable = yes
read only = yes
guest ok = no
```

`[printers]` 部分标识了 Samba 服务器如何处理来自 Windows 客户端的打印机识别请求和打印请求，而 `[print$]` 部分将传统的 `print$` 共享名称映射到你 Linux 系统上的一个目录，你可以在那里放置打印机驱动程序，以便当你的 Windows 客户端机器上没有这些驱动程序时能够定位并加载它们。

此外，用户想要从其 Windows 系统访问的最自然资源就是主目录。这提供了一种简单的方法，将 Samba 服务器上的主目录用作存储文件的地方，同时也让你能够从 Windows 系统中自动备份文件，并让你能够利用在 Samba 服务器上进行的任何标准备份（有关在 Ubuntu 系统上备份文件的更多信息，请参阅第 22 节）。

Samba 的配置文件已经默认设置为支持共享主目录，只要 Linux 和 Windows 用户名匹配即可。Samba 配置文件中支持主目录的部分如下：

```
[homes]
comment = Home Directories
browseable = no
writable = no
create mask = 0700
directory mask = 0700
```

从此配置文件片段可以看出，主目录是默认共享的，但无法从 Windows 客户端访问。这非常不方便，所以你可能希望将 `[homes]` 配置中的 `writable` 条目改为 `yes`，如下例所示：

```
writable = yes
```

这允许用户在其主目录中进行读取和写入操作。

如果你的 Windows 和 Ubuntu 用户恰好具有不同的登录，你可以通过在 `/etc/samba/smbusers` 文件中创建相应的条目将两者关联起来。该文件中的条目格式为 `LinuxLogin = WindowsLogin`。例如，为了将 Ubuntu 用户 `wvh` 映射到 Windows 用户 `hagen`，我会在 `/etc/samba/smbusers` 文件中创建以下条目：

```
wvh = hagen
```

### 检查配置文件

`samba` 包还提供了一个实用工具，可以测试 Samba 配置文件的有效性并识别任何错误。如果配置文件包含无效条目，Samba 将无法加载。如果不是该包还提供了一个测试文件语法的工具，这可能会非常令人沮丧。该工具是 `testparm`，你可以在不带任何参数的情况下运行它来查看服务定义的导出。输出如下：

```
[global]
workgroup = WVH
server string = Samba (Ubuntu)
obey pam restrictions = yes
passdb backend = tdbsam
log file = /var/log/samba.%m
max log size = 1000
resolve order = lmhosts host wins bcast
```

![](img/e8880e40d650bfe19d5b6927bd86568_884_0.png)

## Samba 可用性服务

工具包包含一个名为 `smbclient` 的应用程序，它是用于访问和浏览 Samba 服务器的命令行客户端。你还可以使用此实用工具测试 Samba 服务器是否运行并列出它提供的服务。在修改 Samba 配置文件后，你应该重启 Samba 服务器以强制其读取更新后的配置文件。执行此操作，请运行以下命令：

```
sudo /etc/init.d/samba restart
```

完成后，你可以通过使用 `smbclient` 应用程序查询 Samba 服务器；使用 `-L` 选项列出可用资源；要连接的主机名称；以及默认未验证用户看到的 `-U%` 选项。该命令及其输出示例如下：

```
smbclient -L ulaptop -U%
ain=[WVH] OS=[Unix] Server=[Samba 3.0.22]

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| ADMIN$ | IPC | IPC 服务 (ulaptop server (Samba, Ubuntu)) |
| IPC$ | IPC | IPC 服务 (ulaptop server (Samba, Ubuntu)) |
| print$ | Disk | 打印机驱动 |

ain=[WVH] OS=[Unix] Server=[Samba 3.0.22]

| Server | Comment |
| :--- | :--- |
| ULAPTOP | ulaptop server (Samba, Ubuntu) Workgroup Master WVH ULAPTOP |
```

此输出的第一部分列出了当前用户（一个未身份验证的用户）可用的共享列表。第二个部分提供了有关你所连接的 Samba 服务器名称以及其所属的域的信息。

! 下一步是查看已身份验证的用户能看到什么。我将使用在本章之前创建的示例用户 `wvh`。这次命令及其输出如下所示：

```
@ulaptop:~$ smbclient -L ulaptop -Uwvh
ain=[ULAPTOP] OS=[Unix] Server=[Samba 3.0.22]

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| ADMIN$ | IPC | IPC 服务 (ulaptop server (Samba, Ubuntu)) |
| IPC$ | IPC | IPC 服务 (ulaptop server (Samba, Ubuntu)) |
| print$ | Disk | 打印机驱动 |
| wvh | Disk | 用户主目录 |

ain=[ULAPTOP] OS=[Unix] Server=[Samba 3.0.22]

| Server | Comment |
| :--- | :--- |
| Workgroup Master WVH ULAPTOP |
```

由于我指定了一个实际用户名，`smbclient` 工具首先提示我输入 Samba 服务器的密码，然后显示了略有不同的信息。唯一的真实区别是已身份验证的用户可以访问其在 Samba 服务器上的主目录，正如你在 `smbclient` 输出的第一部分 `Sharename` 部分中的目录条目中所看到的那样。

! 现在已经很清楚 Samba 服务器正在运行，并且正确配置为允许访问用户特定资源，是时候添加一些所有已身份验证的用户都能使用的系统级资源了。幸运的是，正如下一节所说明，你甚至可以使用工具完成操作。

## 使用共享文件夹工具共享目录

Ubuntu Linux 没有提供用于设置和配置 Samba 本身的图形化工具，但它提供了一个易用的图形化工具 (`shares-admin`)，它可以简化识别和配置你想要通过 Samba 从你的 Ubuntu 系统导出的特定共享。如果你已经使用 NFS 导出了共享目录，那么你对这个工具应该已经熟悉——Ubuntu 和 GNOME 的开发者们很聪明，使用同一个工具来识别和配置 Samba 共享和 NFS 导出。
