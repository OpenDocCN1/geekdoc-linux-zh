
- 可被 Macintosh 系统共享。

- Windows 兼容 TCP/IP 打印机 -

  - 可被 Windows 系统共享。

  - 可在 Linux 中作为共享打印机。

- TCP/IP 兼容 PostScript 打印机 -

  - 可被 Windows 和 Macintosh 系统共享。

  - 可在 Linux 中作为共享打印机。

- Macintosh 兼容打印机 -

  - 只能与连接到它的 Macintosh 使用。

## 在 Linux 中使用共享打印机

### 仅由 Windows 系统共享的打印机

- Windows 兼容打印机。

  - 将主打印机连接到 Linux 并将其作为共享打印机使用。

- Windows 兼容 TCP/IP 打印机。

  - 指定 IP 地址并在 Linux 中将该地址设置为共享打印机。

### 同时兼容 Windows 和 Macintosh 系统的打印机

- PostScript 打印机。

  - 将主打印机连接到 Linux 并将其作为共享打印机使用。

- TCP/IP 兼容 PostScript 打印机。

  - 指定 IP 地址并在 Linux 中将该地址设置为共享打印机。

> 注意：第 5 章引入的 DHCP 服务器用于将其他 PC 连接到网络。如果不提前设置此，它们将无法正常连接。

## 共享打印机

### printcap 和 papd.conf

Linux 通过在 `printcap` 文件中记录连接到 Linux 的打印机和 TCP/IP 打印机来注册打印机。当配置了 `printcap` 时，Samba 使用这些信息允许来自 Windows 的打印机共享。共享时使用的打印机类型区别不大。然而，如果使用的是 PostScript 打印机，通过配置 `papd.conf` 文件并允许 `printcap` 中的注册信息反映，Macintosh 系统也可以共享该打印机。你可以在 `ftp.coriolis.com` 的 `linux_server_vbb` 文件夹在线查找下载 `printcap` 和 `papd.conf`。将这些文件放在 `/etc` 目录。

## 设置不同类型的打印机

Windows 兼容打印机（包括 PostScript 打印机）

按照出现的顺序读取以下所需的配置步骤：

- (1) 拷贝 `printcap`。

- (2) 编辑 `printcap` —— 配置连接到 Linux 的打印机。

Windows 兼容 TCP/IP 打印机（包括 PostScript 打印机）

按照出现的顺序读取以下所需的配置步骤：

- (1) 拷贝 `printcap`。

- (3) 编辑 `printcap`。TCP/IP 打印机配置。

Windows 和 Macintosh 系统共享的 PostScript 打印机

- (1) 拷贝 `printcap`。

- (2) 编辑 `printcap`。配置连接到 Linux 的打印机。

- (4) 从 Macintosh 配置共享的 Linux PostScript 打印机。

Windows-Macintosh 系统共享的 TCP/IP 兼容 PostScript 打印机

按照出现的顺序读取以下所需的配置步骤：

- (1) 拷贝 `printcap`。

- (3) 编辑 `printcap`。（TCP/IP 打印机配置)。

- (4) 从 Macintosh 配置共享的 Linux PostScript 打印机。

## 8.2 共享打印机

### (1) 拷贝 `printcap`。

#### 1 下载 `printcap` 文件。

将 `printcap` 文件下载到 `/usr/local/tmp` 目录。

#### 2 拷贝配置文件。

如果你还没有这样做，请使用 `cp` 命令将 `printcap` 文件拷贝到 `/etc` 目录。这里，`/usr/local/tmp` 是你存储下载文件的目录。

输入命令，如示例所示：

```
[root@server ~]# cp /usr/local/tmp/printcap /etc
[root@server ~]#
```

### (2) 编辑 `printcap`（配置连接到 Linux 的打印机）

#### 1 编辑配置文件。

输入命令。

```
[root@server ~]# vi /etc/printcap
```

编辑器已启动。

```
** Linux Local Printer
*printer:
  * sh:mx=0:
  * ip=/dev/lpd1:
  * sd=/var/spool/lpd/printer:
  * lf=/var/log/lpd-errs:

** TCP/IP Network Printer
*printer:
  * sh:mx=0:
  * rm=printer:
  * sd=/var/spool/lpd/printer:
  * lf=/var/log/lpd-errs:
```

修改此部分。

## 8. 共享打印机

### 重启 lpd。

- 删除井号 (`#`) 使设置生效。

#### 让打印机名称易于理解

在此示例中，共享打印机的名称为 `printer`。你应该使用类似打印机名称，让任何人都能识别分配了哪个打印机。

```
// Linux Local Printer printer:\n:sh.mx0:\n:lp=/dev/lp1:\n:sd=/var/spool/lpd/printer:\n:lf=/var/log/lpd-errs:
```

输入要共享的打印机名称（在列的前面）。

输入要连接的打印机端口（通常为 `/dev/lp1`）。

指定 spool 目录（与指定的打印机匹配）。

日志文件的位置。

- 修改相应位置并保存。

#### 创建 spool 目录。

#### 井号 (`#`) 的含义

查看输出时，你会看到每行开头都有井号 (`#`)。井号后面的内容被注释掉了。初始状态，spool 文件中的每一行都是被注释的，因为还没有设置。删除井号使设置生效。

输入命令。

```
[root@server]# mkdir /var/spool/lpd/printer
[root@server~]#
```

#### 重启 lpd。

重启 `lpd`（向打印机发送数据的服务器）和 `smb` 使更改生效。

- 目录。

- 输入命令。

```
[root@server]# mkdir /var/spool/lpd/lp
[root@server~]# cd /etc/rc/init.d/
[root@server init.d/./lpd restart
Shutting down lpd: lpd
Starting lpd: lpd
[root@server init.d/]#smb restart
Restarting SMB services: Shutting down SMB services: smbd nmbd
Starting SMB services: smbd nmbd
done
[root@server]# init.d/
```

### (3) 编辑 `printcap`（TCP/IP 打印机设置）

#### 1 编辑配置文件。

输入命令。

```
[root@server /root]# vi /etc/printcap
```

## Linux Local Printer

printer:

  :sh:mx0:

  :lp=/dev/lp1:

  :sd=/var/spool/lpd/printer:

  :lf=/var/log/lpd-errors:

## TCP/IP Network Printer

printer:

  :sh:mx0:

  :rm=printer:

  :sd=/var/spool/lpd/printer:

  :lf=/var/log/lpd-errors:

```

`vi` 编辑器已启动。

修改此部分。

- 删除井号 (`#`) 使设置生效。

> 注意：如果连接了多个打印机，通过复制这些行并更改 `printer` 行上的名称来配置每个打印机。

输入要共享的打印机名称（冒号前的部分）。

## TCP/IP Network Printer
printer:
  :sh:mx0:
  :rm=printer:
  :sd=/var/spool/lpd/printer:
  :lf=/var/log/lpd-errors:
```

> 输入 TCP/IP 打印机名称（用于对应 IP 地址）。

> 指定 spool 目录（与指定的打印机匹配）。

- 修改相应位置并保存。

> 提示！让打印机名称易于理解

在此示例中，共享打印机的名称为 `prinner`。你应该使用类似型号/类型的名称，让任何人都能识别分配了哪个打印机。

#### 2 指定连接打印机的 IP 地址。

分配一个 DHCP 之外外的 IP 地址（`192.168.1.27`）。

> 注意：每个 TCP/IP 打印机都有不同的 IP 地址设置方法。使用提供的说明设置 IP 地址。
