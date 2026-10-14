

## Red Hat Linux 6.0 安装指南

如果你希望使用已通过上述方法之一创建的配置文件（/usr/src/linux/.config）来构建内核，可以省略 make mrproper 和 make config 命令，并使用 make dep 命令后跟 make clean 来为构建准备源代码树。

下一步是对源代码组件进行实际编译，生成你的机器可用于启动的工作程序。此处描述的方法在出现意外情况时最易于恢复。如果你对其他可能性感兴趣，详细信息可在 Kernel-HOWTO 中找到，或在 Linux 系统上 /usr/src/linux 中的 Makefile 中找到。

- 使用 make boot 构建内核。
- 使用 make modules 构建你配置的任何模块。
- 使用以下命令将旧的模块集移开：

```
rm -rf /lib/modules/2.0.36-old
mv /lib/modules/2.0.36 /lib/modules/2.0.36-old
```

当然，如果你升级了内核，请将 2.0.36 替换为你正在使用的版本。

- 使用 make modules_install 安装新模块（即使你没有构建任何模块）。

如果你有 SCSI 适配器并且将 SCSI 驱动程序设为模块化，请构建一个新的 initrd 镜像（参见制作 initrd 镜像；请注意，在定制内核中将 SCSI 驱动程序设为模块化在实践中很少有必要）。

为了提供冗余的启动源以防止新内核出现可能的错误，你应保留原始内核。向 LILO 菜单添加内核与重命名 /boot 中的原始内核、将新内核复制到 /boot、在 /etc/lilo.conf 中添加几行并运行 /sbin/lilo 一样简单。以下是随 Red Hat Linux 发行的默认 /etc/lilo.conf 文件示例：

```
boot=/dev/hda
map=/boot/map
```

```
install=/boot/boot.b
prompt
timeout=100
image=/boot/vmlinuz
  label=linux
  root=/dev/hda1
  read-only
```

现在你必须更新 /etc/lilo.conf。如果你构建了新的 initrd 镜像，你必须告诉 LILO 使用它。在此 /etc/lilo.conf 示例中，我们在文件中间添加了四行以指示另一个可启动的内核。我们已将 /boot/vmlinuz 重命名为 /boot/vmlinuz.old 并将其标签更改为 old。我们还为新内核添加了一行 initrd：

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=100
image=/boot/vmlinuz
  label=linux
  initrd=/boot/initrd
  root=/dev/hda1
  read-only
image=/boot/vmlinuz.old
  label=old
  root=/dev/hda1
  read-only
```

现在系统启动时，在 LILO boot: 提示符下按下 [Tab] 时将显示两个选项；

```
LILO boot:
linux old
```

要启动新内核（linux）只需按 [Enter]，或等待 LILO 超时。如果你想启动旧内核（old），输入 old 并按 [Enter]。以下是步骤摘要：

- mv /boot/vmlinuz /boot/vmlinuz.old
- cp /usr/src/linux/arch/i386/boot/zImage /boot/vmlinuz
- edit /etc/lilo.conf
- run /sbin/lilo

你可以通过重新启动计算机并观察消息以确保硬件被正确检测来开始测试你的新内核。

## 制作 initrd 镜像

initrd 镜像用于在启动时加载你的 SCSI 模块。如果满足以下条件，shell 脚本 /sbin/mkinitrd 可以为你的机器构建适当的 initrd 镜像：

- loopback 块设备可用。
- /etc/conf.modules 文件中包含你的 SCSI 适配器的行；例如：
  - alias scsihostadapter BusLogic

要构建新的 initrd 镜像，请使用以下参数运行 /sbin/mkinitrd：

```
/sbin/mkinitrd /boot/newinitrd-image 2.0.36
```

其中 /boot/newinitrd-image 是用于新镜像的文件，2.0.36 是应在其 initrd 镜像中使用其模块（来自 /lib/modules）的内核版本（不一定与当前运行内核的版本号相同）。

## 构建单体内核

要构建单体内核，你遵循与构建模块化内核相同的步骤，只是有所例外。

