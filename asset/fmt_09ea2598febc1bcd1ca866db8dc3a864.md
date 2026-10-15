
接下来你必须从屏幕列表中输入时区。你现在可以选择将计算机时钟设置为本地时区或 GMT。接下来你必须输入计算机的主机名和域名，无论你是否连接到网络。当你输入主机名而不跟随域名时（也就是说，`myhost`, `myhost.domain.net`），接下来你决定你是否将使用真实网络（而不是调制调器）。如果你在网络上，你必须指定如何进行 IPset。你可以使用 DHCP 或静态 IP 地址。如果你选择 DHCP，你不需要输入任何其他内容。如果你使用静态 IP 地址，你必须在下一页输入某些地址。第一个必须输入的选项是用于使用网络的接口类型。如果你计划使用以太网卡，选择 `eth0`。如果你选择 `plip`。

# [第一部分] LINUX 介绍与安装

网络管理员。如果你选择了 `plip`，你必须指定你正在使用的并行端口（`plip0`=并行端口 1，`plip1`=并行端口 2，依此类推）。你还必须指定该端口的 IRQ 和基 IO 地址。如果你不知道这些信息，通常可以从 BIOS 或系统设置菜单获取。在内核版本中，并行端口根据其 IO 基地址进行命名。例如，`0x378` 对应 `plip0`，`0x3bc` 对应 `plip1`。

下一个选项是是否在启动时启动 `inet`。如果你选择启动，你将无法将机器作为服务器使用，因为 Linux 将无法处理任何入站网络请求。大多数用户在此处应选择 Yes（是）。出于类似的原因，你也应该在启动时启动 `portmapper`。如果你打算将计算机用作 NFS（网络文件系统）服务器（它提供网络文件共享），那么你就需要这样做。

对于下一个问题，你应该选择 Yes。你还必须指定你将要使用 DNS 服务器。大多数连接互联网的用户在此处会选择 Yes。如果你不知道 DNS 服务器的 IP 地址，请联系你的网络管理员。如果你正在使用网络，你需要选择你正在使用的网卡类型以便加载驱动程序。从列表中选择你的网卡。如果在列表中没有看到它，尝试查找你网卡的芯片并查看它是否在列表中。如果你仍然无法加载驱动，应该检查硬件兼容性列表，查看你的网卡是否受支持。

接下来，你有三个选项从你的新 Linux 机器发送邮件。大多数用户应该选择第一个选项。如果你不计划在这台机器上发送任何邮件，你可能想使用最后一个选项并且不安装 `/etc/sendmail.cf`。

安装程序现在将启动一个新窗口并完成你的系统配置。你的计算机现在将启动新安装的 SuSE Linux 版本。它将开始加载，然后你必须为 root 账户添加密码。这非常重要，因为该账户用于管理任务。然后你必须确认你的密码。接下来，如果你有调制解器，你还有设置调制解器的选项。如果你有调制解器，发生发生仅仅将是在你调制解器所在的串口和 `/dev/modem` 之间创建一个链接。

接下来，你将设置鼠标。如果你在提供的列表中没有看到鼠标，你应该尝试选择微软兼容串口鼠标（Microsoft Compatible Serial Mouse）或 PS/2 鼠标，取决于你用的是串口鼠标还是 PS/2 鼠标。现在你可以选择在启动时启动 GPM，这样你可以在文本模式下使用鼠标。接下来，你可以通过启动 GPM 来测试鼠标的配置。如果你的鼠标不起作用，你可能需要尝试不同的驱动程序。

你的系统将进行一些最后的配置。这是自动完成的。安装程序 YaST 不会自行终止。系统将进行更多配置，然后提示你按回车键以完成配置脚本。执行此操作，并在在此期间等待几分钟。

## [3] 安装 LINUX

恭喜你！你现在应该看到登录提示符，并可以使用 root 账户登录了。

## 故障排除

如果安装过程中出现任何问题，你应该能够轻松地重新安装程序。如果你在硬件方面遇到问题，建议咨询兼容性列表以确保你的硬件在 Linux 下确实可以工作。如果你在配置网络设置时遇到问题，应该咨询你的网络管理员双检一切。

