
## 表 5.1 继续

| 关键字语法 | 描述 |
|---|---|
| compact | 请求进行优化以减少加载时间并使映射文件更小。 |
| default=name | 指定默认加载的映像。如果省略此关键字，则使用第一个定义的映像。 |
| delay=n | 在启动默认映像前等待 n/10 秒。此选项在您希望有更多时间中断启动序列时很有用。 |
| fix-table | 允许 LILO 调整分区表条目，使分区的第一个和最后一个扇区的线性地址与扇区/磁头/柱面地址匹配。使用时请谨慎。 |
| force-backup=filename | 这与 backup 类似，但会覆盖名为 /lilo.map 的现有文件，而 backup 则不会。 |
| ignore-table | 忽略损坏的分区表并按配置文件中指定的方式安装 LILO。 |
| install=boot_sector | 指定用作新引导扇区的文件。默认值为 /boot/boot.b。 |
| linear | 使用线性寻址模式而不是使用扇区/磁头/柱面方法寻址磁盘。如果指定了 compact，则可能无法工作。 |
| map=filename | 使用指定文件作为映射文件。默认为 /boot/map。 |
| message=filename | 指定一个文件在引导提示符之前显示。您可以使用此文件向用户显示消息或可用映像列表。 |
| prompt | 在无需用户干预的情况下呈现引导提示符。如果存在此关键字而 timeout 关键字不存在，则无法进行无人值守重启。 |
| timeout=n | 如果在 n/10 秒内未收到用户输入，则启动默认映像。 |
| verbose=level | level 指定运行 lilo 时打印的信息量。有效级别为负数，表示仅显示警告和错误，以及范围为 0-5 的数字，每个数字提供更多信息。 |

这些并非所有关键字，但它们是最有可能使用的关键字。除了全局关键字外，还有许多每映像关键字可用。其中一些每映像关键字也可以在全局部分中指定，以作为所有定义映像的默认值。表 5.2 定义了一些最常见的每映像关键字。星号表示那些可以作为每映像关键字或全局关键字指定的关键字。

### 表 5.2 LILO 每映像关键字

| 关键字语法 | 描述 |
|---|---|
| alias=name | 指定当前映像的次要名称。 |
| fallback=command_line * | 如果当前映像正在运行且系统崩溃，则在下次启动时将指定的命令行传递给 LILO。 |
| label=name | 为当前映像命名。 |
| lock * | 允许您无论其在映射中的位置如何都重新启动到当前映像。当前映像成为默认值，直到被用户输入覆盖为止。 |
| password=password * | 在启动此映像之前提示用户输入密码。如果使用此选项，您必须确保 lilo.conf 文件不可被 root 用户以外的人读取，因为密码未加密。 |
| restricted | 此选项仅在 password 选项使用时有效。它修改密码行为，使密码挑战仅在用户在引导提示符处指定命令行参数时才进行。 |
| single-key * | 设置此选项后，如果您定义了单键别名或标签，则可以使用单次按键（无需按 Enter）激活映像。 |

最后的关键字集，描述于表 5.3 中，仅适用于 Linux 内核的引导。

### 表 5.3 LILO Linux 内核关键字

| 关键字语法 | 描述 |
|---|---|
| append=string | 将指定的字符串添加到内核命令行。 |
| initrd=filename | 指定包含要加载到初始 RAM 磁盘映像中的文件。 |
| ramdisk=size | 指定可选 RAM 磁盘的大小，默认值从内核映像中读取。将 size 设置为零表示不应创建 ramdisk。 |
| read-only | 当内核映像启动时，根文件系统将以只读方式挂载，以便使用 fsck 检查然后重新挂载。 |
| read-write | 根文件系统将以读写方式挂载。 |
| root=device | 指定的设备包含根文件系统。 |
| vga=mode | VGA 文本模式基于指定的模式设置，其中 mode 为 normal (80x25)、extended (80x50)、ask 或数字之一。有效数字可通过首先指定 ask 来确定，ask 会给出检测到的模式列表，然后用所呈现的数字之一替换 ask。 |

