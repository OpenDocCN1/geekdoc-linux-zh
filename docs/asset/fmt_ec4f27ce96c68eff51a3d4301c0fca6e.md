
## 6. 设置正确的日期和时间
如果你希望连接 NTP 服务器获取时间，请启用 NTP。你可以指定你的 NTP 服务器的主机名或 IP 地址。如果你不想在此处设置日期/时间，以后可以使用。

## 8. 创建用户账户
如果你想，可以在默认 `root` 用户之外创建一个用户账户。提供用户名和密码信息。密码长度不能小于六位。如果你使用 NIS 或 LDAP 服务器进行用户帐户管理，点击“使用网络登录”并为可用服务配置功能。

# 设置软件更新

它们通过将你的系统连接到 Red Hat Network（免费）来实现软件更新等。

- 你的 Red Hat 主机名或 Red Hat Satellite
- 系统在 网络中的名称
- Red Hat Network Satellite 地址（可选）

如果你没有 Red Hat 登录账号，可以在此处申请。

- 你想在现在注册你的系统吗？
  - [ ] 是，我想现在注册。
  - [ ] 不，我希望稍后注册。

![](img/3f35ec29a294974bc1a4fdae3ae46652_196_0.png)
图 9-44 首次启动 – 网络用户选项

![](img/3f35ec29a294974bc1a4fdae3ae46652_196_1.png)
图 9-45 首次启动 – NIS 用户创建

![](img/3f35ec29a294974bc1a4fdae3ae46652_196_2.png)
图 9-46 首次启动 – LDAP 用户创建

![](img/3f35ec29a294974bc1a4fdae3ae46652_197_0.png)

![](img/3f35ec29a294974bc1a4fdae3ae46652_197_1.png)

## 9. 配置声卡
如果检测到声卡，将会要求你配置它。如果你不想在此阶段配置，稍后可以使用声卡配置器系统 `system-config-soundcard` 进行配置。

## 10. 安装其他软件
如果你想安装任何其他软件，请插入软件 CD 并点击安装（`Install`）。

## 11. 完成首次启动
点击完成（`Finish`）以完成首次启动过程。将出现登录界面，你现在应该以 `root` 或你创建的用户身份登录。

# 安装日志文件

在安装过程中创建了多个日志文件。这些文件记录了配置和状态信息。安装完成后，你可以查看它们的内容以检查安装进度。表 9-5 列出并描述了这些文件。

| 文件 | 说明 |
| :--- | :--- |
| `/root/anaconda-ks.cfg` | 记录安装期间输入的配置。 |
| `/root/install.log` | 列出安装期间安装的包。 |
| `/root/install.log.syslog` | 存储安装期间生成的消息。 |
| `/tmp/anaconda.log` | 该文件在安装完成后会移动到 `/var/log` 目录。包含安装期间生成的信息、调试和其他消息。 |
| `/tmp/anaconda.syslog` | 该文件在安装完成后会移动到 `/var/log` 目录。包含首次执行 `dmesg` 命令时生成的消息。 |
| `/tmp/anaconda.xlog` | 该文件在安装完成后会移动到 `/var/log` 目录。包含安装期间关于 X 的信息。只有在你执行图形化安装时才会创建此日志文件。 |

表 9-5 安装日志文件

以下是其中一些文件的内容：

```
# cat /root/anaconda-ks.ksf
# 由 anaconda 自动生成的 Kickstart 文件。

install
cdrom
key --skip
lang en_US.UTF-8
```

![](img/3f35ec29a294974bc1a4fdae3ae46652_198_0.png)

```
keyboard us
xconfig --startconboot --bootstrap static --ip 192.168.0.201 --netmask 255.255.255.0 --gateway
192.168.0.1 --nameserver 192.168.0.1 --hostname rhel01
rootpw--encrypted $1$ONM5QUi$u6j2G96l.dEE2ztqAWWgg
firewall --enabled --port=22:tcp
authconfig --enableshow --enabled
selinux --enforcing
timezone --utc America/New_York
bootloader--location=mbr --drivecode=sda --append="rhgb quiet"

...
%packages
@editors
@system-tools
@text-internet
@legacy-network-server
```

```
# cat /root/install.log
```

```
# cat /root/install.log.syslog

<8Dec 02 08:42:57 groupadd[822]: new group: name=rpm, GID=37
<8Dec 02 08:42:57 useradd[826]: new user: name=rpm, UID=37, GID=37, home=/var/lib/rpm, shell=/sbin/nologin
<8Dec 02 08:42:59 useradd[836]: new group: name=dbus, GID=81
<8Dec 02 08:42:59 useradd[836]: new user: name=dbus, UID=81, GID=81, home=, shell=/sbin/nologin
<8Dec 02 08:43:29 groupadd[882]: new group: name=utmp, GID=22
<8Dec 02 08:43:29 groupadd[886]: new group: name=utempter, GID=35
<8Dec 02 08:43:53 useradd[974]: new group: name=avahi, GID=70
<8Dec 02 08:43:53 useradd[974]: new user: name=avahi, UID=70, GID=70, home=, shell=/sbin/nologin
<8Dec 02 08:44:08 useradd[1021]: new group: name=mail, GID=47
...
```

# 控制台屏幕

安装期间有五个控制台屏幕用于管理和监控安装过程。如果安装过程是图形化的，还有一个第六个屏幕用于程序交互。你可以通过组合键在屏幕之间切换。控制台显示的信息也会记录在日志文件中。

## 控制台 #1
`Alt-F1` 文本模式，图形模式。这是默认的文本模式控制台。

## 控制台 #2
`Alt-F2` 文本模式，图形模式。用于运行命令的 BASH shell 界面。
![](img/3f35ec29a294974bc1a4fdae3ae46652_200_0.png)
图 9-50 第二虚拟控制台

## 控制台 #3
`Alt-F3` 文本模式，图形模式。显示安装日志，也存储在 `/tmp/anaconda.log`。除了其他信息外，该文件中还记录了硬件信息。
![](img/3f35ec29a294974bc1a4fdae3ae46652_200_1.png)
图 9-51 第三虚拟控制台

## 控制台 #4
`Alt-F4` 文本模式，图形模式。显示内核消息，也存储在 `/tmp/install.syslog`。该文件中更详细地记录了硬件信息。

## 控制台 #5
`Alt-F5` 文本模式，图形模式。显示系统创建信息。

```
mkfs 29 May 2006
Filesystem label: 
size: 2 GB
Block size: 1024 (KiB)
Number of blocks: 2097152
6144 blocks, 16384 blocks reserved for super user
First block: 0
Maximum Filesystem blocks: 671088
8192 blocks per group, 0
backups stored on blocks: 8193, 24577, 40961, 57345, 73729
Creating journal...
Creating journal (4096 blocks) done.
Writing superblocks and Filesystem accounting information, done.
This filesystem will be automatically checked every 20 分钟或自上次检查以来 10 天 - to override.
Setting journal count: 1
Setting interval between checks to 0 seconds
```

图 9-52 第四虚拟控制台

## 控制台 #6
`Alt-F6` 图形模式。此控制台在图形安装期间可用。

# 总结
