
`drwx-xr-x- 1 root 40996 Oct 17 13:05 usr`

`drwx-xr-x- 2 root 1024 Nov 8 09:55 var`


# `crontab -r`

# `crontab` for root


第一个命令显示了你创建的文件内容。接下来，执行 `crontab` 命令安装 `listing`。接着，执行 `crontab -l` 查看已安装的 `crontab` 文件。然后，以下示例显示了处理名为 `listing` 的 `crontab` 文件的过程：
（注：此处原文存在重复，翻译已去重）

## 表 10-2 Linux 设备文件示例

| 设备 | 注释 |
| :--- | --- |
| `/dev/hda` | 第一块 IDE 硬盘 |
| `/dev/hda1` | 第一块 IDE 硬盘的主分区 1（后续为 2、以此类推） |
| `/dev/hdb` | 第二块 IDE 硬盘（后续为 c、以此类推） |
| `/dev/hdb1` | 第二块 IDE 硬盘的主分区 1（后续为 2、以此类推） |
| `/dev/sda` | 第一块 SCSI 硬盘 |
| `/dev/sda1` | 第一块 IDE 硬盘的主分区 1（后续为 2、以此类推） |
| `/dev/sdb` | 第二块 SCSI 硬盘（后续为 c、以此类推） |
| `/dev/sdb1` | 第二块 SCSI 硬盘的主分区 1（后续为 2、以此类推） |
| `/dev/fd0` | 第个软驱 (A:) |
| `/dev/st0` | SCSI 带驱动 |
| `/dev/ttyS0` | COM1 上的串口 |

尽管你的系统中存在许多其他设备文件，但这些是较常用的几个。如前所述，设备文件为 Linux 内核提供了有关设备的重要信息。在执行输入/输出操作之前，Linux 内核需要了解关于该设备的大量信息。如果你决定创建自己的设备文件，你需要知道设备文件中的某些嵌入信息。如果你使用 `mknod` 命令创建自己的设备文件，你就需要知道其中的一些信息。在创建设备文件之前，使用 `lsdev` 命令列出 IA32 系统上安装的硬件：

| 设备 | DMA | IRQ | I/O 端口 |
| :--- | :--- | :--- | :--- |
| Com | 0 | 1 | fc80-fcff |
| cascade | 4 | 2 | fc80-fcff |
| dma | 0 | | 0008-008f |
| dmal1 | 0 | | 0000-001f |
| dma2 | 0 | | 00c0-00df |
| eth0 | 14 | | 01f0-01f7 |
| ide0 | 0 | | 03f6-03f6 |
| ide1 | 15 | | 0170-0177 |
| Intel | | | ff80-ff9f |
| isapnp | | | 0213-0213 |
| keyboard | 1 | | 0060-006f |
| Mouse | 12 | | 0cf8-0cff |
| pic1 | | | 0020-003bf |
| pic2 | | | 00a0-03bf |
| rtc | 8 | | 0070-007f |
| serial | 0 | | 03f8-03ff |
| timer | 0 | | 0040-005f |
| usb-uhci | 10 | | ff80-ff9f |
| vga | | | 03c0-03df |

设备文件

此 `lsdev` 列表显示了安装的硬件以及每个设备的相关信息。但请注意，像 `hda` 等设备并没有显示。关于设备文件的许多信息并未在 `lsdev` 中显示。查看 `/dev` 中的设备文件可以发现关于任何给定设备的大量信息。以下是 `mknod`（make node 的缩写）命令的格式，用于在系统中不存在该设备文件时手动创建它们：

现在仔细分析 `/dev` 中的一个设备文件。该设备名称为 `/dev/st0`。它是一个由 `c` 表示的字符设备（相对于块设备 `b` 或命名管道 `p`），主号为 9（对应 SCSI 带驱动器），次号为 0（对应驱动器号）。如果此设备不存在，创建它的 `mknod` 命令将如下：

```bash
mknod /dev/st0 9 0
```

执行此命令后，你就拥有了 SCSI 带驱动器设备文件。图 10-2 显示了 `mknod` 命令中的组件。当你查看 `/dev` 中的设备时，你将看到设备名称、设备类型、主号和次号。你可能永远不需要在系统中创建设备文件；但具备一些设备文件的背景知识是有好处。你无疑需要使用许多设备文件，例如你的硬盘、软盘、带驱动器等。因此，至少你只需要知道访问这些设备时将使用的名称。

图 10-2 `mknod` 命令
| 设备名称 | 主号 | 设备类型 | 次号 |
| ---

## 打印

