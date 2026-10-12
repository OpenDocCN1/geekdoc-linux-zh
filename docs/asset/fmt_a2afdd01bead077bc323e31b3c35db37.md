
# Linux 快速启动指南

## /etc/NETWORKING

(Slackware)

`HOSTNAME=hostname.domain.com`

Jialong He
jialong_he@bigfoot.com
http://www.bigfoot.com/

启动项和名称从这些文件中读取。可以手动更改。

# NFS 文件共享

# 用户管理

## 文件

- `/etc/group`
- `/etc/passwd`
- `/etc/shadow`
- `/etc/bashrc`
- `/etc/profile`

用户账户信息。

- `/etc/fstab`
- `/etc/exports`
- `/etc/auto.master`

启动期间挂载的文件系统。NFS 服务器导出列表。auto 主文件。

- `/etc/ssh_config`
- `/etc/login`
- `$HOME/.bashprofile`
- `$HOME/.bashrc`

bash 系统级和用户初始化文件。

### 命令

- `/etc/resolv.conf`

指定服务器 DNS、DNS 域

`search 192.168.1.200`

- `/etc/hosts`

主机名到 IP 地址的映射。

- `/etc/hostname`

查找顺序。

`order hosts, bind`

`multion on`

- `/etc/netswitch.conf`
- `/etc/networks`
- `/etc/protocols`
- `/etc/interfaces`

指定信息的新方式。

- `/etc/rpc`

TCP/IP 服务和端口映射。

RPC 服务映射到程序号。

### 命令

- `mount`
- `exports`
- `showmount -e hostname`

挂载文件系统或 `fstab` 中的所有条目。显示 `exports` 中的导出系统列表。显示已导出的系统。

# 打印机配置

- `netconfig`
- `ppsetup`

菜单驱动的以太网设置程序。设置 PPP 连接 (Slackware)。例如设置启动设置。

## 文件

- `/etc/printcup`
- `/etc/printcap.local`
- `/etc/lpd.conf`
- `/etc/lpds.conf`

打印机功能数据库。LPR 配置。LPR 行打印机池进程的权限控制。

- `/etc/hosts.lpd`
- `/etc/hosts.quiv`

访问控制 (BSD LPD)。受信任主机。打印机的环境变量。

### 命令

- `useradd`, `usermod`
- `usermod`
- `newusers`
- `groupadd`, `groupdel`
- `chage`, `fix`, `chsh`

创建新用户账户的脚本 (slackware) 或链接到用户理想 (Redhat)。删除、创建、修改新用户或更新默认新用户。更新并创建新用户（批量模式）。添加或修改组。

## PRN

- `ifconfig`
- `ppsetup`

```bash
$ifconfig $1 $IPADDR $BROADCAST $($BROADCAST netmask $NETWORK $ETHMASK) out
```

并行端口。

- `host`
- `domainname`
- `arping`
- `ipchains`
- `iptables`

查找主机名 IP（或类似的查找）。DNS 名称查找。先通过以太网地址通过 `arp` 查找。防火墙和 NAT (Redhat 的 `etc/sysconfig/network`) 防火墙和 NAT (Linux 的 `etc/sysconfig/iptables`)。

## 文件

- `sendmail.conf`
- `sendmail.mc`

"`sendmail.conf`" 是配置文件。"`sendmail.mc`" 是一个宏文件，可以通过以下方式通过 `mkmff > sendmail.conf` 生成 "`sendmail.conf`"。

- `aliases`

邮件列表，在任何更改后运行。在文件中包含头部列表。邮件访问控制，`FEATURE(access)`，应在 `sendmail.conf` 中设置。在 `/etc/mail` 访问 `cyberpro.com relay domain.com relay DISCARD`。

- `access`

生成哈希 `/etc/mail access / <etc/mail access all 通过条目组成所有主机和子域名`。

# 网络配置

