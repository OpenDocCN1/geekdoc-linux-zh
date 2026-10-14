
Petitboot (v1.7.5–p8f5fc8) 9006–12C

BOS0026

Petitboot:

Autoboot: ( ) Disabled

(*) Enabled

Boot Order: (0) Any CD/DVD device

(1) disk: `sda2` [uuid: `ebdb022b-96b2-4f4f-ae63-69300ded13f4`]

(2) net: `enP2pls0f0` [mac: `ac:1f:6b:09:c0:52`]

```
{ 添加设备
清除并启动任意
清除 }
```

超时: 30 秒

网络：(*) 在所有活动接口上启用 DHCP

() 在特定接口上启用 DHCP

() 静态 IP 配置

tab=下一个, shift+tab=上一个, x=退出, h=帮助

# Petitboot 系统配置

网络：(*) 在所有活动接口上启用 DHCP

() 在特定接口上启用 DHCP

() 静态 IP 配置

DNS 服务器：(例如 192.168.0.2)

HTTP 代理：

HTTPS 代理：（如果 DHCP 服务器未提供）

磁盘 读/写：

(*) 禁止向磁盘执行所有写入

() 允许引导程序脚本修改磁盘

启动控制台：(*) `/dev/hvc0` [IPMI / 串口]

() `/dev/tty1` [VGA]

当前接口：`/dev/hvc0`

```
[ 好 ] [ 帮助 ] [ 取消 ]
```

tab=下一个, shift+tab=上一个, x=退出, h=帮助

- 现在在 CD/DVD 条目下方选择“安装 Ubuntu Server”条目：

- [CD/DVD: `sr0` / 2020-03-28-02-42-00]

* 安装 Ubuntu Server

- * 并让 Petitboot 从（虚拟）CDROM 镜像启动：

向所有进程发送了 `SIGKILL`

[119.355371]`kexec`: 启动新内核

[194.483947394,5] OPAL: 切换到大端 OS

[197.54612502,5] OPAL: 切换到小端 OS

- * 最后，iquity 安装程序将在控制台中显示：

Willkommen! Bienvenue! Welcome! Welkom

使用 UP、DOWN 和 ENTER 键选择您的语言。

| English (英语) |

| Asturiasian (阿斯图里亚语) |

| Català (加罗尼亚语) |

| Hrvatski (克罗地亚语) |

| Nederlands (荷兰语) |

| Suomi (芬兰语) |

| Français (法语) |

| Deutsch (德语) |

| E |

| Magyar (匈牙语) |

| šLatvie (拉脱语语) |

| Norsk bokmål (挪威语) |

| Polski (波兰语) |

| Español (西班牙语) |

- 剩下的安装将按照常规方式进行 ...

# 在 IBM zVM (s390x) 上进行交互式实时安装

按照此处描述进行 live 安装——意味着无需指定 `parfile`——自 Ubuntu LTS 20.04.1 ('focal') 以及任何新版本 20.10 ('groovy') 起已受支持。

- 下面指南假设 z/VM 虚拟机能够访问公共 cdimage.ubuntu.com 服务器，或者托管有 Ubuntu 20.04 安装镜像的外部 FTP 或 HTTP 服务器，此处的 20.04 focal daily live 镜像位于：http://cdimage.ubuntu.com/ubuntu/20.04/release

- 找到一个下载安装镜像的地方：

```
user@workstation:-$ wget http://cdimage.ubuntu.com/ubuntu/releases/20.04.1/release/ubuntu-20.04.1-live-server-s390x.iso-2020-08-08 16:01:52-http://cdimage.ubuntu.com/ubuntu/releases/20.04.1/release/ubuntu-20.04.1-live-server-s390x.iso
Resolving cdimage.ubuntu.com (cdimage.ubuntu.com)... 2001:67c:1560:8001::1d, 2001:67c:1560:8001::28, =
Connecting to cdimage.ubuntu.com
(cdimage.ubuntu.com)[2001:67c:1560:8001::80]... connected.
HTTP/1.1 request response .. 200 OK
Length: 705628160 (673M) [application/x-iso9960-image]
Saving to: 'ubuntu-20.04.1-live-server-s390x.iso'\ubuntu-20.04.1-live 100%=================> 672.94M 37.1MB/s in 17s
2020-08-08 16:02:10 (38.8 MB/s) - 'ubuntu-20.04.1-live-server-s390x.iso' saved
[705628160/705628160]iso
```

```
user@workstation:~$
* 现在回环挂载 ISO，以提取 z/VM 虚拟机安装所需的四个文件

user@workstation~$ mkdir iso
user@workstation~$ sudo mount -o loop ubuntu-20.04.1-live-server-s390x.iso iso
user@workstation~$ ls -1 /iso/boot/*ubuntu.exec,parmfile,*kernel,initrd.*
./iso/boot/initrd.ubuntu
./iso/boot/kernel.ubuntu
./iso/boot/parmfile
./iso/boot/ubuntu.exec
user@workstation:~$
```

- 现在将这些文件传输到您的 z/VM 虚拟机（例如传输到 'A'），使用终端模拟器或 `ftp`。

* 然后登录到您想要安装的 z/VM 虚拟机，在此例中将是 '102.222.111.24'。

* 执行 `ubuntu` 以启动安装：

如果没有配置 `parfile`，安装系统现在提供交互式配置基础网络：可用 `qeth` 设备：0600:0601:0602 两种配置方法：

* static: 静态配置

* dhcp: 自动配置

* static dhcp (默认 '') `ip`:102.222.111.24 (默认 102.222.111.1):

* `url`: http://cdimage.ubuntu.com/ubuntu/releases/20.04.1/release/ubuntu-20.04.1-live-server-s390x.iso (默认)

* `url`: http://10.222.2/ubuntu-server-20.04.1-live-server-s390x.iso

`http_proxy` (可选):

- 引用相同处的 ISO 镜像用于提取安装程序文件和内核。但也可以位于不同的位置，例如引用公共 cdimage.ubuntu.com：http://cdimage.ubuntu.com/ubuntu/releases/20.04.1/ubuntu-20.04.1-live-server-s390x.

* live-server 启动现在完成：

正在配置网络

`QETH` 设备 0600:0601:0602 已配置

IP-Config: `enc600` 硬件地址 02:28:0a:00:00:39 `mtu` 1500

IP-Config: `enc600` 猜测广播地址 102.222.111.255

IP-Config: `enc600` 完成：

地址: 102.222.111.24 广播: 102.222.111.255 网掩码: 255.255.255.0

| `gateway`: 102.222.111.1 | `dns0`: 102.222.111.1 | `dns1`: 0.0.0.0 |

| `rootserver`: 0.0.0.0 | `rootpath`: | |

`filename` :

连接到 10.222.21 (10.222.21)

`focal-live-server` 5% *****! 35.9M 00:00:08 ETA

`focal-live-server` 19% ******** 129M 00:00:08 ETA

`focal-live-server` 33% ***************** 225M 00:00:05 ETA

`focal-live-server` 49% ***************** 330M 00:00:04 ETA
