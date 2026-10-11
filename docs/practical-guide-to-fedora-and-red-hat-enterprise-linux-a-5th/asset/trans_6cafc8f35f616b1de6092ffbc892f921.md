
## 打印机类（CLASSES）

CUPS 允许你将类似的打印机组织成一个称为“类”的组。对于客户端而言，一个打印机类看起来就像一台单独的打印机。对于每个类，你必须指定一个名称；可选地，你还可以指定位置和描述。一台打印机可以属于多个类。CUPS 会将发送到某个类的作业打印在该类中第一台可用的打印机上。例如，你可以将打印任务分为黑白任务和彩色任务。如果有多台打印机可以分别满足这些角色，你可以允许用户手动选择打印机，或者定义两个打印机类（黑白和彩色），让用户将作业发送到特定的打印机类。

## 面向未来的规划

> **提示：** 如果你预计将向网络中添加更多打印机，建议在设置网络时配置包含现有打印机的类。这样，你以后就可以添加新的打印机，而无需更改客户端系统上的打印机配置。

要定义一个类，首先点击页面顶部的 **Administration**（管理）选项卡，然后点击 **Add Class**（添加类）。至少，你必须为该类输入一个名称。你还可以输入描述和位置。**Members**（成员）列表显示了所有 CUPS 打印机和类的名称。高亮显示你想作为正在定义的类成员的打印机；按住 **Shift** 键并点击另一台打印机以高亮显示多台打印机。

要定义一个包含列表中不相邻打印机的类，先定义一个只有一台打印机的类，然后在创建后修改该类以添加其他打印机。要修改现有类，请在 Administration 选项卡中点击 **Manage Classes**（管理类）。

## 命令行下的 CUPS

除了使用 Web 界面外，你还可以通过命令行控制 CUPS 并管理打印队列。本节介绍了用于管理打印机和打印队列以及建立打印配额的实用程序。

### lpinfo：显示可用驱动程序

**PPD 文件** **lpinfo** 实用程序提供关于 CUPS 可用的打印机驱动程序和接口的信息。**-m** 选项显示可用的 PostScript 打印机定义（PPD）文件/驱动程序的列表。

```
$ lpinfo -m | head
drv:///hp/hpcups.drv/apollo-2100.ppd Apollo 2100, hpcups 3.9.8
drv:///hp/hpcups.drv/apollo-2150.ppd Apollo 2150, hpcups 3.9.8
drv:///hp/hpcups.drv/apollo-2200.ppd Apollo 2200, hpcups 3.9.8
drv:///hp/hpcups.drv/apollo-2500.ppd Apollo 2500, hpcups 3.9.8
drv:///hp/hpcups.drv/apollo-2600.ppd Apollo 2600, hpcups 3.9.8
drv:///hp/hpcups.drv/apollo-2650.ppd Apollo 2650, hpcups 3.9.8
gutenprint.5.2://pcl-apollo-p2100/expert Apollo P-2100 - CUPS+Gutenprint v5.2.4
gutenprint.5.2://pcl-apollo-p2100/simple Apollo P-2100 - CUPS+Gutenprint v5.2.4 Simplified
gutenprint.5.2://pcl-apollo-p2150/expert Apollo P-2150 - CUPS+Gutenprint v5.2.4
gutenprint.5.2://pcl-apollo-p2150/simple Apollo P-2150 - CUPS+Gutenprint v5.2.4 Simplified
```

## URL

CUPS 使用 URL（第 525 页）根据类型和位置来识别打印机端口，正如 Web 浏览器通过协议和位置识别文档一样。并行端口的 URL 格式为 `parallel:/dev/lp0`；远程 LPD 打印机使用格式 `lpd://192.168.0.101`。当以 root 权限运行时，带有 `-v` 选项的 `lpinfo` 提供可用连接的列表：

```
# lpinfo -v
network smb
network socket
network lpd
network ipp
network http
network https
network scsi
direct scsi
parallel:/dev/lp0
serial serial:/dev/ttyS0?baud=115200
serial serial:/dev/ttyS1?baud=115200
direct hp
direct hpfax
```

`lpinfo` 的 `-v` 选项不会显示 socket、HTTP、IPP、LPD 和 SMB 协议的所有可能网络地址，因为 IPv4 地址空间中有超过 40 亿个这样的地址。

## lpadmin：配置打印机

你可以使用 `lpadmin` 实用程序向系统添加和删除打印机、修改打印机配置以及管理打印机类。此实用程序有三个主要选项：`-d`（设置默认打印机）、`-x`（删除打印机）和 `-p`（添加或修改打印机）。前两个选项很简单；示例将在下一个小节中给出。这三个选项中的每一个都接受一个作为打印机名称的参数。打印机名称必须以字母开头，且不能包含空格。

### 添加或修改打印机

通过以下格式的命令来添加打印机或修改现有打印机：

```
$ lpadmin -p printer-name options
```

其中 *printer-name* 是打印机名称，*options* 是以下列表中选项的组合：

