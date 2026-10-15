
# 进入单用户模式时运行 sulogin 命令

`su:s:wait=/bin/sulogin`

系统将等待输入 root 密码后生成 shell。

虽然此步骤可以防止任何人重启系统到单用户模式并获得 root 权限，但它并没有解决其他启动问题。`LILO` 本身在操作系统启动之前提供了一个可行的解决方案。另一种方案是在仅给出启动参数时才要求有效密码。

首先，查看一个 `lilo.conf` 文件示例：

```
boot=/dev/had
map=/boot/map
install=/boot/boot.b
vga=normal
default=linux
keytable=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
image=/boot/mlinuz
label=linux
root=/dev/hda5
read-only
other=/dev/fd0
label=floppy
unsafe
```

在此示例中，我们将编辑 `lilo.conf` 文件，在启动默认操作系统“Linux”之前要求密码。使用你喜欢的编辑器向 `/etc/lilo.conf` 文件的 Linux 部分添加以下内容：

```
password=password-string
```

新条目显示所示：

```
boot=/dev/had
map=/boot/map
install=/boot/boot.b
```

## 破解 Linux 暴露：Linux 安全秘籍与解决方案

```
vga=normal
default=linux
key=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
image=/boot/vmlinuz
label=linux
root=/dev/hda5
read-only
password=password-string
other=/dev/fd0
label=floppy
unsafe
```

现在，当系统启动时，Linux 将需要密码。如果延迟时间到期且 `LILO` 选择了默认项（即 Linux），情况也是如此。你可以为每个操作系统选项设置密码。

但是，如果只有在给 `LILO` 传递启动参数时才需要密码，那不是很好吗？是的，这可以通过使用 `lilo.conf` 文件中的 `restricted` 关键字来实现。这将指示 `LILO` 仅在提供参数时才需要密码，如下所示：

```
boot=/dev/had
map=/boot/map
install=/boot/boot.b
vga=normal
default=linux
key=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
image=/boot/vmlinuz
label=linux
root=/dev/hda5
read-only
restricted
password=password-string
other=/dev/fd0
label=floppy
unsafe
```

## 第 5 章：物理攻击

只有在给 Linux 传递参数时才需要密码。否则，系统不会提示你提供密码。如果系统重启且 `LILO` 延迟到期，它将无人值启动默认系统。由于没有提供参数，因此不需要密码。

你也可以通过 `/etc/lilo.conf` 文件将密码和 `restricted` `LILO` 选项全局应用于所有操作系统。通过将这些条目移动到顶部的全局区域来实现，如下所示：

```
boot=/dev/had
map=/boot/map
install=/boot/boot.b
vga=normal
default=linux
keytable=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
restricted
password=password-string
image=/boot/mlinuz
label=linux
root=/dev/hda5
read-only
other=/dev/fd0
label=floppy
unsafe
```

这将对所有 `LILO` 选择使用相同的密码。如果你希望为每个选择设置不同的密码，则需要在每个 OS 规范部分中添加密码。

该文件中仍然存在一个严重的漏洞。`floppy` 部分旨在从软盘启动镜像，以防你需要恢复损坏的操作系统或使用另一个基于软盘的环境（如 DOS）。如果你在 BIOS 中禁用了从软盘启动，那么这非常有用。问题在于，除非你在 `LILO` 启动提示符处为 `floppy` 选择添加任何参数，否则不需要密码。攻击者可以拿一张软盘，向其写入 Linux 镜像，插入系统并重启。当显示 `LILO` 启动提示符时，他们只需输入 `floppy`，软盘上的镜像就会启动。在软盘上的首次启动可能是写入软盘引导扇区的不同 `LILO` 版本。

该版本的 `LILO` 将不包含你的任何限制。攻击者随后可以输入：

```
LILO Boot: Linux 1
```

## 破解 Linux 暴露：Linux 安全秘籍与解决方案

随后 `LILO` 将在你的系统上启动 Linux 进入单用户模式。或者，如果你修改了 `/etc/inittab` 以在进入单用户模式时运行 `/sbin/sulogin`，他们可能还会获得另一个参数如 `init=/bin/bash`。

解决此问题的可能方法是将 `restricted` 指令移动到 Linux 选择规范部分，如下所示：

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
vga=normal
default=linux
keytable=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
password=password-string
image=/boot/mlin
label=linux
root=/dev/hda5
read-only
restricted
other=/dev/floppy
label=floppy
safe
```

这将允许默认 Linux 在不需要密码的情况下启动。然而，从软盘启动时将始终需要密码。对于希望为每个选择设置不同密码的人，你需要为每个规范准备单独的条目。

可以指定的另一个 `LILO` 指令是 `delay=`。它允许你以十分之一秒为单位指定在启动默认项之前等待用户输入的时间。你可以将其设置为 0 以禁用任何用户输入。问题在于，由于某种原因，你需要启动备用内核、软盘或操作系统时，将被阻止这样做。

> 有关 `/etc/lilo.conf` 内容以及如何更改 `LILO` 行为的更多信息，请参阅 `lilo` 和 `lilo.conf` 的在线手册页。

最后，保护 `/etc/lilo.conf` 文件。如果它是可读的，任何用户都能查看你设置的密码。这些密码没有加密，并且以明文形式显示。首先，让 `/etc/lilo.conf` 文件仅对 root 可见。输入以下命令更改 `lilo.conf` 文件的读写权限：

```
# chmod 600 /etc/lilo.conf
```

## 第 5 章：物理攻击

作为最后的预防措施，使用 `chattr` 为文件设置不可变标志：

```
# chattr +i /etc/lilo.conf
```

这将防止对文件进行修改。要移除标志，请使用：

```
# chattr -i /etc/lilo.conf
```
