
此外你需要通过使用命令 `sudo passwd root` 为 root 账户设置密码来启用 root 账户。不启用 root 账户会阻止你有效地使用 `SWAT`。

在你开始使用 `SWAT` 之前需要执行几个步骤。首先，确保已安装 `Samba` 和 `swat` 包。然后通过编辑 `/etc/inetd.conf` 文件来启用 `SWAT` 对系统的访问权限，将以下行中的 `#<off>#` 注释删除（如果存在）：

```text
#<off># swat  stream  tcp  nowait.400  root\
  /usr/sbin/tcpd  /usr/sbin/swat
```

保存文件，然后使用以下命令重启 `openbsd_inetd` 守护进程：

```bash
$ sudo /etc/init.d/openbsd-inetd restart
```

接下来，启动一个 X 会话，启动 Firefox，并浏览到 `http://localhost:901` 统一资源定位符（URL）。你会看到登录提示。输入 root 用户名和密码，然后单击 OK 按钮。屏幕清空，你会看到主 `SWAT` 页面，如图 16.2 所示。

![](img/8f9e74e2b343ff525bebfb720a3d8441_422_0.png)

FIGURE 16.2 You can use SWAT to easily configure and administer Samba on your system.

##### TIP

你也可以使用 Ubuntu 的 `shares-admin` 客户端配置 Samba。从 X 终端窗口的命令行启动客户端，或选择 System, Administration, Shared Folders 菜单项（如图 16.9 后文所示）。

首先，在 `SWAT` 的主页面单击 Globals 图标。你会看到一个类似图 16.3 所示的页面。窗口中有许多选项，但你只需在 Security Options 部分下的 Hosts Allow 字段中输入一个或多个 IP 地址或子网地址（例如 `192.168.0.`——注意末尾的句点，这允许所有主机访问；在该示例中，为 `192.168.0` 子网），即可快速设置来自 LAN 主机的访问权限。如果需要帮助了解如何格式化条目，请单击字段左侧的 Help 链接。会出现一个新网页，其中包含相关信息。

![](img/8f9e74e2b343ff525bebfb720a3d8441_423_0.png)

FIGURE 16.3  Configure Samba to allow access from specific hosts or subnets on your LAN.

完成后，单击 Commit Changes 按钮保存全局访问设置。下一步是创建 Samba 用户并设置用户的密码。单击主 `SWAT` 页面上的 Password 图标（参见图 16.2）。Server Password Management 页面打开，如图 16.4 所示。在 User Name 字段中输入用户名；然后在 New Password 和 Re-type New Password 字段中输入密码。

> **NOTE**
>
> 你必须提供一个现有系统用户的用户名，但用于 Samba 访问的密码不必与现有用户的密码匹配。

完成后，单击 Add New User 按钮。`SWAT` 然后创建用户名和密码并显示 Added user *username*（其中 *username* 是你输入的名称）。新的 Samba 用户现在应该能够从任何允许的主机访问主目录，前提是 Samba（`smb`）服务器正在运行。

例如，如果你在一台名为 *mini* 的主机上设置了 Samba，该主机上有一个名为 *andrew* 的用户，则该用户可以从任何远程主机（如果 Globals 设置允许）访问 *mini* 上的主目录，也许可以使用 `smbclient` 命令如下：

```bash
$ smbclient //mini/andrew -U andrew
```

```
added interface ip=192.168.0.68 bcast=192.168.0.255 nmask=255.255.255.0
Password:
Domain=[MYGROUP] OS=[Unix] Server=[Samba 3.6.28]
smb: \> pwd
Current directory is \mini\andrew\
smb: \> quit
```

![](img/8f9e74e2b343ff525bebfb720a3d8441_424_0.png)

图 16.4 在 SWAT 密码页面输入 Samba 用户名和密码。

点击状态图标（如图 16.2 或 16.4 所示）以查看 Samba 的状态或启动、停止或重启服务器。你可以使用结果网页上的各种按钮来控制服务器并查看周期性或连续的状态更新。

