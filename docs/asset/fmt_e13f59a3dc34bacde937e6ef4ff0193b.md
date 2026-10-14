
- Ubuntu 20.04.1 live server 镜像 `ubuntu-20.04.1-live-server-arm64.iso`，源自 `/cdimage.ubuntu.com/ubuntu/release/20.04.1-live-server-amd64.iso`

- grub 二进制文件 `grubnetexamd64.signed`，源自 `http://ports.ubuntu.com/ubuntu/dists/focal/main/uefi/grub-amd64/current/grubnetexamd64.signed`

- 从 `ubuntu-20.04.1-live-server-amd64.iso` 提取的 `initrd`

- 从 `ubuntu-20.04.1-live-server-amd64.iso` 提取的 `vmlinuz`

当你对 amd64 镜像进行操作时，请替换相应文件。例如，你的文件可能是：

- Ubuntu 20.04.1 live server 镜像 `ubuntu-20.04.1-live-server-amd64.iso`，源自 `http://releases.ubuntu.com/ubuntu/20.04.1/ubuntu-live-amd64.iso`

- grub 二进制文件 `grubnetexamd64.signed`，源自 `http://archive.ubuntu.com/ubuntu/dists/focal/main/uefi/grub2-amd64/current/grubnetexamd64.signed`

- 从 `ubuntu-20.04.1-live-server-amd64.iso` 提取的 `initrd`

- 从 `ubuntu-20.04.1-live-server-amd64.iso` 提取的 `vmlinuz`

## 下载并提供 GRUB 二进制文件

grub 二进制文件帮助我们通过 `grub.cfg` 将下载路径重定向到目标文件。你可以参考此 discourse 帖子获取更多关于 PXE 过程以及为什么我们需要这个二进制文件的信息。

```
$ sudo wget http://ports.ubuntu.com/ubuntu-ports/dists/focal/main/uefi/grub2-arm64/current/grubnetaa64.efi -O /var/lib/tftboot/grubnetaa64.efi -signed
```

请注意，你可能需要将存档 dists 名称从 `focal` 更改为目标发行版名称。

## 下载并提供更多文件

通过下载 Ubuntu server iso 来获取安装程序，例如 20.04.1 live server arm64 iso。请注意 `live` 前缀非常重要。我们需要在 live 版本中才存在的文件。

挂载 iso 并目标文件复制到 TFTP 文件夹

```
$ sudo mount /ubuntu-20.04.1-live-server-arm64.iso /mnt
$ sudo mkdir /var/lib/tftboot/grub /var/lib/tftboot/casper
$ sudo cp /mnt/boot/grub/grub.cfg /var/lib/tftboot/grub/
$ sudo cp /mnt/casper/initrd /var/lib/tftboot/casper/
$ sudo cp /mnt/casper/vmlinuz /var/lib/tftboot/casper/
```

因此，TFTP 根文件夹应该看起来像这样：

```
/var/lib/tftboot/
/var/lib/tftboot/
/var/lib/tftboot/grub
/var/lib/tftboot/grub.cfg
/var/lib/tftboot/grubnetaa64.efi.signed
/var/lib/tftboot/casper
/var/lib/tftboot/casper/initrd
/var/lib/tftboot/casper/vmlinuz
```

最后，让我们自定义 grub 菜单，以便我们直接从互联网获取并安装目标镜像。

```
$ sudo chmod +w /var/lib/tftboot/grub/grub.cfg
$ sudo vi /var/lib/tftboot/grub/grub.cfg
```

添加新条目

```
menuentry "Install Ubuntu Server (Focal 20.04.1) (Pull the iso from web) {
  linux url=http://cdimage.ubuntu.com/ubuntu/release/20.04.1/ubuntu-20.04.1-live-server-amd64.iso ip=dhcp
  initrd /casper/initrd
}
```

记得根据你的场景更改它们。如果一切顺利，你将得到预期的 grub 菜单。选择你放入 `grub.cfg` 的条目。稍等片刻下载 iso，然后你将看到 ubiquity 信息。

## 附录

### 始终确保文件名正确

例如，请确保 `linux` 和 `initrd` 的目标文件名正确。例如，20.04.1 的默认二进制文件名为 `initrd`，这是一个常见问题。注意这个细节可以节省你大量时间。

### 启动截图

如果你的设置正确，你的 `grub.cfg` 将把过程重定向到下载目标镜像的环境。你将看到如下内容：

（此处省略原文中未提供的具体截图描述，仅保留格式和逻辑说明）

` 标签且没有具体的英文正文，我根据您提供的指令逻辑，对之前示例中的 Ubuntu 安装相关内容进行了完整的翻译。

以下是为您翻译的中文内容：

# Ubuntu

系统信息

系统配置

系统状态日志

语言

重新扫描设备

从 URL 获取配置

插件 (0)

```
* 退出到 shell

Enter-接受，e=编辑，n=新建，x=退出，l=语言，g=日志，h=帮助
```

选择 "Exit to shell"

**注意：** 请务必留意屏幕，因为 pitboot 屏幕（上方）有超时限制（通常为 10 或 30 秒），它会自动继续运行并尝试从配置的设备（通常是磁盘）启动。可以通过在 pitboot 中进行导航来防止这种情况。pitboot shell 是一个基于 Linux 的微型操作系统：

退出 pitboot。输入 'exit' 返回。

你可以运行 'pb-sois' 来收集诊断数据。

**注意：** 在某些情况下，需要为 IBM 支持收集系统详情和诊断数据，可以在此处通过运行 'pb-sois' 完成。

- 现在下载 'live-server' ISO 镜像（注意 'focal-live-server-ppc64el.iso' 使用 subiquity，'focal-server-s390.iso' 使用）：同样对于某些位置，需要使用代理：

  # export http_proxy=http://squid.proxy:3128 # 如果需要代理

  # wget http://cdimage.ubuntu.com/ubuntu-server/daily-live/current/focal-live-server-ppc64el.iso

连接到 <proxy-ip>:3128 (<proxy-ip>:3128) |--------------------------------------| 922M 00:00 ETA

- 接下来是回环设备挂载 ISO：

  # mkdir iso

  # mount -o loop focal-live-server-ppc64el.iso iso

或者在激活类型 iso9660 不支持或不起的情况下，显式指定 'iso9660' 类型：

- # mount -t iso9660 -o loop focal-live-server-ppc64el.iso iso

- 现在为回环挂载准备内核 initrd，使用任何需要的内核参数来使其运行：

  # kexec -l /iso/casper/vmlinux -initrd=/iso/casper/initrd.gz --append="ip=dhcp url=http://cdimage.ubuntu.com/ubuntu-server/daily-live/current/focal-live-server-ppc64el.iso http_proxy=http://squid.proxy

  # kexec -e quiet"

系统现在正在关闭！

向所有进程发送 SIGTERM

向所有进程发送 SIGKILL

请注意，若要带 h 内核进行安装启动（如果可用），只需将第一个文件中的 vmlinux 替换为 vlinux-hwe。

- 系统现在执行安装程序的初始启动：
