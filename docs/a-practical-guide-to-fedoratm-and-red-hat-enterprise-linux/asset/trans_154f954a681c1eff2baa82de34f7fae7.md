

以这种方式安装内核会更新 grub.cfg（第 593 页）GRUB 配置文件，以包含新内核。

通过点击屏幕右上角的用户名，然后选择“关机”再选择“重新启动”来重启系统。如果你在控制台操作，请按 CONTROL-ALT-DEL。你也可以从控制台、基于字符的终端或终端模拟器中执行 `reboot` 命令。当系统重新启动后，你可以使用 `uname` 命令来验证新内核是否已加载：

```bash
$ uname -r
3.9.0-300.sam1307021000.fc19.x86_64
```

# LPI GRUB：LINUX 引导加载程序

- **MBR** 引导加载程序是一个非常小的程序，引导自举（第 1240 页）过程使用它将计算机从关闭或重置状态转变为完全可用的状态。引导加载程序通常位于硬盘的起始扇区，称为 MBR（主引导记录）。

- **GPT** 在新系统上，你可以使用 GPT（GUID 分区表）替代 MBR；将已安装的系统从 MBR 更改为 GPT 是一个破坏性过程。GPT 相比 MBR 有许多优势，包括支持大于 2TB 的磁盘。Linux 和较新版本的 Windows 支持 GPT，并且它是 RHEV-H（Red Hat 企业虚拟化 hypervisor）机器的默认选择。在 GPT 下管理分区必须使用 `parted`（第 614 页）而不是 `fdisk`。更多信息请访问 wiki.archlinux.org/index.php/GUID_Partition_Table。

- **BIOS** BIOS（第 1239 页）存储在系统主板的 EEPROM（第 1248 页）中，当打开或重置计算机时，BIOS 获得系统的控制权。在测试硬件后，BIOS 将控制权转移给 MBR，MBR 通常将控制权传递给分区引导记录。这种控制权的转移启动了引导加载程序，它负责定位操作系统内核（存放在 `/` 或 `/boot` 目录中）、将该内核加载到内存并启动其运行。如果你使用 `/boot` 目录，该目录可能挂载在单独分区上，那么为了系统能够启动 Linux，该目录或分区必须存在。有关从这一点开始发生的情况的更多信息，请参阅第 450 页的“启动系统”。

- **LBA** 所有新硬盘都支持 LBA（逻辑块寻址）模式。LBA 允许 `/boot` 目录出现在硬盘的任何位置。要使 LBA 工作，它必须得到硬盘、BIOS 和操作系统（在 Linux 的情况下是 GRUB）的支持。虽然 GRUB 支持 LBA 模式，但某些 BIOS 不支持。因此，将 `/boot` 目录放置在硬盘开头附近的独立分区中是一个好主意。在这种设置下，根（`/`）文件系统可以位于 Linux 可以访问的任何硬盘上的任何位置，无论是否支持 LBA。在某些情况下，如果没有单独的 `/boot` 分区，系统可能最初可以启动，但随着内核更新，内核文件离硬盘开头越来越远，系统可能会失败。

- **LVM** 使用 LVM 的系统需要一个单独的启动分区，该分区不能是 LV。有关 LVM 的更多信息，请参见第 44 页。

### GRUB 2

Fedora 16 和 RHEL 7 引入了 GRUB 2（Grand Unified Boot loader 2），本书简单地将其称为 GRUB。本书将第一个版本称为 GRUB legacy。GRUB 2 是 GRUB legacy 的完全重写，配置文件很少有相同的。

作为 GNU 计划的产品，GRUB 加载程序符合 *multiboot 规范*（第 1261 页），这允许它直接加载许多免费操作系统，以及 *链式加载*（第 1241 页）专有操作系统。GRUB 加载程序可以识别各种类型的文件系统和内核可执行格式，从而可以加载任意操作系统。当你启动系统时，GRUB 可以显示由 *boot/grub2/grub.cfg* 文件（第 593 页）生成的选项菜单。在此时，你可以修改菜单选择、选择要启动的操作系统或内核，或者什么都不做并让 GRUB 启动默认系统。

当你在安装 Linux 时安装 GRUB，安装程序会自动配置 GRUB。有关 GRUB 的更多信息，请参见 *grub2 info* 页面和 www.gnu.org/software/grub。

## LPI 配置 GRUB

