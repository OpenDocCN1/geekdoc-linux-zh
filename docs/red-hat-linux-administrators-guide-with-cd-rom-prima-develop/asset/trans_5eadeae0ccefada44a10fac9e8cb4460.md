
## 编辑 LILO 配置

如果是第一次编译，且通常使用 LILO 来配置启动顺序，则可能需要编辑 `/etc/lilo.conf` 文件。否则，您可能需要一个 LILO 引导扇区位于软盘上。这是一种较小的安全措施，以防不希望他人能够将机器重启进入单用户模式并重新设置 root 密码。您可以随身携带软盘，从而防止未经防护的重启。强烈建议对机器采取物理安全措施，以防止未经授权的访问。然而，如果您将 LILO 放置在主引导记录（MBR）或 `/dev/hda1` 上，并且机器确实重启，它应在片刻后恢复启动，无需手动更换引导软盘。

请务必备份发行版提供的 lilo.conf 文件副本。如果进行了更改后发现新设置可能无效，拥有此备份副本将使您能够轻松恢复默认设置。将预装的 lilo.conf 复制到其他文件名。以下是一种可能的建议：

```bash
# cp /etc/lilo.conf /etc/lilo.conf.DIST
```

`DIST` 扩展名将该文件标识为发行版文件，即随默认安装提供的文件。

此文件在很大程度上取决于您的系统。清单 14.1 展示了包含注释的来自我本人系统的示例。第一部分是新内核的默认位置，通常是 `/boot/vmlinuz` 文件。第二部分列出了您可能当前正在使用的旧文件。这是一个经过验证的内核，因此我通常将其发布版本号作为其名称。最后一个内核版本通常是较旧的发行版内核。如果使用 Red Hat 5.x 或 6.x 版本，这可能是 2.0.x 或 2.2.x 内核，因此命名为 linux.old。

### 清单 14.1 示例 lilo.conf 文件

```ini
#
# general section
#
boot=/dev/hda
# install=/boot/boot.b
# message=/boot/message
prompt

#
# wait 20 seconds (200 10ths) for user to select
# the entry to load
#
timeout=200

#
# default entry
#
image=/boot/vmlinuz
  label=linux
  root=/dev/hda1
  read-only

#
# golden entries
#
image=/boot/vmlinuz-2.2.16
  label=linux.golden
  root=/dev/hda1
  read-only

#
# older entries
#
image=/boot/vmlinuz-old
  label=linux.old
  root=/dev/hda1
  read-only

#
# end of file
#
```

在此文件中，我授予了自己几个安全选项。首先，当 Linux 首次启动时，通常会在 LILO: 提示符处停止。我给自己预留了 20 秒时间来选择希望启动的内核类型。在该提示符下，我可以按 Tab 键查看可用选项：linux、linux.golden 和 linux.old。如果机器是双启动或三启动机器，您可能还需要包含特定 Windows 版本或其他操作系统的设置。您可以在 lilo.conf 中输入备用启动分区的设置。

在初始安装期间，确保其他操作系统已经安装，因为 LILO 会覆盖主引导记录上的任何引导记录。Red Hat 还将尝试检测其他系统，并允许您选择将其中一个设置为默认系统。

lilo.conf 中的第一个条目也是默认操作系统。由于标记为 linux 的内核是第一个条目，该内核将在 20 秒后开始启动，无需我进行任何交互。通过在第一节中放置 Windows 分区的条目，我确保 Windows 是我的默认启动操作系统。如果新内核出现问题，我还有选择退回旧内核的选项。务必保存 `/boot` 目录中的 System.map 和 vmlinuz 文件。它们的名称应与其在 lilo.conf 中相应的条目相对应。

![](img/a0884097af3186d9b4f616aaa3f065b0_503_0.png)

如果要启动其他操作系统，清单 14.2 展示了如何设置 Windows 作为默认操作系统。尽管 Linux 分区没有列在前面，但 Linux 提供默认选项，用于指定 Windows 为系统可以启动的默认操作系统。

