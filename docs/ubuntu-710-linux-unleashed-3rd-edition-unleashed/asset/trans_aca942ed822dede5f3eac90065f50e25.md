

![](img/7aaa8e4f2209bf9f2fb443905096e94c_408_0.png)

FIGURE 16.6  通过编辑共享默认值配置 Samba 共享。

## 使用 Ubuntu 进行网络和远程打印

第 8 章“使用 Ubuntu 打印”讨论了如何设置和配置本地打印机及相关打印服务。本节介绍如何配置打印机以在网络上共享和访问。

世界各地的办公室都受益于使用打印服务器和共享打印机。在我的办公室里，我有一台打印机通过装有 Ubuntu 的 Mac mini 连接到网络，这样我的妻子就可以通过无线链路从楼下打印，而我可以在办公室的三台电脑上打印。这是一件很简单的事情，即使在小型环境中也能带来真正的生产力效益。

### 创建网络打印机

设置远程打印服务涉及配置打印服务器，然后在网络上的一台或多台计算机上创建远程打印机条目。本节介绍了一种快速方法，使一台 Linux 工作站能够向 LAN 上的另一台 Linux 计算机打印。你还将了解使用 Samba 及其实用程序的 SMB 打印。最后，本节讨论如何配置网络连接打印机并使用它们打印单个或多个文档。

### 在 LAN 上启用网络打印

如果连接了打印机的计算机使用的是 Ubuntu，并且你想将其设置为打印服务器，请再次使用 `system-config-printer` 客户端创建新打印机。

要启用共享，你必须执行以下几个步骤，因为默认情况下 CUPS 未设置为在网络间共享打印机。

首先，使用以下命令编辑你的 `/etc/cups/cupsd.conf` 文件：

```
```bash
$ sudo gedit /etc/cups/cupsd.conf
```
```

在此示例中我使用了 gedit，但请随意替换为你喜欢的文本编辑器。

然后，查找以 `<Location />` 开始的部分并将其修改为如下所示：

```
```text
<Location />
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
Allow From 192.168.0.*
</Location>
```
```

这告诉 CUPS 在网络 192.168.0.* 上共享你的打印机，例如。确保将其更改为与你自己的网络设置相匹配。

接下来你需要在同一文件中查找以

```
```text
Listen localhost:631
```
```

开始的部分并将其修改为如下所示：

```
```text
Listen 631
```
```

这告诉 CUPS 在端口 631 上监听任何打印请求。现在你只需在客户端上打开 `system-config-printer` 并在“全局设置”菜单下选择“检测 LAN 打印机”。在短短几秒钟后，打印机应该会出现在你的窗口中，如图 16.7 所示

![](img/7aaa8e4f2209bf9f2fb443905096e94c_409_0.png)

**FIGURE 16.7**  已高亮的打印机已在网络上共享。Ubuntu 使这一过程尽可能简单无痛。

### 会话消息块打印

打印到 SMB 打印机需要 Samba，以及诸如 smbclient 和相关的 smbprint 打印过滤器等实用程序。你可以使用 Ubuntu 随附的 Samba 软件打印到 Windows 网络上的共享打印机，或将连接到系统的打印机设置为 SMB 打印机。本节描述如何创建本地打印机条目以使用 SMB 打印到远程共享打印机。

在 Windows 操作系统下设置 SMB 或共享打印机通常是通过使用控制面板的网络设备进行配置设置来完成的。启用打印共享后，重新启动计算机。在“我的电脑”、“打印机”文件夹中，右键单击要共享的打印机的名称或图标并从弹出菜单中选择“共享”。设置“共享为”项，然后输入描述性的共享名称，例如 HP2100，并输入密码。

在 Linux 上配置打印机时，必须输入共享名称和密码。你还需要知道打印机的 workgroup 名称、IP地址和打印机名称，并准备好用户名和密码。要查找此信息，请选择“开始”、“设置”、“打印机”；然后在“打印机”窗口中右键单击共享打印机的列表并从弹出窗口中选择“属性”。

你可以使用 CUPS 通过编辑 smb.conf 文件来配置 Samba 使用你的打印机。

在全局部分输入以下行，如果它们尚未存在：

```
...
load printers = yes
printing = cups
printcap name = cups
```

这告诉 Samba 使用 CUPS 提供打印服务。接下来你需要在 smb.conf 文件末尾创建一个新部分，如下所示：

```
[printers]
comment = Use this for All Printers
path = /var/spool/samba
browseable = no
public = yes
guest ok = yes
writable = no
printable = yes
printer admin = root, andrew
```

这会将你的打印机发布到网络上并允许其他人通过 Windows 客户端连接。