你也可以使用 `SWAT` 来共享 Linux 目录。首先，点击主 Samba 页面顶部工具栏中的 Shares 图标（参见图 16.2）。然后，在 Create Shares 字段中输入共享名称，然后点击 Create Shares 按钮。`SWAT` Shares 页面会以对话框形式显示详细配置信息，如图 16.5 所示，提供对新 Samba 共享的详细配置访问。

![](img/8f9e74e2b343ff525bebfb720a3d8441_425_0.png)

图 16.5 使用 SWAT Shares 页面设置 Linux 文件系统部分共享。

另外，可以从命令行使用 `shares-admin` 客户端或在系统设置菜单中使用服务器设置 Samba 服务器菜单项。图 16.6 显示了名为 `/home/andrew/music` 的共享目录的属性。点击解锁按钮解锁工具，使用添加按钮创建新共享，并使用属性按钮编辑共享的访问选项。

![](img/8f9e74e2b343ff525bebfb720a3d8441_425_1.png)

图 16.6 通过编辑共享默认值配置 Samba 共享。

## 使用 Ubuntu 进行网络和远程打印

第 8 章“使用 Ubuntu 打印”讨论了如何设置和配置本地打印机及相关打印服务。本节介绍如何配置打印机以在网络上共享和访问。

世界各地的办公室都受益于使用打印服务器和共享打印机。在我的办公室，我有一台通过装有 Ubuntu PPC 的 Mac mini 连接到网络的两台打印机，这样我的妻子就可以通过无线链路从楼下打印，而我可以在办公室的三台电脑上打印。这是一件简单的事情，即使在小型环境中也能带来真正的生产力效益。

### 创建网络打印机

设置远程打印服务涉及配置打印服务器，然后在网络上的一台或多台计算机上创建远程打印机条目。本节介绍一种快速方法，使一台 Linux 工作站能够向局域网上的另一台 Linux 计算机打印。你还将了解使用 Samba 及其实用程序的 SMB 打印。最后，本节讨论如何配置网络连接打印机并使用它们打印单个或多个文档。

### 在局域网上启用网络打印

如果连接打印机的计算机使用的是 Ubuntu，并且你想将其设置为打印服务器，再次使用 `system-config-printer` 客户端创建新打印机。

要启用共享，你必须执行以下几个步骤，因为默认情况下 CUPS 未设置为在网络间共享打印机。

首先，使用以下命令编辑你的 `/etc/cups/cupsd.conf` 文件：

```
$ sudo gedit /etc/cups/cupsd.conf
```

在本例中我使用了 `gedit`，但请随意替换为你喜欢的文本编辑器。

然后，查找以 `<Location />` 开始的部分并将其修改为如下所示：

```
<Location />
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
Allow From 192.168.0.*
```

</Location>

这告诉 CUPS 在 `192.168.0.*` 网络上共享你的打印机，例如。确保将其更改为与你自己的网络设置相匹配。

接下来你需要在同一文件中查找以

```
Listen localhost:631
```

开始的部分并将其修改为如下所示：

```
Listen 631
```

这告诉 CUPS 在端口 `631` 上监听任何打印请求。

### 会话消息块打印

打印到 SMB 打印机需要 Samba，以及诸如 `smbclient` 和相关 `smbprint` 打印过滤器之类的实用程序。你可以使用 Ubuntu 包含的 Samba 软件打印到 Windows 网络上的共享打印机，或将连接到系统的打印机设置为 SMB 打印机。本节描述如何创建本地打印机条目以使用 SMB 打印到远程共享打印机。

在 Windows 操作系统下设置 SMB 或共享打印机通常是通过控制面板的网络设备使用配置设置来完成的。启用打印共享后，重新启动计算机。在我的电脑、打印机文件夹中，右键单击要共享的打印机名称或图标并从弹出菜单中选择共享。设置共享为项目，然后输入描述性共享名称，例如 `HP2100`，以及密码。