### 清单 14.2 Red Hat 安装过程中生成的默认 lilo.conf 文件

```ini
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
linear
default=windows

image=/boot/vmlinuz-2.2.14-5.0
label=linux
read-only
root=/dev/hda2

other=/dev/hda1
label=windows
```

用户可以配置 lilo.conf 文件中指定的选项。您可以指定任何您想要的系统。要更改默认操作系统，只需在 `default=` 选项下用 `linux` 替换 `windows` 即可。如您所见，此驱动器被划分为两个分区：`/dev/hda1` 和 `/dev/hda2`。Linux 安装在 `/dev/hda2` 上，因此使用 `root=` 变量。

对于一些人来说，直接将内核保存回硬盘是不切实际的，或者至少是令人不快的。他们希望在更改机器的任何配置或设置之前，绝对确保新编译的内核可以正常工作。确保内核正常工作通常首先涉及将新内核直接复制到可引导软盘上。将内核存储在软盘后，将软盘插入软盘驱动器并重启机器。如果机器成功启动，您可以安全地将内核加载到驱动器上。完成后，您可以编辑 lilo.conf 文件以指向新内核，并使其成为默认内核。确保重命名或备份原始内核，以便在新内核无法启动时有所回退。

## 将新内核放置在启动介质上

既然您的内核和模块都已成功编译，并且您已经编辑了启动配置，现在可以将新内核和 System.map 放置在启动介质上。这意味着将它们定位在硬盘上的某处，或者将它们放置在软盘上。如果您选择将新内核保留在硬盘上，则需要定位现在称为 `vmlinuz` 的新内核，并将其放置在 `/boot` 目录和 `/`（根）目录中。由于 Red Hat 的默认内核安装在 `/boot` 目录中，在那里保留较新的内核也会很方便。

如果希望手动将新内核复制到 `/boot` 目录，请使用以下两条命令将新创建的文件复制到其默认位置。

```bash
cp /usr/src/linux/arch/i386/boot/bzImage /boot/vmlinuz
cp /usr/src/linux/System.map /boot/System.map
```

另一个我喜欢的移动选项是 System.map 文件。它通常直接在 linux/ 目录中创建，也可以放置在 /boot 目录中。

在最新的 Red Hat 版本中，有几个符号链接指向 vmlinuz 和/或 System.map 文件。您可以删除这些符号链接。它们指向的文件通常可以通过其发行版本号来识别。

安装新编译的 Linux 内核的更简单方法是在运行 `make modules` 和 `make modules_install` 命令后发出以下命令。

```bash
make install
```

此命令将正确的内核复制到正确的位置。前面手动复制内核的示例是 x86 特定的。在 Red Hat 下使用 `make install` 命令将定位适合您发行版的正确内核，然后将其复制到正确的引导目录。它还会移动旧内核并保留符号链接，使其指向新内核。最后，它还会运行 `/sbin/lilo` 命令并重新读取您的 lilo.conf 文件。这就是为什么在安装内核之前编辑 LILO 配置的原因。

如果希望将新创建的内核和 System.map 文件放置在软盘上，请使用以下命令进行复制：

```bash
cp /usr/src/linux/arch/i386/boot/bzImage /dev/fd0
```

一旦新内核就位，就需要让 lilo 知道所有内容的位置。运行以下命令使 lilo 可执行文件重新读取配置文件，并让 lilo 能够识别新创建的内核。该命令还告知系统在哪里查找旧内核。

如果要从软盘驱动器启动内核，请更改 `/etc/lilo.conf` 文件以指向正确的位置。不要使用 lilo.conf 文件中的 `root=/dev/hda1`，而是将其替换为 `root=/dev/fd0`。

同样，如果希望跳过 `make install` 命令并手动运行 lilo，请使用以下命令。

```bash
/sbin/lilo
```

您可能还希望运行一个类似的较旧命令，该命令工作良好，可以自动完成更多任务。

```bash
make zlilo
```

此命令安装内核并使软盘可引导，但不处理模块。

