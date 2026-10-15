
如果你尚未运行 NFS 服务器，请按照以下步骤在你的 Ubuntu 14.04 主机上安装并配置：

```
~ sudo apt-get install nfs-kernel-server
```

`/nfsroot` 目录将用作 NFS 服务器的根目录，因此目标文件系统将从 Yocto 构建目录解压到此处：

```
$ sudo mkdir -m 777 /nfsroot
$ cd /nfsroot
~/nfsroot$ sudo tar xvf ~/fsl-release-bsp/build_imx6_qt5_x11/tmp/deploy/images/imx6qqsabres/fsl-image-qt5-imx6qqsabres.tar.bz
```

接下来，将配置 NFS 服务器以导出 `/nfsroot` 文件夹。编辑 `/etc/exports` 文件并添加下行代码：

```
/nfsroot/ * (rw,no_root_squash,async,no_subtree_check)
```

然后重启 NFS 服务器以使配置更改生效：

```
$ sudo service nfs-kernel-server restart
```

## 安装 DHCP 服务器

安装 DHCP 服务器：

```
$ sudo apt-get install isc-dhcp-server
```

在 Ubuntu 上，编辑 `/etc/dhcp/dhcpd.conf` 并添加以下代码：

```
subnet 10.0.0.0 mask 255.255.255.0 {
  host target {
    fixed-address 10.0.0.10;
  }
}
```

重启 DHCP 服务器：

```
$ sudo service isc-dhcp-server restart
```

## 为开发环境配置网络启动

在驱动实验室开发期间，我们在主机系统中同时使用 TFTP 和 NFS 服务器，只有 U-Boot 引导加载程序（bootloader）会存储在 SD 卡中。引导加载程序将从 TFTP 服务器获取 Linux 内核，而内核将从 NFS 服务器挂载根文件系统。对内核或根文件系统的任何更改都可以在无需重新编程 SD 卡的情况下生效。

## 安装 TFTP 服务器

如果你尚未运行 TFTP 服务器，请按照以下步骤在你的 Ubuntu 14.04 主机上安装并配置 TFTP 服务器：

```
~ sudo apt-get install ttfpd-hpa
```

`ttfpd-hpa` 配置安装在 `/etc/default/ttfppd-hpa`。默认情况下，它使用 `/var/lib/tftpboot` 作为根 TFTP 文件夹。使用以下命令更改文件夹权限以允许所有用户访问：

```
~ sudo chmod 1777 /var/lib/tftpboot
```

使用 "`netstat -a | grep tftp`" 检查 TFTP 服务器状态。如果没有结果，：

## 安装 NFS 服务器

如果你尚未运行 NFS 服务器，请按照以下步骤在你的 Ubuntu 14.04 主机上安装并配置：

```
~ sudo apt-get install nfs-kernel-server
```

`/nfsroot` 目录将用作 NFS 服务器的根目录，因此目标文件系统将从 Yocto 构建目录解压到此处：

```
$ sudo mkdir -m 777 /nfsroot
$ cd /nfsroot
~/nfsroot$ sudo tar xvf ~/fsl-release-bsp/build_imx6_qt5_x11/tmp/deploy/images/imx6qqsabres/fsl-image-qt5-imx6qqsabres.tar.bz
```

接下来，将配置 NFS 服务器以导出 `/nfsroot` 文件夹。编辑 `/etc/exports` 文件并添加下行代码：

```
/nfsroot/ * (rw,no_root_squash,async,no_subtree_check)
```

然后重启 NFS 服务器以使配置更改生效：

```
$ sudo service nfs-kernel-server restart
```

## 安装 DHCP 服务器

安装 DHCP 服务器：

```
$ sudo apt-get install isc-dhcp-server
```

在 Ubuntu 上，编辑 `/etc/dhcp/dhcpd.conf` 并添加以下代码：

```
subnet 10.0.0.0 mask 255.255.255.0 {
  host target {
    fixed-address 10.0.0.10;
  }
}
```

重启 DHCP 服务器：

```
$ sudo service isc-dhcp-server restart
```

## 与 iMX6 SABRE 开始上手

iMX6 SABRE 引入了 iMX6 系列处理器。由于其可扩展性设计，该开发板与 iMX6 兼容，并能快速进入市场。

[image](img/739a35b9067f8a55eff80a587614f)

## 设置系统

按照以下步骤设置你的系统：

1. 将 SD 卡插入 SD3。
2. 连接 USB 线到 J5。
3. 连接以太网线到 J7。
4. 连接电源线到 J1。
5. 设置拨码开关（SW6）：

| D1 | D2 | D3 | D4 | D5 | D6 |
| --- | --- | --- | --- | --- | --- |
| Off | On | Off | Off | On | Off |

6. 开启 SW1 电源。使用 SW2 按钮重置系统。

## 设置以太网通信

你将通过 TFTP 协议从主机传输文件到目标。

1. 在主机上，点击桌面上的网络管理器，选择“有线连接”并点击“编辑”。

[image](img/739a35b9067f8a55eff80a587651)

2. 选择“IPv4 设置”选项卡，并将方法选择为“手动”。点击“添加”，并设置 IP 地址、子网掩码和网关：

- 地址：10.0.0.1
- 子网掩码：255.255.255.0
- 网关：无或 0.0.0.0

最后点击“保存”按钮。

[image](img/739a35b9067f8a55eff80a587652)

3. 点击“有线连接”以激活此接口。

## 设置 U-Boot 环境变量

## 指定内存地址

内核和设备树加载到的内存地址不会根据运行的设备而改变。指令使用环境变量 `loadaddr` 和 `fdt_addr` 来指示这些值。下表显示了不同 i.MXX 板上使用的地址：

| 变量 | 6Quad 和 6Dual SABRE (AI 和 SD) | SoloLite | SoloX | 说明 |
| --- | --- | --- | --- | --- |
| loadaddr | 0x12000000 | 0x80800000 | 0x80800000 | 内核加载到的内存地址 |
| fdt_addr | 0x18000000 | 0x83000000 | 0x83000000 | 设备树代码拷贝到的内存地址 |

板的顶部视图如下图所示：

[image](img/739a35b9067f8a55eff80a587658)

底部视图如下所示：

[image](img/739a35b9067f8a55eff80a587659)

开启 SABRE 板上的“SW1 电源按钮”。在主机上启动并配置 minicom 以查看系统启动。在图中你可以看到所需的

37

## 构建系统

配置（终端窗口配置：115.2 kbaud，8 数据位，1 停止位，无校验位）。

确保硬件和软件流控均已禁用。

```
$ minicom -w -s
```

![](img/739a35b59067f8a55eff80a58765146f_63_0.png)

按下 RESET SW2 按钮重置系统并启动引导序列。按任意键停止 U-Boot 序列。

![](img/739a35b59067f8a55eff80a58765146f_63_1.png)

运行以下命令将环境变量重置为默认值：

```
U-Boot > env default -f -a
U-Boot > saveenv
U-Boot > reset
```

要使用 DHCP 服务器进行网络启动，请在 U-Boot 提示符设置以下环境变量：
