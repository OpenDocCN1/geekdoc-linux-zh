
显示如下：

| 权限 | 所有者 | 组 | 大小 | 日期 | 名称 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `rw-r--r--` | `root` | `root` | `17335` | `Sep 25 2000` | `/etc/rc.d/lpd.cout` |
| `rw-r--r--` | `root` | `root` | `10420` | `Sep 25 2000` | `/etc/rc.d/lpd.perms` |
| `-rwxr-xr-x` | `root` | `root` | `2277` | `Sep 25 2000` | `/etc/rc.d/init.d/lpd -> ../init.d/lpd` |
| `-rwxr-xr-x` | `root` | `root` | `0` | `Mar 13 14:03` | `/etc/rc.d/rc.d/k601 -> ../init.d/lpd` |
| `-rwxr-xr-x` | `root` | `root` | `0` | `Mar 13 14:03` | `/etc/rc.d/rc.d/k602 -> ../init.d/lpd` |
| `-rwxr-xr-x` | `root` | `root` | `0` | `Mar 13 14:03` | `/etc/rc.d/rc.d/k603 -> ../init.d/lpd` |
| `-rwxr-xr-x` | `root` | `root` | `0` | `Mar 13 14:03` | `/etc/rc.d/rc.d/k604 -> ../init.d/lpd` |
| `-rwxr-xr-x` | `root` | `root` | `0` | `Mar 13 14:03` | `/etc/rc.d/rc.d/k605 -> ../init.d/lpd` |
| `-rwxr-xr-x` | `root` | `root` | `0` | `Mar 13 14:03` | `/etc/rc.d/rc.d/k606 -> ../init.d/lpd` |

`rc3.d` 中的 "3" 是我们感兴趣的。将 `S601lpd` 链接到 `rc3.d` 意味着当系统进入级别 3（即是系统的正常运行状态）时，`lpd` 将启动。

注意 `RedHat` 的 `setup` 命令有一个“系统服务（System Services）”菜单选项。服务列表将允许你管理哪些服务在启动时激活，从而创建符号链接。

### 21.4.7 临时文件 (Spool files)

用户程序位于某个一个 `bin` 目录中。在这种情况下，我们可以看到 `lpc`、`lpr`、`lprm` 和 `lptest`，以及它们相关的帮助页。

### 21.4.8 日志 (Log files)

守护进程和管理员命令位于 `ssbin` 目录中。在这种情况下，我们可以看到 `lpc`、`lpd`、`lpf` 和 `pac`，以及它们相关的帮助页。唯一的守护进程（后台）程序实际上是 `lpd` 程序本身，它是整个软件包的核心。

### 21.4.9 日志轮转 (Log rotation)

### 21.4.10 环境变量 (Environment variables)

# 21. 系统服务与 lpd

## 21.6 PostScript 与打印过滤器

它将 PostScript 通过 `lpr` 的 `stdin` 发送。所有没有自带打印机驱动程序的应用程序都会这样做。这意味着我们通常可以依赖这样一个事实：打印过滤器总是会接收到 PostScript。另一方面，`gs` 可以将 PostScript 转换为任何打印机的格式，因此剩下的工作就是确定它的命令行选项了。

如果你选择了“打印到文件（Print To: File）”，则可以使用 `gv` 程序查看生成的输出。尝试使用 `gv netscape.ps`，它会显示预览。在 Unix 上，大多数桌面应用程序没有自带的预览功能，因为 PostScript 打印机本身是由 `gv` 模拟的。

注意，过滤器程序不应与远程过滤器配合；远程打印机队列会“原样”发送其 PostScript 文件（如上面示例 `printcap` 文件中的 `if=/bin/cat:`）。这样一来，连接到设备的机器只需要唯一地为它进行特殊配置即可。

我们在本地打印队列使用的过滤器程序将是一个 脚本 `/var/spool/lpd/lp/filter`。通过以下命令创建过滤器：

```bash
/var/spool/lpd/lp/filter

chmod +x /var/spool/lpd/lp/filter
```

然后编辑它使其看起来像：

```bash
#!/bin/bash

cat gs -sDEVICE=ljet4 -sOutputFile=- -sPAPERIZE=a4 -r600x600 -q

exit 0
```

`-sDEVICE` 选项描述打印机，在本例中是惠尔士洛电 LaserJet 1100。许多打印机具有相似或兼容的格式；因此，不同于许多打印机的 `DEVICES` 数量少得多。要获取支持设备的完整列表，请使用 `gs -h` 并咨询以下内容（取决于你的发行版）：

```
/usr/doc/ghostscript-??devices.txt

/usr/share/doc/ghostscript-??Devices.htm

/usr/share/doc/gs/devices.txt
```

`-OutputFile=` 设置为写入到 `stdout`（作为过滤器时已加引号）。`-sPAPERIZE` 可以设置为 `11x17`、`a3`、`a4`、`a5`、`b3`、`b4`、`b5`、`halffetter`、`ledger`、`legal`、`letter`、`note` 以及手册页列出的其他值。你还可以使用 `-g<width=height>` 设置精确的像素大小，`-r600x600` 设置分辨率，`-q` 表示设置静默模式，抑制任何可能破坏 PostScript 输出的信息性消息，并从 `stdin` 而不是文件读取。

我们的打印机配置现在已完成。剩下的是设置 `lpd` 并打印。你可以在命令行上使用 `enscript` 包完成此操作。`enscript` 是将纯文本文件转换为格式良好的 PostScript 页的程序。`enscript` 的帮助页显示了大量的选项，但我们可以简单地尝试：

## 21.7 访问控制

```bash
echo hello | enscript -p - | lpr
```

在任何暴露在互联网上的机器上运行 `lpd` 都应该非常小心。`lpd` 出现过多次安全警报（参见第 44 章），实际上应该只在信任的局域网（LAN）内使用。

为了防止任何远程机器使用你的打印机，`lpd` 首先查找文件 `/etc/hosts.equiv`。这是一个允许打印到你的打印机的机器简单列表。我自己的文件如下：

```
192.168.3.8

192.168.3.9

192.168.3.10

192.168.3.11
```

`/etc/hosts.lpd` 文件执行相同的操作，但不会赋予这些机器对打印队列的管理权限。注意，其他服务（如 `sshd` 和 `rsh`（或 `in,rsh`））也会检查 `hosts.equiv` 文件，并将列表中的任何机器视为等效的。这意味着它们是完全信任的，且 `rsh` 不会在机器之间请求用户登录以进行身份验证。因此，这种行为是一个严重关注的问题。

`RedHot 7.0` 上的 `LPRng` 具有不同的访问控制机制。它可以根据多种方式进行任意限制，取决于远程用户和操作（即谁被允许操作队列）。`/etc/lpd.perms` 文件包含配置。文件格式非常简单，尽管 `LPRng` 的功能相当复杂——简而言之，`lpd.perms` 最等同于 `hosts.equiv`：

```bash
ACCEPT SERVICE-* REMOTEIP=192.168.3.8

ACCEPT SERVICE-* REMOTEIP=192.168.3.9

ACCEPT SERVICE-* REMOTEIP=192.168.3.10

ACCEPT SERVICE-* REMOTEIP=192.168.3.11

DEFAULT REJECT
```
