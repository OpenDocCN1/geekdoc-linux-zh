
| `/etc/cron.daily` | 每天执行任务的文件夹 |
| `/etc/cron.weekly` | 每周执行任务的文件夹 |
| `/etc/cron.monthly` | 每月执行任务的文件夹 |
| `/etc/cron.yearly` | 每年执行任务的文件夹 |
| `/etc/cron.hourly` | 每小时执行任务的文件夹 |
| `/etc/cron.allow` | 允许提交 cron 任务的用户 |
| `/etc/cron.deny` | 禁止访问 cron 的用户 |

**表 8-6: Cron 文件脚本**

# 第3 部分：管理

```bash
SHELL=/bin/bash
PATH=/bin:/bin:/usr/sbin:/usr/bin
MAILTO=
HOME=/
### cron-parts
01 * * * root run-parts /etc/cron.hourly
02 4 * * root run-parts /etc/cron.daily
22 4 * * 0 run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

提示：`cron` 文件夹内的脚本按字母顺序执行。如果你需要某个特定的脚本在其他脚本之前运行，你可能需要更改它的名称。一种方法是在名称前加上数字。例如，在 `/cron.weekly` 文件夹中，`anacron` 脚本被命名为 `0anachron`，这样它就会在任何其他脚本之前运行。

请记住，这些仅仅是包含可执行文件的文件夹。实际的调度是由 `/etc/crontab` 文件中的条目的。例如，如果将 `cron.weekly` crontab 条目中的字段从 `0` 改为 `*`，将分钟字段改为 `1`（变为 `22 4 1 * *` 而不是 `22 4 * * 0`），则任务将每天运行，而不是每周运行。

### Cron 文件夹名称

这些文件夹使用的名称仅仅是约定。它们对 `cron` 守护进程没有特殊意义。事实上，你可以创建自己的文件夹，将脚本放入其中，并调度 `run-parts` 在指定时间运行这些脚本。在下一个示例中，放置在 `/etc/cron.mydocs` 中的脚本将在每周三的下午 12 点运行。

- `12 * * 3 root run-parts /etc/cron.mydocs`

### Anacron

对于一个在 `cron` 可能运行的时间通常处于关机状态的系统，你可能需要用 `anacron` 来补充 `cron`。当需要执行调度任务时，`anacron` 会激活。例如，如果系统在调度了 `cron` 任务的周末处于关机状态，这些任务将不会执行；然而，`anacron` 会检查系统启动时需要执行哪些任务，然后运行它们。它是为每天或或每周运行的任务设计的。

对于 `Anacron` 任务，你将 `crontab` 条目放在 `/etc/anacrontab` 文件中。对于每个调度任务，你需要指定它执行时的间隔天数（7 为每周，30 为每月）、当天运行的时间（以分钟为单位）、任务描述以及要执行的命令。对于备份，使用的命令将是 `tar` 操作。你可以使用 `system-config-services` 来运行 `anacron` 服务，或让它在启动机时自动启动。

### KDE 任务调度器 (Kcron)

在 KDE 上，你可以使用 KDE 任务调度器 (`Kcron`) 来设置用户级和系统级的调度任务（安装 `kdedaemon` 包）。你可以访问 KDE 系统设置中的任务调度器窗口，路径为：高级设置 | 任务调度器（“系统”部分）。任务调度器将列出你所有的调度任务（见图 8-4）。点击“新建”按钮打开“新建任务”窗口，你可以在此处输入要运行的命令，添加注释，然后通过简单的排列按钮指定月、天、小时和分钟的时间。在任务调度器窗口中，你可以选择一个任务并使用按钮对其进行修改、删除任务、运行或打印其副本。对于使用相同命令或参数的任务，你可以创建一个变量，然后在命令中使用该变量。变量列在“环境变量”部分。要在调度任务中使用变量，在输入命令时在变量名称前加上 `$` 字符。在“命令”框中输入 `$` 符号将显示一个你可以使用的 `PATH` 和 `SEARCH` 等预定义系统变量的下拉列表。

![](img/99301381a0d2790a6cdc2798147cbdad_250_0.png)

图 8-4：KDE 任务调度器

### 通用引导加载程序 (GRUB)

通用引导加载程序 (`GRUB`) 是红帽企业 Linux 的多引导加载程序。通过 `GRUB`，你可以在系统启动时显示的菜单界面上选择运行的操作系统。使用方向键移动到条目并按回车键启动。按 `e` 进入编辑模式，允许你更改内核参数。`c` 命令将你置于命令行界面。你的 BIOS 支持非常大的硬盘，`GRUB` 可以从其中任何一个硬盘启动。Linux 和 Unix 操作系统被称为多引导操作系统，并在启动时接收传递的参数。检查 `GRUB` 管理器以获取 `GRUB` 选项。

`GRUB` 配置存储在 `/boot/grub/grub.conf` 文件中（你也可以通过 `/etc/grub.conf` 访问）。你只需要创建条目，`GRUB` 就会在你重启时自动读取它们。你可以设置几个选项，例如超时时间和使用的背景图像。检查 `GRUB` info 文档以获取详细描述，`info grub`。

你可以通过为系统创建一个带有 `title` 术的条目来指定系统。然后你必须指定操作系统内核或程序的位置，即在该块硬盘上的哪个硬盘和分区。这些信息列在 `root` 选项后的括号中。从 0 开始而不是 1，且硬盘用 `hd` 前缀表示，无论它们是 IDE、SATA 还是 SCSI 硬盘。或者是该硬盘上的第三个分区（`sda3`）。对于 Linux 系统，你还必须使用 `kernel` 选项来指示要运行的内核程序，使用完整路径以及内核可能需要的选项。RAM 磁盘由 `initrd` 选项指示。

```
title Red Hat Enterprise Linux Server
root (hd0,0)
kernel vmlinuz root=/dev/sda config
initrd initrd.img
```

*(注：由于原文最后一段代码块似乎存在大量乱码或重复错误，此处根据前文逻辑进行了推断并补全了标准的 GRUB 配置格式)*

# 252 第 3 部分：管理

### 示例 grub.conf

示例 `grub.conf` 文件包含了适用于 Linux 和 Windows 的条目。请注意，内核参数列在内核选项的内核选项中。根目录安装在逻辑卷 `/dev/mapper/vg_richard4-lv_root` 上。

### 由 anaconda 生成的 grub.conf

### 注意，对此文件进行更改后，并不需要重新运行 grub

# 注意：你有一个 /boot 分区。这意味着

# 所有内核和 initrd 路径都是相对于 /boot/ 的相对路径，例如：

### root (hd0,1)

### kernel /vmlinuz-linux root=/dev/mapper/vg_richard4-lv_root

### initrd /initrd-[generic-version].version.img

```
#boot=/dev/sda
default=0
timeout=5
splashimage=(hd0,0)/grub/splash.xpm
hiddenmenu
```

Red Hat Enterprise Linux Server (2.6.32-71.14.1.el16.i686)

root (hd0,0)

kernel /vmlinuz-2.6.32-71.14.1.el16.i686 root=/dev/mapper/vg_richard4 

lv_root rd_VM=vg_richard4/lv_root rd_VM=vg_richard4/lv_swap rd_NO_LUKS

rd_NO_MD rd_NO_DM LANG=en_US.UTF-8 SYSOFONT=latarcyerb-sun16 KEYBOARDTYPE=pc

KEYTABLE=us crash-kernel=auto quit

initrd/initramfs-2.6.32-71.14.1.el16.i686.img

title windows 7

rootnotify (hd0,0)

chainloader +1

### Puppet

`Puppet` 允许你自动配置远程系统，即使它们可能运行带有不同配置文件的 Linux 发行版。你不需要手动配置网络上的每个系统，而是可以使用 `Puppet` 自动配置它们。`Puppet` 将管理任务抽象为资源抽象层 (`RAL`) 中的资源。然后，你可以使用 `Puppet` 配置语言为特定资源指定基本值或操作。管理类型包括服务、用户、组等。例如，你可以使用 `puppet` 对使用 `APT` 或 `PackageKit` 等不同包管理器的系统上的服务（服务器）执行更新。
