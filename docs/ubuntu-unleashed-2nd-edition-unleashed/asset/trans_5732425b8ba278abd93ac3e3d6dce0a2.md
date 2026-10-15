

FIGURE 22.5 使用 SWAT Shares 页面设置 Linux 文件系统的部分共享。

![](img/e464b828c497c99e41f61d4c55f1c0db_554_0.png)

![](img/e464b828c497c99e41f61d4c55f1c0db_554_1.png)

FIGURE 22.6 通过编辑共享默认值配置 Samba 共享。

## 使用 Ubuntu 进行网络和远程打印

第 12 章“使用 Ubuntu 打印”讨论了如何设置和配置本地打印机及相关打印服务。本节介绍如何配置打印机以在网络上共享和访问。

世界各地的办公室都受益于使用打印服务器和共享打印机。在我的办公室里，我有一台通过装有 Ubuntu PPC 的 Mac mini 连接到网络的两台打印机，这样我的妻子就可以通过无线链路从楼下打印，而我可以在办公室的三台电脑上打印。这是一件简单的事情，即使在小型环境中也能带来真正的生产力效益。

### 创建网络打印机

设置远程打印服务涉及配置打印服务器，然后在网络上的一台或多台计算机上创建远程打印机条目。本节介绍了一种快速方法，使一台 Linux 工作站能够向局域网上的另一台 Linux 计算机打印。你还将了解使用 Samba 及其实用程序的 SMB 打印。最后，本节讨论如何配置网络连接打印机并使用它们打印单个或多个文档。

### 在局域网上启用网络打印

要在局域网上的两台 Linux 工作站之间设置打印，你需要 root 权限并访问两台计算机，但过程简单易行。

首先，登录或通过 ssh 登录到打印机连接的计算机。该计算机将是打印服务器。使用 hostname 或 ifconfig 命令获取主机名或 IP 地址，并记下打印机队列的名称。如果系统使用 LPRng 而不是 CUPS，你需要编辑名为 /etc/lpd.perms 的文件。滚动到文件末尾并查找远程权限条目：

```
# allow local job submissions only
REJECT SERVICE=X NOT SERVER
```

默认情况下未启用远程打印，因此你必须用井号（#）注释掉服务拒绝行：

```
# allow local job submissions only
#REJECT SERVICE=X NOT SERVER
```

保存文件，然后重启 lpd 守护进程。

这样就可以将来自任何远程主机的、具有正确队列名称（本地打印机名称）的传入打印请求路由到打印机。完成后，注销并转到局域网上没有连接打印机的远程计算机。

### TIP

LPRng 与 CUPS 一样，可以配置为将打印服务限制为单个主机、一个或多个特定本地或远程用户、整个或部分域，或局域网段（通过指定 IP 地址范围）。例如，/etc/lpd.perms 中允许仅来自 192.168.2.0 的主机打印请求的条目如下所示：

```
ACCEPT SERVICE=X REMOTEIP=192.168.2.0/255.255.255.0
```

lpd.perms 手册页（作为 LPRng 文档的一部分包含）包含可用于创建自定义权限的关键字索引。不要忘记在对 /etc/lpd.perms（或 /etc/lpd.conf）进行任何更改后重启 lpd 守护进程。

如果连接有打印机的计算机使用的是 Ubuntu，并且你想将其设置为打印服务器，再次使用 gnome-cups-manager 客户端创建新打印机。

要启用共享，你必须执行几个步骤，因为默认情况下 CUPS 未设置为在网络上共享打印机。

首先，使用以下命令编辑你的 /etc/cups/cupsd.conf 文件：

```
$ sudo gedit /etc/cups/cupsd.conf
```

在此示例中我使用了 gedit，但请随意替换为你喜欢的文本编辑器。

然后，查找以 <Location /> 开始的部分并将其修改为如下所示：

```
<Location />
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
Allow From 192.168.0.*
</Location>
```

这告诉 CUPS 在网络 192.168.0.* 上共享你的打印机，例如。请确保将其更改为与你的网络设置相匹配。

接下来你需要编辑 /etc/cups/cups.d/ports.conf 文件，告诉 CUPS 监听特定端口。

将此行

```
Listen localhost:631
```

修改为

```
Listen 631
```

