
此示例显示你的电脑上有三个可启动分区，分别称为 `linux`、`linux-up` 和 `dos`。前两个指的是可以启动 LILO 分区的不同启动镜像。第三个指的是一个可启动的 DOS 分区（假设包含 Windows 操作系统）。如果你在几秒后没有输入其他分区的名称，系统将加载第一个可启动分区。

如果你有多个启动镜像，请按 `Shift` 键，LILO 会询问你想启动哪个镜像。可用的启动镜像和其他选项定义在 `/etc/lilo.conf` 文件中。

## 设置 `/etc/lilo.conf` 文件

`/etc/lilo.conf` 文件是 LILO 获取查找和启动可启动分区及镜像所需信息。通过向 `/etc/lilo.conf` 文件添加选项，你可以更改启动过程的行为。以下是 `/etc/lilo.conf` 文件内容示例：

> 由于 Fedora Core 和其他 Linux 系统未使用 LILO，可能没有 `/etc/lilo.conf` 文件。然而，Fedora 安装程序会创建一个 `/etc/lilo.conf.anaconda` 文件以适应你的安装。如果你从 GRUB 切换到 LILO，可以将该文件复制到 `/etc/lilo.conf`。

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_296_0.png)

```
prompt

timeout=50

default=linux

boot=/dev/hda

map=/boot/map

install=/boot/boot.b

message=/boot/message

linear
```

```
image=/boot/vmlinux-2.6.5-1.327

label=linux

initrd=/boot/initrd-2.6.5-1.327.img

read-only

root=/dev/hda6

append=root-LABEL="/"
```

```
other=/dev/hd1

optional

label=dos
```
