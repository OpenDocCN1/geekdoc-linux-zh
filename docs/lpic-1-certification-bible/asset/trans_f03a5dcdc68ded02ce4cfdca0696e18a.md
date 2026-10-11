
## 使用 modprobe

**表 13-3 modinfo 选项**

| 选项 | 功能 |
| :--- | :--- |
| -a, --author | 显示作者信息。 |
| -d, --description | 显示描述信息。 |
| -n, --filename | 显示模块文件名。 |
| -f *<字符串>*, --format *<字符串>* | 打印查询字符串。 |
| -p, --parameters | 显示模块参数。 |
| -V, --version | 显示 modinfo 的版本。 |
| -h, --help | 显示选项帮助信息。 |

> 考试提示：modinfo 可以显示关于某个模块的描述和作者信息。

添加和删除模块可以通过另一个名为 modprobe 的工具来处理。它比其他工具提供了一点更多的灵活性，并且可以接受一些配置信息。当 Linux 内核自动加载或卸载模块时，它实际上会以相应的选项运行 modprobe。可用的选项如表 13-4 所示。

**表 13-4 modprobe 选项**

| 选项 | 功能 |
| :--- | :--- |
| -a, --all | 加载所有匹配的模块，而不仅仅是第一个成功加载的模块。 |
| -c, --showconfig | 显示当前使用的配置。 |
| -d, --debug | 显示关于模块堆栈的内部信息。 |
| -k, --autoclean | 将所有已加载的模块设置为自动清理。 |
| -l, --list *模式* | 列出所有匹配的模块。 |
| -n, --show | 不实际加载任何模块。仅显示如果它们已被加载时会产生的输出。 |
| -q, --quiet | 当模块加载失败时不输出错误。 |
| -r, --remove | 移除模块或执行自动清理。 |
| -s, --syslog | 将输出发送到 syslog 而不是控制台。 |
| -t, --type moduletype | 仅考虑此类型的模块。 |
| -v, --verbose | 在命令执行时打印所有命令。 |
| -V, --version | 显示 modprobe 的版本。 |
| -C, --config configfile | 使用指定的模块配置文件，而不是 `/etc/modules.conf`。 |

modprobe 工具可用于加载和卸载模块组。单独使用 -a 选项将使 modprobe 加载其配置文件中定义的所有模块。-r 选项将使其卸载所有当前未使用的自动清理模块。

默认的 modprobe 配置文件是 `/etc/modules.conf` 或 `/etc/conf.modules`，具体取决于发行版。此文件的可能语法如下：

```
[add] above module module_list
alias alias_name result
[add] below module module_list
define VARIABLE WORD
depfile=A_PATH
else
elseif EXPRESSION
endif
if EXPRESSION
include PATH_TO_CONFIG_FILE
insmod_opt=GENERIC_OPTIONS_TO_INSMOD
install module command ...
keep
[add] options module MODULE_SPECIFIC_OPTIONS
path=TAG=A_PATH
pclmapfile=A_PATH
isapnpmapfile=A_PATH
usbmapfile=A_PATH
[add] probe name module_list
[add] probeall name module_list
prune filename
post-install module command ...
post-remove module command ...
pre-install module command ...
pre-remove module command ...
remove module command ...
```

不要被这种复杂的语法外观吓到。你很少会使用比最基本行更多的内容。以下是一个工作站上 `conf.modules` 文件的示例。

```
alias eth0 tulip
alias parport_lowlevel parport_pc
sb
options sb irq=5 dma=1
```

通常，你只会使用 `alias` 和 `options` 这两个选项。别名允许你为模块指定不同的名称。在这个示例中，`tulip` 网络驱动器已被别名为设备名 `eth0`。如果别名的结果字段设置为 off，则模块无法加载。如果结果字段设置为 null，模块加载将始终成功，但实际上不会安装任何模块。

在之前的示例中，名为 `tulip` 的模块（这是使用 Tulip 芯片组的网卡驱动器）已被别名为 `eth0`。这使得系统能够以新名称访问该设备。

模块名称或别名可以通过 `options` 进行配置。这些选项因模块而异，通常用于告知驱动器使用哪个硬件信息。如果在模块名称之前使用了 `-k` 选项，模块上的自动清理设置将被移除。

在之前的示例中，`options` 行配置了 `sb` 模块，这是 Sound Blaster 声卡的驱动器。`options` 行指定该卡已配置为中断请求 5 和直接存储器存取通道 1。并非所有驱动器都要求你告诉它们卡使用的硬件地址。

> 一些发行版仍然使用 `conf.modules` 文件名，但当前的名称是 `modules.conf`。请检查你的发行版使用哪个名称。

使用以下命令：