如果由于更改了某些设置导致系统由于某些原因无法启动，有三种修复方法。在启动时的 LILO 提示符处，你可以进入用户模式（single mode）或紧急模式（emergency mode）。单用户模式允许你以最少设置且无网络连接的状态加载系统。此模式用于修复错误的脚本、驱动程序或网络问题。你必须知道 root 密码才能进入。要启动单用户模式，请重启计算机并在 LILO 提示符处输入 `single` 来启动系统。

紧急模式允许在系统损坏到无法修复时恢复系统上的任何重要文件。紧急模式将启动并在只读模式下挂载主分区，仅加载最基本的要求。你现在可以将系统上的任何内容备份到软盘或其他类型的备份源（磁带、zip 磁盘等）。但是，你无法向主 Linux 分区写入内容。这应该只在重新安装整个系统之前使用。你可以在 LILO 提示符处输入 `linux emergency` 进入紧急模式。你需要 root 密码才能进入紧急模式。

如果系统出现任何问题，你还有第三种选择——可以使用救援盘。如果内核损坏、LILO 损坏或所有启动文件损坏导致完全无法启动，可以使用救援盘。救援盘可以使用 CD-ROM 上的镜像之一制作：`rescue.img`。只需使用 UNIX 下的 `write` 或 `dt` 命令将此镜像写入软盘。将此镜像插入你的驱动器并从其启动。

## 安装与配置 LILO

LILO 代表“Linux Loader”，它是允许你从硬盘启动到 Linux 的程序。LILO 从 `/etc/lilo.conf` 读取几个配置选项，然后当你在提示符处输入 `lilo` 时，它会配置你的系统以启动 Linux。以下是一个仅启动 Linux 的 `/etc/lilo.conf` 文件的示例：

```
%cat /etc/lilo.conf
boot=/dev/hda
read-only
prompt
```

# [第一部分] LINUX 介绍与安装

```
timeout=10
vga=normal
#Beginning of Linux section
root=/dev/hda1
image=/boot/vmlinuz
label=linux
```

第一行指定写入 写入的位置。在这种情况下，它被写入 `/dev/hda` 的开头（512 字节），称为主引导记录（MBR）。MBR 是 BIOS 在尝试加载操作系统时通常查找的地方。

第二行指定硬盘应以只读方式挂载。这是为了在启动时运行 `fsck`（检查坏块）。操作系统随后将将其重新挂载为读写。

第三行使其在不按键的情况下显示启动提示符。如果省略，LILO 将默认启动 `/etc/lilo` 中指定的第一个操作系统。

在第四行中，`timeout` 之后的数字是在加载默认操作系统之前等待启动提示符的时间（以秒为单位）。示例中只有一个操作系统，因此它是默认的。如果配置文件中有多个操作系统，请添加 `default=imagename` 行。

在第五行中，`vga=` 指定显示内容的默认分辨率。三个常用设置：Normal（80x25 文本模式）、Extended（80x50 文本模式）和 Ask（提示用户输入自定义分辨率）。

第六行是添加到文件的注释，显示接下来的三行是关于操作系统的信息，而不是 LILO 的自定义选项。文件中任何以 `#` 开头的文本 LILO 都无法读取，仅有助于读者更好地理解文件。

第七行告诉 LILO 哪个分区将挂载为根分区。它需要根目录的位置因为 `/etc`

第八行告诉 LILO 内核的位置。内核是 `/boot/vmlinuz`。

第九行告诉 LILO 如何命名此操作系统。如果你在 LILO 下安装了多个操作系统，你只需在启动提示符处输入 `linux` 即可启动（在此示例中为 `label=linux`）。

如果你以后编辑了此文件，重要的是务必始终输入 `lilo` 以便新更改写入驱动器。否则，尽管文件更改了，LILO 将仍使用其旧配置。

在 LILO 中为备份内核（一个你确定可以工作的内核）创建一个条目可能是个好主意，以防你决定升级到一个损坏的内核。这可以通过简单在 LILO 中为 Linux 添加另一个条目来实现：

```
%cat /etc/lilo.conf
boot=/dev/hda
read-only
prompt
timeout=100
vga=normal
#Beginning of Linux section
root=/dev/hda
image=/boot/vmlinuz #new kernel
label=linux
#Beginning of Backup section
image=/boot/backup #backup kernel
label=backup
```

注意，没有必要定义两次根分区的位置。只有当两个内核都位于同一个分区时才需要这样做。若要在出现问题时使用此备份内核，只需在启动提示符处十秒内输入 `backup`（否则默认将启动第一个内核）。

