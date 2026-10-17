
在可能没有桌面管理器的服务器上安装 GUI 工具的一个用处是，它带有一个命令行语法验证器（`ksvalidator`）。该命令可以用于验证你的 kickstart 文件的语法，有助于故障排除过程。我目前的生产环境 kickstart 文件每个都有几百行，因此有一个可以检查语法的工具总是很有帮助。

## 自动化 Kickstart

到本章目前为止，我们已经查看了如何设置 kickstart 服务器并为客户端制作 kickstart 文件。现在我们可以更进一步，使用 PXE 启动和 TFTP 服务器来自动化此过程。协议仍然保持使用 `HTTP`，以便客户端从你这里获取 kickstart 文件。你可以使用上一节中为客户端创建的 kickstart 文件。

### TFTP 服务器

首先，让我们设置一个 TFTP 服务器，使其能够处理预启动环境的引导文件。在章章的第一部分，你已经准备好了一个 kickstart 服务器，大部分工作已经为你完成了。

步骤 1. 检查目录结构，它应该看起来如下所示：

```bash
# tree /var/www/pub
| /var/www/pub
|-- EFI
|   -- BOOT
|   |    BOOT64.conf
|   |   -- TRANS.TBL
|   |   -- splash.xpm.gz
|-- EULA
|   -- GPL
|   -- HighAvailability
|   -- LoadBalancer
|-- Packages
|   -- README
|   -- ResilientStorage
|   -- ScalableFileSystem
|-- Server
|   -- images
|   |   -- README
|   |   -- TRANS.TBL
|   |   -- efiboot.img
|   |   -- efidisk.img
|   |   -- install.img
|   |   -- product.img
|   |   -- pxboot
|   |       -- initrd.img
|   |       -- vmlinuz
|-- isolinux
|   -- boot.cat
|   -- boot.msg
|   -- grub.conf
|   -- initrd.img
|   -- isolinux.bin
|   -- isolinux.cfg
|   -- memtest
|   -- splash.jpg
|   -- vesamenu.c32
|   -- vmlinuz
|-- kickstart
|   -- redhat-base.cfg
|-- media.repo
|-- repodata
```

Red Hat® 考试实战指南：RHCSA® 和 RHCE® 认证指南与实验手册

如果缺失了任何内容，你可以创建它以匹配此处的目录结构。你还需要为 TFTP 服务器创建一个目录结构，以便从中提供文件：

```bash
# cd / 
# mkdir -p tftpboot/(images,pxelinux.cfg)
```

步骤 2. 你可以使用以下命令进行验证：

```bash
# tree /tftpboot/
/tftpboot/
|-- images
|-- pxelinux.cfg
```

你需要将内核文件从 `/var/www/pub/images/pxboot` 目录拷贝到 TFTP 目录结构，这些文件可能会提供给客户端。

```bash
# cp /var/www/pub/images/pxboot/vmlinuz /tftpboot/images
# cp /var/www/pub/images/pxboot/initrd.img /tftpboot/images
```

步骤 3. 在继续后续之前，你需要安装所有软件包。安装 TFTP 服务器：

```bash
# yum install -y tftp
# yum install -y syslinux
```

安装这些软件包后，你需要配置 TFTP 服务器。步骤 4. 你的配置文件应该如下：

```text
# /etc/xinetd.d/tftp
service tftp {
	server_root = /var/tftp;
	type = udp;
	allow all;
}
```

步骤 5. 对文件进行任何更改后，重启 xinetd：

```bash
# service xinetd restart
Stopping xinetd: [ OK ]
Starting xinetd: [ OK ]
```

步骤 6. 你还需要确保 TFTP 已启动：

```bash
# chkconfig tftp
```

步骤 7. 使用以下命令进行验证：

```bash
# chkconfig tftp
```

步骤 8. 你还需要创建一个名为 `default` 的空文件，这是 PXE 启动的地方：

```bash
# touch /tftpboot/pxelinux.cfg/default
```

步骤 9. 这完成了 TFTP 设置。你现在应该拥有结构：

```bash
# tree /tftpboot/
/tftpboot/
|-- images
|   -- initrd.img
|   -- vmlinuz
|-- menu.c32
|-- pxelinux.cfg
    default
```

## PXE 启动

为了让客户端进行 PXE 启动，你需要确保两项内容已正确设置。首先，你需要一个 DHCP 服务器为客户端提供 IP 地址。这让客户端知道 PXE 服务器的位置。

步骤 1. 使用默认设置 DHCP 服务器：

```bash
# yum install -y dhcp
```

步骤 2. 验证 DHCP 服务器是否安装正确：

```bash
# rpm -qa | grep dhcp
dhcp-4.1.1-12.P1.e16.x86_64
```

步骤 3. 为 DHCP 服务器使用以下示例：

```text
# /etc/dhcp/dhcpd.conf
dns-update-style none;
authorative;

subnet 172.168.1.0 netmask 255.255.255.0 {
	routers 172.168.1.1;
	subnet-mask 255.255.255.0;

	option domain-name "example.com";
	option domain-name-servers 172.168.1.1;

	default-lease-time 21600;
	max-lease-time 43200;

	range dynamic-boot 172.168.1.100 172.168.1.200;

	### PXE Server IP ###
	next-server 172.168.1.1;
	filename "pxelinux.0";
}
```

> 迁移提示
> 在 RHEL5 中，DHCP配置文件是 `/etc/dhcpd.conf`。在 RHEL6 中，它被移动到了 `/etc/dhcp` 目录，因为现在也支持 DHCP IPv6。

步骤 4. 保存你对文件进行的任何更改并重启 DHCP 服务：

```bash
# service dhcpd restart
Stopping dhcpd: [ OK ]
Starting dhcpd: [ OK ]
```

### 第 5 步。启用 DHCP 服务器在系统启动时启动：

```
# chconfig dhcpd on
```

### 第 6 步。验证 DHCP 服务已设置为在启动时启动：

```
# chconfig dhcpd -list
dhcpd 0:off 1:off 2:on 3:on 4:on 5:on
6:off
```

PXE 启动的最后一步是创建一个 PXE 菜单，客户端可以从从中选择启动所需的 kickstart 文件。在此之前，你创建了 `/tftpboot/pxelinux.cfg/default` 文件，它是空的。以下是完整的菜单文件内容：

```
# /tftpboot/pxelinux.cfg
default menu.cfg
prompt 0
timeout 10

MENU TITLE PXE Menu

LABEL RedHat 6.0 x64
MENU LABEL RedHat 6.0 x64
KERNEL images/vmlinux
append initrd-images/initrd.img linux
ks=http://172.168.1.11/pub/kickstart/test.cfg
```

`timeout` 定义了系统在显示默认选项之前等待多长时间。在这里，你还为 PXE 菜单定义了标题，创建了两个不同类型的标签来代表你将要的系统，并定义了一个带有如何启动 kickstart 文件选项内核。保存并关闭文件以完成 PXE 设置。

## 防火墙和 SELinux 配置
