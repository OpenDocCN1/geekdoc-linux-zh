
```
#
# /etc/lilo.conf 的全局部分
#
nbboot = /dev/hda
install = /boot/boot.b
prompt
timeout = 100
default = linux
#
# /etc/lilo.conf 中的镜像列表
#
other = /dev/hda1
label = win
image = /boot/vmlin-2.2.16
label = linux
root = /dev/hda4
vga = 775
append = "hdc-ide-scsi"
read-only
image = /boot/vmlin-2.4.0-t9
label = new
root = /dev/hda4
vga = 775
append = "hdc-ide-scsi"
read-only
```

```
#
# end /etc/lilo.conf
#
```

大多数 Linux 系统至少会列出一个内核镜像，默认命名为 `linux`。双启动系统通常还会有一个或多个 `other=` 镜像，这允许 LILO 管理 Windows 的启动。列表 4.1 显示的文件是不安全的 LILO 配置；任何看到 LILO 启动提示的用户都可以自由启动系统或向内核发送参数，这可能会完全破坏系统安全。

## password 关键字

保护此 LILO 配置文件的首要任务是在需要时添加 `password` 关键字。该关键字允许系统要求用户在启动由 LILO 管理的某些或所有镜像之前输入由管理员提供的密码。使用 `password` 关键字有两种方法：

- 如果放置在文件顶部的全局配置部分，无论内核镜像如何，所有的启动尝试都要求用户提供密码。
- 如果在文件的 `image=` 部分（例如，仅在 `read-only` 关键字上方），则启动该镜像时需要密码。其他镜像不受影响。

例如，我们将修改文件，要求在启动系统中的任何镜像之前必须输入密码 "A4ni77a*"。新的 `/etc/lilo.conf` 文件如列表 4.2 所示。

### 列表 4.2 更新后的 /etc/lilo.conf 文件

```
#
# /etc/lilo.conf 的全局部分
#
nboot = /dev/hda
install = /boot/boot.b
prompt
timeout = 100
default = linux
password="A4ni77a*"
#
# /etc/lilo.conf 中的镜像列表
#
other = /dev/hda1
label = win
image = /boot/vmlinuz-2.2.16
label = linux
root = /dev/hda4
vga = 775
append = "hdc=ide-scsi"
read-only
```

### 列表 4.2 续

```
image = /boot/vmlinux-2.4.0-t9
label = linux-new
root = /dev/hda4
vga = 775
append = "hdc-ide-scsi"
read-only

#
# end /etc/lilo.conf
#
```

由于 `password=` 关键字已放置在文件全局配置部分的第一个 `other=` 关键字之前，因此启动任何镜像都需要上述列出的密码。

## restricted 关键字

保护此 LILO 配置的下一项任务是向配置文件中添加 `restricted` 关键字。`restricted` 关键字允许受密码保护的镜像在不向内核发送命令行参数的情况下无需密码即可启动。与 `password` 关键字一样，`restricted` 关键字可以通过两种方式之一放入 `/etc/lilo.conf` 文件：

- 如果放置在文件顶部的全局配置部分，所有内核镜像都将被限制，在未先提供相关镜像密码的情况下，无法传递任何内核参数。
- 如果放置在文件的 `image=` 部分（例如，仅作为 `read-only` 关键字之后），可以在无需提供密码的情况下向特定内核传递参数。其他内核镜像不受影响。

例如，我们修改文件使得所有镜像都受到限制。新的 `/etc/lilo.conf` 文件如列表 4.3 所示。

### 列表 4.3 更新后的 /etc/lilo.conf 文件

```
#
# /etc/lilo.conf 的全局部分
#
boot = /dev/hda
install = /boot/boot.b
prompt
timeout = 100
default = linux
password="A4ni77a*"
```

### 列表 4.3 续

```
restricted

#
# /etc/lilo.conf 中的镜像列表
#
other = /dev/hda1
label = win
image = /boot/vmlinuz-2.2.16
label = linux
root = /dev/hda4
vga = 775
append = "hdc=ide-scsi"
read-only
image = /boot/vmlinuz-2.4.0-t9
label = linux-new
root = /dev/hda4
vga = 775
append = "hdc=ide-scsi"
read-only

#
# end /lilo.conf
#
```

这个新的 `/etc/lilo.conf` 文件允许在不提供内核参数的情况下密码启动任何镜像。如果用户尝试输入内核参数，LILO 将要求输入相关密码。

## 将 password 和 restricted 结合

当然，并非所有情况都如描述的那么简单。有时在保护其他镜像的同时，允许某些镜像在不提供密码的情况下启动是有用的。列表 4.4 提供了这种配置的示例。

### 列表 4.4 同时使用 restricted 和 password

```
#
# /etc/lilo.conf 的全局部分
#
boot = /dev/hda
install = /boot/boot.b
prompt
timeout = 100
default = linux
password="A4ni77a*"
```

### 列表 4.4 续

```
#
# /etc/lilo.conf 中的镜像列表
#
other = /dev/hda1
label = win
image = /boot/vmlinuz-2.2.16
label = linux
root = /dev/hda4
vga = 775
append = "hdc=ide-scsi"
restricted
read-only
image = /boot/vmlinuz-2.4.0-t9
label = linux-new
root = /dev/hda4
vga = 775
append = "hdc=ide-scsi"
read-only

#
## /etc/lilo.conf
```
