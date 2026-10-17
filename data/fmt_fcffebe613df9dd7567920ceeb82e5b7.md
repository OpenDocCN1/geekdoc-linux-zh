
```
user 0.0 0.0 4084 1008 pts/1 Ss Nov01 0:00 -bash
```

我忘记了 root 密码。我该如何重置它？

现在，你根分区中的文件将位于 `/tmp/hd` 目录中，你可以对它们进行必要的修改。

## 我忘记了 root 密码。我该如何重置它？

从 Fedora CD 启动，并在启动提示符处输入 `linux rescue`。这将让你进入 Linux 安装的“单用户模式”，并以 root 身份登录。输入 `passwd`，你就可以更改 root 密码了。完成后，从机器上移除 CD 并重启（输入 `reboot`）。你的 root 密码将会被更改。

## 程序运行异常。发生是怎么了？

程序运行可能由于多种可能的原因而出现异常故障，但最常见的解释是你的磁盘空间已满。在终端中使用 `df` 命令检查磁盘使用情况：

```
kermit@swinetrek ~]$ df -h

Filesystem Size Used Avail% Mounted on

/dev/mapper/VolGroup00-LogVol010 12G 1.8G 8.8G 17% /

/dev/hda2 99M 9.8M 84M 11% /boot

/dev/shm 62M 0 62M 0% /dev/shm
```

`Used` 和 `Avail` 列显示了你机器上每个分区已用和可用的空间。如果某个分区几乎或完全满了，它可能是你问题的根源；尝试从该分区删除一些文件，看看是否有帮助。不错的选择是日志文件，它们存储在 `/var/log` 目录中。

附录 B：故障排除

## 服务没有运行。问题所在？

你可以使用“服务配置”工具（桌面 > 系统设置 > 服务器设置 > 服务）来停止和启动服务，但如果某个服务不断停止，你可能想尝试从命令行重启它：如果在从命令行运行服务时发生错误，可能会显示该错误。使用 `/sbin/service daemonname start` 重启服务，并观察是否显示了任何错误。

如果重启服务没有显示错误，那么值得调查该服务创建的日志文件。你已经知道 Apache 服务器在 `/var/log/apache` 中的日志文件了；查看 `/var/log` 看看是否存在你该故障服务的日志文件，并检查系统日志。

## 我看不到网络。我该怎么办？

你已经知道如果 LAMP 服务器可以访问网络需要采取大部分步骤：检查电缆是否插好、相邻机器是否可以访问网络，以及网卡上的灯是否在闪烁。所有常用的命令行网络工具（如 `ping` 和 `traceroute`）在 Linux 上都有。检查 `ifconfig` 的输出可能也是值得的：

```
[kermit@swinetrek ~$ /sbin/ifconfig -a

[kermit@swinetrek ~$ /sbin/ifconfig -a

eth0 Link encap:Ethernet HWaddr 00:03:FF:42:E1:92

inet addr:192.168.69.3 Bcast:192.168.255.255 Mask:255.255.0.0

inet6 addr:fe80::ffff:fe42:e19264/64 Scope:Link

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:22548 errors:0 overruns:0 frame:0

TX packets:24780 errors:0 overruns:0 carrier:0

collisions:0 txqueuel:1000

RX bytes:2294916 (2.1 MiB) TX bytes:18896789 (18.0 MiB)

Interrupt:11 Base address:0x0000

lo Link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.0.0.0

inet6 addr::1/128 Scope:Host

UP LOOPBACK RUNNING MTU:16436 Metric:1

314

RX packets:31198 errors:0 dropped:0 overruns:0 frame:0

TX packets:31198 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuelen:0

RX bytes:24317998 (23.1 MiB) TX bytes:24317998 (23.1 MiB)

sit00 Link encap:IPv6-in-IPv4

NOARP MTU:1480 Metric:1

RX packets:0 errors:0 dropped:0 overruns:0 frame:0

TX packets:0 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuelen:0

RX bytes:0 (0.0 b) TX bytes:0 (0.0)

[kermit@swinetrek ~]$
```

