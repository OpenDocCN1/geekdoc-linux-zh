
## 600 第四部分 OpenLinux 网络和服务器设置

其他可用于 `COAS` 驱动程序的选项包括发送 `EOF`（如果打印机需要结束-of-文件代码来结束打印），纸张尺寸（用于选择所用纸张的尺寸），以及双面打印（如果打印机支持双面打印）。

因为大多数 `Caldera` 驱动程序使用依赖 `Ghostscript`（`gs` 命令）的打印过滤器，您可以在 `Additional GS` 框中输入额外的选项。

- `Uniprint` 驱动程序——选择 `Uniprint` 驱动程序后，您不仅选择打印机的型号名称，还选择其他属性。这些属性可以包括所用的纸张类型（或其他材料）、速度、彩色端口以及渲染信息。与 `COAS` 驱动程序相比，`Uniprint` 驱动程序允许您设置 `EOF`、双面打印和纸张尺寸。

5. 点击保存。打印机管理界面应出现，新打印机将被添加到列表中。

6. 为了使打印机可访问，您可能需要停止并重新启动打印机调度器。从打印机管理界面，点击打印机调度器按钮，然后点击启动调度器按钮。

### 使用 COAS 添加打印机

要在桌面上安装本地或远程 `Linux`/`Unix` 打印机，您可以使用 `COAS` 打印机配置窗口。虽然该工具比 `Webmin` 打印机界面更简单，但它仍然可以添加、删除和编辑打印机，并且可以启动和停止打印服务（`lpd` 守护进程）。`lpd` 守护进程在本章后面有描述。

1. 要从 `KDE` 桌面打开打印机配置窗口，请选择 `K⮕ Settings ⮕ COAS⮕ Peripherals ⮕ Printer`。图 18-2 显示了打印机配置窗口的示例。（如果在安装期间已添加打印机，它将出现在此窗口中）。

![](img/f0f494d795c6ea03cd25d687dd72914c_634_0.png)

> 图 18-2：在 `COAS` 打印机配置窗口中添加打印机并启动打印守护进程。

## 第 18 章 ♦ 设置打印服务器 601

2. 点击 `Printer ⇆ Add`。将出现选择打印机窗口。

3. 点击与您要添加的打印机最匹配的打印机型号。如果打印机是远程 `Linux` 或 `UNIX` 打印机，请点击 `Generic remote printer`。

如果打印机列表中没有出现，但它支持 `HP Printer Control Language`（`PCL`），您可以尝试选择一款 `HP` 打印机（例如 `HP LaserJet`）。对于 `PostScript` 打印机，如果列表中没有，您可以选择 `Generic PostScript`。

4. 在 `Name` 框中输入代表打印机的名称类型。（名称通常较短，例如 `ps1`、`hp3`、`lp0` 等。）

如果您正在配置远程 `Linux` 或 `UNIX` 打印机，将被要求输入远程主机名称和远程队列名称。远程主机是打印机连接的计算机的 `TCP/IP` 名称。它可能是本地网络中 `/etc/hosts` 文件中的打印机名称，或是经过域名系统解析的完全限定域名（`FQDN`）。远程队列是远程计算机用于本地标识打印机的名称。

5. 添加一些打印机属性。这些属性包括以下内容：

- 纸张尺寸——打印机使用的纸张尺寸（通常为 `Letter` 尺寸）。
- 设备——打印机连接的端口设备，通常为 `/dev/lp0`（第一个并行端口）。
- 速度——数据传输到打印机的速度。通常选择 `57600`，虽然速度范围从 `300 bps` 到 `468000 bps`。

其他属性可能因打印机类型而异。例如，通用 `PostScript` 打印机允许您每张纸打印两页。（此选项适用于打印草稿，并可将纸张消耗减半。）

6. 点击 `OK`。

7. 如果修改内容满意，点击保存按钮。

8. 如果您被询问是否要为新打印机创建打印机队列，请点击 `OK`。`lpd` 守护进程将重新启动（以激活新打印机），新打印机将出现在打印机配置窗口中。

![](img/f0f494d795c6ea03cd25d687dd72914c_634_2.png)

## 602 第四部分 OpenLinux 网络和服务器设置

要检查打印机是否正常工作，请尝试打印文档。例如，如果您的打印机名称为 `psl`，您可以如下打印 `/etc/printcap` 文件：

```
# /etc/printcap
# Please don't edit this file directly unless you know what you are doing!
# Be warned that COAS requires a very strict format!
# Other applications (like WordPerfect) cannot cope with LPRng-extensions
# to the syntax (those are best hidden in a 'lpd-printcap')
# The preferred method to modify this file is COAS.

lp:\
lp=/dev/lp0:\
br=57600:\
rm=\n rp=\nsd=/var/pool/lpd/lp:\
```

