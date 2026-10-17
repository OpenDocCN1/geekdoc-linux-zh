
- 使用命令将`/usr/src/linux/include/net/tcp.h`中的`Myrinet` `MAX_WINDOW`设为`262144`以提高TCP性能：

```
#define MAX_WINDOW 262144
```

- 在`/usr/src/linux/Makefile`顶部将`EXTRAVERSION`改为`smpx`

```
EXTRAVERSION = smpx
```

## 编译内核

内核现在可以进行编译。构建程序如下所示；但是，如果你不理解它，请参考`Kernel-HOWTO`。从使用命令开始：

```
### cd /usr/src/linux
# make oldconfig
# make dep clean bzimage modules
```

一旦成功编译了内核，你应该使用命令安装模块、内核和`map`，并创建一个`ramdisk`镜像：

```
### cd /usr/src/linux
# make modules_install
# cp arch/i386/boot/bzimage /boot/bzImage-2.2.18smpx
# cp System.map /boot/System.map-2.2.18smpx
### cd /boot
# mkinitrd initrd-2.2.18smpx.img 2.2.18smpx
# ln -f bzImage-2.2.18smpx bzimage
# ln -f System.map-2.2.18smpx System.map
# ln -f initrd-2.2.18smpx.img initrd.img
```

接下来，将内核段添加到`/etc/lilo.conf`并更改默认参数（参见示例 6-5）。请务必检查`root=`段是否与`lilo.conf`中的其他项匹配。在开始之前，确保清楚自己在修改此文件，并进行备份。

### 示例 6-5 提取 /etc/lilo.conf

```
default=linux-smpx
image=/boot/bzImage
initrd=/boot/initrd.img
```

```
label=linux-smpx
read-only
root=/dev/sda6
```

当你更改了`/etc/lilo.conf`后，你必须运行`lilo`命令来实际安装`lilo`加载程序，如示例 6-6 所示。

### 示例 6-6 使用 lilo 命令安装 lilo loader

```bash
[root@master]# /sbin/lilo
Added linux-smpx *
Added linux-smp
Added linux
[root@master ~root]#
```

注意，星号（`*`）表示默认内核，它应该与你刚刚添加到`lilo.conf`中的`label=`行匹配。

## 安装以太网驱动程序

为了完成内核安装，请下载并编译`Intel`以太网驱动程序。你可以从以下地址下载：

```
http://support.intel.com/support/network/
```

按照该网站提供的编译说明进行。

> **提示：** 在我们的实验室，我们使用以下命令来安装快速以太网适配器和千兆适配器的驱动：

（安装快速以太网）

```bash
### mkdir -p /usr/local/e100
# cd /usr/local/e100
（下载文件 e100-1.5.5a.tar.gz）
# tar zzvf e100-1.5.5a.tar.gz
### cd e100-1.5.5/src
# make install
```

（安装千兆适配器）

```bash
# mkdir -p /usr/local/e1000
# cd /usr/local/e1000
（下载文件 e1000-3.0.7.tar.gz）
# tar zzvf e1000-3.0.7.tar.gz
# cd e1000-3.0.7/src
# make install (采用所有默认值)
```

**注意：** 为了验证`e100`和`e1000`驱动程序是否安装成功，我们需要重启系统并通过执行以下命令来探测驱动程序：

```bash
(modprobe 命令将尝试为快速以太网适配器加载 e100 驱动程序 - 如果安装未成功，你将收到错误)
# modprobe e100
（验证文件 e100 是否存在）
# ls /lib/modules/2.2.18smpx/net/e100.o
(modprobe 命令将尝试为千兆适配器加载 e1000 驱动程序 - 如果安装未成功，你将在这里收到错误)
# modprobe e1000
（验证文件 e100 是否存在）
# ls /lib/modules/2.2.18smpx/net/e1000.o
```

# 剩余接口配置

在重启之前，你应该配置剩余的以太网适配器。你可以通过`linuxconf`为`eth1`和`eth2`添加配置，或者手动执行更新。在为 10/100 卡选择驱动程序时，请记住使用`Intel` `e100`驱动程序而不是内核的`eprop100`。

我们在集群实验室中使用的配置文件如示例 6-7、示例 6-8 和示例 6-9 所示。

### 示例 6-7 /etc/conf.modules

```bash
alias scsi_hostadapter aic7xxx
alias scsi_hostadapter ips
alias parport_lowlevel parport_pc
alias eth0 pcnet32
alias eth1 e1000
alias eth2 e1000
```

### 示例 6-8 /etc/sysconfig/network-scripts/ifcfg-eth1

```bash
DEVICE=eth1
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.0.254
NETMASK=255.255.255.250
```

### 示例 6-9 /etc/sysconfig/network-scripts/ifcfg-eth2

```bash
DEVICE=eth2
BOOTPROTO=static
ONBOOT=yes
IPADDR=192.168.2.254
NETMASK=255.255.255.0
```

你的内核安装和配置现在应该已经完成。重启管理节点，确保系统无问题地启动。如果发生问题，在修复它之前请不要进行下一步。务必使用`ping`检查所有网络接口是否已启动。使用命令：

```bash
# shutdown -r now
```

最后，你必须将内核打包，以便将来安装到节点上。使用以下命令：

> **注意：** 在实验室中我们发现带有通配符的项必须放在第一个。

注意：以下是一个长行，不应拆断：

```bash
# cd /install/post/
# tar zzvf kernel.tgz /boot/*2.2.18smpx /boot/System.map /boot/initrd.img /lib/modules/2.2.18smpx /usr/src/linux-2.2.18smpx
```

# 6.4.2 bind

`bind`是`DNS`示例之一，它能从`/etc/hosts`自动生成名称服务器配置文件并被`xCAT`使用。从`http://ftp.org/pub/examples/bind/`下载书籍的示例，并将`bind`脚本提取到`/local/xcat/lib`。例如：

```bash
# tar xvzf dns.tar -C /local/xcat/lib
# chmod 755 /local/xcat/lib
```

# 6.4.3 pxlinux

`pxlinux`是来自`DNS`的示例之一，它能从`/etc/hosts`自动生成名称服务器配置文件并被`xCAT`使用。从`http://ftp.org/pub/examples/bind/`下载书籍的示例，并将`bind`脚本提取到`/local/xcat/lib`。例如：

```bash
# tar xvzf dns.tar -C /local/xcat/lib
# chmod 755 /local/xcat/lib
```

# 6.4.4 bind

`pxbind`是来自`DNS`的示例之一，它能从`/etc/hosts`自动生成名称服务器配置文件并被`xCAT`使用。从`http://ftp.org/pub/examples/bind/`下载书籍的示例，并将`bind`脚本提取到`/local/xcat/lib`。例如：

```bash
# tar xvzf dns.tar -C /local/xcat/lib
# chmod 755 /local/xcat/lib
```

# 6.4.5 pxlinux

`pxlinux`是来自`DNS`的示例之一，它能从`/etc/hosts`自动生成名称服务器配置文件并被`xCAT`使用。从`http://ftp.org/pub/examples/bind/`下载书籍的示例，并将`bind`脚本提取到`/local/xcat/lib`。例如：
