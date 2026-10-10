
如果你专门与 Fedora、Red Hat Enterprise Linux 和其他 UNIX 系统工作，NFS 可能是你共享文件系统的最佳选择。如果你的网络主要连接 Microsoft Windows 计算机或组合系统，你可能希望考虑使用 Samba 进行文件共享。

# 设置 Samba 文件服务器

Samba 是一个随 Fedora 和 Red Hat Enterprise Linux 系统自带的软件包。Samba 允许你与使用 Server Message Block (`SMB`) 协议的计算机共享文件系统和打印机。`SMB` 是 Windows 操作系统自带的用于共享文件和打印机的协议。

尽管你不能总是认为 Windows 客户端上安装了 NFS（除非你手动安装），但 `SMB` 总是可用的（只需进行少量设置）。如果目前未安装 Samba，请参考本章的“获取并安装 Samba”部分。

在 Fedora 或 RHEL 上，Samba 软件包包含各种守护进程、管理工具、用户工具和配置文件。要进行 Samba 配置，你可以从 Samba 服务器配置窗口开始。它提供了一个配置服务器和共享目录的图形界面。

大多数 Samba 配置最终都位于 `/etc/samba/smb.conf` 文件中。如果你需要访问 Samba 服务器配置窗口未的功能，可以手动编辑 `/etc/samba/smb.conf` 或使用 `SWAT`（一个用于配置 Samba 的 Web 界面）。

# 第四部分：Fedora 和 RHEL 网络与服务器设置

守护进程由 `smbd`（SMB 守护进程）和 `nmbd`（NetBIOS 名称服务器）组成。`smbd` 守护进程负责文件共享和打印。

# 获取并安装 Samba

要查看 Fedora 上是否安装了 Samba，请输入：

```
# rpm -qa | grep samba
samba-*
system-config-samba
samba-swat
samba-common-*
samba-client-*
```

你应该看到五个软件包的名称，后面跟着版本号（我用星号表示版本号）。虽然不是通过安装组安装，但组成 Samba 的软件包都包含在 DVD 中。要安装 Samba，请插入 DVD。然后运行以下命令（注意设备名称可能不是 `cdrecorder`，如果它自动挂载，你可以跳过第一步）：

```
# mount /media/cdrecorder
# cd /media/cdrecorder/Fedora/RPMS
# rpm -Uv samba*
# cd ; umount /media/cdrecorder
```

如果有 Internet 连接，可以尝试使用 `yum install samba`。在开始配置 Samba 之前，请阅读位于 `/usr/share/doc/samba*` 的 README 文件。

# 配置简单的 Samba 服务器

服务器配置窗口允许你进行基础 Samba 配置，然后识别你想共享的目录。为了使此过程有用，我正在设置一个特定类型的共享环境（你可以进行修改）。其特点如下：

- **单一局域网**：包含多台 Windows 和 Linux 机器。
- **用户级安全**：任何想要访问共享 Samba 文件的用户必须在 Linux 服务器上拥有有效的登录和密码。
- **加密密码**：许多客户端默认对 Samba (`SMB`) 使用加密密码。我将描述如何为不使用加密密码的客户端开启加密密码。
- **客用账户**：客用账户以后很有用，因此你可以设置 Samba 让没有特殊账户的用户通过 Samba 使用服务器的打印机。

以下步骤描述了如何配置 Samba 并在 Samba 中创建共享目录：

1. 要打开 Samba 服务器配置窗口，点击 System $\rightarrow$ Administration $\rightarrow$ Server Settings $\rightarrow$ Samba。Samba 服务器配置窗口将打开。（可能需要输入 root 密码。）
2. 点击 Preferences $\rightarrow$ Server Settings。出现服务器设置窗口，如图 18-3 所示。
3. 输入组名称（以与你想要共享文件的其它计算机匹配）和简短描述。

# 第四部分：Fedora 和 RHEL 网络与服务器设置

![](img/c7605e408543e0a1829c1fd0cf2f687d_799_0.png)

图 18-3：为你的 Samba 服务器定义工作组和描述。

- 点击“安全”（Security）选项卡。会出现一个如图 18-4 所示的窗口。

![](img/c7605e408543e0a1829c1fd0cf2f687d_799_1.png)

图 18-4：为你的 Samba 服务器填写安全信息。

- 为“安全”选项卡上的字段提供以下信息并点击 OK：
