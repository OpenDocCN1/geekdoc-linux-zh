
```
# pap -P LaserJet2100M /etc/hosts
```

`-p` 选项用于指定你的 `netatalk` 打印机。在此示例中，它将打印 `/etc/hosts` 文件的一份副本。或者，你只需检查打印机的状态：

```
# papstat -P LaserJet2100M
```

### 故障排除 netatalk

有多种工具可供使用，以查看 AppleTalk 网络的状态。`aecho` 命令可以测试特定的 AppleTalk 主机计算机是否在线。

# 第四部分：Fedora 网络与服务器设置

`nbplookup` 命令可用于查看当前 AppleTalk 网络上可用的服务。

> 注意：通常，AppleTalk 应仅在受信任的网络上使用。但是，如果你在 `netatalk` 服务器上运行防火墙，则必须开放多个端口才能使其正常工作。具体来说，你可能需要开放端口 `548`（基于 TCP/IP 的 AFP）、`201`（AppleTalk 路由）、`202`（AppleTalk 名称绑定）、`204`（AppleTalk 回显）和 `206`（AppleTalk 区域）。

使用 `aecho` 命令（类似于 `TCP/IP ping` 命令）来检查 AppleTalk 主机计算机是否在线。`aecho` 命令向你想要检查的主机发送 Apple Event Protocol（`aep`）数据包。以下是一个示例：

```
# aecho toys
14 bytes from 65280.115: aep_seq=0. time=0, ms
14 bytes from 65280.115: aep_seq=1. time=0, ms

---65280.115 AEP Statistics---
2 packets sent, 2 packets received, 0% packet loss
round-trip (ms) min/avg/max = 0/0/0
```

如果 AppleTalk 服务器正在运行，你可以使用 `nbplookup` 命令查看当前可用的打印机和卷。对于大型网络，你可以通过添加共享名称或打印机名称（如 `:hphjet`），或输入主机名（例如 `toys`）来限制 `nbplookup` 的输出。以下是一个示例：

```
# nbplookup :APFServer
duck:APFServer         65280.115:130
User  Volume:APFServer 65280.21:129
Guest Volume:APFServer  65280.21:130
```

通过查询 `:APFServer`，`nbplookup` 列出了本地网络上所有的 AppleTalk 文件服务器。第一个显示的是来自主机名为 `duck` 的计算机。第二行和第三行来自同一台计算机（地址为 65280.21），但被注册为不同的服务器。

在重启 `netatalk` 服务器后，你可以检查所有守护进程是否已正常启动。以下是 `/var/log/messages` 文件中的几行内容：

```
Mar 14 17:44:23 toys atalkd[2013]: zip_getnetinfo for eth0
Mar 14 17:44:33 toys atalkd[2013]: zip_getnetinfo for eth0
Mar 14 17:44:33 toys atalkd[2013]: config for no router
Mar 14 17:44:46 toys atalkd[2013]: ready 0/0/0
Mar 14 17:44:44 toys atalk: atalkd startup succeeded
Mar 14 17:44:57 toys atalk: paps startps succeeded
Mar 14 17:44:57 toys paps[2070]: restart ( 1.5.5 )
Mar 14 17:44:57 toys atalk: afpd startup succeeded
Mar 14 17:45:03 toys afpd[2074]: toys:APFServer@ started on
65280.96:128 ( 1.5.5 )
Mar 14 17:45:03 toys afpd[2074] : ASIP started on 10.0.0.100:548(1) 
(1.5.5) 
Mar 14 17:45:03 toys afpd[2074]: uam: uams_clrtxt.so loaded 
Mar 14 17:45:03 toys afpd[2074]: uam: uams_dhx.so loaded 
Mar 14 17:45:03 toys afpd[2074]: uam: “DHCAST128” available 
Mar 14 17:45:03 toys afpd[2074]: uam: “ClearExt_Passwd” available
```