```
post-install module command ...
post-remove module command ...
pre-install module command ...
pre-remove module command ...
remove module command ...
```

你可以在模块加载或卸载之前或之后执行任何命令。这种功能对于准备或清理过程非常有用。

`modprobe` 工具可用于执行许多进程管理任务。

## 使用 depmod

模块在加载时有时依赖于其他模块。如果自动加载模块，系统必须知道要加载哪些其他模块。depmod 工具负责创建此依赖列表，该列表存储在 `/lib/modules/kernel-version/modules.dep` 中。以下是一个部分示例：

```
/lib/modules/2.2.17/fs/fat.o:
/lib/modules/2.2.17/fs/msdos.o: /lib/modules/2.2.17/fs/fat.o
/lib/modules/2.2.17/fs/ntfs.o:
/lib/modules/2.2.17/fs/vfat.o: /lib/modules/2.2.17/fs/fat.o
/lib/modules/2.2.17/misc/emu10k1.o:
/lib/modules/2.2.17/misc/soundcore.o
/lib/modules/2.2.17/misc/parport_pc.o:
/lib/modules/2.2.17/misc/parport.o
/lib/modules/2.2.17/misc/soundcore.o:
/lib/modules/2.2.17/net/3c501.o:
/lib/modules/2.2.17/net/3c503.o:
/lib/modules/2.2.17/net/8390.o
/lib/modules/2.2.17/net/3c505.o:
```

通常，depmod 在启动时由 rc 文件运行，但如果你手动编辑了 `modules.conf` 文件，你应该再次运行它。表 13-5 显示了 depmod 的可用选项。

**表 13-5 depmod 选项**

| 选项 | 功能 |
| :--- | :--- |
| -a, --all | 搜索由 `modules.conf` 文件指定的所有目录中的所有模块。 |
| -A | 比较文件时间戳，如果有任何更改，则运行 `depmod -a`。 |
| -e, --errsyms | 显示每个模块的所有未解析符号。 |
| -n, --show | 将模块依赖信息输出到控制台，而不是 `modules.dep` 文件。 |
| -s, --syslog | 将所有错误信息输出到 `syslog`，而不是控制台。 |
| -v, --verbose | 启用详细模式，在加载时列出每个模块的名称。 |
| -q, --quiet | 不显示缺失符号错误。 |
| -V, --version | 显示 `depmod` 版本信息。 |
| -r, --root | 覆盖默认的安全预防措施，该措施防止模块实用工具加载由非 root 用户拥有的模块。 |

> 考试提示：每当模块更改时，你都应该运行 depmod。

# 重新配置和安装新内核

## 1.5 内核

- 重新配置、构建并安装自定义内核和模块。
- 获取并安装经过批准的内核源代码和头文件（来自你站点的存储库、CD、kernel.org 或你的供应商）。
- 自定义内核配置（即，在需要时使用 oldconfig、menuconfig 或 xconfig 从现有的 .config 文件重新配置内核）。
- 创建新的 Linux 内核和模块。
- 将新的内核和模块安装到正确的位置。
- 重新配置并运行 lilo。
- 注意：这不要求将内核升级到新版本（完整源代码或补丁）。
- 需要命令：make (dep, clean, menuconfig, bzImage, modules, modules_install), depmod, lilo。
- 需要查看或编辑以下文件：/usr/src/linux/.config, /usr/src/linux/Makefile, /lib/modules/[kernelversion]/modules.dep, /etc/conf.modules | /etc/modules.conf, /etc/lilo.conf。

编译新内核是一个非常直接的过程。首先，你必须获取新的内核源代码或将当前源代码补丁升级到你想要编译的版本。然后，你必须配置内核并启用你需要的选项、功能和驱动器。最后，你编译新内核并安装它，以便可以启动它。

## 获取内核源代码

内核源代码在多个位置可用。你从哪里获取源代码取决于你打算做什么。内核源代码应解压到 /usr/src/linux 目录。如果你需要保留多个版本，最好在 /usr/src 下的每个版本都有自己独立的目录，并为需要编译和使用的那个创建一个指向 /usr/src/linux 的链接。

## 使用发行版源代码

发行版在其随附的内核源代码上包含在 CD-ROM 中。如果你只需要更改现有的内核，最好使用此源代码，因为它将包含发行版制造商提供的任何调整。在基于 RPM 的系统中，包含内核源文件的包通常命名为 kernel-source-<版本>-<发行版补丁级别>.rpm。你还需要安装内核头文件，通常存储在 kernel-headers-<版本>-<发行版补丁级别>.rpm 中。如果你使用 Debian，可以通过发出以下命令获取内核源代码：

```
apt-get install kernel-source-<版本>
```

