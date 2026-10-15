
`lpadmin` 命令从 `/usr/share/ppd/` 文件解压并复制打印机驱动信息到 `/etc/cups/ppd`。生成的文件赋予了打印机名称：`/etc/cups/ppd/ColorPtr.ppd`。

你可以使用添加打印机时相同的选项通过 `lpadmin` 修改打印机配置。当你指定现有打印机的名称时，`lpadmin` 修改的是打印机而不是创建一个新的。

# 564 第 14 章 使用 CUPS 打印

下一条命令配置了一个带有 JetDirect 接口的 HP LaserJet 打印机，该接口直接连接到 LAN 的 192.168.1.103，并将该打印机命名为 HPLJ。在 URI 的协议中指定 `socket` 会指示 CUPS 使用 JetDirect 协议，这是 HP 为连接到网络的打印机开发的私有协议。

```
$ lpadmin -p HPLJ -E -v socket://192.168.1.103 -P /usr/share/ppd/custom/laserjet.ppd.gz
```

带有 `-d` 选项的 `lpstat` 显示默认打印机的名称：

```
$ lpstat
system default destination: MainPrinter
```

CUPS 会自动将你定义的第一个打印机设置为默认打印机。以下命令将 HPLJ 设置为默认打印机：

```
$ lpadmin -d HPLJ
```

以下命令移除 ColorPrt 打印机的配置：

```
$ lpadmin -x ColorPrt
```

## 打印配额

CUPS 提供了基本的打印配额。你可以定义两种形式的配额：页数和文件大小。文件大小配额几乎没有意义，因为一个小的 PostScript 文件可能需要很长时间来解释，而打印一个大文件需要大量的墨水。页数配额更有用，尽管它们的实现方式存在缺陷。要确定文档的页数，CUPS 会检查 PostScript 输入。如果作业是以打印机的原生语言（如 PCL）提交的，例如每张纸打印多页的脚本文件，CUPS 会计算原始文档中的每一页，而不是计算打印出来的每一张纸。

使用 `quota-period` 和 `job-quota-limit` 为每个用户建立配额。`job-quota` 选项指定配额有效的秒数。以下命令为名为 HPLJ 的打印机上的用户设置了每天 20 页的配额：

```
$ lpadmin -p HPLJ -o job-quota-period=86400 -o job-quota-limit=20
```

`job-quota-limit` 选项的工作原理类似，但它定义的是千字节（KB）为单位的文件大小限制。该限制是每个用户在配额期间可以打印的千字节总数。一旦用户超过了配额，在下一个配额周期之前，她将不允许再打印。

## 管理打印队列

当打印机正常运行时，它会将作业接收到队列中并按照接收顺序持有这些作业。你可以向打印机执行 `cupsreject` 命令后跟打印机名称，使其不再接受作业进入打印队列；执行 `cupsaccept` 命令。你也可以使用 `system-config-printer` 来控制打印队列；请参考第 551 页的“设置”。有两个因素决定打印机如何处理作业：打印机是否接受作业以及它是否已启用。第 551 页的表 14-1 描述了这两个因素各种组合的情况。

更改这些因素的工具是 `cupsdisable`、`cupsenable`、`cupsreject` 和 `cupsaccept`。每个工具接受打印机名称作为参数。以下命令禁用后重新启用名为 HPLJ 的打印机：

```
$ cupsdisable HPLJ
$ cupsenable HPLJ
```

接下来的命令导致 HPLJ 拒绝后接受作业：

```
$ cupsreject HPLJ
$ cupsaccept HPLJ
```

## 共享 CUPS 打印机

IPP 促进了远程打印。CUPS 配置文件 `/etc/cups/cupsd.conf` 中的 `Listen` 指令指定了哪个 IP 地址或哪个域接套字路径绑定并接受请求。`Listen` 指令具有以下格式：

```
Listen IP:port | path
```

其中 IP 是接受连接的地址，port 是 CUPS 用于连接的端口号，IP 和 path 是 CUPS 用于与打印机通信的域接套字路径。CUPS 通常使用端口 631。默认情况下，它绑定到 localhost。它还通过 `/var/run/cups.sock`（一个本地域接套字）与本地打印机通信。它还可以使用 Port 指令来指定它监听 HTTP 请求的端口。

```
$ grep -i listen /etc/cups/cupsd.conf
# 监听本地连接
Listen localhost:631
Listen /var/run/cups.sock
```

要允许其他系统连接到本地系统的 CUPS 服务器，你必须指示 CUPS 绑定到其他系统可以访问的 IP 地址。对于运行在 192.168.0.12 的 CUPS 服务器，以下指令是合适的：

```
Listen 192.168.0.12:631
```

该指令如果放在其他 Listen 指令之后，将导致 CUPS 在 IP 地址 192.168.0.12 端口 631 上监听。当你更改 `cupsd.conf` 时，需要调用 `cupsctl` 脚本来重启 `cupsd` 守护进程（第 549 页）。

`cupsd.conf` 中的某些指令使用 `@LOCAL` 宏，它是 CUPS 内部的并指定本地系统。该宏接受任何解析为本地系统的地址。

一旦重启 `cupsd`，远程系统就可以使用本地系统的 IP 地址在本地打印机上打印。或者，你可以使用访问列表来允许特定的机器。以下示例显示了如何使用 `<Location>`：

```
<Location />
  Allow @LOCALLOCAL
</Location>
```

访问列表定义在 `<Location>` 标签内。以下示例显示了如何使用 `<Location>`：

```
<Location />
  Allow 192.168.0.12
</Location>
```

访问列表定义在 `<Location>` 标签内。以下示例显示了如何使用 `<Location>`：

```
<Location />
  Allow 192.168.0.12
</Location>
```

访问列表定义在 `<Location>` 标签内。以下示例显示了如何使用 `<Location>`：

```
<Location />
  Allow 192.168.0.12
</Location>
```

允许 Linux 用户启动打印任务并使其能够删除该任务，但拒绝用户删除其他用户的打印任务的能力。请确保此目录存在并具有正确的所有权和权限：

```bash
$ ls -ld /var/spool/samba
drwxr-xr-x 2 root root 4096 Oct 10 10:29 /var/spool/samba
```

将以下两行放入 `/etc/samba/smb.conf` 文件的 `[global]` 部分中：

```
[global]
printing = cups
printcap = cups
```

打印机列表位于 `smb.conf` 中的 `[printers]` 部分。在接下来的示例中，该路径是 Samba 用作缓存目录的路径，而不是普通的共享目录。这些设置允许包括访客在内的任何用户使用打印机。默认 `smb.conf` 中的 `[printers]` 部分包含以下条，它们适用于大多数设置：

```
[printers]
comment = All Printers
path = /var/spool/samba
browable = no
guest ok = no
writable = no
printable = yes
```

理想情况下，每个计划打印的用户都应该有一个账户。否则，如果多个用户共享同一个账户（例如 `nobody`），他们可能会相互删除对方的打印任务。

### 打印到 Windows

CUPS 待 Windows 机器上的打印机的方式与看待任何打印机完全相同。唯一的区别在于你在连接时需要指定的 URI。要配置连接到 Windows 机器的打印机，请进入 CUPS Web 界面中的打印机页面，并选择“添加打印机”，就像你添加本地打印机一样。当要求你选择设备时，通过 Samba 选择 Windows。按以下格式输入打印机的 URI：

```
smb://system/printername
```