- `/etc/rc.d/1` (Slackware)
- `/etc/sysconfig/network-scripts/ifcfg-eth0` (Redhat)
- `/hostname`

IP 地址、网络掩码。默认网关在这些文件中。可以手动编辑以修改网络参数。`hostname` 由 `hostname` 设置。

## 配置文件 /etc/sysconfig

- `keyboard`

`keyboard_map`, eg.

`KEYBOARD="/usr/lib/keysmaps.map"`

鼠标类型，例。

`MOUSEYPE=`

- `network`

网络设置，包含 `NETWORKING=`

### 命令

重建邮件别名数据库。

- `newaliases`

创建新的别名数据库，例如。

- `makemap`

构建访问数据库哈希值。

### 有用配置文件

- `httpd`

Apache Web 服务器配置。

- `smb`

Samba 服务器文件 (for print)。

- `lilo`

LILO 引导加载器配置。

- `syslog`

系统守护进程 (`syslog`) 配置。

- `ssh_config`

SSH 客户端和服务器配置。

- `ldconfig.conf`

默认路径 (`ldconfig`)。

- `tools.conf`

工具配置 (`access`)。

- `named.conf`

DNS 服务器名称 (Redhat)。

- `sysctl.conf`

通过 `sysctl` 设置内核参数。

- `ntp.conf`

时间服务器。

- `arada.conf`

Internet 服务器。

- `/etc/resolv.conf`

扩展索引配置。

- `postfix.conf`

`postfix` 服务器。

- `protpd.conf`

网络备份服务器。

- `mime.conf`

邮件服务器配置。

# 配置内核

- `makeconfig`

使用菜单配置内核，或 X Window 接口。

- `makedep`

构建并安装内核。

## 管理模块

`insmod`, `lmmod`, `modprobe`, `rmmod`, `depmod`

可加载模块。

## 杂文件

- `/etc/shells`

允许登录的 shell

- `/etc/ftpsusers`

用于 ftp 的用户名。

- `/etc/htost.allow`

TCP wrapper 配置。

- `/etc/host.deny`

包含系统配置。

- `/etc/sysconfig` (redhat)

软驱驱动。

- `/dev/loop`

系统运行级。

- `/etc/init.d`

转换文件到 linux 格式。

- `toml.conf` (Slackware)

`zux`, `unit`。

- `unit.conf` (Redhat)

权限和组文件。

- `pwck`
- `grpcnv`

转换 shadow 和组。

- `shadowconf`
- `quota`
- `quotacheck`

配额

- `quotas`
- `quotaf`

请求配额

- `lilo - D`

设置 LILO OS (默认在 `lilo.conf` 中)

- `crontab`

显示或编辑 cron 任务。

- `sys-unconfig`

未配置系统

- `chfkroot-list`

在运行级启动的服务。探测新硬件 (Redhat)。

- `rpm`

```bash
rpm -i package
rpm -U package
rpm -q package
rpm -U package
```

## 配置 Apache 2.0 带 SSL

- `mod_ssl`

当 apache 时，指定 `--enable-ssl` 配置。默认情况下，ssl 未启用。编译后，使用 "mod-ssl" 位于模块列表中，“mod-ssl" 应在头部中。

(2) 生成私钥

(3) 生成证书

(4) 生成自签名证书

```bash
openssl -x509 -days 365 -newkey server.key -out server.key -out server.crt
```

(5) "mod_ssl", 将包含在 `httpd.conf` 中。否则包含 `<IfModule SSL>`。

## Syslog

每行由一个选择器和一个动作组成。部分包含部分：优先级和设施，用括号 () 分隔。你可以使用等号 (=`) 定义优先级以指定此优先级或其他。如果两者有效，工具将通过感叹号 (!) 包括此优先级以外的任何更高优先级。

示例：

```
* *emerg /var/log/log 到文件
* #myhost.domain.com # 日到远程主机
```

- `facilities`
