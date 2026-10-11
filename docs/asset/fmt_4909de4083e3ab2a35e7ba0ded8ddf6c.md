
```
下载期间你会看到一个进度条，下载完成后将返回 shell。
```
- 2. 使用大小适中的 USB 闪盘（5GB 或更大），按照附录 A 中的说明创建一个包含 openSUSE 安装程序的可启动 USB 闪盘。
- 3. 将新创建的可启动 USB 闪盘插入到要安装 openSUSE 的目标系统的相应端口。

4. 一旦启动，你将看到显而易见的 openSUSE 主题，类似于接下来的插所示。从列表中选择 Installation（安装）选项并按 ENTER 键。

![](img/3abd8558488b5c70f9f85ba63df43bc0_713_0.png)

5. 你将看到一个许可协议屏幕。点击 Next（下一步）以同意许可条款并继续安装。

6. 在安装程序的安装模式屏幕上，你将面临执行 New Installation（新安装）或 Updating Existing System（更新现有系统）的选择。选择 New Installation 。为了进一步加速并强制安装程序为目标系统选择某些标准默认值，请勾选 Use Automatic Configuration（使用自动配置）复框并点击 Next。

7. 在安装程序的 Clock and Time zone（时钟时区）处，为你的系统选择合适的 Region（地区）和 Time Zone（时区），并点击 Next。

8. 在桌面选择界面，选择你偏好的桌面环境。第二章讨论了各种桌面环境（GNOME、KDE 等）的细微差别。你也可以选择 Other（其他）选项（其中你可以选择 Minimal Server Selection [Text Mode] ），以避免安装任何图形化桌面环境。这对于服务器类型的系统可能特别有用。

# Linux 管理：入门指南

9. 安装过程的下一步是 Disk partitioning（磁盘分区）阶段。你将看到建议的分区方案/布局。选择 Use Btrfs as default Filesystem（使用 Btrfs 作为默认文件系统）选项并选择 Propose Separate Home Partition（建议单独划分 Home 分区）。最后的屏幕将类似于此处：

![](img/3abd8558488b5c70f9f85ba63df43bc0_714_0.png)

10. 在 Create New User（创建新用户）屏幕上，用以下信息填写字段：

| Field（字段） | Value（值） |
| :--- | :--- |
| User’s Full Name（用户全名） | Master Admin |
| Username（用户名） | master |
| Password/Confirm Password（密码/确认密码） | 72erty7&8 |

选择 Use this for system administrator（将此作为系统管理员）选项。
取消勾选 Automatic Login（自动登录）选项。
完成后点击 Next。

11. 你将看到安装 summary/settings（摘要/设置）屏幕。此屏幕详细列出了你为要安装的系统手动选择的所有选项。它还了根据第 6 步中的选择（Use Automatic Configuration）而自动为你选择的设置。查看摘要。如果你想更改任何设置，只需点击该设置的标题（例如 Partitioning 分区、Booting 引导、Software 软件、Time Zone 时区等）并在其中修改。一旦对选择满意，点击弹出 Install 对话，点击 Install 确认并继续。

12. 安装完成后，你将看到标准的登录屏幕。如果你在第 8 步中安装了桌面环境，你将看到图形化登录屏幕。但如果你选择的是 Minimal Server Selection (Text Mode)，你将看到经典的 Linux/GNU 操作系统登录提示符。

使用第 10 步中创建的用户名和密码登录系统。别忘了玩得开心！

# 索引