## /sbin/lilo 的命令行选项

除了配置文件中所有可用的选项外，还有许多命令行选项可以改变 LILO 的行为。其中许多会导致行为模仿配置文件关键字。这些选项显示在表 5.4 中。

### 表 5.4 LILO 命令行选项

| 命令行选项 | 配置文件关键字 |
|---|---|
| -b boot_dev | boot = boot_dev |
| -c | compact |
| -d N | delay = N |
| -D name | default = name |
| -i boot_sector | install = boot_sector |
| -l | linear |
| -m file | map = file |
| -P fix | fix-table |
| -P ignore | ignore-table |
| -s filename | backup = filename |
| -S filename | force-backup = filename |
| -v | verbose = level |

其他可与映射安装程序一起使用的 lilo 选项包括查询映射文件、为下次重启填充命令行或指定不同的配置文件名的选项。表 5.5 显示了这些选项及其含义。

### 表 5.5 更多 LILO 命令行选项

| 命令行选项 | 描述 |
|---|---|
| -C filename | 使用 filename 作为配置文件而不是默认的 /etc/lilo.conf。 |
| -q | 查询映射文件以获取映像列表。 |
| -r directory | 在执行命令之前 chroot 到 directory。这在从修复磁盘启动时很有用。 |
| -R string | 将此字符串存储在映射文件中，以用作下次重启的命令行。这可以在测试时临时更改默认内核。此命令行在使用后会从映射文件中删除。 |
| -t | 仅测试模式。这会执行命令行和配置文件中指定的所有操作，但不会安装新的映射。 |
| -u [device_name] | 恢复指定设备引导扇区的备份副本。验证是通过检查时间戳来执行的。 |
| -U [device_name] | 与 -u 相同，但不执行验证。 |

## LILO 技巧和窍门

现在我们已经初步了解，让我们看一个更复杂的示例。在此示例中，我们安装了多个操作系统，并希望 LILO 启动它们全部。以下列表描述了构建 /etc/lilo.conf 文件所需的数据。

- 第一个分区，/dev/hda1，包含 Windows
- 分区 2 包含 Fred 的 Linux 0.5
- 分区 3 包含 Red Hat Linux
- 分区 4 是 Linux 交换分区
- 分区 5 包含 FreeBSD

出于各种原因，我们希望 Fred 的 Linux 和 Red Hat 完全独立于彼此。此外，这是一台现代机器，不会因大驱动器而出现 1024 柱面问题。现在问题参数已经定义，请参阅清单 5.1 查看 lilo.conf 文件的样子。

## 清单 5.1 /etc/lilo.conf

```
#
# General section
#
boot = /dev/hda
compact
install = /boot/boot.b
message = /etc/lilo.msg
verbose = 2
lock

# After 10 seconds, boot the default image
prompt
timeout = 100

#
# Boot my Linux 2.2.5 kernel from /dev/hda5
# This kernel requires a password to boot if you specify any
# kernel command options.
#
image = /boot/vmlinuz-2.2.5
    label = Red Hat
alias = 1
root = /dev/hda5
read-only
password = s0l@r$
restricted
initrd = /boot/initrd.gz

#
# Boot my experimental Linux 2.3.8 kernel from /dev/hda5.
# This kernel requires a password to be specified.
#
image = /boot/vmlinuz-2.3.8
label = Testing
alias = 2
root = /dev/hda5
read-only
password = d9j+@01
initrd = /boot/initrd-2.3.8.gz
fallback = Red Hat

#
# Boot Windows from /dev/hda1.
#
other = /dev/hda1
label = Windows
alias = 3
single-key
table = /dev/hda

#
# Boot Fred's Linux from /dev/hda2.
#
other = /dev/hda2
label = Fred
alias = 4
single-key
table = /dev/hda

#
# Boot FreeBSD from /dev/hda7.
#
other = /dev/hda7
```
