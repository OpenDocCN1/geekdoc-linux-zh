
# 第 21 章 . 设置安装服务器

列表 21.2 示例配置中最重要的部分是类定义。`next-server` 语句指向 TFTP 服务器的 IP 地址。`filename` 语句指向 `pxelinux.0` 文件，该文件位于 `/var/lib/tftpboot/pelinux` 目录。这是 PXE 客户端获取启动镜像的地方。

## 创建 TFTP 服务器

列表 21.2 示例配置中最重要的部分是类定义。`next-server` 语句指向 TFTP 服务器的 IP 地址。`filename` 语句指向 `pxelinux.0` 文件，该文件位于 `/var/lib/tftpboot/pelinux` 目录。这是 PXE 客户端获取启动镜像的地方。

## 练习 21.2

### 为 PXE 启动配置 TFTP 服务器

为了设置 TFTP 服务器，你将配置 DHCP 服务器和 TFTP 服务器。注意，在你的网络上配置 DHCP 导致问题。一个复杂的因素是 KVM 虚拟机网络环境可能运行着 DHCP 服务器。这意味着你不能使用将配置为服务虚拟机的 DHCP 服务器。为了成功，请确保你的 Red Enterprise Linux 断开网络，并仅连接到能够执行 PXE 启动的电脑。

+ 1. 使用 `yum install tftp-server` 安装 TFTP 服务器。因为 TFTP 由 xinetd 管理，使用 `chkconfig` 将其添加到运行级别中。
+ 2. 使用编辑器打开 `/etc/xinetd.d/tftp` 配置文件，并将 `disabled = yes` 行改为 `disabled = no`。
+ 3. 如果需要，安装 DHCP 服务器。打开 `/etc/dhcp/dhcpd.conf` 配置文件，并赋予其列表 21.2 所示的精确内容。
+ 4. 从 RHEL 安装光盘的 `Packages` 目录将 `syslinux-<version>.rpm` 复制到 `/tmp`。你需要从中提取 `pxelinux.0` 文件。这是设置 PXE 启动环境的关键文件。要提取 RPM 包，使用 `cd /tmp` 进入目录，然后使用 `rpm2cpio syslinux-<version>.rpm | cpio -idmv` 提取该文件。

## 练习 21.2（续）

- 6. 使用 `mkdir /var/lib/tftboot/pxelinux/pxelinux.cfg` 创建存储 pxelinux 配置文件的目录。
- 7. 在 `/var/lib/tftboot/pxelinux/pxelinux.cfg` 中，创建一个名为 `default` 的文件，包含以下内容：

```
default Linux
prompt 1
timeout 10
display boot.msg
label Linux
menu label ^Install RHEL
menu default
kernel vmlinux
append initrd=initrd.img
```

- 8. 如果你想在进行 PXE 启动时使用启动画面（splash image），将 `/boot/grub/splash.x.gz` 文件复制到 `/var/lib/tftboot/pxelinux/`。
- 9. 你可以在 `images/pxeboot` 目录下找到 `vmlinux` 和 `initrd.img` 这 Red Hat 安装配置文件。将它们复制到 `/var/lib/tftboot/pxelinux/` 目录。
- 10. 使用 `service dhcp restart` 和 `service xinetd restart` 来重启所需的服务。
- 12. 如果你想继续安装，当安装程序提示“What media contains the packages to be installed?”时，选择 URL。接下来，输入你在练习 21.1 中创建的 Web 服务器安装镜像的 URL：`http://server1.example.com/install`。

在练习 21.2 中，你设置了一个 PXE 服务器来安装系统。你也可以使用同一个服务器添加额外的部分。例如，救援系统是一个很有用的部分，添加一个允许从本地磁盘启动的部分也会很有用。列表 21.3 中 `default` 文件的示例内容展示了如何操作。

如果你正在向 PXE 菜单添加更多选项，那么增加 `timeout` 值也是合理的。在列表 21.3 中，使用 `timeout 600` 值就实现了这一点。但是，你应该注意，如果你想按照后续节描述的那样使用 kickstart 文件通过 PXE 服务器进行自动化安装，这通常不是你需要的。

### 列表 21.3：为 PXE 启动菜单添加更多选项

```
default Linux

prompt 1

timeout 600

display boot.msg

label Linux

    menu label ^Install RHEL

    menu default

    kernel vmlinuz

    append initrd=initrd.img

label Rescue

    menu label ^Rescue system

    kernel vmlinuz

    append initrd=initrd.img rescue

label Local

    menu label Boot from ^local drive

localboot 0xffff
```

## 创建 Kickstart 文件

你现在已经创建了一个环境，安装服务器所需的所有内容都可以在另一台服务器可用。这意味着你不再需要使用光盘来执行安装，然而，你仍然需要回答正常安装过程中的所有问题。Red Hat 为这一挑战提供了一个极佳的解决方案：kickstart 文件。在本节中，你将学习如何使用 kickstart 文件进行完全自动化的安装，以及如何优化 kickstart 文件以符合你的需求。

## 使用 Kickstart 文件执行自动化安装

当安装 Red Hat 系统时，在 root 用户的家目录下会创建一个名为 `anaconda-ks.cfg` 的文件。该文件包含了安装电脑时使用的大部分设置。如果你想尝试执行自动化 kickstart 安装，这是一个很好的起点。

要指定你想使用 kickstart 文件来安装服务器，你需要告诉安装程序去哪里找到该文件。如果你想从本地 Red Hat 安装盘进行安装，请在安装时添加 `linux ks=` 引导参数。（确保在 `=` 之后包含了 kickstart 文件的确切位置。）作为该参数的参数，添加文件的完整链接。例如，如果你将 kickstart 文件复制到 `server1.example.com` 服务器的文档根目录下，在从 DVD 安装时添加以下行作为启动选项：
`linux ks=http://server1.example.com/anaconda-ks.cfg`

要在从 TFTP 服务器的自动化安装中使用 kickstart 文件，你将将 kickstart 文件添加到 TFTP 文件中启动安装的区域。在这种情况下，你需要安装服务器的区域显示如下：

```
label Linux

menu label ^Install RHEL

menu default

kernel vmlinuz

append initrd=initrd.img

ks=http://server1.example.com/anaconda-ks.cfg
```