A
A address records（A 记录）, 409–410
acl keyword（关键词）, 402
Active Directory (AD，活动目录）, 15
Address Resolution Protocol。查看 ARP
Advanced Maryland Automatic Network Disk Disk Archiver。查看 AMANDA
all, 575
AMANDA, 669
anycast addresses（任播播地址）, 303
Apache
Alias（别名）, 460
configuration（配置）, 454–461
creating a simple root-level page（创建一个简单的根级页面）, 454
DocumentRoot（文档根目录）, 456
ErrorLog（错误日志）, 458
Group（组）, 370
Include（包含/包含）, 458
installing from source（从源码安装）, 450
installing the Apache HTTP Server（安装 Apache HTTP 服务器）, 449
Listen（监听）, 455
LoadModule（加载模块）, 456
LogLevel（日志级别）, 460
MaxClients（最大客户端数）, 456
modules（模块）, 451, 457
overview（概述）, 446
process ownership（进程所有权）, 448
ScriptAlias（脚本别名）, 460
ServerAdmin（服务器管理员）, 456
ServerName（服务器名称）, 455–456
ServerRoot（服务器根目录）, 455
startup and shutdown（启动与关闭）, 452–453
testing the installation（测试安装）, 453–454
troubleshooting（故障排除）, 461–462
User（用户）, 457–458
UserDir（用户目录）, 458
VirtualHost（虚拟主机）, 460–461
另见 HTTP
AppArmor, 370
Application layer（应用层）, 271–272
APT, 62–63
common apt-get options（常用 apt-get 选项）, 65
installing DHCP（安装 DHCP）, 629–630
installing OpenSSH（安装 OpenSSH）, 498
APT（续）
installing Postfix（安装 Postfix）, 468
installing Samba（安装 Samba）, 537
ARP
headers（头部）, 286–287
view（查看）, 285–286
authconfig-ui, 581
authentication（认证，使用 OpenLDAP 进行用户身份验证）, 607–610
automated monitoring（自动监控）, 372
pipes（管道）, 110
redirection（重定向）, 111
binary（二进制）, 92
BIND
downloading, compiling and installing ISC BIND from source（从源码下载、编译和安装 ISC BIND）, 400–401
setting up BIND database files（设置 BIND 数据库文件）, 412–418
understanding the configuration file（理解配置文件）, 401–402

# B
background（背景）, 107
backticks（反引号）, 113
backup（备份）
AMANDA, 669
amount of data（数据量）, 665–657
BackupPC, 669
Bacula, 669
command-line tools（命令行工具）, 663–669
data deduplication（数据去重）, 659–660
Dirvish, 669
dump（转储）, 663–666
evaluating backup（评估备份）, 665
hardware and medium（硬件与介质）, 657–658
Mondo Rescue, 669
network throughput（网络吞吐量）, 658
restore（恢复）, 667–668
sync（同步）, 668–669
speed and ease of data recovery（恢复速度与便利性）, 658–659
tape management（磁带管理）, 660–662
tar, 668
blocks（块）, 117
blocks, 173–174
boot（启动）, 28
另见 GRUB 2; GRUB Legacy; LILO
boot managers（启动管理器）, 367
booting into single-user mode（进入单用户模式）, 169–170
bootstrapping（引导）, 158
Bourne Again Shell（Bash）
另见 Bash
bricks（砖块）, 560
B-tree file system。另见 Btrfs
bzip2, 125

# C
caching servers（缓存服务器）, 399
canonical name（规范名称）, 411
cat, 128–129
CentOS, setting up NICs（设置网卡）, 313–316
cgroups。另见 control groups (cgroups)
chains（链）, 335–336, 343–344
character devices（字符设备）, 117
chmod, 119–122, 361
choke points（瓶颈）, 332
chow, 119
chgrp（更改组）, 119
chroot（切换根）, 366–369
CIDR, 291
class interdomain routing (CIDR，域间路由）, 291
CNAME, 411
command-line user management（命令行用户管理）, 85
groupadd（添加组）, 89, 101
groupdel（删除组）, 89, 103
BackupPC, 669
Bacula, 669
bandwidth（带宽，使用 MRTG 监控）, 384
bare-metal virtualization,（裸金属虚拟化）, 643
bash, 52–54
backticks（反引号）, 113
environment variables（环境变量）, 108–110
filename expansion（文件名扩展）, 111–112
introduction to（简介）, 106–107
job control（作业控制）, 107
multiple commands（多个命令）, 112–113
useradd（添加用户）, 86, 87, 100–101
usermod（修改用户）, 90, 102
userdel（删除用户）, 88, 102
compatible addresses（兼容地址）, 304
compressing files（压缩文件）, 125
connection tracking（连接跟踪）, 334
control groups (cgroups，控制组）, 208, 259–261
copying files（复制文件）, 122–123
cp, 122–123
cron, 224–225
crontab file（crontab 文件）, 225–226
cross-mounting disks（跨挂载磁盘）, 525
CUIS, 612, 613
accepting, and rejecting jobs（接受和拒绝作业）, 622–623
adding, printers（添加打印机）, 616–621
configuring（配置）, 615–616
enabling, and deleting, printers（启用和删除打印机）, 622
printing（打印）
setting the default printer（设置默认打印机）, 621–462
implementations（实现）, 559–565
metadata（元数据）, 560
overview（概述）, 556–558
POSIX compliance（POSIX 合规性）, 561
replication（复制）, 560
client daemon（客户端守护进程）, 637–639
configuring the DHCP client（配置 DHCP 客户端）, 338–339
configuring the DHCP server（配置 DHCP 服务器）, 330–336
declarations（声明）, 331–332
downloading, compiling and stalling ISC DHCP from source（从源码下载、编译和启动 ISC DHCP）, 330
installing DHCP via RPM（通过 RPM 安装 DHCP）, 629
installing via APT in Ubuntu（在 Ubuntu 中通过 APT 安装）, 629–630
leases（租）, 628
options（选项）, 335–336
overview（概述）, 328
parameters（参数）, 333–335
sample dhcpconf file（示例 dhcpconf 文件）, 336–337
dig, 419–421
directories（目录）, 116
creating（创建）, 126
removing（删除）, 126
showing directory location of a file（显示文件位置）, 130
showing present work directory（显示当前工作目录）, 126
directory（目录）, 81–83
Dirvish, 669
Discretionary Access Control (DAC，自主式访问控制）, 369
disk free（磁盘可用空间）, 131
disk utilization（磁盘利用率）, 129–130
disks（磁盘）
D:
daemons, Samba, 536
data deduplication（数据去重）, 659–660
Data Encryption Standard (DES，数据加密标准）, 80
Data Link layer（数据链路层）, 270
Debian Package Management System。另见 DPSMS
debuging hardware conflicts（调优硬件冲突）, 257
defragmentation（碎片整理）, 176
Destination NAT (DNAT，目标网络地址转换）, 332
destination ports（目标端口）, 376
df, 131, 371–372
DFS
adding a new disk（添加新磁盘）, 185–187
cross-mounting disks（跨挂载磁盘）, 525
naming conventions（命名规范）, 186–187
Distributed File Systems。另见 DFS
distributed volumes（分布式卷）, 563
DMZ, 4
NAT, See Destination NAT
bricks, 560
fault tolerance（容错性）, 560
distributions（发行版）, 4
DPMS, 48

# DNS
A address records（A 记录）, 409–410
CNAME records（CNAME 记录）, 411
configuring the DHCP server（配置 DHCP 服务器）, 330–336
configuring DHCP clients（配置 DHCP 客户端）, 338–339
declarations（声明）, 331–332
Domain Name Service。另见 DNS
domains, 15, 570
setting the domain name（设置域名）, 584
downstream components（下游组件）, 8
DPMS, 48
APT, 62–63
dpkg, 62
DPMS triangle, 63
overview（概述）, 62
du, 129–130
dump, 663–666
Dynamic Host Configuration Protocol。另见 DHCP
dynamic routing（ with RIP，动态路由）, 292–297

# E
echo, 215–217
editors（编辑器）
emacs, 142
joe, 142
pico, 143
vi, 141–142
edubuntu, network device configuration（网络设备配置）, 316–318
emacs, 142
encryption（加密）
how it works, 80
passwords, 535
environment variables（环境变量）, 108–110
as parameters, 112
printing（打印）
setting, 109–110
unsetting, 110
/etc/exports, 518–522
/etc/stab, 180–183
/etc/group, 84–85
/etc/hosts, 392–393
/etc/initab, 204–206
/etc/nsswitch, editing, 580
/etc/nsswitch.conf, 425–426
/etc/pam.d/other, 98
/etc/passwd, 79, 587

/etc/resolv.conf, 424–425
/etc/rsyslog.conf, 220–221
样本文件, 224
/etc/shadow, 83–84
/etc/xinetd.conf, 211–212
变量及其含义, 212–214
/etc/yp.conf, 编辑, 578–579
Ethereal. 参见 Wireshark
以太网, 233–274
报文件, 274
事件, 203
ext2, 174–175
ext3, 174–175
ext4, 175–176
extxtents, 175–188

文件系统检查 (fsck), 168–169
文件系统
  - 创建, 197–199
  - 管理, 177
  - 挂载和卸载本地磁盘, 177–183
  - 卸载, 180
  - 应该使用哪一个, 176–177
参见 Btrfs; ext2; ext3; ext4; fsck
文件传输协议 (FTP). 参见 FTP
文件名扩展, 111–112
文件名，设计, 574–575
文件
  - 压缩, 125
  - 合并, 128–129
  - 复制, 122–123
  - 分页屏显示, 129
  - 查找, 124
  - 链接, 124
  - 移动, 123–124
  - 显示文件的目录位置, 130

# F

容错性, 560
Fedora
  - 配置引导加载程序, 37
  - 配置网络, 25–27
  - 创建用户, 40
  - 日期时间和配置, 40
  - 下载 ISO 和 DVD 镜像, 22
  - GUI 包管理, 61, 62
  - GUI 用户管理器, 90
  - 硬件配置, 40
  - 初始系统配置, 40–41
  - 初始化磁盘, 24–25
  - 安装, 23–39
  - 登录, 41
  - 概览, 21
  - 选择包组, 37–39
  - 设置根密码, 27
  - 设置网卡 (NIC), 313–316
  - 存储配置, 28–37
  - 时间配置, 27
FHS. 参见文件层次结构标准 (FHS)
文件层次结构标准 (FHS), 9
文件权限, 121–122
find, 124–125
  - 查找文件, 124–125
  - finger, 215
防火墙
  - 配置简单的防火墙, 352–355
  - 参见 Netfilter
进程炸弹 (fork bomb), 364
FORWARD, 337
正向解析, 397
第四扩展文件系统. 参见 ext4
帧, 267
  - 空闲空间，显示, 131
FreeIPA, 610
fsck, 168–169, 183–185
FTP, 230
  - 主动 FTP, 431
  - 客户端/服务器交互, 430–431
  - 被动 FTP, 431
安全文件传输协议 (sftp), 507–508
  - 使用虚拟用户设置服务器, 440–443

# Linux 系统管理：初学者指南

FTP (续)
  - 设置仅限匿的服务器, 439–440
  - 启动并测试服务器, 436–438
  参见 vsftpd
完全限定域名 (FQDN), 393

GRUB, 37
GRUB 2, 156
  - 特性, 157
GRUB Legacy, 146, 147
  - 引导时添加新内核, 154–156
  - 备份 MBR, 149
  - 进入单用户模式, 169–170
  - 配置, 152–153
  - 使用的惯例, 148
inetd, 153

# G

比尔·盖茨, 11
gcc, 安装, 56–57
GECOS, 81
通用电气综合操作系统. 参见 GECOS
Ghostscript, 612
GlusterFS, 559, 561–565
GNOME, 12–13
GNU, 7
  - 从 GRUB Shell 安装, 149–150
  - 使用 USB GRUB Legacy 盘在 MBR 上安装, 151–152
  - 阶段 1, 147
  - 阶段 2, 147–148
  - USB GRUB Legacy 启动盘, 150–151
客体操作系统 (VM), 643
GUI, 与内核分离, 12–13
  - UI 用户管理器, 90–91
gzip, 125
  - 清理, 72–73
  - 编译包, 70–71
  - 配置包, 69–70
  - 获取并解压包, 66–69
  - 安装包, 71–72
  - 查找文档, 69
  - 测试软件, 72
GPL, 7, 9–10
组 ID 字段, 81
组 ID (GID), 78
  groupadd, 89
  - 创建组, 101
  groupdel, 89, 103
  groupmod, 90
  - 修改组属性, 102–103
组, 78
  - 更改, 119
  - 使用 groupadd 创建, 101
  - 使用 groupdel 删除, 103
  - 将组密码与真实组合并, 574
  - 使用 groupmod 修改属性, 102–103
硬链接, 116
硬挂载，软挂载, 525
硬件, 18
硬件仿真, 643
ARP, 286–287
以太网, 274
HTTP, 446–447
TCP/IP, 267, 273–282
UDP/IP, 281–282
home, 28
家目录, 81–83
移动用户及其家目录, 132–134

# 索引

host, 418–419
主机操作系统, 643
主机名配置, 326–327
HTTP, 20, 446
报头, 446–447
端口, 447
进程所有权与安全, 448
目录, 459
安装方法, 20–21
安装软件
  - 使用 RPM, 54–57
  - 使用 Ubuntu, 64
互联网控制消息协议 (ICMP). 参见 ICMP
互联网系统联盟 (ISC), 399
互联网数据包交换, 525–326
ip, 310–312
Hyper-V, 644
虚拟机管理器 (VMM), 643
icmp, 348
ifconfig, 310–312
IMAP, 478–480
检查 IMAP 功能, 485–486
命令, 480
断开模式, 479
安装 IMAP 服务器, 480–486
从源码, 481–482
离线模式, 479
在线模式, 479
运行 IMAP, 483–484
in-addr.arpa 域, 397
include 关键字, 402
include 语句, 403
inetd, 210–211
info, 114
init, 158–192
/etc/iptables, 204–206
systemd, 206–210
telnet, 206
upstart, 202
初始序列号 (ISN), 图表, 301–302
i-nodes, 172–173
INPUT, 337
  - IP 报头, 275–277
  - 和 tcpdump, 277
IP 地址，Linux 如何选择, 326
ip route, 322–323
IPng, IPv6
iptables, 343–351
IPv6, 302
  - 地址格式, 302–303
  - 地址类型, 303
  - 向后兼容, 303
IPX, 314

# J

  - 任务, 107, 203
joe, 142
日志记录, 175

# K
  - KDE, 12–13
内核执行, 158
内核加载, 158
基于内核的虚拟机. 参见 KVM
内核, 4
避免意外升级, 235
启动, 244
构建内核, 234–235
编译, 240–241
配置, 236–239
定义, 230–231
差异, 6
查找源码, 231–232
获取正确的内核版本, 232–233
安装, 241–244
内核模块, 240
内核发布候选, 247
微内核, 12
单体内核, 12
补丁, 245–248
准备配置, 235–236
稳定点发布, 233
解压内核源码, 233–234
ubuntu 设备配置, 316–318
KVM, 644, 645
管理 KVM 虚拟机, 649–650
在 Ubuntu/Debian 中设置, 650–653
概览, 592
架构, 595
租赁, 628
libc, 260
带有 libc, 73
限制, 348–349
链接文件, 124
Linux 与 Windows, 10–15
系统, 4–5
列出文件, 118
列出进程, 135–136
显示交互进程列表, 137–138
本地安全
AppArmor, 370
chroot, 366–372
df, 371–372
资源限制, 363–366
邮件文件, 372
监控你的系统, 370–372
非人类账户, 363
选择正确的范围, 362
ps, 371
SELinux, 369–370
定位命令, 130
日志解析, 383
存储日志条目, 383–384

# L
层 8, 272
LDAP, 595
客户端/服务器模型, 594
目录, 593
目录信息树 (D), 593
条目, 595
nss_ldap, 598–599
objectClass, 595
对象, 595
逻辑卷管理 (LVM), 187
逻辑卷 (LV), 188, 189
  - 创建, 188–190, 197
环回地址, 288
LPD, 612, 617
lpr, 624–626
LPRng, 612
LSB. 参见 Linux Base规范 (LSB)
Lustre, 559
lynx, 54–56
mknod, 661–662
模式，更改, 119–122
模块, 308–309
Apache, 451, 457
Mondo 救援, 669
单体内核, 12
MooseFS, 559
挂载命令, 178, 523, 525
选项, 179
NFS 选项, 523–524
挂载, 13
远程共享, 549
挂载/卸载本地磁盘, 177–183
移动文件, 123–124
使用 MRTG 监控带宽, 384
62–663
多播地址, 303
多个命令, 112–113
mv, 123–124
MX (邮件交换记录), 411

# M
邮件服务器
可用性, 488
日志文件, 488–489
SSL 安全, 486–487
通过 SSL 测试 IMAP 和 POP3 连接, 487
邮件列表, 372
makefile, 70
man, 1115
强制性访问控制 (MAC), 369
映射地址, 304
伪装地址, 331, 332
mobx, 478
元数据, 560
微内核, 12
Microsoft DFS (MS-DFS), 559
migrationtools,rpm, 608
MindTerm, 497
MINGID, 573
MINUID, 573
mkdir, 126

# 696 Linux 系统管理：学者指南

网络地址翻译 (NAT), 331–332
链 (chains), 335–336, 343–344
连接跟踪与, 334
目标网络地址翻译 (DNAT), 332
示例, 332–333
FORWARD, 337
INPUT, 337
伪装 (Masquerading), 331, 332
NAT 友好型协议, 334–335
OUTPUT, 337
ROUTING, 337
PREROUTING, 336
源网络地址翻译 (SNAT), 331, 332
网络信息服务 (Network Information Service)。见 NIS 接口 interfaces, 308–309
网络层, 270–271
网络邻域 (Network Neighborhood), 13–14
网络安全
- 绑定到接口, 379–380
- 处理攻击, 384–385
- 使用 MRTG 监控带宽, 384
- 监控你的系统, 383–384
- netstat, 377–379
- 关闭服务, 380–382
- 关闭 xinetd 和 in 服务, 381
- SSH 隧道技巧, 380
- 以及 TCP/IP, 376–377
- 工具, 385–387
- 跟踪服务, 377–379
网络用户, 11
网络, 287–288
- 一致性的网络设备命名, 309–310
- 使用 RIP 的动态路由, 292–297
- 子网掩码 (netmasks), 289–292
- 路由表, 292
- 静态路由, 291–292
- 分划分, 289
NFS, 20
- 常见用途, 530
- 组件, 517–518
- 配置 NFS 服务器, 518–522
- 配置 NFS 客户端, 522–526
- 跨挂载磁盘, 525
- 在 Fedora 中启用, 515–516
- 在 Ubuntu 中启用, 516–517
- /etc/exports, 518–522
- tr , 518
- 内核支持, 518
- 运行机制, 512
- mount 命令, 523–525
- 挂载并访问分区, 514
- 性能调优, 526
- 拒绝访问, 527
- 权限, 519
- 示例配置, 527–529
- 软挂载与硬挂载, 525
- 过期文件句柄 (stale file handles), 526
- 排除服务器-NFS 故障
- 版本, 513–514
- FSv2, 513
- FSv3, 513
- FSv4, 513
NICs, 启动时设置, 313–316
NIS
- 配置备 NIS 服务器, 584–585
- 配置 NIS 客户端, 578–580
- 配置 NIS 主服务器, 570–578
- 域 (domains), 570
- 编辑 .hosts 文件, 572–575
- 建立域名, 571
- GUI 工具, 581–582
- 主服务器, 569–570
- 在大于 588–589 的网络中
- 概述, 568–569
- 示例用法, 582–583
- 在分段网络中, 568–570
- 设置域名, 584
- 设置 NIS 主服务器向从服务器推送, 585
- 从服务器 (slave servers), 569, 573
- 在小型网络中, 587–588
- 启动, 572
- 测试客户端配置, 583
- 工具, 586
- 更新 NIS 映射, 578
- 在配置文件中使用, 586–587
ypbind, 569, 579–580
ypinit, 575–577, 585
ypserv, 569
ypxfrd, 569
nmap, 386
nmbd, 536
非商业发行版, 5
非人类用户账户, 363
普通文件, 116
普通用户, 778
NS 记录, 409
snookup, 421
ss_ldap, 598–599
supdate, 422
空密码, 550
- OpenSSH 客户端使用的文件, 508
- 在 Ubuntu 中通过 APT 安装, 498
- 在 Fedora 中通过 RPM 安装, 498
- 适用于 Mac OS X, 497
- 安全复制 (scp), 507
- 安全文件传输协议 (sftp), 507–508
- Shell 技巧, 506
- ssh 客户端程序, 503–506
opensUSE
- GUI 包管理, 61
- GUI 用户管理器, 91
- 关键字, 403
OSI 模型, 269–272
OUTPUT, 337
所有权, 119
PAM, 15, 93
- 字节 (octets), 288
在线碎片整理 (online defagment), 176
开放最短路径优先 (OSPF), 293, 297
- 优点, 9–10
- 缺点, 10
OpenAFS, 559
BSD, 496
OpenLDAP, 15
- 配置, 598–603
- 配置客户端, 504–606
- 创建后端, 204–606
- 数据库端 (ends), 501
- 安装, 597–598
- 概述, 595
- 查询和修改目录, 606–607
slapd, 599–603
用于用户认证, 607–610
OpenSSH, 496
- 创建安全隧道, 503–506
- 从源码下载, 498–500
- 配置参数, 97
- 控制标志, 96
- 调试, 99
- /etc/pam.d/other, 98
- 示例文件和位置, 94–95
- 登录问题, 99
- 模块类型, 95
- 用户名和密码, 535
pam_ldap, 598–599
半虚拟化 (paravirtualization), 643
- 分区, 188–193
- 命名规范, 186–187
- 概述, 186
- 密码字段, 80–81
- 密码, 534–535
- 使用 passwordd 修改, 550–551
- 加密, 535
- 与 shadow 密码组合并, 574
- 与 real 密码合并, 574
- 空, 550
- 补丁, 245–248
PDL, 612
Perl, 535
文件权限, 121–122
NFS, 519
物理层, 270
物理卷 (PV), 187, 189
pico, 140
管道 (pipes), 110
可插认证模块 (Pluggable Authentication Modules)。见 PAM
POP, 478
- 检查 POP3 功能, 484–488
- 安装 POP3 服务器, 480–488
端口号, 376–377
portmap, 512
POSIX 兼容性, 561
Postfix, 467
- 检查邮件队列, 474
- 配置服务器, 471–474
- 刷新邮件队列, 474
inet_protocols, 473
- 从源码安装, 469–470
- 在 Ubuntu 中通过 APT 安装, 468
- 在 Fedora 中通过 RPM 安装, 467–468
邮件日志, 475
mail_spool_directory, 472
main_cf 文件, 471–473
目标, 472
hostname, 471
mynetworks, 472
myorigin, 471–472
新别名 (newaliases), 475
运行服务器, 474
smtpd_banner, 473
POSTROUTING, 337
PostScript, 612
PREROUTING, 336
打印机队列, 620
打印
- 接受和拒绝打印任务, 622–623
- 添加打印机, 616–625
- 客户端打印工具, 624–626
- CUPS, 612–616
- 启用、禁用和删除打印机, 622
- 过滤器, 613
- 任务, 625
lpr, 624–626
网络打印机, 618
打印机, 512
- 设置默认打印机, 621–622
溢打印器 (spoolers), 612
- 使用命令行工具添加打印机, 620–621
私有 IP 段, 288
/proc 目录, 250–251
- 常用设置和报告, 254–255
- 调试硬件冲突, 257
- 枚举条目, 254
- 高流量服务器上的问题, 256–257
SYN 洪水防护, 255–256
微调 fuses 索引, 251
- 有用条目, 252–254
进程所有权, 448
进程
- 列出, 135–136
- 向进程发送信号, 138–139
- 显示交互式列表, 137–138
/proc/interrupts, 257
/proc/io, 257
ps, 135–136, 371
伪终端 (pseudo-tty), 107
PTR 记录, 410
公钥加密, 492–494
加密参考, 495
密钥特性, 494–495
公钥加密, 492–494
服务器设置和关闭, 501
SSHD 配置文件, 502
版本, 495–498

# 索引 701

- 源代码, 48, 49
- 损坏, 74
- 编译并安装 Samba, 537–539
- 从源码下载、编译并安装 ISC BIND, 400–401
- 从源码下载、编译并安装 DHCP, 630
- 从源码下载、编译并安装 OpenSSH, 498–500
- 469–470
- 从源码构建 Postfix，构建时的问题，73–74
- 源, NAT, 331, 332
- 旋转 (spins), 4
- 溢打印器 (spoolers), 612
- SSH. 见安全外壳 (SSH)
- SSL. 见安全套接层 (SSL)
- 斯托曼，Richard Matthew, 5
- 标准, 8–9
- 启动脚本, 22
- 状态, 349
- 状态的连接, 334
- 静态路由, 291–292
- su, 140–141
- 子域, 396–397
- 子网掩划分, 289
- sudo 命令, 64
- 超块 (superblocks), 174
- 超级用户, 78
- SUSE Linux 企业版. 见 SLE
- 交换文件, 28
- SWAT
- 菜单, 543–544
- 访谈, 540–541
- 设置, 541–542
- 另见 Samba
- 符号链接, 117
- SYN 标志 (SYN flags), 255
- SYN 洪水攻击保护, 255–388
- 同步 (sync), 131
- 同步磁盘, 131
- syncookies, 256
- sysctl, 327
- SysFS, 257–259
- syslog, 383–384
- syslogd, 217
- 系统文件. 见 SysFS
- 系统名称, 139–140
- system-config-authentication, 581–582
- system-config-services 实用, 165, 166
- systemd, 206–207
- 益处, 207–208
- 控制组 (cgroups), 208
- 作用, 207
- 套接字激活, 208
-  (units), 209–210
- 标签 (tags), 53
- 磁带存档 (tape archive), 126–128
- 磁带管理, 660–662
- tar, 126–128, 666
- tar 包 (tarball), 67
- tcp, 349–350
- TCP
- 校验和 (checksum), 279
- 关闭连接, 284–285
- 标志 (flags), 278–279
- 报头 (headers), 277–281
- 打开连接, 282–283
- 纯确认 (pure acknowledgment), 284
- 滑动窗口, 280
- 传输数据, 283–284
- 紧急指针 (urgent pointer), 281
- tcpdump, 297, 302–387
- 与 IP, 277
- TCP/IP: 266
- 报头, 267, 273–282
- 与网络安全, 376–377
- 数据包, 266–269
- 栈 (stacks), 266
- TCP/IP 模型, 269
- tcpmss, 350
- telimit, 206
- 文本文件 vs. 注册表 (Registry), 14–15

# Linux 员：入门指南

- textinfo, 115–116
- 精简服务器, 362
- 第种扩展文件系统. 见 ext3
- 三路握手, 282
- /tmp, 278
- top, 137–138
- Torvalds, Linux, 10
- 传输层, 271
- 故障排除
- Apache, 461–462
- 客户端 NFS 问题, 526–527
- 内核, 244–245
- Samba, 554
- 服务端 NFS 问题, 522
- 可信存储池, 562–563
- 隧道技术 (tunneling), 304
- SSH 隧道小技巧, 380
- TXT 记录, 412
- 输入命令, 51
- UNIX 纪, 84
- 卸载文件系统, 180
- 不必要的进程, 361–362
- upstart, 202–204
- 另见 init
- 上游组件, 82
- 运行时间 (uptime), 20, 231
- 用户 ID 字段, 81
- 用户 ID (UID), 78
- MINUID, 573
- 用户管理工具
- 命令行用户管理, 85–90
- GUI 用户管理器, 90–91
- useradd, 86–87
- 创建用户, 100–101
- userdel, 88, 103
- 用户态 (user-land), 62
- usermod, 88
- 修改用户属性, 102
- 用户名字段, 79–80
- 用户名, 534–535

# U

- Ubuntu 服务器
- 启动管理器 (Boot-Up Manager), 167
- 常用 apt-get, 65
- GUI 包管理器, 65–66
- GUI 用户管理器, 91
- 安装, 41–45
- 安装 DHCP, 629–630
- 安装软件, 64
- 网络设备配置, 316–318
- 查询信息, 63–64
- 卸载软件, 64–65
- UDP, 271
- 报头, 281–282
- ulimit, 363–366
- Umask, 644
- umount 命令, 180
- uname, 139–140
- 单组播地址 (unicast addresses), 303
- 使用 RPM 卸载软件, 58
- 使用 Ubuntu 卸载软件, 64
- 使用 useradd 卸载用户, 100–101
- 使用 userdel 卸载用户, 103
- 使用 usermod 卸载用户, 102
- 移动用户及其家目录, 132–134
- 非账户, 363
- 概述, 549–551
- 查看登录状态, 140
- 切换, 140
- 存储用户信息的位置, 78–79
- /var, 28
- vi 编辑器, 141
- vim, 142
- virtinstall, 649
- 虚拟机 (VM), 649
- 虚拟机化, 643
- 客户端操作系统 (guest OS), 643
- 宿主机操作系统 (host OS), 643
- Hyper-V, 644
- 虚拟机管理器 (hypervisor), 433
- KVM, 644
- QEMU, 644
- 非技术性, 644
- VirtualBox, 644
- VMware, 644
- Xen, 645
- winbind, 536–551

# X
- X Window 系统, 12
- Xen, 645
- xinetd, 210–211
- 启用/禁用服务, 215–217
- /etc/xinetd.conf, 211–212
- 关闭服务, 381
- 使用 finger, 215
- 变量及其含义, 212–214
- XML, 272
- XFS, 559

# Y
- YaST, 661
- 另一种设置工具. 见 YaST
- ypbind, 569
- ypcat, 586
- ypinit, 575–577, 585
- ypmatch, 586
- ypassword, 586
- ypserv, 569
- ypwhich, 586
- ypxfr, 569
- Yum, 60–61
- 卷组 (VG), 187, 189
- 卷管理分配物理卷, 194–195
- 卷管理创建分区和逻辑卷, 188–197
- 卷管理概述, 187–188
- vfsfpd, 430
- 配置, 432–436
- 与 IPv6, 444
- 获取和安装, 432
- 启动和测试服务器, 436–438

# W
- w, 140
- 已知端口, 377
- whereis, 130
- which, 130
- who, 140
- nhois, 422
- 通配符, 111–112

# Z
- zone 关键字, 403
- 区域 (zones), 404–405

# 安全入门指南系列
为自学 IT 专业人士提供的安全技巧

《安全入门指南》系列为当前及新兴安全主题提供了信赖的实操覆盖。这些书籍由领域专家编写，让您能够轻松将安全概念应用于实践。

![](img/3abd8558488b5c70f9f85ba63df43bc0_734_0.png)

安全指标：入门指南
978-0-07-174400-3
无线网络安全：入门指南
978-0-07-176094-2
计算机取证：入门指南
978-0-07-174245-0
Web 应用安全：入门指南
978-0-07-177616-5

提供纸质版和电子书版。

```