## Windows 9x/DOS 双启动（Dual Boot）

如果你有另一个操作系统，例如 Windows 9x、DOS 或 OS/2，LILO 能够让你在启动电脑时引导到该操作系统或 Linux。要实现此操作，请参考下例 `/etc/lilo.conf` 文件：

```
%cat /etc/lilo.conf
boot=/dev/hda
read-only
prompt
timeout=100
vga=normal
#Beginning of Linux section
root=/dev/hda
image=/boot/vmlinuz
label=linux
#Begin DOS section
other=/dev/hdb1
label=DOS
```

最后两行是启动另一个操作系统所需的全部。第 11 行指定了备用操作系统的位置，`other=/dev/hdb1` 在此处起到相同的作用。第 12 行指定了在启动提示符处输入什么来引导此备用操作系统。在这种情况下，要启动 DOS 或 Windows（取决于 `/dev/hdb1` 上是哪一个），请在启动提示符处输入 `DOS`。如果你想让此操作系统默认启动，可以设置标记 `default=DOS`。

## Windows NT 双启动

如果 NT 在另一个驱动器上，你无法使用之前的方法来安装 LILO。这是因为 LILO 正在被写入 MBR，而 NT 必须从 MBR 启动（LILO 将覆盖 NT，导致 NT 无法访问）。如果你已经写入了 MBR，恢复 NT 的唯一方法是使用 NT 救援磁盘（在安装 NT 期间它提示你制作一个，或者你也可以从别人那里借一个）。然后你必须用此磁盘恢复 MBR。

要实现 NT 和 Linux 的双启动，你有两个选择：你可以每次从软盘启动 Linux，或者以一种特殊方式安装 LILO。制作软盘简单的方法是输入以下命令：

```
%cat /boot/vmlinuz > /dev/fd0
```

假设你的内核是 `/boot/vmlinuz`，这将直接将内核写入软盘。你必须确保内核已配置为正确挂载根文件系统。这是通过 `rdev` 命令完成的。将内核写入软盘后，你应该输入类似的内容：

```
rdev /dev/fd0
Root device /dev/hda1
```

如你所示，此启动磁盘的根设备将是 `/dev/hda1`。如果显示的根分区位置错误，你可以输入 `rdev /dev/fd0 [root partition]`，如下所示：

```
rdev /dev/fd0
rdev /dev/hda2
Root device /dev/hda2
```

现在你可以重启系统并从此磁盘启动，而无需配置或安装 LILO。

双启动的另一种方法稍微复杂，涉及安装 LILO，但不是在 MBR 上。技巧是将 LILO 安装在安装 Linux 的 `/dev/hdb1` 所在的硬盘开头。你需要编辑 `/etc/lilo.conf`，使第一行的内容为 `boot=/dev/hdb`。你应当确保 `/etc/lilo.conf` 文件的其余部分只配置了 Linux（应该只有一个 Linux 的条目；这里不应为 NT 设置任何内容）。然后通过命令行提示符处输入 `lilo` 将 LILO 写入驱动器。

接下来，你必须将驱动器的前 512 字节（你写入 LILO 的地方）复制到一个文件中，然后你可以使用该文件从 NT 引导加载程序启动 Linux。这是通过执行类似的命令完成的：

```
%dd if=/dev/hdb of=/tmp/lilo.img bs=512 count=1
```

## [3] 安装 LINUX

这假设 LILO 已写入 `/dev/hdb` 并在 `/tmp` 中创建了 LILO 镜像。该文件现在被称为 `lilo.img`。你现在应该将此文件拷贝到软盘并启动 Windows NT。从 NT 中，你必须将 `lilo.img` 从软盘拷贝到硬盘，最好是 `C:\`。你现在必须手动编辑 `C:\boot.ini` 文件并为 LILO 添加条目。要执行此操作，你必须先更改 `boot.ini`（它默认为只读模式）。通过右键点击它并选择“属性”来实现。你应该添加新行，使软盘看起来如下：

```
[boot loader]
time=3
default=disk(0)disk(0)partition(1)\WINNT
[operating systems]
lilo=disk(0)disk(0)partition(1)\WINNT
```

现在，确保软盘看起来如下：

```
[boot loader]
time=3
default=disk(0)disk(0)partition(1)\WINNT
[operating systems]
lilo=disk(0)disk(0)partition(1)\WINNT
```
