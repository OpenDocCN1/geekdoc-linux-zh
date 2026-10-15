
### 12.4.2 配置 pxelinux 软件

一旦确定 `TFTP` 允许正确访问文件，就可以引入 `DHCP` 并启动客户端引导。

`pxelinux` 软件包要求将 `pxelinux.0` 文件放置在 `tftp` 能够找到的地方并在 `dhcp.conf` 文件中指定其路径。除了启动文件外，还有一个配置目录 `pxelinux.cfg`，`pxelinux` 在启动后访问。该目录包含了通过将系统标识符链接到特定系统或组的唯一配置文件来决定 `pxelinux` 对特定系统行为的信息。

为了区分不同客户端的引导，`pxelinux` 软件包会在配置目录中搜索与请求系统 `IP` 地址的十六进制部分匹配的链接（或文件）。链接名称必须兼容 8.3 格式（也就是说，文件名不超过 8 个字符，扩展名不超过 3 个字符），这就是为什么配置目录命名为 `pxelinux.cfg` 的原因。例如，我选择使用软链接，因为可以多个链接指向同一个配置文件，从而减少不同独立文件之间版本不匹配的概率。

### 通用网络启动设施：pselinux

`pselinux` 引导加载程序首先查找以十六进制形式表示的整个网络地址。如果没有找到该链接，它将从十六进制地址的右侧删除一个字符并重新查找。此过程将持续进行直到找到匹配项或搜索失败。例如，以主机地址 `192.168.0.111` 为例。如果我们保留基于字节的格式，它将转换为十六进制的 `C0.A8.00.6F`。对于此文件，在删除点号后，它的名称将变为 `C0.A8000.6F`。

从搜索顺序中可以看出，`pselinux` 软件首先查找 `COA8006F`，接着是 `COA8006`、`COA8000`、`COA80`、`COA8`，以此类推，直到字符用尽。你可以通过查看 `/var/log/messages` 文件中来自 `TFTP` 的详细输出来观察到这一点。这允许你指定一个链接，该链接仅匹配地址的网络部分。为了提高搜索效率，我选择为每个系统创建一个链接，并使用名为 `make_links` 的脚本从地址列表中创建它们：

```bash
#!/bin/bash -x

SCRIPT="default.net.boot"

if [ -n "$1" ]; then
  SCRIPT="$1"
fi

for HEXIP in $(sed 's/@#\$@//' < IPS.hex); do
  ln -s "$SCRIPT" "$HEXIP"
done
```

传递给脚本的客户端十六进制地址部分列表位于名为 `IPS.hex` 的文件中：

| 地址 | 注释 |
| :--- | :--- |
| `COA8006E` | `# 103` |
| `COA8006D` | `# 109` |
| `COA8006F` | `# 111` |

诚然，这是一种简单的方法，错误检查极少。勤奋的人可以写一个 `Perl` 脚本来完成整个操作，并进行适当的错误检查，而不会有太大麻烦。

### 12.4.3 pselinux 配置文件

现在我们让 `DHCP` 指向 `TFTP`，`TFTP` 指向 `pselinux.0` 文件，该文件将尝试访问 `/tftpboot/pselinux.cfg` 以寻找我们一直讨论的链接。下一步是创建驱动引导行为的配置文件。如果引导加载程序无法找到十六进制 `IP` 地址的匹配项，它将退回到配置目录中名为 `default` 的默认文件。我的默认文件内容仅指定了从本地磁盘引导：

```text
default linux
  label linux
  localboot 0
```

配置目录中的链接都指向一个名为 `default.netboot` 的文件（链接名只需兼容 8.3 格式）。该文件包含以下内容：

```text
# 记住一切都相对于 /tftpboot！
/

default local      # 不间断的网络启动使用此标签
serial 0,38400n8   # 波特率为 38400 的串行端口
# 8 位无奇偶校验 1 位停止位
prompt 0           # 如果按住 Ctrl 和 Alt 或
# 启用 <Caps Lock> 或 <Scroll Lock> 则将停止
F1 help.txt        # 在启动提示处按下功能键将显示帮助
F2 help.txt
F3 help.txt
F4 help.txt
F5 help.txt
F6 help.txt
F7 help.txt
F8 help.txt
F9 help.txt
F0 help.txt
```

```text
label linux9.ks
kernel rh9.0/vmlin
append vga=extended load_ramdisk=1 \
initrd=rh9.0/initrd.img \
ks=nfs:192.168.0.110:/kickstart9.0/
```

```text
label linux9.in
kernel rh9.0/vmlin
append vga=extended load_ramdisk=1 \
initrd=rh9.0/initrd.img
```

```text
label linux.fedora
kernel fedora/vmlin
append vga=extended load_ramdisk=1 \
initrd=fedora/initrd.img
```

```text
label linux.si
kernel si/kernel
append vga=extended load_ramdisk=1 prompt_ramdisk=0 \
initrd=si/initrd.img root=/dev/ram rw \
ramdisk_blocksize=4096
```

```text
label pxes/vmlin
kernel pxes/vmlin
append ramdisk_size=32768 video=yes vga=0 \
initrd=pxes/initrd.img root=/dev/ramA=1 \
ip=192.168.0.110
```

```text
label local
localboot 0
```