UNIX 和类 UNIX 系统运行着多种与打印相关的程序，称为 `lp`（line printing 的缩写，意为“行打印”）。这些程序共同工作，以支持打印文本文件、格式化文档、图形文件等。本节涵盖了打印的基础知识，包括一些打印机管理的基础。

要简单地打印名为 `mbox` 的文件，你可以使用 `lp`（line printer 的缩写）命令，如下例所示：

```bash
martyp $ lp mbox
Job number is: 1
```

在此示例中，你请求打印 `mbox` 文件。你收到来自 `lp` 的返回消息，指示请求标识码。你可以通过一次 `lp` 请求打印多个文件，如下例所示：

```bash
martyp $ ls -l
total 80
-rw-r-- 1 martyp usr 350 Sep 27 07:22 dead.letter
-rw-r-- 1 martyp usr 2476 Sep 6 07:07 inst.out
-rw-r-- 1 martyp usr 0 Aug 21 06:45 lanadmin.list
-rw-r-- 1 martyp usr 1485 Sep 27 08:20 mbox
-rw-r-- 1 martyp usr 353 Sep 29 04:57 trip
martyp $ lp t* perf 635 Mar 21
```

输出显示了你系统中所有可用打印机的状态。在这个示例中，你可以看到有许多打印机连接到此系统。我从此输出中删除了几个打印机，因为内容太长了，无法包含在书中。其中几台打印机报告了警告信息，指示它们处于“离线”（down）状态，这无疑意味着它们无法打印。我们在这里不会讨论此类问题的故障排除，因为这几乎完全是系统管理员处理的问题。如果你想获取刚刚设置的默认打印机的状态，可以使用 `-d` 选项，如下例所示：

```
martyp $ lpstat -d
Queue Dev Status Job Files User PP % Blks Cp Rnk
---- --- --- --------- ---- -- -- --- 
ros2228 ros22 READY
```

我经常提交打印作业后操作得太快，需要取消它。在提交作业后，你可以使用 `cancel` 命令配合作业 ID 将其删除。可以使用之前示例中显示的作业编号配合 `cancel` 命令，或者使用打印机名称配合 `cancel`。较小的打印作业通常处理和打印得非常快。大型打印作业可能会在完成之前被取消。

如果你在提交作业时没有记下作业号，可以使用 `lpstat` 命令来获取作业号。表 10-3 列出了一些最常用的 `lp` 相关命令。请记住，其中某些命令与系统管理工作相关（如配置打印机），用户通常不会使用。

## 表 10-3 `lp` 命令

| 命令 | 说明 |
| --- | --- |
| `/usr/sbin/accept` | 开始接受并加入队列的作业 |
| `/usr/bin/cancel` | 取消已队列的打印作业 |
| `/usr/bin/disable` | 禁用打印设备 |
| `/usr/bin/enable` | 启用打印设备 |
| `/usr/sbin/lpfence` | 设置打印池文件的最小优先级（并非所有 UNIX 变体均可用） |
| `/usr/bin/lp` | 将一个或多个作业加入打印队列 |
| `/usr/sbin/lpadmin` | 使用提供的选项配置打印系统 |
| `/usr/sbin/lpsmove` | 将打印作业从一个设备移动到另一个设备 |
| `/usr/sbin/lpsched` | 启动 `lp` 调度守护进程 |
| `/usr/sbin/lpshut` | 停止 `lp` 调度守护进程 |
| `/usr/bin/lpstat` | 根据提供的选项显示打印状态 |
| `/usr/sbin/reject` | 停止接受并加入队列的作业 |

## Webmin

让我们来看一个 GUI 管理工具，你可以将其下载到 Linux 系统或几种 UNIX 变体之一。该工具是 Webmin，可以在 `www.webmin.com` 获取。我并不提倡使用这个特定的工具（尽管我认为它很棒），相反，我只是将其作为一个示例，说明你可以在各种操作系统上下载并配置的工具，从而在许多平台上拥有一个类似的工具。接下来的步骤在网站上，但我将涵盖安装 `webmin` 的一些较为显著的方面。虽然我尚未在 Integrity 服务器上使用过此工具，但我知道你们许多人正在 IA-32 上尝试 Linux，并可能会发现这个工具很有用。

我们通过下载我们需要的 Linux 版本开始加载 Webmin 过程——在这种情况下，是针对 Red Hat 的。下载的 Linux 软件是 RPM 格式，我们运行以下命令：

```
# RPM -U webmin-0.990-1.norarch.rpm
```

这会自动将 Webmin 安装在 `/usr/libexec/webmin` 中。该目录下创建了许多文件。特别感兴趣的是以 `config-` 开头的文件，它们显示了 Webmin 可用的许多操作系统发行版。还有诸如 `user-min` 等目录，其中包含了通过 Webmin 进行用户管理的相关文件和脚本。要运行 Webmin，打开浏览器窗口并连接到：