- `-c class` 将打印机添加到 *class*（类），如有必要则创建该 *class*。
- `-D info` *info* 是一个用于向用户描述打印机的字符串；它本身对系统没有意义。如果 *info* 包含空格，请将其放在引号内。
- `-E` 启用打印机，指示 CUPS 接受进入其打印队列的作业。
- `-L loc` *loc* 是一个指示打印机物理位置（例如，办公室、建筑物、楼层）的字符串。它对系统本身没有意义。如果 *loc* 包含空格，请将其放在引号内。
- `-m model` *model* 是描述该打印机的 PPD 文件（第 533 页）的名称。使用 `lpinfo -m` 显示已安装 PPD 文件的列表。如果你有制造商提供的 PPD 文件，请将其复制到 `/usr/share/cups/model`。使用 `-P` 选项指定文件的路径名。例如，指定 `-m postscript.ppd.gz` 等同于指定 `-P /usr/share/cups/model/postscript.ppd.gz`。
- `-P file` *file* 是描述该打印机的 PPD 文件（第 533 页）的绝对路径名。使用 `lpinfo -m` 显示已安装 PPD 文件的列表。如果你有制造商提供的 PPD 文件，请将其复制到 `/usr/share/cups/model`。参见 `-m` 了解指定 PPD 文件的另一种方式。
- `-r class` 将打印机从 *class* 中移除。如果移除打印机后 *class* 为空，此选项将移除该 *class*。
- `-v URI` *URI* 是打印机连接到的设备。使用 `lpinfo -v` 列出可能的设备。

### lpadmin 命令示例

向系统添加打印机时，至少需要提供设备（device）和型号（model）。以下命令向系统添加一台 Epson Stylus Color 打印机并启用其使用。该打印机本地连接到第一个并行端口，并命名为 ColorPtr。

```
# lpadmin -p ColorPtr -E -v parallel:/dev/lp0 -m stcolor.ppd.gz
```

上一条命令生成的打印机信息存储在该 `/etc/cups/printers.conf` 文件中：

```
$ sudo cat /etc/cups/printers.conf
# Printer configuration file for CUPS v1.3.9
# Written by cupsd on 2008-10-18 10:46
<Printer ColorPtr>
Info ColorPtr
DeviceURI parallel:/dev/lp0
State Idle
StateTime 1180495957
Accepting Yes
Shared Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
OpPolicy default
ErrorPolicy retry-job
</Printer>
```

`lpadmin` 命令会解压缩并复制打印机驱动信息，从 `/usr/share/cups/model/stcolor.ppd.gz` 文件复制到 `/etc/cups/ppd`。生成的文件以打印机名称命名：`/etc/cups/ppd/ColorPtr.ppd`。

你可以使用 `lpadmin` 和添加打印机时使用的相同选项来修改打印机配置。当你指定一个现有打印机的名称时，`lpadmin` 会修改该打印机，而不是创建一个新打印机。

下一条命令配置一台具有 JetDirect 接口的 HP LaserJet 兼容打印机，该打印机直接连接到位于 192.168.1.103 的局域网，并将此打印机命名为 HPLJ。在 URI 的协议部分指定 `socket` 会指示 CUPS 使用 JetDirect 协议，这是一种由 HP 开发的专用于直接连接到网络的打印机的专有协议。

```
# lpadmin -p HPLJ -E -v socket://192.168.1.103 -m laserjet.ppd.gz
```

带有 **-d** 选项的 `lpstat` 实用程序显示默认打印机的名称：

```
$ lpstat -d
system default destination: MainPrinter
```

CUPS 自动将定义的第一台打印机设置为默认打印机。以下命令将 HPLJ 设置为默认打印机：

```
$ lpadmin -d HPLJ
```

以下命令删除 ColorPtr 打印机的配置：

```
$ lpadmin -x ColorPtr
```

## 打印配额

CUPS 提供基本的打印配额功能。你可以定义两种形式的配额：页数和文件大小。文件大小配额几乎是没有意义的，因为一个小的 PostScript 文件可能需要很长时间来解释，并且可能比大的文件需要更多的墨水。页数配额更有用，尽管其实现存在缺陷。为了确定文档中的页数，CUPS 会检查 PostScript 输入。如果作业是以打印机的母语（如 PCL）提交的，CUPS 会绕过这种统计机制。此外，如果使用 `mpage` 创建在每张纸上打印多页的 PostScript 文件，CUPS 统计的是原始文档中的每一页，而不是它打印的纸张。

使用 **job-quota-period** 以及 **job-page-limit** 或 **job-k-limit** 为给定打印机上的每个用户建立配额。**job-quota-period** 选项指定配额保持有效的秒数。以下命令为名为 HPLJ 的打印机建立每天每用户 20 页的配额：

```
$ lpadmin -p HPLJ -o job-quota-period=86400 -o job-page-limit=20
```

**job-k-limit** 选项工作原理类似，但以千字节定义文件大小限制。限制是每个用户在配额期间可以打印的总千字节数。一旦用户超过其配额，在下一个配额周期之前，他们将不被允许打印。

## 管理打印队列

当打印机正常运行时，它接受进入其打印队列的作业，并按接收顺序打印这些作业。你可以输入命令 **cupsreject** 后跟打印机名称，以指示打印机不接受进入其打印队列的作业；输入命令 **cupsaccept** 以重新启用接受。你也可以使用 **system-config-printer** 来管理打印队列。

