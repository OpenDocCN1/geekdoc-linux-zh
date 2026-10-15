
# cp /boot/vmlinuz /boot/vmlinuz.old

如果内核备份无法在启动期间使用，那么它将毫无用处。为了使其有用，必须将其添加到`lilo.conf`文件中。在下面的示例`lilo.conf`文件中，添加了一个新的镜像命令，以便出现问题时加载旧内核：

```
boot=/dev/hda

map=/boot/map

install=/boot/boot.b

prompt

timeout=50

# 正常的 Linux 启动
image=/boot/vmlinux
label=linux
root=/dev/hdb1
read-only

# 紧急 Linux 启动
image=/boot/vmlinuz.old
label=safe
root=/dev/hdb1
read-only

# DOS 启动
other=/dev/hda1
label=dos
table=/dev/hda
```
