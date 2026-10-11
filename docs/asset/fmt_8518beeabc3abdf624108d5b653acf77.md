
| 分离的 DHCP 和 TFTP 守护进程 | 对于复杂的设置，dnsmasq 的功能集可能太有限，或者您可能希望在已经在运行 DHCP 守护进程的主网络上启用 PXE 启动。在这两种情况下，您将需要配置单独的 DHCP 和 TFTP 守护进程。Debian 安装手册涵盖了用于 PXE 启动的 `isc-dhcp-server` 和 `tftpd-hpa` 的设置。 |
| :--- | :--- |
| https://www.debian.org/releases/stable/amd64/ch04s5.html |  |

为了设置 dnsmasq，您必须首先通过 `/etc/dnsmasq.conf` 对其进行配置。基础配置仅包含几行关键代码：

```
# 处理的网络接口
interface=eth0
# DHCP 选项
# 分配的 IP 范围
dhcp-range=192.168.101.100,192.168.101.200,128
# 向客户端宣告的网关
dhcp-option=router,192.168.101.1
# 向客户端宣告的 DNS 服务器
dhcp-option=dns-server,8.8.8.8,8.8.4.4
# 向客户端宣告的启动文件
dhcp-boot=pxelinux.0
# TFTP 选项
enable-tftp
# 托管服务的文件目录
tftp-root=/tftpboot/
```

配置好 `/etc/dnsmasq.conf` 后，您将需要将安装启动文件放置在 `/tftpboot/` 目录中。Kali Linux 提供了一个专门用于此目的的文件归包，可以直接解压到 `/tftpboot/` 中。只需为您的目标机器选择 32 位（i86）和 64 位（amd64）以及标准或通用（gtk）安装方法，并选择合适的归包：

- http://http.kali.org/dists/kali-rolling/main/installer-amd64/current/images/netboot/gtk/netboot.tar.gz
- http://http.kali.org/dists/kali-rolling/main/installer-amd64/current/images/netboot/txt/netboot.tar.gz
- http://http.kali.org/dists/kali-rolling/main/installer-amd64/current/images/netboot/iso/netboot.tar.gz

一旦选了归包，创建 `/tftpboot/`，下载归包并将其解压到该目录：

```
# mkdir /tftpboot
# cd /tftpboot
# wget http://http.kali.org/dists/kali-rolling/main/installer-amd64/current/images/netboot/gtk/netboot.tar.gz
# tar xf netboot.tar.gz
# ls -l
total 25896
drwxr-xr-x 3 root root 4096 May 6 10:00 .
drwxr-xr-x 2 root root 4096 May 6 10:00 ..
-rw-r--r-- 1 root root 47 May 6 10:00 dldinux.c32
-rw-r--r-- 1 root root 35 May 6 10:00 menu.cfg
-rw-r--r-- 1 root root 265072 May 6 10:00 pselux.cfg
-rw-r--r-- 1 root root 71 May 6 10:00 pselux.info
-rw-r--r-- 1 root root 33 May 6 10:00 pselux.0
-rw-r--r-- 1 root root 78824 May 6 10:00 vesamenu.c32
-rw-r--r-- 1 root root 25896 May 6 10:00 version
```

## 10.2. 利用配置管理

由于能够快速地在多台计算机上安装 Kali，你可能需要帮助来在安装后管理这些机器。你可以利用配置管理工具来管理或将替换计算机配置为任何所需的状态。

Kali Linux 包含了许多流行的配置管理工具（如 `ansible`, `chef`, `puppet`, `saltstack` 等），但在本节中，我们只介绍 SaltStack。

- => https://saltstack.com

## 10.1. 设置 SaltStack

SaltStack 是一种集中化的配置管理服务：一个 `salt master`（主节点）管理许多 `salt minions`（从节点）。你应该在所有你想要管理的主机均可访问的服务器上安装 `salt-master` 包，并在想要管理的主机上安装 `salt-minion`。每个 minion 必须被告知它去哪里寻找主节点。只需编辑 `/etc/salt/minion` 并 `master` 键设置为 Salt master 地址即可。注意 Salt 使用 YAML 进行配置。

```
minion# vim /etc/salt/minion
minion# grep master /etc/salt/minion
master# 192.168.122.105
```

每个 minion 都有一个存储在 `/etc/salt/minion_id` 中的唯一标识符，默认是其主机名。此 minion 标识符将用于配置规则，因此在 minion 开启与 master 的连接之前，正确设置它是非常重要的：

```
minion# echo kali-scratch >/etc/salt/minion_id
minion# systemctl enable salt-minion
minion# systemctl start salt-minion
```

当 `salt-minion` 服务运行时，它将尝试连接到 Salt master 以交换某些加密密钥。在 master 端，你必须接受 minion 用来识别身份的密钥并允许连接继续。后续连接将是：

```
master# systemctl enable salt-master
master# systemctl start salt-master
master# salt-key --list all
Accepted Keys:
Denied Keys:
accepted Keys:
kali-scratch
Rejected Keys:
master# salt-key --accept kali-scratch
The following keys are going to be:
```

Unaccepted Keys:

kali-scratch

Proceed? [n/Y] y

Key for minion kali-scratch accepted.

## 10.2.2. 在 Minions 上执行命令

一旦 minions 连接上，你就可以从 master 在它们上执行命令：

```
master# salt '*' test.ping
kali-scratch:
  True
kali-master:
  True
```

该命令要求所有 minions（`'*'` 是针对所有 minions 的通配符）执行测试执行模块中的 `ping` 函数。该函数在成功时返回 True 值，这是确保 master 与各种 minions 之间连接正常的简单方法。

你也可以通过在第一个参数中提供标识符来针对特定的 minion，通过使用不那么通用的通配符（如 `'*-scratch'` 或 `'kali-*'`）来针对 minions 的子集。以下是在 kali-minion 上执行任意 shell 命令的示例：

```
master# salt kali-scratch cmd.shell uptime -a
kali-scratch:
05:25:48 44 min, 2 users, load average: 0.00, 0.01, 0.05
Linux kali-scratch 4.5.0-kali1-amd64 #1 SMP Debian 4.5.3-2kali1 (2016-05-09) x86_64
GNU/Linux
```

有许多模块可用于各种情况。我们涵盖了所有模块，但完整列表可以在 https://docs.saltstack.com/en/latest/ref/modules/all/index.html 获取。你也可以通过 `salt minion doc` 命令获取给定 minion 上所有执行模块及其可用函数的描述。运行此命令会返回一个很长的函数列表，但你可以通过传递带有父模块前缀的函数或模块名称作为参数来过滤列表：

Salt Module Reference