如前所述，GRUB 2 使用与 GRUB legacy 不同的文件集。你通过编辑 *etc/default/grub* 文件（下文）并运行 *grub2-mkconfig* 来控制 GRUB 大多数经常变更的方面，*grub2-mkconfig* 会生成 *boot/grub2/grub.cfg* 文件（第 593 页）。你可以编辑 *etc/grub.d* 目录（第 592 页）中的文件来执行 GRUB 菜单的高级配置。*grub.cfg* 文件类似于 GRUB legacy 的 */boot/grub/menu.lst* 文件，但编辑 *grub.cfg* 文件是一个糟糕的主意，因为它是 *grub2-mkconfig* 生成的，并且通常会被该实用程序覆盖。

### /etc/default/grub：主要的 GRUB 配置文件

更改 */etc/default/grub* 文件中变量的值允许你修改系统启动方式和 GRUB 显示菜单的许多方面（图 10-2，第 451 页）。在大多数情况下，你可以通过在系统启动时按住 **SHIFT** 键来强制 GRUB 显示其菜单（第 450 页）。

你在 */etc/default/grub* 文件中设置的一些变量的效果取决于 GRUB 是否在机器上找到一个或多个可启动的操作系统。有些变量不需要设置。为此，GRUB 不评估以井号（#；这些行是注释）开头的行。移除或添加井号分别使 GRUB 评估或不评估一个赋值。

*/etc/default/grub* 文件如下所示。

```bash
$ cat /etc/default/grub
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="`$(sed 's, release .*$,,' /etc/system-release)`"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="rd.lvm.lv=fedora/swap rd.md=0 rd.dm=0
vconsole.keymap=$({-x /usr/sbin/rhckrashed-kernel-param ]] &&
/usr/sbin/rhcrashed-kernel-param [ ] ; rd.luks=0
vconsole.font=latarcyrheh-sun16 rd.lvm.lv=fedora/root rhgb quiet"
GRUB_DISABLE_RECOVERY="true"
```

你可以为以下变量赋值：

- **GRUB_TIMEOUT=num**
  **num** 指定 GRUB 在启动系统前等待的秒数。将 **num** 设置为 -1 会使 GRUB 等待直到用户选择菜单项。将 **num** 设置为 0 会使 SHIFT 键失去效果：用户将无法在系统启动前显示 GRUB 菜单。

- **GRUB_DISTRIBUTOR=string**
  *string* 指定 GRUB 显示的发行版名称。Fedora 提供的 *string* 是可执行的，并且因为它被包含在 $(...)（命令替换；第 410 页）中，所以会被替换为其输出：
  
  `$(sed 's, release .*$,,' /etc/system-release)`
  
  `sed` 命令截断 `system-release` 文件中 Fedora 之后的所有内容。

- **GRUB_DEFAULT=num | saved**
  **num** 指定默认菜单项的顺序号。默认菜单项是如果你未在 GRUB 启动系统时选择其他项，GRUB 将启动的那一项。菜单项从 0 开始编号，因此将此变量设置为 0 指定第一个菜单项。将 GRUB_DEFAULT 设置为 saved 会使 GRUB 启动最近启动的菜单项。

- **GRUB_DISABLE_SUBMENU=true | false**
  当设置为 *true* 时，使 `grub2-mkconfig` 不为 GRUB 菜单生成子菜单项。设置为 *false* 会生成子菜单项。

- **GRUB_TERMINAL_OUTPUT="console"**
  指定终端输出设备，如 `console` 或 `serial`。

- **GRUB_CMDLINE_LINUX=string**
  GRUB 将 *string* 追加到 GRUB 在启动 *normal* 和 *single-user* /救援模式（第 450 页）时传递给内核的 **linux** 启动行。在 Fedora 中提供的 *string* 较长，提供 Fedora 启动所需的信息。更多信息请参阅第 59 页的“查看正在发生什么”。你还可以向 *string* 添加启动命令行参数；有关编辑 GRUB 菜单的说明，请参见第 451 页。用空格分隔每个单词，如果 *string* 包含空格，则用双引号将 *string* 括起来。

- **GRUB_DISABLE_RECOVERY=true | false**
  当设置为 *true* 时，使 `grub2-mkconfig` 不为 GRUB 菜单生成恢复项。设置为 *false* 会生成恢复项。

### /etc/grub.d/：GRUB 配置模板

/etc/grub.d 目录中的文件决定了 GRUB 菜单的许多方面。`grub2-mkconfig` 实用程序（下文）按数字顺序处理这些文件。有关更多信息，请参见该目录中的 **README** 文件。

你可以向此目录添加文件并修改现有文件，但通常没有必要这样做。为了使 `grub2-mkconfig` 处理这些文件，每个文件必须是可执行的。