在上面的示例中，你可以看到 `atalk` 启动脚本成功启动了 `atalkd`、`papd` 和 `afpd` 守护进程。`atakd` 守护进程在第一个以太网接口（`eth0`）上查找 AppleTalk 网络信息。`papd` 守护进程已启动，但没有注册任何打印机。`afpd` 守护进程在服务器上（`toys:APFServer`）启动了一个 AppleTalk 文件服务器。然后它标识了可用的用户认证方法（`uams`）（这里可以使用明文密码和加密密码两种方法）。

### 从 Mac 访问 NFS 服务器

多年来，网络文件系统（NFS）一直是 Linux 和其他类 UNIX 计算机系统之间共享文件的首选方法。虽然 Mac OS X 支持通过“连接至服务器”窗口建立 NFS 连接，但你仍需要在 Linux 服务器上执行一些小技巧，以便该服务器接受来自 Mac OS X 计算机的连接。

以下过程描述了如何从 Mac OS X 客户端使用“连接至服务器”窗口来访问共享 Linux NFS 服务器上的文件和目录。然后，你可以使用这些驻留在 Linux NFS 服务器上的文件和目录（也称为文件夹），就像它们位于你的 Mac OS X 计算机上一样。

如前所述，该过程依赖于能够对 Linux NFS 服务器提供共享目录的方式进行少量更改。如果你无法访问 Linux 服务器，你需要请求 Linux 服务器管理员进行此更改，或手动将你的 Mac 连接到 Linux NFS 服务器。（我在本节末尾介绍了手动过程。）

#### 从“连接至服务器”窗口连接 NFS

要在 Linux 中创建 NFS 共享目录并从 Mac 客户端连接，请执行以下操作：

1. 在 Linux 服务器上，使用第 18 章中描述的 NFS 功能导出共享目录。但是，要从 Mac OS X 使用该共享目录，你必须确保添加 `insecure` 选项。例如，要从名为 `jukebox.linuxtoys.net` 的 Linux 服务器共享 `/var/music` 目录，你可以在该服务器的 `/etc/exports` 文件中添加以下行：

   ```
   /var/music (*rw,insecure)
   ```

   此示例允许 `/var/music` 目录与所有计算机（*）共享，并提供读写权限（`rw`）。`insecure` 选项允许请求导出目录的客户端从不安全的端口（1024 以上的端口）发起请求。这很重要，因为 Mac OS X 的“连接至服务器”窗口从 1024 以上的端口发起挂载共享目录的请求，如果没有该选项，请求将会失败。

2. 在 Linux 服务器上，验证 NFS 服务正在运行，并重新导出共享目录，输入以下命令（作为 root 用户）：

   ```
   # exportfs -a -v
   ```

3. 在 Mac OS X 客户端上，选择屏幕顶部 Finder 栏中的“前往”，然后选择“连接至服务器”。此时会出现“连接至服务器”窗口。

4. 在 Mac OS X 客户端上，将共享目录的地址输入到地址框中。例如，要连接到名为 `jukebox.linuxtoys.net` 的计算机上的共享 NFS（`nfs://`）目录 `/var/music`，你可以输入地址：`nfs://jukebox.linuxtoys.net/var/music`（参见图 26-5）。

如果一切正常，代表服务器的图标应该会出现在你的 Mac OS X 桌面上。打开该图标以查看共享目录的内容。你可以使用共享的文件和目录，就像它们在你的 Mac 上一样（前提是服务器权限允许你这样做）。完成操作后，将图标拖入废纸篓。

注意：如果无法连接到共享目录，请更仔细地检查第 18 章中的 NFS 过程。特别是，确保服务器上的防火墙端口已开放，并且用户和主机权限已设置，以允许你所需要的访问级别。

![](img/b22364e57409c2481ba806e4e6b9309c_969_0.png)

图 26-5：从“连接至服务器”窗口连接 NFS 服务器。

#### 通过命令行连接 NFS
