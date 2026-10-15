
# Now we have all of our basic modules loaded and the kernel going,
# let's dump the syslog ring somewhere so we can find it later
`dmesg` > `/var/log/dmesg`

# rc.serial 以及 rc.local

The `/etc/rc.d/rc.serial` file was used in older versions of Linux. It is rarely used on any current systems, and when it is, it is only for backward compatibility. Most of the functionality of the old `rc.serial` file can now be found in the `rc.local` file.

The `/etc/rc.d/rc.local` file is used to configure local machines. All the commands that run with this file are executed after the machine boots, but before anyone logs into the system. The `rc.local` is also executed after a system level is changed. One of `rc.local`'s jobs is to configure the login banner by default displays your kernel version and machine type. To change this, you can simply edit this file. A sample `/etc/rc.d/rc.local` file follows:

```bash
#!/bin/sh
```

# This script will be executed *after* all the other init scripts.
# You can put your own initialization stuff in here if you don't
# want to do the full Sys V style stuff.

```bash
if [ -f /etc/redhat-release ]; then

  R=$(cat /etc/redhat-release)

  arch=$(uname -m)

  a="a"

  case "$arch" in

    _a*) a="an";

    _i*) a="an";

  esac

fi

# This will overwrite /etc/issue every boot. So, make any changes

# you want to make to /etc/issue here or lose them when you reboot.

echo "" > /etc/issue

echo "$R" >> /etc/issue

echo "$(uname -m)" >> /etc/issue

cp -f /etc/issue /etc/issue.net

# The actual prompt is displayed by /etc/issue and /etc/issue.net.

# The file, however, is overwritten by /etc/rc.d/rc.local. Therefore, any manual

# changes to /etc/issue and /etc/issue.net must be reproduced in rc.local.

# The system run-level directories are /etc/rc.d/rc0d through /etc/rc.d/rc6d.

# These directories don't contain real files. Instead,

# they are symlinks to scripts located in /etc/rc.d/init.d. The links in /etc/rc.d/rcXd run when the system accesses

# initialization script. Each directory contains symlinks to real files. Here is

# example of the files in /etc/rc.d/rc0:

| Directory | Symlinks (S) | Symlinks (K) |
| :--- | :--- | :--- |
| rc0.d | S00, S01, S02, S03, S04, S05, S06, S07, S08, S09, S10, S11, S12, S13, S14, S15, S16, S17, S18, S19, S20, S21, S22, S23, S24, S25, S26, S27, S28, S29, S30, S31, S32, S33, S34, S35, S36, S37, S38, S39, S40, S41, S42, S43, S44, S45, S46, S47, S48, S49, S50, S51, S52, S53, S54, S55 | S56, S57, S58, S59 | K60, K61, K62, K63, K64, K65, K66, K67, K68, K69, K70, K71, K72, K73, K74, K75, K76, K77, K78, K79, K80, K81, K82, K83, K84, K85, K86, K87, K88, K89, K90, K91, K92, K93, K94, K95, K96, K97, K98, K99 |
| rc1.d | S00, S01, S02, S03, S04, S05, S06, S07, S08, S09, S10, S11, S12, S13, S14, S15, S16, S17, S18, S19, S20, S21, S22, S23, S24, S25, S26, S27, S28, S29, S30, S31, S32, S33, S34, S35, S36, S37, S38, S39, S40, S41, S42, S43, S44, S45, S46, S47, S48, S49, S50, S51, S52, S53, S54, S55 | S56, S57, S58, S59 | K60, K61, K62, K63, K64, K65, K66, K67, K68, K69, K70, K71, K72, K73, K74, K75, K76, K77, K78, K79, K80, K81, K82, K83, K84, K85, K86, K87, K88, K89, K90, K91, K92, K93, K94, K95, K96, K97, K98, K99 |
| rc2.d | S00, S01, S02, S03, S04, S05, S06, S07, S08, S09, S10, S11, S12, S13, S14, S15, S16, S17, S18, S19, S20, S21, S22, S23, S24, S25, S26, S27, S28, S29, S30, S31, S32, S33, S34, S35, S36, S37, S38, S39, S40, S41, S42, S43, S44, S45, S46, S47, S48, S49, S50, S51, S52, S53, S54, S55 | S56, S57, S58, S59 | K60, K61, K62, K63, K64, K65, K66, K67, K68, K69, K70, K71, K72, K73, K74, K75, K76, K77, K78, K79, K80, K81, K82, K83, K84, K85, K86, K87, K88, K89, K90, K91, K92, K93, K94, K95, K96, K97, K98, K99 |
| rc3.d | S00, S01, S02, S03, S04, S05, S06, S07, S08, S09, S10, S11, S12, S13, S14, S15, S16, S17, S18, S19, S20, S21, S22, S23, S24, S25, S26, S27, S28, S29, S30, S31, S32, S33, S34, S35, S36, S37, S38, S39, S40, S41, S42, S43, S44, S45, S46, S47, S48, S49, S50, S51, S52, S53, S54, S55 | S56, S57, S58, S59 | K60, K61, K62, K63, K64, K65, K66, K67, K68, K69, K70, K71, K72, K73, K74, K75, K76, K77, K78, K79, K80, K81, K82, K83, K84, K85, K86, K87, K88, K89, K90, K91, K92, K93, K94, K95, K96, K97, K98, K99 |
| rc5.d | S00, S01, S02, S03, S04, S05, S06, S07, S08, S09, S10, S11, S12, S13, S14, S15, S16, S17, S18, S19, S20, S21, S22, S23, S24, S25, S26, S27, S28, S29, S30, S31, S32, S33, S34, S35, S36, S37, S38, S39, S40, S41, S42, S43, S44, S45, S46, S47, S48, S49, S50, S51, S52, S53, S54, S55 | S56, S57, S58, S59 | K60, K61, K62, K63, K64, K65, K66, K67, K68, K69, K70, K71, K72, K73, K74, K75, K76, K77, K78, K79, K80, K81, K82, K83, K84, K85, K86, K87, K88, K89, K90, K91, K92, K93, K94, K95, K96, K97, K98, K99 |
| rc6.d | S00, S01, S02, S03, S04, S05, S06, S07, S08, S09, S10, S11, S12, S13, S14, S15, S16, S17, S18, S19, S20, S21, S22, S23, S24, S25, S26, S27, S28, S29, S30, S31, S32, S33, S34, S35, S36, S37, S38, S39, S40, S41, S42, S43, S44, S45, S46, S47, S48, S49, S50, S51, S52, S53, S54, S55 | S56, S57, S58, S59 | K60, K61, K62, K63, K64, K65, K66, K67, K68, K69, K70, K71, K72, K73, K74, K75, K76, K77, K78, K79, K80, K81, K82, K83, K84, K85, K86, K87, K88, K89, K90, K91, K92, K93, K94, K95, K96, K97, K98, K99 |

# Understanding The Linux Kernel

The Linux kernel is the very foundation on which Linux is based. The Linux kernel, in fact, is what Linux gets its name. As discussed in Chapter 3, the Linux kernel was developed as a hobby by Linus Torvalds in Helsinki.

`/lib/modules/` 目录根据内核版本进行区分。例如，在我的系统中，我安装了内核 2.2.5 和 2.2.10。因此，在 `/lib/modules/` 下为每个内核都有一个对应的目录。

当对某个模块发出服务请求时，如果该模块未加载或未直接编译进内核，内核（使用 `kmod`）将尝试加载所需的模块。为了找到所需的模块，`kmod` 会先查找 `/lib/modules/`，然后进入相应的内核目录，如果需要，还会进入相应的设备目录。

Red Hat Linux 软件包包含许多使模块控制变得更简洁的工具。它们包括 `lsmod`、`insmod`、`rmod` 和 `modprobe`。`lsmod` 工具可以告诉你哪些模块正在运行。以下是 `lsmod` 的示例输出。

| Module (模块) | Size (大小) | Used by (使用) |
| :--- | :--- | :--- |
| nls_iso8859-1 | 2020 | 1 (autoclean) |
| isfs | 17400 | 1 (autoclean) |
| id-cd | 22516 | 2 (autoclean) [ide-cd] |
| cdrom | 13272 | 0 (autoclean) |
| floppy | 45964 | 1 (autoclean) |
| vmnet | 9200 | 4 |
| vmon | 10496 | 1 |
| nfsd | 150008 | 8 (autoclean) |
| lockd | 30856 | 1 (autoclean) [nfsd] |
| sunrpc | 52548 | 1 (autoclean) [nfsd locked] |
| pcnet_cs | 7572 | 1 [pcnet_cs] |
| 8390 | 5920 | 0 [pcnet_cs] |
| ds | 5740 | 2 [pcnet_cs] |
| 182365 | 22576 | 2 |
| pcmia_core | 39912 | 0 [pcnet_cs ds 182365] |
| uart401 | 5968 | 0 [uart401] |
| sound | 57176 | 0 [sound] |
| soundlow | 300 | 0 [sound] |
| soundcore | 2372 | 3 [sound] |

`lsmod` 工具用于手动加载特定模块。`rmod` 工具用于删除任何未使用的空闲模块。`modprobe` 工具则自动加载特定服务所需的所有基础模块。

## 模块配置 (Module Configuration)

在 Red Hat Linux 中，模块加载等工作由 `kerneld` 处理。然而，从 Red Hat Linux 6.0 开始，`kerneld` 已过时。Red Hat Linux 内核现在使用 `kmod` 来处理内核模块的加载。

用于模块化内核的一个配置文件是 `/etc/conf.modules`。`/etc/conf.modules` 文件指定了模块的命令、选项、路径等。此外，该文件还设置了可能所需的任何别名和参数。

Red Hat Linux 还有一个内核配置工具 (`kernelcfg`)，它在 X 环境下用于帮助配置内核模块。运行此工具，只需在根提示符处输入“`kernelcfg`”。该窗口列出了系统上安装的模块。

内核配置器列出了系统上安装的模块。可以使用窗口底部的 Add（添加）和 Remove（删除）按钮添加或删除模块。此外，您还可以编辑当前模块以添加任何所需的参数。第四个按钮 Restart kernel（重启内核）允许在旧版本的 Red Hat Linux 系统上重启内核。使用 `kmod`，此按钮已弃用。

## 内核配置 (Kernel Configuration)

启动内核所需的文件位于 `/boot` 目录。这些文件包括 `System.map`、`boot.b`、`boot.0300`、`initrd` 以及内核启动镜像（通常以 `<vmlinuz` 前缀命名）。`System.map` 文件是用于调试内核的文件。`boot.b` 文件是 LILO 创建的文件；用于 LILO 的第二阶段，并由主引导记录中的 LILO 指向它。`boot.0300` 文件是您安装 LILO 时创建的主引导记录备份。在启动过程中使用 SCSI 的系统所使用的初始内存磁盘称为 `initrd`。`vmlinuz` 文件是在内核 `make` 过程中创建的内核启动镜像。

内核源码和文档位于 `/usr/src/linux` 目录下。在此目录下，您将找到许多在编译或调试内核时可能很有帮助的文件和资源。其中一些文件包括 `CREDITS` 文件（它向 Linux 内核的许多贡献者致谢），以及 `Documentation` 目录（它包含了许多关于硬件、内核文件等详细文本细节）。它还包含了编译内核所需的文件，如 `Makefile` 和 `System.map`。默认情况下，您对 Linux 内核进行的任何工作都将在此目录下进行。

图 8.1 内核配置器。

## 高级配置 (Advanced Configuration - p173)

### 内核配置工具 (Kernel Configuration Tools)

编译内核的第一步涉及选择要包含哪些功能。可以通过多种方式实现：

- `makeconfig`: 一个基于文本的界面，允许您从菜单中选择功能。
- `makemenuconfig`: 一个需要 `ncurses` 库的图形化界面。
- `makexconfig`: 一个需要 X Window 系统的图形化界面。
- `oldconfig`: 一个脚本，它读取现有的配置文件并仅对新功能进行询问。