```
http://linuxdev:10000/
```

示例中使用的系统名称为 `linuxdev`，因此你需要将其替换为你的系统名称。这会在你的浏览器窗口中打开 Webmin，如图 10-3 所示。

你可以看到你可以执行各种与系统相关的任务。我们很快会回到“用户和组”（Users and Groups）。主“服务器”（Servers）选择也有许多执行选项，如图 10-4 所示。

## 附加系统主题

“服务器”区域包含了 Apache、FTP 等其他常用配置程序。回到“系统”（System）区域的“用户和组”，你会得到系统上所有用户的列表，如图 10-5 所示。此窗口显示了你可以修改修改的用户相关信息。如果你从此区域选择“创建新用户”（Create a new user），将得到图 10-6 所示的屏幕，在其中我们可以输入相关的用户信息。

查看和创建用户只是许多执行的系统管理任务之一。在“本地磁盘”（Local Disks）的“硬件和分区”（Hardware and Partitions）下，你可以得到图 10-7 所示的视图。

在图 10-7 中，显示有两个带有分区的磁盘。第一个磁盘有几个分区，第二个磁盘只有一个分区。我们可以通过选择相应磁盘并点击“添加”（Add）来添加分区。Webmin 还可以执行许多本节中未显示的功能。与许多工具一样，你可以下载、使用并修改它以自适应你的系统需求。

## Samba

Samba 是一种允许 Linux 或 UNIX 主机充当 Windows 系统文件服务器的应用程序，Windows 系统可以使用其原生网络访问 UNIX 文件系统和打印机。

- 1. 你指定了一个名为 `DEVENV` 的工作组。
- 2. 你希望密码被加密；你希望使用 `/etc/samba/smbpasswd` 文件来存储这些加密密码。你在 Windows 和 Linux 系统上将拥有同名的用户。
- 3. 你有一些关于共享定义（Share Definitions）的信息，例如让主目录（Home Directories）可浏览。

你只对 `smb.conf` 文件进行了这三处修改；然而接下来，你将运行一个名为 `testparm` 的 Samba 工具。该工具会检查你的 `/etc/smb.conf` 文件是否存在错误。该工具会产生很长的输出内容，我在这里不再包含，但你需要运行它并检查它产生的任何警告或错误：

`# testparm smb.conf`

```
Load smb config files from smb.conf
Processing section "[homes]"
Processing section "[printers]"
Loaded services file OK.
Press enter to see a dump of your service definitions
## Global parameters
[global]
ncoding system =
client code page = 850
code page directory = /usr/share/samba/codepages
workgroup = DEVENV
netbios name =
netbios aliases =
netbios scope =
server string = Samba Server
interfaces =
bind interfaces only = No
security = USER
encrypt passwords = Yes
update encrypted = No
allow trusted domains = Yes
hosts equiv =
min passwd length = 5
map to guest = Never
null passwords = No
obey pam restrictions = Yes
password server =
smb passwd file = /etc/samba/smbpasswd
```

## 用户设置

运行 `testparam` 没有产生任何警告或错误，因此继续进行下一步。

你现在需要在 Linux 和 Windows 系统上都创建一个用户，用于我们与 Samba 相关的工作。你的系统中可能已经有了合适的用户。为了演示之目的，你将在两个系统上都创建一个用户。

在 Linux 系统上，你可以使用命令行中的 `useradd` 程序或图形化用户管理器程序（程序-系统-用户管理器）来添加用户。用户在被添加后会出现在 `/etc/passwd` 文件中。然后，执行以下命令将加密后的用户密码添加到 `/etc/samba/smbpasswd` 文件中：

```bash
# smbpasswd -a linuxconnect
```

`linuxconnect` 是本例中创建的用户名称。你可以查看 `smbpasswd` 文件来查看该用户的条目。同一个用户在 Windows 系统上也已经创建了。通过开始-程序-管理工具-计算机管理（本地用户和组-用户）菜单创建了 `linuxconnect`。

## Samba 启动

你可以在每次系统启动时启动 Samba 守护进程或在命令行启动它们。以下命令显示了如何在命令行启动守护进程并查看它们：

## `smb.conf` 设置

```
# /sbin/service smb start
Starting SMB services:   [ OK ]
Starting NMB services:  [ OK ]
# ps -ef | grep mbd
root      10828 1 0 16:59:50 00:00:00 smbd -D
root      10833 1 0 16:59:57 00:00:00 nmbd -D
#
```
