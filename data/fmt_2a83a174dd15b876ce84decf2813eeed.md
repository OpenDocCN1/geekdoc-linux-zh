
当 Mac 客户端打印到以此方式配置的 Linux 打印机时，打印作业会交给标准的 Linux `lpr` 守护进程，并放入 spool 文件以供打印，这与该打印机的其他 Linux 打印作业一起处理。

> **注意：** Mac OS X 计算机可以直接打印到 Linux 打印服务（CUPS 或 LPing），无需使用 netatalk 打印。然而，较旧的 Mac OS 9 客户端可能需要看到您通过 netatalk 设置的 AppleTalk 打印机。

`papd.conf` 文件遵循与 `/etc/printcap` 文件（传统上用于 Linux 打印）相同的基本格式。以下是 `papd.conf` 文件中配置的一个打印机的示例：

```text
LaserJet2100M:\
    :pr=| /usr/bin/lpr -P hp01:\
    :pd=/etc/ataklaserjet.ppd:\
    :op=root:\
    :am:uams_guest,ao:
```

此示例中的打印机名为 `LaserJet2100M`。要从 Mac 客户端打印文件，它会获取输出文件并将其管道传输到 `lpr -P hp01` 命令（`hp01` 是本地打印机的名称）。`ppd` 文件是 `/etc/ataklaserjet.ppd`。root 用户是操作员，并且允许访客打印到该打印机（无需密码）。

打印机定义文件 (`ppd`) 必须安装在 netatalk 服务器（位于 `papd.conf` 文件中注明的位置）和 Mac 客户端上。

要测试您的 AppleTalk 打印机的接口是否正常工作，请使用 `pap` 命令：

```bash
# pap -P LaserJet2100M /etc/hosts
```

`-p` 选项标识您的 netatalk 打印机。在此示例中，它打印 `/etc/hosts` 文件的副本。或者，您也可以只检查打印机的状态：

```bash
# papstatus -p LaserJet2100M
```

## 排查 netatalk 故障

有几种工具可供您查看 AppleTalk 网络的状态。`aecho` 命令可以测试特定的 AppleTalk 主机计算机是否存活。`nbplookup` 命令可用于查看当前在您的 AppleTalk 网络上可用的服务。

> **注意：** 通常，AppleTalk 应在受信任的网络上使用。然而，如果您在 netatalk 服务器上运行防火墙，则必须打开多个端口才能让 netatalk 正常工作。特别是，您可能需要打开端口 548（基于 TCP/IP 的 AFP）、201（AppleTalk 路由）、202（AppleTalk 名称绑定）、204（AppleTalk 回显）和 206（AppleTalk 区域）。

使用 `aecho` 命令（类似于 TCP/IP 的 `ping` 命令）来检查 AppleTalk 主机计算机是否存活。`aecho` 命令向您要检查的主机发送 Apple 回显协议（`aep`）数据包。以下是一个示例：

```bash
# aecho toys
14 bytes from 65280.115: aep_seq=0, time=0. ms
14 bytes from 65280.115: aep_seq=1, time=0. ms

----65280.115 AEP Statistics----
2 packets sent, 2 packets received, 0% packet loss
round-trip (ms) min/avg/max = 0/0/0
```

如果 AppleTalk 服务器正在运行，您可以使用 `nbplookup` 命令查看当前可用的打印机和卷。对于大型网络，您可以通过添加共享名称或打印机名称（如 `:hpjet`）或输入主机名（例如 `toys`）来限制 `nbplookup` 的输出。以下是一个示例：

```bash
# nbplookup :APFServer
duck:APFServer				65280.115:130
User Volume:APFServer			65280.21:129
Guest Volume:APFServer			65280.21:130
```

通过查询 `:APFServer`，`nbplookup` 列出了本地网络上的所有 AppleTalk 文件服务器。显示的第一个是来自主机名为 `duck` 的服务器。第二行和第三行来自同一台计算机（地址为 `65280.21`），但被注册为独立的服务器。

重启 netatalk 服务器后，您可以检查所有守护进程是否都正常启动。以下是 `/var/log/messages` 文件中的几行内容。

```text
May 14 17:44:23 toys atalkd[2013]: zip_getnetinfo for eth0
May 14 17:44:33 toys atalkd[2013]: zip_getnetinfo for eth0
May 14 17:44:43 toys atalkd[2013]: config for no router
May 14 17:44:44 toys atalkd[2013]: ready 0/0/0
May 14 17:44:44 toys atalk: atalkd startup succeeded
May 14 17:44:57 toys atalk: papd startup succeeded
May 14 17:44:57 toys papd[2070]: restart (1.5.5)
May 14 17:45:03 toys atalk: afpd startup succeeded
May 14 17:45:03 toys afpd[2074]: toys:APFServer/* started on 65280.96:128 (1.5.5)
```

```
May 14 17:45:03 toys afpd[2074]: ASIP started on 10.0.0.100:548(1.5.5)

May 14 17:45:03 toys afpd[2074]: uam: uams_clrtxt.so loaded

May 14 17:45:03 toys afpd[2074]: uam: uams_dhx.so loaded

May 14 17:45:03 toys afpd[2074]: uam: *D82Qst28* available

May 14 17:45:03 toys afpd[2074]: uam: "Cleartext Password" available
```

在前面的示例中，你可以看到 atalkd 启动脚本成功启动了 atalkd、papd 和 afpd 守护进程。atalkd 守护进程在第一个以太网接口（eth0）上查找 AppleTalk 网络信息。papd 守护进程已启动，但没有打印机可以注册。afpd 守护进程在服务器（toys:APPServer）上启动了一个 AppleTalk 文件服务器。然后它识别了可用的用户认证方法（uams）（此处明文密码和加密密码均可用）。

## 从 Mac 访问 NFS 服务器

多年来，网络文件系统（NFS）一直是 Linux 和其他类 UNIX 计算机系统之间共享文件的首选方法。虽然 Mac OS X 支持从其“连接到服务器”窗口进行 NFS 连接，但你需要在 Linux 服务器上做一些特殊处理，以便该服务器能够接受来自 Mac OS X 计算机的连接。

以下步骤说明了如何使用 Mac OS X 客户端的“连接到服务器”窗口访问共享 Linux NFS 服务器上的文件和目录。然后你可以使用位于 Linux NFS 服务器上的文件和目录（也称为文件夹），就像它们存在于你的 Mac OS X 计算机上一样。

正如我之前提到的，该过程依赖于能够对 Linux NFS 服务器提供共享目录的方式做一些小的更改。如果你无法访问 Linux 服务器，你需要请求 Linux 服务器管理员进行更改，或者手动将你的 Mac 连接到 Linux NFS 服务器。（我将在本节末尾描述手动操作过程。）

### 通过“连接到服务器”窗口连接到 NFS

要在 Linux 中创建 NFS 共享目录并从 Mac 客户端连接，请执行以下操作：

1. 在 Linux 服务器上，使用 NFS 功能导出共享目录，如第 18 章所述。不过，为了能够从 Mac OS X 使用共享目录，务必添加 `insecure` 选项。例如，要从名为 juicebox.linuxtoys.net 的 Linux 服务器共享 `/var/music` 目录，可以在该服务器的 `/etc/exports` 文件中添加以下行：

```
   /var/music        *(rw,insecure)
```