如果打印不工作，请尝试重新启动打印守护进程（`lpd`）。在打印机配置窗口中，点击 `Daemon <` 选择 `Daemon > Start`。这应该能工作。如果仍然失败并出现 “`device busy`” 错误信息时，您可能需要重新启动 `Linux` 计算机。

## 第 18 章 设置打印服务器 603

![](img/f0f494d795c6ea03cd25d687dd72914c_636_0.png)

在 `OpenLinux` 中启动和停止守护进程的首选方式是使用 `COAS` 系统服务窗口。您可能需要检查该窗口，确保 “`Print server (LPD)\`” 已打开。系统服务窗口在第 13 章中有描述。

## 第 18 章 ♦ 设置打印服务器 603

### 理解 LPRng 打印服务

`OpenLinux` 打印由 `LPRng` `spooling` 系统提供。`LPRng` 代表 `LPR Next Generation`。`LPRng` 软件在安全性方面提供了许多优势，相较于最初在 `UNIX` 系统中使用的旧 `LPR` `spooling` 设施。

`LPRng` 基于旧 `UNIX` 行式打印机设施（`lpr`）。这款新软件提供了管理多台打印机和队列的扩展功能，并具备许多安全特性。拥有数百台打印机的公司和学院使用开放的 `LPRng` 打印服务。

如果您只有一台用于家用电脑的打印机，您可能不需要了解 `mucho` 关于 `LPRng`。如果您管理着众多资源需求量大的计算机（例如大型企业），`LPRng` 为您提供了大量的控制权和安全性。

当有人在 `OpenLinux` 中发送打印请求时，`lpd`（行式守护进程）会处理该请求。`lpd` 进程处理本地用户的打印请求以及通过网络发送的打印请求。在 `OpenLinux` 中，`lpd` 进程在启动时由 `/etc/rc.d/init.lpd` 脚本启动（该脚本实际上链接到运行级别目录 `/etc/rc.d/rc?` 中的文件）。

## 604 第 IV 部分 OpenLinux 网络和服务器设置

```
:mx#0:
:sh:
:if=/var/spool/lpd/lp/printfilter:
```

打印机的名称是 `lpd`。发送到打印机的文件会 `spool` 到 `/var/spool/lpd/lp` `spool` 目录 (`sd`)，在那里它们等待直到被打印。打印机连接的设备是本地系统上的 `/dev/lp0`，它代表计算机上的第一个并行端口。负责会计的打印机文本过滤器是 `/var/spool/lpd/lp/printfilter`。

每个打印机条目实际上是一行。为使其更易阅读，惯例是把每个选项单独放在一行，并在行末加上反斜杠。请注意，最后一行没有反斜杠（表示条目结束）。

### 远程打印机示例

这是 `/etc/printcap` 文件中远程打印机条目的示例。如果您要添加名为 `altaps` 的打印机，它连接到名为 `alta` 的计算机上，并且名为 `psl`（`alta`），则 `/etc/printcap` 条目可能如下所示：

```
altaps:
:lp=/dev/lp0:
:br#57600:
:rm=alta:
:rp=ps1:
:sd=/var/spool/lpd/altaps:
:mx#0:
:sh:
:if=/var/spool/lpd/altaps/printfilter:
```

该条目中的关键信息是 `rm=alta` 行（标识远程打印机）和 `rp=ps1` 行（标识 `/var/spool/lpd/altaps` `spool` 目录，打印作业在此等待传输到远程计算机）。（虽然远程打印机条目中包含的其他选项可能并非必需，但它们不会造成伤害。）

如果在测试打印机时发送的打印作业被拒绝，可能是因为打印服务器计算机未允许您访问该打印机。请让远程计算机的管理员在 `/etc/hosts.equiv` 或 `/etc/hosts.lpd` 文件中添加您的主机名。

[PAGE 638]

## 第 18 章 + 设置打印服务器 605

```
snops:Postscript printer on Snowbird (SMB):
:lp=/dev/null:
:br#57600:
:rm=-
:rp=-
:sd=/var/spool/lpd/snops:
:max#0:
:if=/etc/sbin/ladmin/drivers/snops.smb:
```

在此情况下，打印机名为 `snops`（连接到名为 `Snowbird` 的计算机的 `Postscript` 打印机）。打印文件被发送到 `/var/spool/lpd/snops` 目录。打印过滤器是 `/etc/sbin/ladmin/drivers/snops.smb`。如果查看打印过滤器，可以看到对 `SMB` 打印机的打印工作正常。下面是创建的 `snops.smb` 过滤器：

```
#/bin/sh
# Name: snops
# Server: 10.0.0.18
# Share: snowps
# User:
# Password:
# Workgroup:
# Program: /var/spool/lpd/snops/printfilter
PATH_bin:/usr/bin:/sbin:sbin
export
PATH
/var/spool/lpd/snops/printfilter "$1" "$2" "$3" "$4" \
"$5" "$6" "$7" "$8" "$9" "$10" \
"$11" "$12" "$13" /tmp/$\$.smb \
smbclient '\$10.0.0.18\snowps' -n -c "print /tmp/\$.smb" -P
rm /tmp/$\$.smb
```

从 `Linux` 打印到 `SMB` 打印机的关键是使用 `smclient` 命令发送作业。在此示例中，打印文件由 `printfilter`（位于 `/var/spool/lpd/snops`）处理并复制到临时文件 (`/tmp/$\$.smb`)。随后 `smclient` 命令将文件 (`/tmp/$\$.smb`) 发送到计算机 (`10.0.0.18`) 和打印队列 (`snowps`)。

如果您尝试向 `SMB` 打印机打印但打印失败，请参阅本章后关于检查 `SMB` 打印机的章节。

[PAGE 639]

## 606 第 IV 部分 OpenLinux 网络和服务器设置

`OpenLinux` 没有提供简单创建远程 `NetWare` 打印机条目的方法。因此，您需要手动创建自己的 `/etc/printcap` 和过滤器文件。由于 `nwprint` 命令的限制，我们创建的过滤器假设 `NetWare` 打印设施有开放访问（例如 `GUEST` 登录），且使用打印机不需要密码。

以下是 `/etc/printcap` 中可能的 `NetWare` 打印机条目示例：

```
nwps:
  sd=/var/spool/lpd/nwps:
  mx#0=
  sh:
  af=/var/spool/lpd/nwps/acct:
  ip=/dev/null:
  if=/var/spool/lpd/nwps/nwprint1:
