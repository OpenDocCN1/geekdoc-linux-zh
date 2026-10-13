
- d. `/etc/pxe.conf`

- 6. 哪个 RPM 包包含了在 PXE 环境使用的引导加载程序，用于向客户端提供所有可用启动选项？

- a. syslinux

- b. lilo

- c. grub

- d. grub2

- 7. 从安装 DVD 提供的 GRUB 2 启动提示符上必须使用哪种启动参数来引用 Kickstart 文件？

- a. install=

- b. ks=

- c. kickstart=

- d. anaconda=

- 8. 安装 RHEL 服务器后创建的默认 Kickstart 文件名称是什么？

- a. `/root/kickstart.cfg`

- b. `/root/anaconda.cfg`

- c. `/root/anaconda-ks.cfg`

- d. `/root/anaconda-kickstart.cfg`

- 9. 提供菜单驱动界面以创建 Kickstart 文件的工具名称是什么？

- a. kickstart-config

- b. system-config-kickstart

- c. config-kickstart

- d. system-config-install

- 10. 下列哪项*无法*使用 `system-config-kickstart` 指定？

- a. LVM 逻辑卷

- b. 个别 RPM 包

- c. Firewalld 服务

- d. 以上所有

## 基础主题

## 设置安装服务器

在本章中，你将学习如何设置一个安装服务器。如果你需要安装多个实例红帽企业 Linux（RHEL），这将非常有用。使用安装服务器意味着你可以避免通过向每台物理服务器都插入 DVD 来完成安装。相反，你将通过网络安装新服务器。此外，它还允许你安装没有光驱驱动器的服务器（例如刀片服务器）。

设置安装服务器涉及不同的步骤。

- 设置安装服务器以使安装文件可用。要做到这一点，你需要配置网络服务器。这可以是 NFS、FTP 或 HTTP 服务器。
- 接着，你需要向需要安装的客户端交付启动镜像。为了实现全自动化安装，你需要设置 PXE 启动，通过与 DHCP 服务器协作为你的客户端提供启动镜像。
- 作为设置安装服务器的最后一步，创建一个 Kickstart 文件。该文件包含了安装你的服务器所需的所有设置，并提供全自动化安装，但它也可以在 USB 设备上提供。

## 配置网络服务器作为安装服务器

设置安装服务器的第一步是配置网络服务器。这涉及将整个安装 DVD 拷贝到网络共享中，使安装服务器成为一个在线存储库。完成后，你可以使用客户端访问安装文件。设置好后，你可以从普通 DVD 进行测试。一旦服务器完全启动，该程序将变得简单得多，因为启动镜像将由 TFTP 服务器提供。由于还没有 TFTP 服务器，你将必须使用 HTTP。练习 20.1 将将介绍这一过程。

### 练习 20.1 设置网络安装服务器

在本次练习中，你将通过将安装所需的所有文件拷贝到 HTTP 服务器提供的目录中来设置网络安装服务器。完成后，你将使用第 17 章创建的 Apache 服务器从虚拟机上测试安装。

1. 在服务器的光驱驱动器中插入红帽企业 Linux DVD，并导航到安装目录。
2. 使用 `mkdir /var/www/html/install` 在 Apache 文档根目录下为 `example.com` 创建一个子目录。
3. 从挂载红帽 Linux DVD 的目录使用 `cp -R * /var/www/html/install` 将所有文件拷贝到安装目录。
4. 修改 `/etc/httpd/conf.d/` 中虚拟主机的配置文件，并确保它包含了 `Options Indexes` 这一行。如果没有此行，虚拟主机仅在目录包含 `index.html` 文件时才会显示目录内容。
5. 使用 `service httpd restart` 重启 Apache 服务器。
6. 启动浏览器并访问 `http://localhost/install`。你现在应该能看到安装 DVD 的内容。
7. 启动虚拟机管理器（Virtual Machine Manager）并创建一个虚拟机。给虚拟机命名为 `test` 并选择网络安装（Network Install）。
8. 当询问安装 URL 时，输入 `http://localhost/install`（并解析）。
9. 你可以中断安装并移除虚拟机。你现在已经看到安装服务器可以运行。

## 为 PXE 启动设置 TFTP 和 DHCP 服务器

现在你已经设置了网络安装服务器，是时候配置 PXE 启动了。这允许你从网卡启动要安装的服务器（通常需要在启动时按下某个键）。PXE 服务器将分发启动镜像，用于启动初始阶段。

这涉及两个步骤：你需要安装 TFTP 服务器并为 PXE 客户端提供启动镜像，你需要配置 DHCP 连接 TFTP 服务器以提供启动镜像。

**注意** 在本节中，你将学习如何设置一个为客户端提供启动镜像的网络安装服务器。作为替代方案，你可以选择设置一个简单的环境，让从本地启动镜像的客户端引用网络服务器上的安装文件。为此，红帽在 RHN 上提供了 boot.image。

## 安装 TFTP 服务器

安装的第一部分很简单：你需要使用 `yum -y install tftp-server` 安装 tftp-server 包。tftpd 服务由 xinetd 服务管理，为了允许访问 TFTP，你需要打开 `/etc/xinetd.d/tftp` 文件（见列表 20.1）并将默认参数更改为 `no`。

**注意** xinetd 服务也称为互联网超级服务。它源于内存资源受限的时代；为了尽可能有效地利用内存，xinetd 可以配置为监听许多端口，从而访问许多不同的服务。使用 xinetd 仍然很有帮助，特别是对于访问不频繁的服务。xinetd 服务会确保在某些进程访问其端口时启动服务，并在空闲一段时间后关闭它。

在启用 tftp 服务后，完成以下步骤使其可用：

1. 使用 `systemctl start xinetd` 启动 xinetd 服务。
2. 确保将 xinetd 包含在启动程序中，使用 `systemctl enable xinetd`。
3. 确保在你的防火墙配置中允许 tftp，使用 `firewall-cmd --permanent --add-service=tftp`。
4. 重新加载防火墙配置使防火墙修改生效，使用 `firewall-cmd --reload`。

### 列表 20.1 用于 TFTP 的 xinetd 文件

```
[root@server1 ~]# cat /etc/xinetd.d/tftp
# default: off
# description: The tftp server serves files using the trivial file
# transfer (\
#      protocol. The tftp protocol is often used to boot diskless \
#      workstations, download configuration files to network-aware
#      printers\,
#      and to start the installation process for some operating
#      systems.
service tftp
(
    socket_type = dgram
    protocol = udp
    wait = yes
    user = root
    server = /usr/sbin/in.tftpd
    server_args = -s /var/lib/tftpboot
    disable = no
    per_source = 100 2
    flags = IPv4
)
```

此时，简单文件传输协议 (TFTP) 服务器已运行。你现在需要配置主机主机协议 (DHCP)，通知 TFTP 服务器发放启动镜像。

## 为 PXE 启动配置 DHCP

在安装服务器上，没有 DHCP 服务器，TFTP 服务器就无法存在。在进行 PXE 启动时，DHCP 服务器第一个响应，提供所有所需的 IP 相关配置以及将要使用的 DHCP 服务器信息。因此，你现在必须安装 DHCP 服务器。使用 `yum install -y dhcp` 安装该服务器。然后，你需要创建一个子网并修改 DHCP 服务器配置，使其能够向 PXE 客户端发放启动镜像。要做到这一点，请确保在你的 `dhcpd.conf` 中包含以下内容（参见列表 20.2）并重启 DHCP 服务器。

### 列表 20.2 在 dhcpd.conf 中添加 PXE 启动行