上面的行被**加粗**显示了：它列出了 `eth0` 接口的 IP 地址。如果没有出现该行，说明该接口没有 IP 地址。一个快速解决方案是使用 `service network restart` 重启网络，看看这是否让网络接口恢复正常。

## 注意！

> 如果你正在远程操作一台拥有两块网卡的机器，请注意此操作将短暂断开与该机器的所有网络连接。如果你通过 SSH 连接，那么该 SSH 连接也会被断开。如果可以，请从机器本身重启网络，而不是通过网络连接。

# 索引

# 符号

`!` command, 94

#

`+` 引入注释, 116

`root` 用户提示符, 92

`root` 目录符号, 64

`\` 分割日志命令, 92

`~` 主目录提示符, 88

# A

`+` 使用符号链接的抽象, 74

访问日志, Apache, 261, 264

意外删除, 94

缩写, 27

新增入站规则, Firestarter, 284

添加/删除工具, 245

额外的软件, Fedora, 30

管理员软件包, 26

管理员账户（见 `root` 账户）, 92

警报, 294

添加, Webmin, 213

别名文件, 132

允许连接, Firestarter, 283

允许列表, 179

`AllowOverride` 指令, `httpd.conf`, 185

`Anaconda` 安装程序, 50

`acron` 工具, 129

Apache 配置文件（见 `httpd.conf`）, 187

Apache 组, 157

`+` 访问日志, 261, 264

配置, 167–186

Apache Web Server, 157–196

配置安全连接, 186–196

使用 `MySQL` 和 `PHP` 配置, 163–166

错误日志, 166, 261

安装, 158–162

性能调整, 181

启动和停止, 162, 194

自动启动, 193

Apache Web Server 工具, Webmin, 205

应用程序 菜单, `GNOME`, 58

存档管理器, 146

`at` 命令, 131, 203, 300

审计, 268

授权图标, 105

使用 `.bashrc` 执行, 111

自动监控, 116, 118

自动分区, 11, 36

自动, 193

服务, 123, 286

自动化任务, 124–132

# B

`+` 后台应用程序（见 守护进程）, 92

反斜杠, 91

引号, 127

`backup.sh` 脚本, 127

备份, 253–260

`dump` 工具, 117

移除旧的, 85, 126

# 索引

简单备份, 254–260

Webmin 文件系统工具, 203

带宽调整, 265

带宽监控模块, 208

`bash` shell, 95–101

`.bashrc`, 111

二进制文件, 65

启动配置工具, 139

启动 目录, 65

启动失败, 312

启动加载器（见 `GRUB`）, 65

启动和停止工具, Webmin, 203

`Red Hat`, 214

中断, 98

管理用户和组, 110–112

挂载软盘, 112

# C

大小写敏感, 299

`cat` 命令, 91, 300

`cd` 命令, 90, 302

`cd` 命令, 157, 300

`CD-ROM`, 35

`CPAN`, 213

`CVS`, 205

并发版本系统（`CVS`）, 205

协调世界时（`UTC`）, 141

连接速度, 177

内容, 183

配置为, 186

配置设置, 183

# 索引

- 加密, 161（另参见密码学）

- 为 `HTTPS` 配置 Apache, 186

- `RPM` 软件包下载, 219

- 企业级备份工具, 260

- 环境变量, 100

- `anacron` 工具和, 130

- `crontab` 文件和, 125

- 虚拟主机选项, 176

- 错误日志

  - Apache, 266, 261

  - `HTTP` 配置工具, 174

  - 错误页面，定义, 172

- `escap` 转义特殊字符, 91

- `/etc` 目录, 65

- 以太网卡, 17, 151

- `Events` 屏幕, `Firestarter`, 282

- `Evolution` 邮件客户端, 59

- 可执行脚本, 65, 255

- `exit` 命令, 93, 303

- `export` 命令, 101

- `ext2` 文件系统, 64

- `ext3` 文件系统, 63, 117

- 提取对话框, 归档管理器, 148

- 文件所有者/组列表, 权限

  - 对话框, 72

- 文件权限, 70–73

  - 修改, 93, 99, 302

  - `ls` 命令列出, 89

  - 使脚本变为可执行, 255

  - 设置, 73

- 文件优先级设置, Web 服务器, 172

- 文件

  - 归档, 146

  - 复制、移动和重命名, 91

  - 删除, 87, 94

  - 下载, 131, 161, 308

  - 列表出, 88

  - 列出最后几行, 262

  - 文件系统浏览器标签页, `Kate`, 81

- 文件系统, 62

  - 自动挂载, 118

  - `ext2` 文件系统, 64

  - `ext3` 文件系统, 63

  - `fstab` 文件, 114

  - 图标, 068

  - `Linux` 文件权限, 70–73

  - `Windows` 不识别 `Linux`, 4

  - 挂载可移动介质, 112–119

  - 从命令行导航, 90–95

  - 使用 `Nautilus` 导航, 68

  - 其他操作系统和, 63

  - 使用 `NFS` 共享, 136

  - `instab` 类型列出, 116

  - 卸载介质, 114

- `Webmin` 文件管理器访问, 212

- `Webmin` 系统组工具, 203

- `Windows` 文件访问, 4, 234

- `find` 命令, 85, 126, 303

- `Firefox` 浏览器, 58–196

- `Firestarter` 工具, 278–288

- 防火墙, `Firestarter`, 279

# F

- `Fedora` `Core` 发行版, xi

  - `bash` 壳, 95–101

  - 桌面环境, 36

  - `ext3` 文件系统, 64

  - `Firestarter` 工具, 278

  - 硬件浏览器, 150

  - 硬件兼容列表, 2

  - 初始安装屏幕, 7, 32

  - 安装光, 5

  - 提供的软件, 25

  - 特殊安装类型, 10, 35

  - `SuSE` 挂载点规范和, 118

- 文件浏览器应用程序, 67

# 防火墙

- 组，软件（另参见软件包组）

- 组：（参见用户组）

- `GRUB` 启动引导程序, 16, 39

- （另参见安全级别配置）

  - 启用 `Webmin` 访问, 198

  - `Fedora` `Core` 默认, 20

  - 分层安全和, 268

  - 远程配置, 284

  - 文本界面安装, 45

- 启动配置工具和, 139

  - 启动位置, 43

  - `Webmin` 和, 210

  - `GUI` 编辑器, 76

    - `Webmin` 网络模块和, 209

- 软磁盘，挂载, 112

- 软磁盘格式化工具, 149

- 强制删除, 94, 307

- 强制覆盖, 301

- `fsck` 实用, 117

- `fstab` 文件, 114

# H

- 硬件浏览器 (`Hardware Browser`), `Fedora` 150

- 硬件兼容列表, 2–3

- 硬件组模块, `Webmin`,

- `hello_world.sh` 示例, 97

- 帮助，在线, 26, 249

- 隐藏文件, 89, 111

- `history` 命令, 95

- `/home` 目录,

  - 回到主目录, 90

- 主页图标，文件系统视图, 70

- 主密钥，`SSH`, 231

- `.htaccess` 文件, 183–184

- `FTP` (`文件传输协议`), 21, 207

# G

- 网关机, 280

- `GDM` (`GNOME` 显示管理器), 60

- `edit` 编辑器工具, 72, 76

- `GNOME` 桌面, 55–60

  - （参见 `Nautilus`）

  - 底部面板, 56

  - 定制 `GNOME` 终端, 84

  - `edit` 编辑器工具, 72, 76

  - `GUI` 命名规范, 78

  - 安装, 24

  - `root` 密码提示, 104

  - 顶部面板, 57

  - `VNC` 启动和, 250

  - 窗口显示, 60

- `GNOME` 显示管理器 (`GDM`), 60

- `GNOME` `Terminal` 应用程序, 84

- `GNU` 隐私守护 (`GPG`), 161

- 图形化安装, 5–31

- `grep` 命令, 304, 311

- 组权限, 71

- `groupadd` 命令, 110, 304

- `groupdel` 命令, 112, 304

- Apache 服务器端口, 169

- 图形化配置工具, 137

- `HTTP` 配置工具, `Fedora`, 167–183

- `HTTP` 守护进程, 119, 158

- `httpd.conf` 文件, 167

- `apachectl` 工具和, 163

- 配置 Apache 使用证书, 195

- 使用 `Webmin` 编辑, 205

- `.htaccess` 和, 183

- `HTTP` 配置工具, 167

- 使用 `Kate` 的示例, 79

- 停止 Apache 守护进程, 184

- `httpd.package`, 160

# HTTP

- Apache 服务器默认端口, 169

- 为 Apache 配置, 186–196

- 虚拟主机选项, 173

- `Snort` `IDS` 和, 292

- 基于 `IP` 的虚拟主机, 170

- `iptables` 工具, 278–286

# I

- 授权令牌, 105

- `ISO` 镜像, 5, 257–258

- `GNOME` 桌面快捷方式, 59

- 主页图标, 70

- `Webmin` 界面, 202

- `IDS` (`入侵检测系统`), 268, 287–297

- 包含虚拟主机, 178

- `ifconfig` 命令, 314

- 自增运算符

- 依赖检查, 44

- 图形化安装, 5–31

- 组权限, 71

- `groupadd` 命令, 110, 304

- `groupdel` 命令, 112, 304

- Apache 服务器端口, 169

- 图形化配置工具, 137

- `HTTP` 配置工具, `Fedora`, 167–183

- `HTTP` 守护进程, 119, 158

- `httpd.conf` 文件, 167

- `apachectl` 工具和, 163

- 配置 Apache 使用证书, 195

- 使用 `Webmin` 编辑, 205

- `.htaccess` 和, 183

- `HTTP` 配置工具, 167

- 使用 `Kate` 的示例, 79

- 停止 Apache 守护进程, 184

- `httpd.package`, 160

... (此处由于重复内容已按逻辑处理) ...

- 环境变量, 100

- `anacron` 工具和, 130

- `crontab` 文件和, 125

- 虚拟主机选项, 176

- 错误日志

  - Apache, 266, 261

  - `HTTP` 配置工具, 174

  - 错误页面，定义, 172

- `escap` 转义特殊字符, 91

- `/etc` 目录, 65

- 以太网卡, 17, 151

- `Events` 屏幕, `Firestarter`, 282

- `Evolution` 邮件客户端, 59

- 可执行脚本, 65, 255

- `exit` 命令, 93, 303

- `export` 命令, 101

- `ext2` 文件系统, 64

- `ext3` 文件系统, 63, 117

- 提取对话框, 归档管理器, 148

- 文件所有者/组列表, 权限

  - 对话框, 72

- 文件权限, 70–73

  - 修改, 93, 99, 302

  - `ls` 命令列出, 89

  - 使脚本变为可执行, 255

  - 设置, 73

- 文件优先级设置, Web 服务器, 172

- 文件：

  - 归档, 146

  - 复制、移动和重命名, 91

  - 删除, 87, 94

  - 下载, 131, 161, 308

  - 列表出, 88

  - 列出最后几行, 262

  - 文件系统浏览器标签页, `Kate`, 81

- 文件系统, 62

  - 自动挂载, 118

  - `ext2` 文件系统, 64

  - `ext3` 文件系统, 63

  - `fstab` 文件, 114