```

`spool` 目录的位置是 `/var/spool/lpd/nwps`。会计过滤器是 `acct`，位于 `spool` 目录中。由于文件未本地打印，`lpd` 设备名为 `/dev/null`。最后，我们创建的打印过滤器名为 `nwprint1`（它使用 `nwprint` 命令将文件传输到 `NetWare` 打印机）。

关于 `NetWare` 打印机的其他具体信息位于打印机的 `.config` 文件中（在我们的示例中位于 `/var/sp/lpd/nwps`）。

以下是远程 `NetWare` 打印机 `.config` 文件的示例内容：

```
server=nwps
queue=postpr1
```

如您所见，服务器和队列名称保存在该文件中。接下来，您需要创建 `spool` 文件并为其设置正确的权限。假设 `/var/sp/lpd/nwps` 是您的 `spool` 目录，以下是您在终端（以 `root` 用户身份）需要输入的命令：

```
cd /var/sp/lpd/nwps
touch acct nwprint1
chown daemon.lp .config *
chmod 600 *
chmod 700 nwprint1
```

首先，您进入 `spool` 目录（`cd`）。然后创建 `acct` 文件和 `nwprint1` 文件（`touch acct nwprint1`）。最后，将所有命令的所有权更改为 `daemon` 用户和 `lp` 组（`daemon.lp`）。

[PAGE 640]

## 第 18 章 + 设置打印服务器 607

最后，您需要创建过滤器，实际将文档发送到 `NetWare` 队列进行打印。在此情况下，我们调用过滤器 `nwprint1`。下面是该文件可能的内容示例：

```
eval acct_file=$$
spool_dir=`dirname "$acct_file"`
config_file="$spool_dir/.config"

logfile=/tmp/nw-print.log

cat "$config_file"

cat /usr/bin/nwprint -s server -q queue >> $logfile 2>&1
```

再次，这是一个非常简单的脚本，假设对 `NetWare` 打印有开放访问。要验证它是否工作，请在命令行中运行它。例如，要打印 `/etc/hosts` 文件，请在打印机的 `spool` 目录中输入以下命令：

```
cat /etc/hosts | sh -x /nwprint1
```

在此示例中，我通过将 `/etc/hosts` 文件与 `sh -x` 管道连接，能够看到脚本执行时的每一行。可以看到 `nwps` 服务器名称和 `ps1` 队列名称是从 `.config` 文件中读取的。这些值被传递给 `nwprint` 命令。如果文件未打印，您可以检查 `/tmp/nw-print.log` 文件以查看是否有错误报告。

[PAGE 641]