当系统发出 `DHCP` 或 `BOOTP` 请求时，它会获取 `pselinux.0` 文件，除非在 `pselinux` 获取控制时按住了 `Ctrl` 或 `Alt` 键，否则它将继续从本地磁盘引导。如果引导中断，将输出一个提示，等待配置文件中标签的匹配链接。对于特定的十六进制地址，默认行为是从本地磁盘引导。按下 `F1`-`F8` 将输出一个列出选项的彩色菜单。带有 `^` 前缀的颜色属性信息（例如 `^L`）位于单独的文本文件 `/tftpboot/help.txt` 中：

```text
^L
```

| 选项 | 说明 |
| :--- | :--- |
| `COA8006E` | 选项 |
| `COA8006D` | 选项 |
| `COA8006F` | 选项 |
| `COA8006` | 选项 |
| `COA800` | 选项 |
| `COA80` | 选项 |
| `COA8` | 选项 |

### 12.5 配置网络

注意，文件中的分区语句已经从自动生成的文件中取消注释。通常会将它们设置为保留目标磁盘上现有的分区。这可以通过软盘、`CD-ROM` 或网络访问馈送到安装过程中。

#### 12.5.1 Kickstart 文件格式

如果你查看 `kickstart` 文件，你会发现几个语句将文件分为多个部分：一个"command"部分，接着是 `%packages`、`%pre` 和 `%post`。部分的顺序很重要，尽管某些信息可以按任意顺序指定。`%pre` 和 `%post` 部分可以按任意顺序定义，只要它们位于文件末尾，在 `%packages` 之后即可。

命令部分有大量可能的选项，在示例文件中你指定了 `install`，这将重新从指定源加载系统：`cdrom`。（可能的源介质包括 `CD-ROM`、本地磁盘、`NFS`、`FTP` 和 `HTTP`。你可能需要为您的网络接口硬件安装过程提供网络磁盘。）图形界面或文本界面中提供的所有选项，甚至更多选项，都可以在命令和选项中指定。我们在这里将不再介绍细节，`redhat-config-kickstart` 命令的文档位于 `/usr/share/doc/redhat-config-kickstart-version/` 下的 HTML 格式。Red Linux 文档在介绍这些功能方面也做得很好。

命令部分之后是 `%package` 部分，它指定了要从源介质加载哪些软件包。以 `@` 开头的行表示软件包组，不带 `@` 符号的行指定单个软件包。我们的示例文件指定了 `@everything`，这会加载所有可用软件包。在进行 `kickstart` 的最终配置时，你不希望这样做。安装时间与你加载的软件包数量成正比。如果你想让 `kickstart` 安装保持简短，只需指定你需要的软件包。这可能需要一些尝试，并要密切关注正在加载的软件包[以及自动选择的依赖项]。

如果你想查看 `Red Hat` 介质上软件包的定义，它们包含在 `CD-ROM` 介质上名为 `system.xml` 的扩展标记语言 (`XML`) 文件中。该文件位于安装介质根目录下的 `RedHat/base` 目录。如果你想检查它，该格式“大部分”可以使用文本编辑器读取。它驱动了安装工具中可用语言、软件包和其他选项的列表。

`%pre` 部分允许你指定在安装内核解释 `kickstart` 文件后立即运行的命令。理解此脚本执行的环境至关重要，特别是对可用命令和资源的限制。正在安装的目标系统硬件已由 `Linux` 内核进行扫描，网络在没有名称服务的情况下是可用的，且安装内核在 `RAM` 磁盘中运行，本地磁盘挂载在特殊目录下（而不是根目录）。

`/proc` 文件系统将包含有关目标硬件的有用信息，你的安装脚本可以使用这些信息做出决策和调整。在交互式安装期间，你可以通过按 `Ctrl-Alt-F2` 来检查此环境的精确配置，这将切换到使用 `VGA` 文本模式运行的 `X-Windows` 虚拟显示。整个环境都在那里供你检查。输入 `Ctrl-Alt-F7` 回到 `anaconda` 安装脚本。

幸运的是，`%post` 脚本的环境要文明得多。该脚本在安装过程完成且系统重启之前执行。脚本中的操作均相对于新系统的根文件系统，除非你正在工作。如果你使用 `DHCP`，名称解析将无法工作，但可以在 `%pre` 脚本环境中直接使用 `IP` 地址。

如果你为安装文件指定了 `NFS` 源，该服务器目录将挂载在 `/mnt/source` 下。你的 `%post` 脚本可以挂载其他文件系统，并访问 `RPM` 文件、压缩 `tar` 包、原型配置文件或你可能需要的任何信息。完全可以利用 `kickstart` 安装一个最小环境，然后在 `%post` 脚本中执行大部分的系统软件配置和加载。我见过一些完全以这种方式实现的强大安装过程。

#### 12.5.2 为 kickstart 提供安装介质

使安装介质适用于网络安装的最简单方法之一是将文件放置在服务器（`NFS`、`FTP` 或 `HTTP`）上，并允许安装内核访问远程位置的数据。对于 `NFS`，文件路径必须通过 `/etc/exports` 文件导出，并且 `NFS` 客户端必须访问 `NFS` 服务而不受 `TCP` 封装的干扰。

安装介质可以卸载到目录结构中，也可以作为国际标准组织 ISO `CD-ROM` 镜像提供给安装过程。（注意 `ISO` 并不是缩写，它是希腊语，意为“相等”。）要将二进制 `RPM` 软件包卸载到目标本地目录 `/export/RedHat/9.0`，请对安装集中的所有 `CD-ROM`（通常是三个四个）执行以下命令：

```bash
# mount /mnt/cdrom
# cp -var /mnt/cdrom/RedHat /export/RedHat/9.0
# umount /mnt/cdrom
# eject
```
