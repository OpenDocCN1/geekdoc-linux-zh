# CompTIA Linux+ 实践指南：考试 XK0-004，第2版



![](img/cover.jpg)

![](img/advart-1.jpg)

资深策划编辑：Kenyon Brown

开发编辑：Tom Cirtin

技术编辑：Kevin Ryan

制作编辑：Amy Odum

文字编辑：Tiffany Taylor

编辑部经理：Pete Gaughan

制作经理：Kathleen Wisor

执行编辑：Jim Minatel

校对：Kathryn Duggan

索引员：Ted Laux

封面协调：Brent Savage

封面设计：Wiley

封面图片：© Jeremy Woodhouse/Getty Images, Inc.


*致 Tim Krause*

# 致谢

感谢协助完成本书书编写的团队：Pete Gaughan（编辑部经理）、Kenyon Brown（策划编辑）、Kevin Ryan（技术编辑）、Tom Cirtin（项目编辑）、Amy Odum（制作编辑）、文字编辑 Tiffany Taylor 以及 Aptara 的排字师。

感谢在整个书籍编写和项目努力期间支持我的每一个人，包括我的家人、Partners 的 Patti、Rob 和 Jim、Soundworks 的所有人，以及我在 UWSP 的同事们。

# 关于作者

`Steve Suehring` 是威斯康星大学斯蒂文斯点分校计算与新媒体技术助理教授。在 2015 年加入教职之前，Steve 在各种技术工程、系统和网络管理以及系统架构角色方面拥有 20 年的实地经验。Steve 写过几本书并并担任 *LinuxWorld* 杂志的编辑。

# 引言

本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。本书是 *CompTIA Linux+ Study Guide: Exam XK0-004*（第 4 版）的配套读物。





## 4.1 给定场景，分析系统属性并进行相应的修复
## 4.2 给定场景，分析系统进程以优化性能
## 4.3 给定场景，分析并排排除用户问题
## 4.4 给定场景，分析并排排除应用程序和硬件问题

# 领域 5.0 自动化与脚本 (14% - 5)
## 5.1 给定场景，部署并执行基础 `Bash` 脚本
## 5.2 给定场景，使用 `Git` 进行版本控制
## 5.3 总结编排过程和概念


152. 配置 WiFi 时，以下哪个命令显示有关无线设备 `wlan0` 的链路状态等信息？
1. `iw dev wlan0 link`
2. `wlan0 list`
3. `iw wlan0 -l`
4. `iw dev link`

153. 你正在配置一个 DHCP 服务器。以下哪个命令将检查系统日志以获取有关 DHCP 活动的信息？
1. `grep -i dhcp /var/log/syslog`
2. `grep -v dhcp /var/log/syslog`
3. `grep -vi dhcp /var/log/kern.log`
4. `dmesg | grep dhcp`

154. `dmesg` 的哪个选项在读取一次后清除内核环形缓冲区的内容？
1. `-C`
2. `-c`
3. `-a`
4. `-e`

155. `rsync` 命令的哪个选项提供了归档模式（archive mode）？
1. `-r`
2. `-o`
3. `-a`
4. `-f`

156. 在使用 `gcc` 编译器编译软件时，包含用于 `make` 命令的命令和关系的文件的推荐名称是哪个？
1. `Makefile`
2. `makefile`
3. `make.file`
4. `Makefile.txt`

157. 你下载了一个扩展名为 `.gz` 的源文件。以下哪个命令将解压该文件？
1. `unzip`
2. `gunzip`
3. `dezip`
4. `uncomp`

158. `make` 的哪个目标（通常包含大多数项目的 `makefile` 中）会将编译后的文件放置到最终位置，并执行诸如将适当的文件设置为可执行等操作？
1. `list`
2. `distclean`
3. `run`
4. `install`

159. 在创建本地软件包仓库时，`/etc/yum.repos.d/` 下的 `.repo` 文件中的哪个选项用于设置仓库的 URL？
1. `url`
2. `repourl`
3. `httpurl`
4. `baseurl`

160. 运行 `lsblk` 命令时，`/boot` 没有单独分区。系统是从哪个分区启动的？
1. 在 `/` 分区下有一个 `/boot` 目录。
2. `/boot` 分区被隐藏了。
3. 系统尚未构建 `/boot` 分区。
4. `/boot` 分区没有在 `lsblk` 中显示。

161. 可以使用哪个命令来搜索当前位置下方所有包含 `DB` 字符的文件内容？
1. `grep -r "DB" *`
2. `grep -ri "DB" *`
3. `cat * | less`
4. `cat *. | grep`

162. 你正在操作一个文件服务器，客户端报告通过 NFS 连接的文件系统已无法访问。应该向 `umount` 传递哪个选项以强制卸载文件系统？
1. `-nfs`
2. `--fake`
3. `-f`
4. `-n`

163. 使用 `mail` 命令时，哪个字符组合将消息正文设置为 `STDIN`？
1. `<`
2. `>`
3. `<<<`
4. `|`

164. 下列哪个命令显示登录到服务器的用户列表及其登录时间？
1. `whois`
2. `who`
3. `loggedin`
4. `curusers`

165. 哪个配置文件被用作 BIND 服务器的默认文件？
1. `named.conf`
2. `named.cfg`
3. `bind.cfg`
4. `bind.conf`

166. 在创建证书机构角色时，以下哪个命令生成用于 SSL 的私钥并将其放入文件 `/etc/ssl/example.com.private` 中？
1. `openssl genrsa -out /etc/ssl/example.com.private`
2. `openssl generate-private > /etc/ssl/example.com.private`
3. `openssl genpriv > /etc/ssl/example.com.private`
4. `openssh genkey -out /etc/ssl/example.com.private`

167. 在创建 Squid 代理配置时，你需要为本地网络创建一个访问控制列表（ACL）。哪个配置选项为 Squid 创建访问控制列表？
1. `accesscontrol`
2. `acl`
3. `access-control`
4. `access-control-list`

168. Squid 配置中的哪个指令配置了给定的 ACL 是否可以使用代理？
1. `access_allow`
2. `http_access`
3. `proxy_access`
4. `enable_access`

169. 哪个 Samba 守护进程负责响应 NetBIOS 服务请求？
1. `smbd`
2. `nmbd`
3. `winbindd`
4. `samba`

170. OpenSSH 服务器配置中的哪个选项用于确定 root 用户是否可以直接通过 SSH 客户端登录？
1. `PermitRootLogin`
2. `AllowRoot`
3. `RootLogin`
4. `PermitDirectRootLogin`

171. OpenVPN 配置中的哪个选项让客户端知道它可以可以访问网络 `192.168.5.0/24`？
1. `client-route 192.168.5.0`
2. `push "route 192.168.5.0 255.255.255.0"`
3. `send "route 192.168.5.0/24"`
4. `client-route "192.168.5.0/24"`

172. 如果你的显示会话使用 Wayland，设置的环境变量名称是什么？
1. `WAYLAND_DISPLAY`
2. `WAYLANDORG`
3. `WAYLAND_SESSION`
4. `WAYLAND_DISP`

173. 可以使用哪个命令查看中断等设备信息？
1. `lsint`
2. `ls -interrupts`
3. `lsdev`
4. `ls-int`

174. 使用 `udevadm` 命令时，你需要重新加载规则以添加新的客户端设备。可以使用哪个选项来实现此更改？
1. `udevadm control -R`
2. `udevadm --stop`
3. `udevadm -stop-queue`
4. `udevadm -R`

175. 你将部署一个以 Linux 为基础操作系统的大型服务器解决方案。服务器资源将被分为多个运行 Linux 和 Windows 的较小虚拟服务器。以下哪个项最描述这种服务器角色和技术的名称？
1. `Systemization`
2. `MultiSys`
3. `Containers`
4. `UserDev`





## 176. 你需要重启运行在旧版本、非 `systemd` 的 Linux 发行版上的 Apache 服务器。假设该服务器名称为 `apache2`，使用以下哪个命令可以用于重启 Apache 服务器？
1. `apache2.service restart`
2. `restart-daemon apache2`
3. `service apache2 restart`
4. `service restart apache2`

## 177. 使用 NX 或 NoMachine 显示进行访问时，哪个配置选项用于设置显示端口？
1. `DisplayPort`
2. `DisplayBase`
3. `ListenPort`
4. `ListenXPort`

## 178. 在选择登录类型时，以下哪项最准确描述了 Cinnamon 和 Cinnamon (Software Rendering) 两个选项之间的区别？
1. 描述为 Software Rendering 的选项用于图形生产环境。
2. 描述为 Software Rendering 的选项使用 3D 加速。
3. 描述为 Software Rendering 的选项用于增强视频驱动程序。
4. 描述为 Software Rendering 的选项会禁用了 3D 加速。

## 179. 在带有 Raspbmc Linux 的树莓派上，你需要配置系统以打开 LED。以下哪个是通常用于此目的的接口？
1. USB
2. HBA
3. GPIO
4. SNP

## 180. 以下哪个命令可以用于排查各种服务的启动耗时？
1. `time`
2. `bootmsg`
3. `systemd-boot`
4. `systemd-analyze blame`

## 181. 你正在排查作为负载均衡器的 HAProxy 的问题。用户报告他们收到了来自 HAProxy 服务器的“400”响应。“400”响应意味着什么？
1. 请求无效或过大。
2. 请求未授权。
3. 请求超时。
4. 存在内存溢出情况。

## 182. 在 MATE 桌面环境中，以下哪项是文件管理器的名称？
1. Naut
2. caja
3. fm
4. fileexp

## 183. SSH 的哪个选项可以创建允许远程客户端也连接的端口转发？
1. `-L`
2. `-R`
3. `-P`
4. `-E`

## 184. `wget` 命令的哪个选项用于记录输出？
1. `-r`
2. `-o`
3. `-b`
4. `-k`

## 185. 在启用了 `systemd` 的服务器上执行时，`service status` 命令等于哪个命令？
1. `systemd status`
2. `journald status`
3. `service-systemd status`
4. `systemctl status`

## 186. 你需要比较两个文件以确定它们之间是否存在差异。可以使用哪个命令实现此目的？
1. `dcat`
2. `tar`
3. `diff`
4. `dtool`

## 187. Apache 配置文件中的哪个指令有助于使用单个 IP 地址为多个域名提供网站服务？
1. `<VirtualServer>`
2. `<VirtualHost>`
3. `<VirtContainer>`
4. `<Virtualization>`

## 188. `openssl` 的哪个子命令用于创建证书签名请求 (CSR)？
1. `req`
2. `csr`
3. `gencsr`
4. `newcsr`

## 189. `kill` 命令的哪个信号可以用于指示 BIND 重新加载（包括其配置）？
1. `-15`
2. `-1`
3. `-9`
4. `-2`

## 190. 你正在排查一个守护进程，并从命令行手动启动了该守护进程，使其不会 fork 到后台。可以使用哪个组合键来终止该守护进程？
1. Ctrl+A
2. Ctrl+B
3. Ctrl+C
4. Ctrl+D

## 191. 你需要将输出重定向到文件，但不是覆盖现有文件，而是追加输出。使用哪个字符组合来表示应追加 `STDOUT`？
1. `<>`
2. `a>`
3. `>a`
4. `>>`

## 192. 哪个服务命令用于停止服务？
1. `shutdown`
2. `stop`
3. `norun`
4. `runstop`

## 193. 哪个端口是 VNC 使用的默认基础端口？
1. 59
2. 59000
3. 5900
4. 590

## 194. 以下哪个目录用于 CentOS 7 中的自动错误报告工具？
1. `/var/spool/abrt`
2. `/var/spool/autobug`
3. `/var/tmp/abrt`
4. `/var/tmp/autobug`

## 195. 以下哪个命令配合 `udevadm` 重新重放事件？
1. `replay`
2. `trigger`
3. `play`
4. `evplay`

## 196. `hostnamectl` 的哪个命令可以设置运行它的机器类型？
1. `set-machine`
2. `machine-type`
3. `set-type`
4. `set-chassis`

## 197. 作为系统管理员，你有一个需要在启动时执行的自定义服务。然而，该服务没有传统的服务管理脚本。你可以将命令放在哪个文件中，以便其在启动时执行？
1. `/etc/rcd`
2. `/etc/custom.service`
3. `/etc/rc.local`
4. `/etc/rc.d/rc.service`

## 198. 以下哪个命令用于控制 BIND 名称服务器？
1. `bind-config`
2. `named-config`
3. `rndc`
4. `rdmc`

## 199. 你被要求使用 Red Hat Linux 配置集群角色。以下哪个文件系统可能会被使用？
1. `ext2`
2. `GFS`
3. `CIFS`
4. `FAT`

## 200. 在配置远程访问时，你会在哪个段（stanza）中添加视频设备？
1. `<display>`
2. `<video>`
3. `<videoDisplay>`
4. `display=`

## 211. 你需要重定向 `STDIN` 直到遇到特定的字符组合。以下运算符可以用于此目的？
1. `>STDIN`
2. `<<`
3. `<&`
4. `>`

## 202. `chkconfig` 的哪个选项允许你设置给定服务的运行级别 (runlevels)？
1. `--level`
2. `--runlevel`
3. `-l`
4. `-rl`

## 203. `curl` 命令的哪个选项设置保存输出的本地文件名？
1. `-f`
2. `-o`
3. `-O`
4. `-l`

## 204. 以下哪个命令用于添加组？
1. `groupadd`
2. `addgrp`
3. `grpadd`
4. `creategroup`

## 205. 哪个命令允许你确定与当前用户 ID 关联的用户名？
1. `uid`
2. `myid`
3. `whoami`
4. `w`

## 206. 登录时运行的脚本和其他文件应该存储在哪个目录下？
1. `/etc/login`
2. `/etc/profile`
3. `/etc/bash.defs`
4. `/etc/profile.d`

## 207. Unity 桌面通常出现在哪个 Linux 发行版中？
1. Ubuntu
2. Red Hat
3. Slackware
4. SuSE

## 208. 在 Debian 系统上，`udev` 启动时执行的启动命令可以在哪个目录找到
1. `/etc/udev`
2. `/etc/rcS.d`
3. `/etc/rc5.d`
4. `/etc/rc5/udev`

## 209. 你正尝试在一个以前使用 SysVinit 但现在使用 `systemd` 的系统上停止守护进程。在该系统中停止服务的正确命令和顺序是？
1. `systemctl <service> stop`
2. `systemctl stop <service>`
3. `systemd stop <service>`
4. `systemd <service> stop`

## 210. 在配置用于 X11 的显示器时，应该在哪个部分更改显示器的细节？
1. `Video`
2. `Display`
3. `Monitor`
4. `Disp`

## 211. 你需要重定向长时间运行进程的输出，但不需要查看或捕获输出。可以将输出重定向到哪个位置以不占用磁盘空间？
1. 普通文件
2. `/dev/null`
3. `/dev/random`
4. 网络接口

## 212. `paste` 命令的哪个选项用于设置分隔符？
1. `-f`
2. `-d`
3. `-o`
4. `-m`

## 213. `service` 命令的哪个目标（target）会导致守护进程重新读取其配置文件而不重启守护进程本身？
1. `read`
2. `load`
3. `start`
4. `reload`





## 214. 在为 `systemd` 配置环境参数时，用于创建变量的键名是什么？

1. `ENV`
2. `Environment`
3. `Envvar`
4. `ENVPARAM`

## 215. 使用哪个操作符来重定向 `STDIN`，例如从文件重定向输入？

1. `>`
2. `<`
3. `^`
4. `*`

## 216. 在使用 `udev` 配置网络适配器以使其特定且一致名称时，你编辑了 `udev` 规则文件。规则文件中的哪个选项可以确保设备始终具有 `eth0` 的名称？

1. `ATTR-NAME="eth0"`
2. `NAME="eth0"`
3. `DEV_NAME="eth0"`
4. `NAME_DEV="eth0"`

## 217. 通常在哪个目录下找到 Xorg 配置文件 `xorg.conf`？

1. `/etc/xorg`
2. `/etc/x`
3. `/etc/Xorg`
4. `/etc/X11`

## 218. 在使用 ALSA 配置音频时，使用哪个命令查看混音器卷？

1. `alsaconfig`
2. `alsacfg`
3. `alsamixer`
4. `amix`

## 219. 哪个软件包提供了远程桌面协议的开源实现？

1. `ordp`
2. `xrdp` 
3. `tdpx`
4. `xr`

## 220. 你正在配置一个数据库服务并需要为 MySQL 打开默认端口。MySQL 的默认端口是？

1. 6592
2. 25
3. 389
4. 3306

## 221. 你需要确定 Linux 系统中安装了哪种显卡。哪个命令可以帮助实现此目的？

1. `dmesg | grep -i vga`
2. `vgadetect`
3. `lsvid`
4. `lsvga`

## 222. 你从命令行手动执行了一个守护进程，现在需要挂起该进程。可以使用哪个组合键来实现此目的？

1. Ctrl+S
2. Ctrl+C
3. Ctrl+Z
4. Ctrl+B

## 223. 在为 Apache 配置 Web 服务器角色时，以下哪个指令告诉服务器 SSL 私有钥的位置？

1. `SSLKeyFile`
2. `SSLCertificatePrivateKey`
3. `SSLCertificateKeyFile` 
4. `SSLPrivateKey`

## 224. 哪个命令用于为无线设备设置 essid、通道和其他相关选项？

1. `ifconfig`
2. `iwconfig`
3. `wlancfg`
4. `iconf`

## 225. 哪个命令可以将整个文件中的小写字母转换为大写字母？

1. `du`
2. `touc`
3. `conv`
4. `tr`

## 226. 你被要求为初学者推荐一个简单的基于命令行的文本编辑器。你应该推荐哪一个？

1. Vi
2. Nano
3. `nc`
4. ShellRedirect

## 227. 你需要确保服务不在 `systemd` 系统上启动。应该使用哪个 `systemctl` 命令来实现此目的？

1. `disable`
2. `delete`
3. `mask`
4. `norun`

## 228. 以下哪个命令是大多数 Linux 系统上都有的简单分页器？

1. `more`
2. `pg`
3. `grep`
4. `mr`

## 229. 以下哪个是重定向 `STDOUT` 和 `STDERR` 的操作符？

1. `&>`
2. `>`
3. `~`
4. `!`

## 230. 哪个设备作为当前进程的终端？

1. `/dev/termcur`
2. `/dev/tdev`
3. `/dev/tty`
4. `/dev/curproc`

## 231. 哪个命令可以用于特殊格式的字符串进行打印？

1. `printf`
2. `echo`
3. `print`
4. `here`

## 232. 你需要通过脚本程序化地删除一系列文件。哪个命令可以删除这些文件？

1. `remove`
2. `rmfile`
3. `unlink`
4. `rem`

## 233. 你需要将文件拷贝到远程系统，但该远程系统运行 FTP。以下哪个命令用于此操作？

1. `scp`
2. `sftp`
3. `ftp`
4. `curl`

## 234. 当 Apache 设置为 Off 时返回什么状态码？

1. 405
2. 100
3. 302
4. 200

## 235. 你正在后台运行一个进程并需要它在注销后继续运行。应该使用哪个命令来实现？

1. `set`
2. `cont`
3. `nohup`
4. `proc`

## 236. 你插入了一个 USB 设备。以下哪个命令用于确定设备是否被检测？

1. `set`
2. `blue`
3. `ls`
4. `usb`

## 3.1 给定场景，配置并实施相应的访问和身份验证方法

### PAM
- 密码策略
- LDAP 集成
- 用户锁定
- 必须、允许或足够
- `/etc/pam.d/`
- `pam_tally2`
- `faillock`

### SSH
- `~/.ssh/`
    - `known_hosts`
    - `authorized_keys`
    - `config`
    - `id_rsa`
    - `id_rsa.pub`
- 用户特定访问
- TCP Wrappers
- `/etc/sshd/`
    - `ssh.conf`
    - `sshd.conf`
- `ssh-copy-id`
- `ssh-keygen`
- `ssh-add`

### TTYs
- `/etc/securetty`
- `/dev/tty#`

### PTYs

### PKI
- 自签名
- 私钥
- 公钥
- 哈希处理
- 数字签名
- 消息摘要

### 作为客户端的 VPN
- SSL/TLS
- 传输模式
- 隧道模式
- IPSec
- DTLS

## 3.2 给定场景，应用或获取权限和所有权

### 权限
- 读、写、执行
- 用户、组、其他
- SUID
- 进制表示
- 粘滞位
- 继承
- 工具
    - `chmod`
    - `chown`
    - `chgrp`
    - `getfacl`
    - `setfacl`
    - `ls`
    - `ulimit`
    - `chage`

### SELinux
- 上下
- 禁用
    - 宽容 (Permissive)
    - 强制 (Enforcing)
- 策略
    - 目标型 (Targeted)
- 工具
    - `setenforce`
    - `getenforce`
    - `sestatus`
    - `setsebool`
    - `getsebool`
    - `concon`
    - `restorecon`
    - `ls -Z`
    - `ps -Z`
- AppArmor
    - 禁用 (disable)
    - 投诉模式 (complain)
    - 无限制 (unconfined)
    - `/etc/apparmor.d/`
    - `/etc/apparmor.d/tunables`
- 权限提升
    - `su`
    - `sudo`
    - `wheel`
    - `visudo`
    - `sudoedit`

## 3.3 总结 Linux 环境下的安全最佳实践

### 安全
- 引导程序密码
- UEFI/BIOS 密码

### 额外的身份验证方法
- 多因素身份验证
    - 令牌
    - (i) 硬件
    - (ii) 软件
    - OTP (一次性密码)
    - 生物识别
- RADIUS
- TACACS+
- LDAP
- Kerberos
    - `kinit`
    - `klist`

### 禁用 SSH 根登录的重要性





-   无密码登录
    -   强制使用 PKI
-   Chroot 监狱服务
-   不共享 ID
-   拒绝主机（denying hosts）的重要性
-   将操作系统数据与应用程序数据分离
    -   通过磁盘分区以最大化系统可用性
-   更改默认端口
-   禁用或卸载未使用且不安全服务的重要性
    - FTP
    - Telnet
    - Finger
    - Sendmail
    - Postfix
-   启用 SSL/TLS 的重要性
-   启用 auditd 的重要性
-   CVE 监控
-   限制使用 USB 设备
-   磁盘加密
    - LUKS
-   限制 cron 访问
-   禁用 Ctrl+Alt+Del
-   添加横幅（banner）
-   MOTD（当日登录消息）

## ![images](img/correction.png) 3.4 给定场景，实现日志服务
-   关键文件位置
    - `/var/log/secure`
    - `/var/log/messages`
    - `/var/log/[application]`
    - `/var/log/kern.log`
-   日志管理
    -   第三方代理
    - `logrotate`
    - `/etc/rsyslog.conf`
    - `journald`
        - `journalctl`
-   `lastb`

## ![images](img/correction.png) 3.5 给定场景，实现并配置 Linux 防火墙
-   访问控制列表
    - 源
    - 目的地
    - 端口
    - 协议
    - 日志
    - 状态化 vs 无状态
    - 接受（Accept）
    - 拒绝（Reject）
    - 丢弃（Drop）
    - 记录（Log）
-   技术
    - `firewalld`
        - 区域（Zones）
        - 运行时（Runtime）
    - `iptables`
        - 持久化（Persistency）
        - 链（Chains）
    - `ufw`
        - `/etc/default/ufw`
        - `/etc/ufw/`
    - Netfilter
-   IP 转发
    - `/proc/sys/net/ipv4/ip_forward`
    - `/proc/sys/net/ipv6/ip_forward`
-   动态规则集
    - DenyHosts
    - Fail2ban
    - IPset
-   常见应用防火墙配置
    - `/etc/services`
    - 特权端口

## ![images](img/correction.png) 3.6 给定场景，备份、恢复和压缩文件
-   归档与恢复工具
    - `tar`
    - `cpio`
    - `dd`
-   压缩
    - `gzip`
    - `xz`
    - `bzip2`
    - `zip`
-   备份类型
    - 增量
    - 全量
    - 快照克隆
    - 差异
    - 镜像
-   离线/离系统存储
    - SFTP
    - SCP
    - `rsync`
-   完整性检查
    - MD5
    - SHA

1. 哪条命令将为 `/dev/sda1` 磁盘分区创建镜像，并将该镜像放入名为 `output.img` 的文件中？
    1. `dd if=sda of=/dev/sda1`
    2. `dd if=output.img of=/dev/sda1`
    3. `dd if=/dev/sda1 of=output.img`
    4. `echo /dev/sda1 > output.img`

2. 哪条命令将监控 `/var/log/httpd/access.log` 的 Apache 日志，并在新日志项创建时持续滚动？
    1. `watch /var/log/httpd/access.log`
    2. `tail /var/log/httpd/access.log`
    3. `tail -f /var/log/httpd/access.log`
    4. `mon /var/log/httpd/access.log`

3. 你收到一个扩展名为 `.lzma` 的文件。可以使用哪条命令解压此文件？
    1. `xz`
    2. `lz`
    3. `gz`
    4. `bzip`

4. 下列哪条命令将正确将名为 `a.out` 的文件的组所有更改更改 users？
1. `chgrp users a.out`
    2. `chgrp a.out users`
    3. `groupchg a.out users`
    4. `grpchg users a.out`

5. `umask` 的哪个选项将以 POSIX 格式显示将要使用的权限？
    1. `-P`
    2. `-p`
    3. `-S`
    4. `-v`

6. 根据 FHS（文件系统层次结构），服务器特定数据的正确位置是？
    1. `/etc`
    2. `/var`
    3. `/tmp`
    4. `/srv`

7. 下列哪条命令为名为 `homescript.sh` 的文件启用粘滞位（sticky bit）？
    1. `chmod +sticky homescript.sh`
    2. `chmod 755 homescript.sh`
    3. `chmod u+s homescript.sh`
    4. `chown u+sticky homescript.sh`

8. `umask` 报告为 022。对于新生成的不可执行文件，生效的权限是什么？
    1. `u+rw, g+r, w+r`
    2. `755`
    3. `022`
    4. `a+r`

9. `chown` 的哪个选项会递归更改所有权？
    1. `-f`
    2. `-R`
    3. `-a`
    4. `-m`

10. `chgrp` 的哪个选项将更改给定目录内所有文件的组所有权？
    1. `-directory`
    2. `-d`
    3. `-R`
    4. `-V`

11. 命令通过 `ls -la` 显示如下：`-rwsr-xr-x 1 suehring suehring Nov 2 13:53 script.sh`。权限中的 `s` 代表什么？
    1. 该程序设置了 `suid` 位。
    2. 这是一个符号链接。
    3. 该文件将不可执行。
    4. 该文件是一个特殊文件。

12. 在 `bash` 中源（source）文件时，假设你的当前用户拥有该文件，哪条 `chmod` 命令将为该文件的源提供最小权限顺序？
    1. `chmod 600`
    2. `chmod 755`
    3. `chmod 777`
    4. `chmod 400`

13. 下列哪条命令会移除过期时间？
    1. `sudo chage -l`
    2. `sudo chage -E`
    3. `sudo chage now`
    4. `sudo chage --noexpire`

14. 你需要确定 LDAP 集成工作正常。为了这样做，你想通过 `nsswitch.conf` 获取用户列表。哪条命令可用于此目的？
    1. `getuser`
    2. `getent`
    3. `usermod`
    4. `list`

15. 哪个文件包含了允许创建 `cron` 任务的用户？
    1. `/etc/cron`
    2. `/etc/deny`
    3. `/etc/allow`
    4. `/etc/user`

16. 哪种系统日志设施用于来自内核的消息？
    1. `syslog`
    2. `kernel`
    3. `kern`
    4. `system`

17. 下列哪条命令用于检查 `systemd` 日志或文件？
    1. `journallist`
    2. `ctlj`
    3. `journalctl`
    4. `jctl`

18. 提供日志功能的 `systemd` 服务名称是什么？
    1. `systemd-journald`
    2. `systemd-loggingd`
    3. `systemd-syslog`
    4. `systemd-logger`

19. `logrotate.conf` 中的哪个配置选项会在处理选定日志运行时将日志发送到 admin@example.com？
    1. `mail@example.com`
    2. `sendmail@example.com`
    3. `maillog@example.com`
    4. `logmail@example.com`

20. 假设在 `/etc/rsyslog.conf` 配置中设置了 `$ModLoad imudp` 选项，哪个额外选项用于配置服务器监听的端口？
    1. `$Port 514`
    2. `$UDPServerRun 514`
    3. `$Listen 514`
    4. `$UDPListen 514`





## 24. 为了让主、备名称服务器针对特定域名进行通信，需要在防火墙中开放哪些端口和协议？

1. `udp/53`
2. `Both tcp/53 and udp/53`
3. `tcp/53`
4. `udp/53 and tcp/503`

## 25. 在检查服务器上的开放端口时，你发现 TCP 端口 3000 在列列表中，但没有对应的协议名称（如 `smtp`、`imaps` 等）。在哪个文件中可以找到端口到协议的转换列表，并对其自定义以添加此新端口？

1. `/etc/ports`
2. `/etc/p2p`
3. `/etc/ppp`
4. `/etc/services`

## 26. ICMP 运行在哪个端口上？

1. `TCP/43`
2. `UDP/111`
3. `UDP/69`
4. `ICMP 不使用端口。`

## 27. 下列哪种协议使用了三次握手？

1. `ICMP`
2. `TCP`
3. `UDP`
4. `IP`

## 28. 下列哪个命令可以显示账户信息，如过期日期、上次密码更改和其他相关细节？

1. `usermod -l`
2. `userinfo -a`
3. `chageuser -l`
4. `chage -l`

## 29. 哪个命令用于创建用于 SSH 的公/私钥对？

1. `ssh -k`
2. `ssh-keygen`
3. `ssh-genkey`
4. `ssh -key`

## 30. 你应该将公钥放在哪个文件中，以便接受服务器基于密钥的 SSH 认证？

1. `~/.ssh/authorized_keys`
2. `~/.ssh/keys`
3. `~/.ssh/keyauth`
4. `~/.sshd/authkeys`

## 31. 你需要以特定用户执行命令。下列哪个命令可以实现这一操作？

1. `sudo -u`
2. `sudo -U`
3. `sudo -s`
4. `sudo -H`

## 32. `/etc/sudoers` 中的哪个选项会导致指定的命令不再提示输入密码？

1. `PASSWORD=NO`
2. `NOPASSWD`
3. `NOPASSWORD`
4. `NOPROMPT`

## 33. 下列哪个命令将显示当前登录用户的 CPU 时间、内存和其他限制条件？

1. `reslimit`
2. `limitres -a`
3. `ulimit -a`
4. `proclimit -n`

## 34. 在使用 TCP wrappers 时，`/etc/hosts.deny` 文件中的哪一行将阻止 192.168.1.0/24 网络内的任何主机访问从 `xinetd` 运行的服务？

1. `BLOCK: 192.168.1.0/24`
2. `REJECT: 192.168.1.0`
3. `ALL: 192.168.1.0/255.255.255.0`
4. `NONE: 192.168.1/255.255.255.0`

## 35. 你对 SSH 使用基于 RSA 的密钥对。默认情况下，`~/.ssh` 中私钥文件的名称是什么？

1. `id_rsa`
2. `id_rsa.priv`
3. `id_rsa.key`
4. `rsa_key.priv`

## 36. `su` 命令的哪个选项将以非交互式会话执行单个命令？

1. `-s`
2. `-u`
3. `-c`
4. `-e`

## 37. 在指定密钥服务器后，`gpg` 的哪个选项用于指定发送到密钥服务器的密钥？

1. `key-name`
2. `keyname`
3. `send-key`
4. `sendkey`

## 38. 下列哪个命令应该用于编辑 `/etc/sudoers` 文件？

1. 任何文本编辑器，如 Vi 或 emacs
2. `editsudo`
3. `visudo`
4. `visudoers`

## 39. 哪个文件可以用于存储已知 SSH 密钥的服务器全局主机缓存？

1. `/etc/sshd_known_hosts`
2. `/etc/ssh_known_hosts`
3. `~/.ssh/known_hosts`
4. `/root/ssh_known_hosts`

## 40. 为了让 X11 转发工作，目标服务器上的 `/etc/sshd/sshd.conf`（或 `/etc/ssh/sshd_config`）必须启用哪个选项？

1. `XForward yes`
2. `Xenable yes`
3. `X11Forwarding yes`
4. `Xconnection yes`

## 41. 下列哪个命令用于生成 GnuPG 密钥对？

1. `gpg --gen-key`
2. `gpg --key`
3. `gpg --send-key`
4. `gpg --create-key`

## 42. 你需要禁用 `/etc/inetd.conf` 中的一个服务。下列哪个字符被用作注释字符？

1. `-`
2. `#`
3. `/`
4. `%`

## 43. 哪个文件被用作 `gpg` 密钥环的默认存储？

1. `publickeys.gpg`
2. `pubring.gpg`
3. `public.gpg`
4. `pubkeys.gpg`

## 44. `su` 命令的哪个选项用于获取登录环境？

1. `-u`
2. `-U`
3. `-`
4. `-login`

## 45. LUKS 使用哪种密钥派生函数？

1. `PBKDF2`
2. `SSL`
3. `RSA`
4. `DSA`

## 46. 下列哪个命令用于配置 `dm-crypt` 卷？

1. `cryptsetup`
2. `dm-crypt`
3. `dm-setup`
4. `crypt-config`

## 47. 下列哪个通配符在 `/hosts.allow` 中用于指定匹配匹配 IP 地址的主机？

1. `*`
2. `ALL`
3. `IP`
4. `MATCH`

## 48. `tar` 命令的哪个选项用于创建归档？

1. `-c`
2. `-b`
3. `-f`
4. `-d`

## 49. `tar` 命令的哪个选项用于删除归档中的文件？

1. `-d`
2. `-delete`
3. `-rem`
4. `-remove`

## 50. 下列哪个文件应在成功登录后显示消息？

1. `/etc/net`
2. `/etc/issue`
3. `/etc/motd`
4. `/etc/banner`

## 51. `rsync` 的哪个选项用于删除不存在的文件？

1. `--delete`
2. `--remove`
3. `-del`
4. `-rem`

## 52. `rsync` 命令的哪个选项用于确定文件的修改？

1. `--mod-time`
2. `--modify-time`
3. `--mod-res`
4. `--modify-window`

## 53. 下列哪个 `gzip` 选项将输出发送到 `STDOUT`？

1. `-s`
2. `-c`
3. `-d`
4. `-f`

## 54. 下列哪个 `gzip` 选项会抑制所有警告信息？

1. `-v`
2. `-q`
3. `-L`
4. `-r`

## 55. `rsync` 的哪个选项指定同步过程的远程 shell 或传输使用 SSH？

1. `-t ssh`
2. `--overssh`
3. `-e ssh`
4. `-F ssh`

## 56. 配置 BIND 的 `chroot` 时，应该在下列哪个文件中设置 `chroot` 用户的家目录？

1. `/etc/bind.home`
2. `/etc/bind.user`
3. `/etc/passwd`
4. `/etc/bindauth`

## 57. 在生成密钥时，`rndc` 认证必须使用哪种算法？

1. `sha1`
2. `sha256`
3. `md5`
4. `hmac-md5`

## 58. `tar` 命令的哪个选项用于解压使用 `gzip` 压缩的文件？

1. `-z`
2. `-x`
3. `-c`
4. `-f`

## 59. 哪个选项用于从归档排除某些文件？

1. `-x`
2. `-exclude`
3. `-ex`
4. `-remove`





2. `/etc/pam`

3. `/etc/pam.d`

4. `/etc/pam.conf.d`

66. `slapd` LDAP 守护进程在哪个端口监听连接？

1. 389
2. 3389
3. 3306
4. 110

67. 当文件 `/etc/nologin` 存在时，哪个 PAM 模块会防止 root 以外的账户登录？

1. `pam_login.so`
2. `pam_preventlogin.so`
3. `pam_nologin.so`
4. `pam_logindef.so`

68. 哪个 PAM 模块负责普通或标准的密码认证？

1. `pam_auth.so`
2. `pam_login.so`
3. `pam_unix.so`
4. `pam_standardlogin.so`

69. 哪个 PAM 模块提供了检查和强制密码强度的机制，以执行密码策略？

1. `pam_passwdstr.so`
2. `pam_cracklib.so`
3. `pam_libpasswd.so`
4. `pam_strpass.so`

70. Postfix TLS 配置的证书和密钥应该是什么什么格式？

1. PKCS
2. PEM
3. TLS
4. SSL

71. 哪个 `iptables` 链用于创建端口重定向？

1. `REDIRECT`
2. `PREROUTING`
3. `PORTREDIR`
4. `ROUTING`

72. 下列哪个命令可以将当前的 `iptables` 规则保存到文件中？

1. `save-iptables`
2. `iptables-create`
3. `iptables-save`
4. `ipt-save`

73. 下列哪个命令列出当前的 `iptables` 规则，同时不尝试解析主机或端口名？

1. `iptables -L`
2. `iptables -List -no-resolve`
3. `iptables -a`
4. `iptables -nL`

74. 下列哪个目录包含 `fail2ban` 系统的配置文件？

1. `/etc/fail2ban.cfg`
2. `/etc/fail2ban.d`
3. `/etc/f2b`
4. `/etc/fail2ban`

75. 在 OpenSSH 配置中，哪个选项禁用了空密码？

1. `DisableEmptyPass`
2. `PermitEmptyPasswords`
3. `EmptyPasswordAuth`
4. `PermitPasswordLength`

76. 下列哪个命令将 `INPUT` 链的默认策略设置为丢弃没有特定允许规则通过的数据包？

1. `iptables INPUT DROP`
2. `iptables chain INPUT policy DROP`
3. `iptables -P INPUT DROP`
4. `iptables POLICY=DROP CHAIN=INPUT`

77. OpenVPN 在哪个端口和协议上监听？

1. ICMP/1194
2. UDP/1194
3. TCP/1194
4. VPN/1194

78. 下列哪项最准确描述 `iptables` 中 `DROP` 和 `REJECT` 目标之间的区别？

1. `DROP` 和 `REJECT` 的作用相同。
2. `DROP` 静默丢弃数据包，而 `REJECT` 发回 ICMP 确认包。
3. `REJECT` 静默丢弃数据包，而 `DROP` 发回 ICMP 确认包。
4. `DROP` 发回直接消息，而 `REJECT` 发重定向。

79. 下列哪个部分 `iptables` 规则设置了每分钟限制三条日志目的配置？

1. `-m limit 3 -j LOG`
2. `-m limit --limit 3/minute --limit-burst 3 -j LOG`
3. `-m limit --limit 3`
4. `-m limit --limit-minute 3 --burst 3 -j LOG`

80. 下列哪个部分 `iptables` 规则允许入的 ICMP 流量？

1. `-A INPUT -p ICMP -j ACCEPT`
2. `-A IN -P ICMP`
3. `-A INPUT -P ACCEPT-ICMP`
4. `-A IN -P ICMP -j ACCEPT`

81. 下列哪个部分 `iptables` 规则阻止了来自源 IP 192.168.51.50 的所有流量？

1. `-A INPUT -p ALL 192.168.51.50 -j ACCEPT`
2. `-A INPUT -p ALL -s 192.168.51.50 -j DROP`
3. `-A INPUT -p ALL -s 192.168.51.50 -j BLOCK`
4. `-A INPUT -p ALL -f 192.168.51.50 -j DISCARD`

82. 下列哪个部分 `iptables` 规则将允许所有主机连接到 TCP 端口 2222？

1. `-A INPUT -p TCP -s 0/0 --destination-port 2222 -j ACCEPT`
2. `-A TCP -s ALL -p 2222 -j ACCEPT`
3. `-A INPUT -p TCP -s *.* --destination-port 2222 -j ALLOW`
4. `-A INPUT --destination-port */* -j ACCEPT`

83. 下列哪个命令启用了用于 NAT 的转发？

1. `echo "1" > /proc/sys/net/ipv4/nat`
2. `echo "1" > /proc/sys/net/ipv4/ip_forward`
3. `iptables --enable-forwarding`
4. `ip-forward --enable`

84. 在 `fail2ban` 的 jail 配置中，哪个配置选项设置了监控失败的日志文件的名称和位置？

1. `logpath`
2. `monitor`
3. `logfile_mon`
4. `monitor_log`

85. 哪个命令将公钥身份发送到另一台服务器供 SSH 使用？

1. `ssh-key`
2. `ssh-copy-key`
3. `ssh-sendkey`
4. `ssh-copy-id`

86. `/etc/sudoers 中的哪个选项设置了与 `sudo` 相关的管理和安全邮件的目标地址？

1. `mail`
2. `mailto`
3. `secmail`
4. `adminmail`

87. NTP 通信应该通过防火墙允许哪个端口？

1. Port 139
2. Port 119
3. Port 123
4. Port 194

88. 调用 `-a` 时，包含了下列哪些选项？

1. `-rlpt`
2. `-rlgo`
3. `rsync`
4. `-ptD`

89. 你正在寻找与 SSL 相关的文件，它们可能位于哪个目录？

1. `/etc/`
2. `/share/`
3. `/usr/`
4. `/private`

90. 哪个 OpenSSH 指令用于指定允许的用户？

1. `AllowUsers`
2. `PermitUsers`
3. `Allowed`
4. `UsersAllowed`

91. `iptables` 的 `LOG` 目标中的哪个选项设置了将加在前面的字符串？

1. `--log-prefix`
2. `--prepend`
3. `--log-prepend`
4. `--log-str`

92. 在 SELinux 配置中，哪个选项控制策略将使用目标模式？

1. `SEPOLICY`
2. `SELINUXTYPE`
3. `TARGET`
4. `SELINUX`

93. 当 `getenforce` 返回 `Permissive` 时，下列哪项最准确描述 SELinux 的状态？

1. `Permissive` 返回意味着 SELinux 已启用，但未执行规则，尽管 DAC 规则有效。
2. `Permissive` 返回意味着 SELinux 未启用。
3. `Permissive` 返回意味着 SELinux 已启用且未执行规则。
4. `Permissive` 返回意味着 SELinux 正在使用强制策略。

95. 使用 PAM 时，一个标记为 `required` 的模块失败了。下列哪项描述了该领域内其他模块会发生什么？

1. `required` 模块失败时立即停止处理。
2. 处理完所有 `required` 模块后停止处理。
3. 继续直到遇到另一个 `required` 模块。
4. 继续处理其他模块但最终失败。

96. root 账户的 UID 是多少？

1. 1000
2. 0
3. 100
4. 65535

97. 使用如 Google Authenticator 的系统提供双因素认证是哪种类型令牌的示例？

1. 硬件
2. 软件
3. 基于令牌的
4. 基于使用的





### 98. 你需要禁用使用 `Ctrl+Alt+Del` 键组合重启 Linux 计算机的功能。你会在哪个文件中找到此键组合的配置？
1. `/etc/ctrlaltdel`
2. `/etc/shutdown`
3. `/etc/keymap`
4. `/etc/inittab`

### 99. `firewalld` 的预定义区域（zones）位于哪个目录下？
1. `/etc/firewalld/`
2. `/usr/lib/firewalld/zones/`
3. `/usr/firewalld/zones/`
4. `/etc/firewall/zones`

### 100. 你需要为 GRUB 设置引导加载程序密码。为了实现这一点，应该在 `/boot/grub/grub.conf` 中设置以下哪个配置选项？
1. `login`
2. `prompt`
3. `boot-passwd`
4. `password`

### 101. 假设 `sestatus` 命令的输出显示 SELinux 处于 `Permissive` 模式，使用哪个命令可以将将其模式更改为 `Enforcing`？
1. `setenforce en`
2. `setenforce 1`
3. `setenforce on`
4. `setenforce --enable`

### 102. 你的组织使用 `ssh-agent` 进行 SSH 身份验证辅助。可以使用哪个命令将私钥添加到 `ssh-agent`？
1. `ssh-privkey`
2. `ssh-agent-key`
3. `ssh-add`
4. `ssh-addkey`

### 103. 以下哪个命令用于显示给定文件的访问控制列表（ACL）信息？
1. `getfacl`
2. `getacl`
3. `acldisp`
4. `showacl`

### 104. 以下哪个命令可以防止 root 用户在控制台上登录？
1. `echo > /etc/securetty`
2. `echo "NoRootCon" > /etc/securetty`
3. `rm /etc/securetty`
4. `echo "RootCon=no" > /etc/securetty`

### 105. 你需要为通过 SSH 连接的特定主机提供特殊的用户名和其他相关参数。你应该向哪个文件添加这些信息？
1. `~/.ssh/hosts`
2. `~/.ssh/known_hosts`
3. `~/.ssh/config`
4. `~/.ssh/hostconfig`

### 106. 你正在使用 `chmod` 修改几个与 Web 相关的文件，以便 Web 服务器/公共用户读取它们。你应该在 `chmod` 命令中添加哪个选项以使权限继承到其他文件？
1. `-R`
2. `-v`
3. `-i`
4. `-M`

### 107. 以下哪个命令可以用于获取有关 GUID 分区表的更多信息？
1. `guidinfo`
2. `guid -info`
3. `gdisk`
4. `blkguid`

### 108. `setsebool` 的哪个选项会将当前值写入磁盘，以便它们在下次重新启动时生效？
1. `-A`
2. `-P`
3. `-D`
4. `-M`

### 109. 在使用 AppArmor 时，配置文件（profiles）位于哪个目录？
1. `/etc/apparmor/`
2. `/etc/apparmor.d/`
3. `/etc/appa.d/`
4. `/etc/armor.d/`

### 110. 以下哪个协议提供数据报安全（datagram security）？
1. DS
2. DSSL
3. DTLS
4. DLS

### 111. 以下哪个命令显示失败登录尝试的列表？
1. `badlogin`
2. `lastb`
3. `lastf`
4. `flogins`

### 112. 使用 Kerberos 身份认证时，以下哪个命令显示票缓存（ticket cache）？
1. `ktix`
2. `ktel`
3. `kinit`
4. `klist`

### 113. 你怀疑第三方日志代理正在消耗大量的系统资源。以下哪个命令可以帮助诊断此问题？
1. `ps aux | grep <agent>`
2. `uptime`
3. `sysreport <agent>`
4. `psrep`

### 114. `ls` 命令的哪个选项显示所有权和权限信息？
1. `-m`
2. `-l`
3. `-b`
4. `-f`

### 115. `getsebool` 的哪个选项返回整个 SELinux 布尔值的完整列表？
1. `-a`
2. `-b`
3. `-c`
4. `-d`

### 116. 哪个 AppArmor 命令使用 `netstat` 来确定没有 AppArmor 配置配置文件的网络相关进程？
1. `aa-profiles`
2. `aa-netstat`
3. `aa-unconfined`
4. `aa-netlist`

### 117. 哪个组可以限制执行 `su` 命令的访问？
1. `super`
2. `admins`
3. `wheel`
4. `runsu`

### 118. 你需要更改文件的 SELinux 安全上下文。应该使用以下哪个命令来实现此目的？
1. `setcontext`
2. `esecon`
3. `chcon`
4. `setcon`

### 119. 以下哪是基于 SSL 的 VPN 客户端的优点？
1. 传输层可能绕过阻止 VPN 流量的防火墙。
2. 使用 `SSL` 使默认配置更简单。
3. 使用 `SSL` 意味着不需要配置密钥。
4. 使用 `SSL` 没有区别。

### 120. 在 Red Hat 系统上配置 PKI 时，当使用 `RSA` 作为密钥类型时，哪些哈希算法可用？
1. `SHA256withRSA`
2. `MD4`
3. `SHA2048`
4. `SHA1withEC`

### 121. 哪种类型的备份捕获自上次备份的变化并仅备份已更改的文件？
1. `Full`（全量）
2. `Snapshot`（快照）
3. `Incremental`（增量）
4. `Image`（镜像）

### 122. 组织中的两个个人共享同一个管理员账户的用户名和密码。这违反了哪项最佳实践？
1. `Integrity`（完整性）
2. `Availability`（可用性）
3. `Shared IDs`（共享 ID）
4. `Password policy`（密码策略）

### 123. 以下哪个密码可以用于保护系统，使得即使攻击者有物理访问并在计算机中插入 USB 启动盘，系统也不会启动？
1. `GRUB password`（GRUB 密码）
2. `UEFI/BIOS password`（UEFI/BIOS 密码）
3. `Root password`（Root 密码）
4. `SHA1 password`

### 124. 以下哪项可以用于 Linux 以提供生物识别认证？
1. `finger`
2. `fprint`
3. `bio`
4. `freader`

### 125. `restorecon` 工具的哪个选项可以在不做出更改的情况下查看当前上下文？
1. `-n`
2. `-r`
3. `-g`
4. `-p`

### 126. 你需要允许用户编辑一个由 root 拥的文件。假设使用 `sudo` 执行命令，应该使用以下哪个命令来实现目的？
1. `vim`
2. `nano`
3. `sudoedit`
4. `visudo`

### 127. 你需要查看系统中进程的 SELinux 上下文。以下哪个命令可以完成此任务？
1. `showcon`
2. `proccon`
3. `lcon -Z`
4. `ps -Z`

### 128. 哪个 PAM 模块可以在登录失败后锁定账户？
1. `pam_lock`
2. `pam_tally2`
3. `pam_loginlock`
4. `pam_watchlog`

### 129. 哪种 VPN 通常用于客户端到服务器的流量？
1. `Tunnel`（隧道）
2. `Transport`（传输）
3. `Site-to-Site`（站点站点）
4. `Site-to-Server`（站点到服务器）

### 130. Linux 中指示伪终端的设备命名规范是什么？
1. `/dev/ttyS0`
2. `/dev/ttyP0`
3. `/dev/pty`
4. `/dev/tys`

### 131. 以下哪个命令将所有 AppArmor 配置文件放入抱怨模式（complain mode）？
1. `aa-complain /etc/apparmor.d/*`
2. `aa-enable-complain /etc/apparmor.d/*`
3. `aa-enable-complain /etc/apparmor/*`
4. `aa-complain /etc/apparmor/*`

### 132. 以下哪个日志用于存储与身份验证和授权相关？
1. `/var/log/sec.log`
2. `/var/log/messages`
3. `/var/log/kern.log`
4. `/var/log/secure`

### 133. `sshd_config` 文件中的哪个选项控制 root 用户是否可以通过 SSH 直接登录？
1. `PermitRoot`
2. `PermitRootLogin`
3. `RootDirectLogin`
4. `AllowRootLogin`

### 134. RADIUS 为远程登录提供 AAA 服务。AAA 指的是什么？
1. Authentication, Authorization, Availability（身份验证、授权、可用性）
2. Authentication, Authorization, AppArmor
3. Authentication, Authorization, Assistance（身份验证、授权、协助）
4. Authentication, Authorization, Accounting（身份验证、授权、审计）





### 135. `firewall-cmd` 命令的哪个选项可以将当前的运行时配置设置为在计算机下次重启后仍然可用？

1. `--set-perm`
2. `--make-perm`
3. `--runtime-to-permanent`
4. `--current-to-persistent`

### 136. 你的一个客户需要传输一个大文件，并要求在服务器上启用 FTP。考虑到安全性，你可以提供哪些更安全的候选项？

1. `USB`
2. `Email (SMTP)`
3. `SSL`
4. `SFTP`

### 137. 你应该使用哪个网站来监控通过 CVE 流程报告的新型安全通告？

1. 新闻网站
2. `https://cve.mitre.org`
3. `https://www.example.com`
4. 供应商网站

### 138. 在使用 `ufw` 时，你需要允许 SSH 流量。以下哪个命令可以实现这一场景？

1. `ufw allow tcp/22`
2. `ufw enable ssh`
3. `ufw allow ssh`
4. `ufw enable tcp/21-22`

### 139. 哪个守护进程可以监控系统文件发生的变化？

1. `end`
2. `alogd`
3. `auditd`
4. `mond`

### 140. 你需要为企业网络内的路由器和交换机等各种网络组件提供身份验证。可以将哪个身份验证服务添加到 Linux 服务器上来实现这一场景？

1. `SSH`
2. `Kerberos`
3. `TACACS+`
4. `Telnet`

### 141. 以下哪项是与 Netfilter 相关的防火墙控制软件的名称？

1. `iptables`
2. `ipt`
3. `netfw`
4. `netfilterfw`

### 142. 你需要从旧版本 HPUX 创建的备份中提取文件。`tar` 命令似乎对这些文件不起作用。以下哪个工具可能从此备份中提取文件？

1. `gzip`
2. `bzip2`
3. `cpio`
4. `hpb`

### 143. 使用 `scp` 复制文件时，防火墙需要开放哪个端口？

1. `TCP/21`
2. `TCP/22`
3. `TCP/20` 和 `TCP/21`
4. `UDP/53`

### 144. 你使用 `ls` 命令查看目录内容，但看不到以单个点 (`.`) 开头的文件。`ls` 的哪个选项可以显示这些文件？

1. `-a`
2. `-b`
3. `-c`
4. `-d`

### 145. 你认为系统已被入侵且文件可能已被更改。在脱离系统并卸载受影响的分区之一后，你可以做什么？

1. 使用 `dd` 创建分区的镜像以进行保存。
2. 使用 `tar` 创建备份。
3. 使用 `fdisk` 检查分区。
4. 使用 `mkfs` 重新格式化分区。

### 146. SSH 的哪个选项指定了用于身份验证的私钥？

1. `-m`
2. `-i`
3. `-k`
4. `-a`

### 147. 哪个实用程序可以创建文件的校验和以确保其完整性？

1. `sha1sum`
2. `mdsum`
3. `shasum`
4. `shacheck`

### 148. `zip` 命令的哪个选项会导致命令遍历目录？

1. `-g`
2. `-m`
3. `-r`
4. `-a`

### 149. 你正在一个 Debian 系统上工作，需要设置文件的所有权，使得执行 Apache 的用户可以写入该文件。可以使用哪个命令来确定 Apache 以哪个用户身份运行？

```bash
ps auwx | grep apache
```
2. `ls -a`
3. `free | grep httpd`
4. `monapache`

### 150. 你发现 Apache 进程的所有者是 `www-data`。哪个命令可以更改名为 `<filename>` 的文件的所有权，使得 `www-data` 可以写入该文件？

```bash
chown www-data <filename>
```
2. `chown apache-www-data <filename>`
3. `chmod www-data +w <filename>`
4. `chmod www-data.apache <filename>`

### 151. 在脚本环境中使用 `sudo` 时，哪个选项可以指定非交互模式？

1. `-f`
2. `-m`
3. `-n`
4. `-l`

### 152. telnet 运行在哪个端口上？

1. `TCP/22`
2. `TCP/20`
3. `TCP/100`
4. `TCP/23`

### 153. 哪个命令用于关闭 AppArmor 配置文件？

1. `aa-disable`
2. `aa-turnoff`
3. `aa-enable -d`
4. `aa-off`

### 154. 使用哪个命令和选项查看给定文件的 SELinux 安全上下文？

1. `ls -context`
2. `file -Z`
3. `ls -Z`
4. `sel -context`

### 155. Linux 中可以通过以下哪些命令提供数字签名？

1. `gds`
2. `gpg`
3. `dmc`
4. `gds2`

### 156. 你需要对系统更改。与其编辑全局配置，哪个目录包含了这些设置？

1. `/etc/apparmor.d`
2. `/etc/apparmor`
3. `/etc/apparmor/d`
4. `/etc/tunables`

### 157. 以下哪项是与 Netfilter 相关的防火墙控制软件的名称？

1. `iptables`
2. `ipt`
3. `netfw`
4. `netfilterfw`

### 158. 哪个守护进程可以监控系统文件发生的变化？

1. `end`
2. `alogd`
3. `auditd`
4. `mond`

### 159. 哪个命令用于关闭 AppArmor 配置文件？

1. `aa-disable`
2. `aa-turnoff`
3. `aa-enable -d`
4. `aa-off`

### 160. 使用哪个命令和选项查看给定文件的 SELinux 安全上下文？

1. `ls -context`
2. `file -Z`
3. `ls -Z`
4. `sel -context`

*(注：由于输入文本中存在重复和逻辑错乱，上述部分已根据核心语义进行了去重与排版)*





1. `pam_fileauth.so`
2. `pam_listfiles.so`
3. `pam_filesauth.so`
4. `pam_fileauth.so`

173. `ssh-keygen` 的哪个选项用于设置将创建的密钥类型？
1. `-k`
2. `-t`
3. `-e`
4. `-i`

# 第 4 章

Linux 故障排除与诊断

本章涵盖了以下 CompTIA LINUX+ 考试目标：

## ![images](img/correction.png)  4.1 给定场景，分析系统属性并进行相应的修复

### 网络监控与配置
- 延迟
    - 带宽
    - 吞吐量
- 路由
- 饱和度
- 丢包
- 超时
- 域名解析
- Localhost 对 Unix 套接字
- 适配器
    - RDMA 驱动
- 接口配置
- 命令
    - `nmap`
    - `netstat`
    - `iftop`
    - `route`
    - `iperf`
    - `tcpdump`
    - `ipset`
- Wireshark
    - `tshark`
- `netcat`
- `traceroute`
- `mtr`
- `arp`
- `nslookup`
- `dig`
- `host`
- `whois`
- `ping`
- `nmcli`
- `ip`
- `tracepath`

### 存储监控与配置
- `iostat`
- `ioping`
- I/O 调度
    - `cfq`
    - `noop`
    - `deadline`
- `du`
- `df`
- LVM 工具
- `fsck`
- `partprobe`

### CPU 监控与配置
- `/proc/cpuinfo`
- `uptime`
- 负载平均 (loadaverage)
- `sar`
- `sysctl`

### 内存监控与配置
- `swapon`
- `swapoff`
- `mkswap`
- `vmstat`
- 内存溢出杀进程 (OOM killer)
- `free`
- `/proc/meminfo`
- 缓冲区缓存输出

### 丢失 root 密码
- 单用户模式

## ![images](img/correction.png)  4.2 给定场景，分析系统进程以优化性能

### 进程管理
- 进程状态
    - 僵尸进程 (Zombie)
        - 不可睡眠
        - 可中断睡眠
        - 运行中
- 优先级
- 杀死信号
- 命令
    - `nice`
    - `renice`
    - `top`
    - `ps`
    - `lsof`
    - `pgrep`
    - `pkill`
- 进程 ID (PIDs)

## ![images](img/correction.png)  4.3 给定场景，分析并排除用户问题

### 权限
    - 文件
    - 目录
- 访问
    - 本地
    - 远程
- 身份验证
    - 本地
    - 外部
    - 策略违反
- 文件创建
    - 配额
    - 存储
    - Inode 耗尽
    - 不变文件
- 授权权限不足
    - SELinux 违反
- 环境和 shell 问题

## ![images](img/correction.png)  4.4 给定场景，分析并排除应用程序和硬件问题

### SELinux 上文违反
### 存储
    - 降级存储
    - 缺少设备
    - 缺少卷
    - 缺少挂载点
    - 性能问题
    - 资源耗尽
    - 适配器
        - SCSI
        - RAID
        - SATA
        - HBA
            - `/sys/class/scsi_host/host#/scan`
    - 存储完整性
        - 坏块
### 防火墙
    - 限制性 ACL
    - 阻塞的端口
    - 阻塞协议
### 权限
    - 所有权
    - 可执行文件
    - 继承
    - 服务账户
    - 组组成
### 依赖关系
    - 补丁
    - 更新问题
    - 版本
    - 库
    - 环境变量
    - GCC 兼容性
    - 仓库
### 排除其他硬件问题
    - 内存
    - 打印机
    - 视频
        - GPU 驱动
    - 通信端口
    - USB
    - 键盘映射
    - 硬件或软件兼容性问题
    - 命令
        - `dmidecode`
        - `lshw`

1. 你正在排查存储设备的故障。以下哪个可能的设备名称？
1. `/dev/hd`
2. `/dev/sata`
3. `/dev/sd`
4. `/dev/ata`

2. 你正在排查与 USB 相关的问题。使用哪个命令列出 USB 设备？
1. `list`
2. `usb`
3. `usb-list`
4. `ls`

3. 你丢失了密码并需要进入单用户模式。以下哪个会启动系统？
1. `single-user`
2. `su`
3. `single`
4. `root`

4. 未检测到磁盘。以下哪项是较良好的第一步？
1. 拔掉磁盘。
2. 检查系统。
3. 重启服务。
4. 运行 `disk-detect`。

5. 你最近添加了一个 DVD 驱动器，现在系统无法启动。可能的原因是什么？
1. BIOS 将 DVD 识别为第一个磁盘。
2. 硬盘在安装时损坏了。
3. BIOS 中未启用热插拔选项。
4. 计算机未检测到 DVD 驱动器，需要启用。

6. 你连接了一个 USB 磁盘并需要找到它的设备。以下哪种是执行此任务的最佳方法？
1. 重启系统
2. 查看 `/var/log/usb` 内容
3. 将驱动器连接到一个知道编号的 USB 端口
4. 运行 `dmesg`

7. 每个总线支持多少 SCSI 设备？
1. 7 到 15
2. 2 到 4
3. 12
4. 4

8. 使用哪个命令更新共享库的链接和缓存？
1. `ldcache`
2. `cache-update`
3. `link-update`
4. `ldconfig`

9. 使用哪个命令和选项将 Debian 系统更新到最新软件？
1. `apt-update`
2. `apt-get upgrade`
3. `dpkg -U`
4. `apt-cache clean`

10. 给 `yum` 命令的哪个选项将安装软件包？
1. `update`
2. `configure`
3. `install`
4. `get`

11. 使用 bash shell 时，以下哪个命令将 `/usr/local/lib` 添加到 `LD_LIBRARY_PATH`？
1. `set PATH=/usr/local/lib`
2. `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib`
3. `LD_LIBRARY_PATH=/usr/local/lib`
4. `connectpath LD_LIBRARY_PATH=/usr/local/lib`





### 13. 在哪个目录下可以找到 Yum 使用的存储库？

1. `/etc/yum.conf`
2. `/etc/repos`
3. `/etc/yum.conf.d`
4. `/etc/yum.repos.d`

### 14. 使用哪个命令可以确定给定命令依赖于哪些库？

1. `ldconfig`
2. `librarylist`
3. `listdeps`
4. `ldd`

### 15. 关于 Linux 交换空间（swap space），以下哪项是正确的？

1. Swap 用于存放临时数据库表。
2. 当 RAM 不够用时，Swap 用作额外的内存使用。
3. Swap 邮件服务器用于安全性。
4. Swap 用于临时从网络清除数据。

### 16. 下列哪项通常不用于存储库？

1. `/lib`
2. `/etc/lib`
3. `/usr/lib`
4. `/usr/local/lib`

### 17. 你正尝试从仓库在 Debian 系统上安装新软件包。该软件包似乎不存在。以下哪个命令可以更新 Debian 系统的软件包缓存？

1. `apt-get cache-update`
2. `apt-cache update`
3. `apt-get update`
4. `apt-get upgrade`

### 18. Debian 系统中，当前软件包存储库的详细存储在哪个文件中？

1. `/etc/apt.list`
2. `/etc/sources.list`
3. `/etc/apt/sources.list`
4. `/etc/apt.d/sources.list`

### 19. 哪个命令可以初始化物理磁盘分区以供 LVM 使用？

1. `lvmcreate`
2. `pvcreate`
3. `fvcreate`
4. `lvinit`

### 20. 使用哪个命令可以创建 LVM 逻辑卷？

1. `pvcreate`
2. `lvmcreate`
3. `lvcreate`
4. `volcreate`

### 21. 创建 LVM 逻辑卷的逻辑顺序是什么？

1. 物理卷创建、卷组创建、逻辑卷创建
2. 物理卷创建、逻辑卷创建、卷组创建
3. 逻辑卷创建、物理卷创建、卷组创建
4. LVM 创建、格式化、分区

### 22. `yum` 的哪个选项可以执行软件包缓存搜索？

1. `seek`
2. `query`
3. `--search`
4. `search`

### 23. `rpm` 的哪个命令选项可以显示内核版本？

1. `rpm kernel`
2. `rpm -q kernel`
3. `rpm search kernel`
4. `rpm --list kern`

### 24. `/etc/yum.conf` 中的哪个选项用于确保在系统更新时不更新内核？

1. `exclude=kernel*`
2. `exclude-kernel`
3. `updatekernel=false`
4. `include-except=kernel`

### 25. Linux 系统应该创建哪种类型的分区（非交换分区）？

1. 82
2. 83
3. 84
4. L

### 26. 哪个命令可以在 Debian 系统上搜索并提供有关给定软件包的信息，包括该软件包当前是否已安装？

1. `dpkg -i`
2. `dpkg -s`
3. `apt-cache`
4. `apt-info`

### 27. 哪个命令用于搜索供 LVM 使用物理卷？

1. `lvmcreate`
2. `pvcreate`
3. `lvmdiskscan`
4. `lvmscan`

### 28. 下列哪项可以安装之前下载的 Debian 软件包？

1. `dpkg -i <package name>`
2. `apt-install <package name>`
3. `apt-slash <package name>`
4. `dpkg -U <package name>`

### 29. 你正在排查用户报告的问题，并怀疑可能与他们的环境变量有关。在使用 bash 时，用户应该运行哪个命令来查看其当前的环境设置？

1. `environment`
2. `env`
3. `listenv`
4. `echoenv`

### 30. 你需要编写一个脚本来收集系统上运行的所有 Apache 实例的进程 ID（PID）。以下哪个命令可以完成此任务？

1. `ps auwx | grep apache`
2. `pgrep apache`
3. `processlist apache`
4. `ls -p apache`

### 31. 用户报告各种程序在服务器上崩溃。检查日志时，你看到某些进程报告内存溢出（out-of-memory）。你可以使用哪个命令来查看整体内存？

1. `tree`
2. `pgrep`
3. `uptime`
4. `free`

### 32. 哪个命令可以确定自上次启动以来的时间？

1. `uptime`
2. `sysinfo`
3. `bash`
4. `u`

### 33. 你需要在后台启动一个进程。以下哪个命令用于将将其调至前台？

1. `fg`
2. `bg`
3. `kill`
4. `screen`

### 34. 哪个命令可以更改进程的优先级？

1. `nice`
2. `renice`
3. `priority`
4. `prio`

### 35. 哪个命令可以显示运行作业的列表？

1. `jobs`
2. `ps`
3. `kill`
4. `free`

### 36. 哪个命令可以更改主机名？

1. `hostnamectl`
2. `setname`
3. `hostname`
4. `changehost`

### 37. 在 ext3 文件系统上运行 `fsck` 时，耗的时间比预期长。可以给 `fsck` 添加什么选项来自动修复错误？

1. `-y`
2. `-V`
3. `-o`
4. `-f`

### 38. 哪个命令允许将文件系统挂载为只读？

1. `mount -o ro`
2. `tune2fs`
3. `remount`
4. `mount`

### 39. 你正在使用一个经常报错存储区域网络（SAN）。你可以使用哪个命令和选项重新挂载文件系统？

1. `mount -o remount`
2. `tune2fs`
3. `mkfs`
4. `mount`

### 40. 哪个命令用于格式化交换分区？

1. `fdisk`
2. `mkswap`
3. `format`
4. `s`

### 41. 系统主目录磁盘空间不足，且未启用配额。你可以使用哪个命令确定可能包含大文件的目录？

1. `du`
2. `df`
3. `ls`
4. `locate`

### 42. 在文件系统上设置哪个选项以启用用户配额？

1. `quotaon`
2. `enquota=user`
3. `usrquota`
4. `userquota`

### 43. `quotacheck` 的哪个选项用于首次创建文件？

1. `-f`
2. `-u`
3. `-m`
4. `-c`

### 44. 在 bash 脚本的 `if` 条件中，以下哪个测试可以确定文件是否存在并可被执行测试的用户读取？

1. `-e`
2. `-s`
3. `-a`
4. `-r`

### 45. 在配置本地用户访问时，LightDM 通常允许访客登录。SeatDefaults 中的哪个配置选项可以禁用访客？

1. `guest-login=false`
2. `guest=false`
3. `allowg=false`
4. `allow-guest=false`

### 46. 下列哪个命令允许名为 `cwa` 的主机连接到 X 服务器？

1. `xconnect cwa`
2. `xterm +cwa`
3. `xhost +cwa`
4. `xf cwa`
### 47. 如果不允许用户交互式登录计算机，用户账户可以设置到哪个 shell 中？

1. `/bin/bash`
2. `/bin/tcsh`
3. `/bin/zsh`
4. `/bin/false`





## 48. 在排查磁盘使用情况时，使用哪个命令可以确定 systemd journal 日志文件使用的磁盘空间？

1. `journalctl --disk`
2. `journalctl -du`
3. `journalctl --disk-usage`
4. `journalctl -ls`

## 49. 你在服务器接口上遇到了困难，且该接口目前处于关闭状态。假设设备本身没有硬件故障，你可以使用哪个命令和选项来显示接口信息？

1. `ifconfig -a`
2. `ifup`
3. `netstat -n`
4. `ifconfig`

## 50. 下列哪个不被用内部、非互联网使用的私有地址？

1. 172.16.4.2
2. 192.168.40.3
3. 10.74.5.244
4. 143.236.32.231

## 51. 下列哪个命令为接口 eth0 添加了默认网为 192.168.1.1？

1. `route add default gateway 192.168.1.1 eth0`
2. `eth0 --dg 192.168.1.1`
3. `route add default gw 192.168.1.1 eth0`
4. `route define eth0 192.168.1.1`

## 52. `host` 命令的哪个选项会查询给定域名的权威名称服务器？

1. `-t ns`
2. `-t all`
3. `-ns`
4. `-named`

## 53. `ping` 命令的哪个选项允许你选择生成 ICMP 数据包的接口？

1. `-i`
2. `-I`
3. `-t`
4. `-a`

## 54. 下列哪个命令用于域名 `example.com` 域名的邮件服务器？

1. `dig example.com mx`
2. `dig example.com`
3. `host -t smtp example.com`
4. `dig example.com smtp`

## 55. `traceroute` 命令的哪个选项将使用 TCP SYN 数据包进行路径追踪？

1. `-T`
2. `-t`
3. `-s`
4. `-i`

## 56. 哪个命令可以监听网络上的 netlink 消息？

1. `ip monitor`
2. `netlink -a`
3. `ip netlink`
4. `route`

## 57. 下列哪个 `dig` 命令会将对 `example.com` 的查询直接发送到 192.168.2.5 服务器，而不是发送本地配置的解析器？

1. `dig example.com @192.168.2.5`
2. `dig -t 192.168.2.5 example.com`
3. `dig -s 192.168.2.5 example.com`
4. `dig server=192.168.2.5 example.com`

## 58. 下列哪个命令将列出 `hosts` 数据库？

1. `getent hosts`
2. `gethosts`
3. `nslookup`
4. `host`

## 59. 下列哪个配置行将使用 `/etc/resolv.conf` 将 DNS 服务器设置为 192.168.1.4？

1. `dns 192.168.1.4`
2. `dns-server 192.168.1.4`
3. `nameserver 192.168.1.4`
4. `name-server 192.168.1.4`

## 60. 下列哪个命令为服务器添加网络 192.168.51.0/24 的路由，通过其网关 192.168.51.1？

1. `route add -net 192.168.51.0 netmask 255.255.255.0 gw 192.168.51.1`
2. `route add -net 192.168.51/24 gw 192.168.1.51`
3. `route -net 192.168.51.0/24 192.168.51.1`
4. `route add 192.168.51.1 -n 192.168.51.0//255.255.255.0`

## 61. 下列哪个命令显示当前正在监听套字以及未监听套字的网络服务？

1. `netstat -a`
2. `netlink -a`
3. `sockets -f`
4. `opensock -l`

## 62. 下列哪个代表 `/etc/hosts` 的正确配置行？

1. `192.168.1.4 cwa.braingia.org cwa`
2. `cwa.braingia.org cwa 192.168.1.4`
3. `cwa.braingia.org 192.168.1.1 alias cwa`
4. `alias cwa.braingia.org cwa 192.168.1.4`

## 63. 下列哪个命令将 eth0 设备配置为 IP 地址 192.168.1.1 并位于 /24 网络中？

1. `ifconfig eth0 192.168.1.1/24`
2. `ifconfig eth0 192.168.1.1/255.255.255.0`
3. `ifconfig eth0 192.168.1.1 netmask 255.255.255.0`
4. `ifconfig 192.168.1.1 netmask 255.255.255.0 eth0`

## 64. 下列哪个命令将使用 `eth0` 将默认网关更改为 192.168.1.1？

1. `ip route default gw 192.168.1.1`
2. `ip route change default via 192.168.1.1 eth0`
3. `ip route default update 192.168.1.1`
4. `ip route update default 192.168.1.1 eth0`

## 65. 在排查 SSH 连接超时的问题时，你认为防火墙正在阻止连接。下列哪个端口用于安全外壳（Secure Shell）通信？

1. `TCP/23`
2. `TCP/25`
3. `TCP/22`
4. `TCP/2200`

## 66. `netcat` 的哪些选项会创建一个在端口 8080 上监听的服务器？

1. `netcat -p 8080`
2. `nc -l -p 8080`
3. `nc -p 8080`
4. `nc -s 8080`

## 67. 下列哪个命令显示域名 `example.com` 的起始权威信息（Start of Authority）？

1. `dig example.com soa`
2. `dig example.com authority`
3. `dig example.com -auth`
4. `dig -t auth example.com`

## 68. 假设你想允许本地客户端服务直接访问网络上的主机，而不需要通过为 `example.com` 或 `example.org` 添加域名来完全限定名称/etc/resolv.conf` 中的哪个选项将提供此功能？

1. `search`
2. `domain`
3. `local-domain`
4. `local-order`

## 69. 下列哪个命令阻止流量到达主机 192.168.1.3？

1. `route add -host 192.168.1.3 reject`
2. `route -nullroute 192.168.1.3`
3. `route add -nullroute 192.168.1.3`
4. `route -block 192.168.1.3`

## 70. 下列哪项描述了 `traceroute` 和 `tracepath` 之间的区别？

1. `traceroute` 命令需要 root 权限。
2. `tracepath` 命令提供每个跳的 MTU。
3. `tracepath` 不能用于外部网络。
4. `traceroute` 命令不支持 IPv6。

## 71. 下列哪个命令在 Windows 中模拟 `ping` 命令，并在发送四个数据包后退出？

1. `ping -n`
2. `ping -t`
3. `ping -p`
4. `ping -c`

## 72. 你使用 `dig` 命令排查 DNS 问题并收到“status: NXDOMAIN”消息。下列哪项描述了 NXDOMAIN 的含义？

1. NXDOMAIN 表示你收到了非权威答案。
2. NXDOMAIN 表示找不到域或主机。
3. NXDOMAIN 表示查询成功。
4. NXDOMAIN 表示已添加新的记录。

## 73. 在执行 `ip route` 之后应该执行哪个命令？

1. `ip route flush`
2. `ip route reload`
3. `ip route cache reload`
4. `ip route restart`

## 74. 使用 `dig` 发送 SPF 记录的 DNS 查询应该使用哪个选项？

1. `-t txt`
2. `-t spf`
3. `-t mx`
4. `-t mailspf`

## 75. 在排查连接问题时，你发现可以通过 Web 访问服务器但无法 ping 它。下列描述了可能的原因？

1. 防火墙阻止了 TCP 流量。
2. DNS 查找失败。
3. ICMP 流量被阻止。
4. 存在拒绝路由。

## 76. 使用 `route` 命令查看可用路由时，一条路由包含标志 `UG`，而其他包含 `U`。路由表中字母 `G` 表示什么？

1. `G` 表示路由是良好的。
2. `G` 表示路由不可用。
3. `G` 表示这是一个网关。
4. `G` 表示该路由是聚合的。

## 77. 下列哪个命令向 192.168.1.4 服务器请求 `example.org` 的区域传输？

1. `dig example.org @192.168.1.4 axfr`
2. `dig example.org @192.168.1.4`
3. `dig example.org @192.168.1.4 xfer`
4. `dig example.org #192.168.1.4 xfer`





### 78. 你需要临时防止用户通过 SSH 或其他手段登录系统。以下哪项描述了实现此任务的方法？

1. `touch /etc/nologin`
2. 禁用 `sshd`。
3. 移除 `/etc/login`。
4. 添加一个 shadow 文件。

### 79. 下面哪个命令会在整个文件系统中搜索搜索设置了 `setuid` 位的文件？

1. `find ./ -perm suid`
2. `find / -perm 4000`
3. `find / -type suid`
4. `find / -type f -perm setuid`

### 80. 下面哪个命令可以扫描 IP 地址 192.168.1.154 的开放端口？

1. `nmap 192.168.1.154`
2. `lsof 192.168.1.154`
3. `netstat 192.168.1.154`
4. `netmap 192.168.1.154`

### 81. 下面哪个配置选项在 `/etc/security/limits.conf` 中为名为 suehring 的用户设置 25 个进程的硬限制？

1. `suehring hard proc 25`
2. `suehring hard nproc 25`
3. `suehring proc 25 hard-limit`
4. `proc 25 suehring hard`

### 82. 下面哪个命令可以显示当前打开的端口以及使用该端口的进程？

1. `netstat -a`
2. `lsof -i`
3. `ps auwx`
4. `netlist`

### 83. 你正在使用 `nmap` 扫描主机的开放端口。然而，服务器拦截了 ICMP 回显请求。你可以设置 `nmap` 的哪个选项来继续扫描？

1. `-P0`
2. `-no-ping`
3. `-s0`
4. `-ping-0`

### 84. `/etc/security/limits.conf` 中的哪个选项用于控制给定账户同时登录的次数？

1. `nlogins`
2. `loginmax`
3. `maxlogins`
4. `loginlimit`

### 85. `nmap` 的哪个选项设置扫描使用 TCP SYN 数据包来查找开放端口？

1. `-sS`
2. `-sT`
3. `-sY`
4. `-type SYN`

### 86. 下面哪个命令在服务器中搜索启用了 `setgid` 位的文件？

1. `find / -perm 4000`
2. `find ./ -perm setgid`
3. `grep setgid *`
4. `find / -perm 2000`

### 87. 使用 `iostat` 评估性能时，哪个选项会按分区显示块设备的信息？

1. `-a`
2. `-c`
3. `-d`
4. `-p`

### 88. 下面哪个命令可以显示与 I/O 相关的输入数据块（blocks in）和输出数据块（blocks out）？

1. `iorpt`
2. `iptraf`
3. `vmswap`
4. `vmstat`

### 89. 下面哪个命令可以显示当前登录用户列表以及当前负载平均值和自上次重启以来经过的时间？

1. `uptime`
2. `w`
3. `swap`
4. `sysinfo`

### 90. 下面哪项描述了在在使用 `top` 命令时更改排序顺序的方法，使得内存占用最高的用户显示在列表顶部？

1. 在 `top` 中，输入 `o` 然后选择 `mem`。
2. 在 `top` 中，按 Shift+F，滚动到 %MEM，按 S 选择，然后按 Q 退出。
3. 在 `top` 中，按 S 然后选择 %MEM。
4. 在 `top` 中，按 Shift+S，选择 %MEM，然后按 Q 退出。

### 91. 下面哪个监控工具可以使用 SNMP 和脚本来收集数据，用于吞吐量和带宽等性能相关图表的绘图？

1. `ptop`
2. `pstree`
3. Cacti
4. Grafr

### 92. 哪个 `swapon` 选项会静默跳不存在的交换分区？

1. `-u`
2. `-e`
3. `-i`
4. `-o`

### 93. `fsck` 命令的哪个选项会导致即使文件系统被标记为清洁（clean）也会运行检查？

1. `-f`
2. `-m`
3. `-a`
4. `-c`

### 94. 下面哪个命令可以停用交换空间？

1. `swapoff`
2. `swap -off`
3. `unmountswap`
4. `uswap`

### 95. 下面哪个 `swapon` 选项显示交换空间的大小及其已用空间？

1. `--list`
2. `-a`
3. `--show`
4. `-h`

### 96. 下面哪个命令可以显示 LVM 设置中给定物理卷的信息？

1. `pvdisp`
2. `pvlist`
3. `pvdisplay`
4. `pvl`

### 97. 下面哪个命令查找参与 LVM 配置的 LVM 物理卷和卷组？

1. `vgscan`
2. `lvmscan`
3. `lvlist`
4. `pvlist`

### 98. 下面哪个命令用于显示参与 LVM 的物理卷列表？

1. `pvdisp`
2. `pvlist`
3. `pvscan`
4. `pvmm`

### 99. 使用 `ip` 命令时，如果没有另行指定，默认使用哪个协议族？

1. `tcpip` 
2. `ip`
3. `inet`
4. `arp`

### 100. 你正在使用 `route` 命令查看路由。然而，名称解析花费很长时间，导致 `route` 命令的响应延迟。可以添加 `route` 的哪个选项使其不执行名称解析？

1. `-d`
2. `-e`
3. `-f`
4. `-n`

### 101. 你替换了网络上的一个设备，但使用了来自另一个活动设备的 IP。可以运行哪个命令从计算机中删除 MAC 地址条目，使其重新执行地址解析？

1. `arp -d`
2. `netstat -rn`
3. `hostname`
4. `dig`

### 102. 在解析 `ip` 的输出时，哪个选项可以像 `grep` 那样删除换行？

1. `-n`
2. `-o`
3. `-l`
4. `-f`

### 103. `arp` 命令的哪个选项为给定的地址创建新条目？

1. `-s`
2. `-c`
3. `-d`
4. `--add`

### 104. `tcpdump` 的哪个选项显示了 `tcpdump` 可以操作的可用接口列表？

1. `-a`
2. `-d`
3. `-D`
4. `-i`

### 105. `nmap` 的哪个选项将始终执行名称解析？

1. `-n`
2. `-R`
3. `-b`
4. `-a`

### 106. 下面哪个命令可以近乎实时提供每个跳数的实时 `traceroute`？

1. `traceroute --live`
2. `mtr`
3. `route -update`
4. `liveroute`

### 107. 你正在使用本地数组并调查性能问题。在监控模式下使用 `mdadm` 时，哪个选项设置间隔？

1. `--delay`
2. `--internal`
3. `--interval`
4. `--poll`

### 108. 在查看 `traceroute` 结果时，你看到 `!H`。`!H` 指的是什么？

1. 网络不可达（Network unreachable）
2. 主机可用（Host available）
3. 主机不可达（Host unreachable）
4. 高长度（High length）

### 109. 假设内核中已启用策略路由，`ping` 命令的哪个选项可以标记发出的请求，以指示数据包根据特定策略进行处理？

1. `-m`
2. `-a`
3. `-p`
4. `-k`

### 110. 在检查磁盘可能的坏块时，`fsck` 的哪个选项会在完成 `fsck` 操作后报告 CPU 时间统计信息？

1. `-s`
2. `-r`
3. `-l`
4. `-f`

### 111. 下面哪个文件提供了空空内存、缓冲区、缓存以及若干其他项目的内存利用率信息？

1. `/proc/cpuinfo`
2. `/proc/memtime`
3. `/proc/memuse`
4. `/proc/meminfo`

### 112. `nmap` 的哪个扫描模式提供 Xmas 扫描？

1. `-sT`
2. `-sS`
3. `-sP`
4. `-sX`

### 113. `tcpdump` 的哪个选项设置捕捉数据包的快照长度

1. `-s`
2. `-l`
3. `-d`
4. `-c`

### 114. `ping` 命令在哪个端口运行 ICMP 回显请求？

1. 53
2. 1337
3. 33433
4. ICMP 不使用端口。

### 115. 在运行 `df` 命令时，你需要更改比例，使报告以太字节（TB）而不是字节显示。哪个选项可以完成此任务？

1. `-ST`
2. `-BT`
3. `-j`





### 4. `-T`

### 116. `mke2fs` 的哪个选项用于在创建文件系统时检查坏块？
1. `-a`
2. `-b`
3. `-c`
4. `-d`

### 117. `ping` 命令的哪个选项显示延迟而不是往返时间？
1. `-L`
2. `-i`
3. `-U`
4. `-d`

### 118. 下面中哪个命令被用于测量网络吞吐量？
1. `tp`
2. `iperf`
3. `ith`
4. `ithrough`

### 119. 你想在 Linux 服务器上实时监控中断使用情况，以排查通信端口的使用。以下哪个命令可以用于此目的？
1. `int`
2. `moni`
3. `itop`
4. `imon`

### 120. 你正在配置一个 RDMA 接口。以下哪个命令可以显示 InfiniBand 设备的信息？
1. `ibmon`
2. `ibstat`
3. `rdmon`
4. `rdstat`

### 121. 你需要通过更改进程 ID 4382 的优先级来提高其性能。以下哪个命令可以完成此任务？
1. `renice -5 -p 4382`
2. `renice 5 -p 4382`
3. `renice 100 4382`
4. `renice 4382 +5`

### 122. `netstat` 的哪个选项用于禁用 DNS 或主机查找？
1. `-b`
2. `-h`
3. `-q`
4. `-n`

### 123. 你想在 Ubuntu 系统上找到与 `sshd` 进程相关的所有进程 ID（PID）。以下哪个命令可以完成此任务？
1. `ps -sshd`
2. `pidof sshd`
3. `pids sshd`
4. `ps --a=sshd`

### 124. 哪个 kill 信号向给定的进程发送挂断（hangup）信号？
1. 1
2. 5
3. 24
4. 30

### 125. 哪个命令用于为添加到系统的新 GPU 驱动配置内核参数？
1. `gpuctl`
2. `gpuload`
3. `sysconfig`
4. `sysctl`

### 126. 你想更改新文件系统的字节与 inode 比例，以防止 inode 耗尽。`mke2fs` 的哪个选项可以完成此任务？
1. `-b`
2. `-r`
3. `-i`
4. `-u`

### 127. 哪个目录包含光通道 HBA 端口的信息？
1. `/sys/fc/ports`
2. `/sys/class/hba`
3. `/sys/class/fc_host`
4. `/sys/class/fc/ports`

### 128. PAM 的哪种类型模块接口用于设置策略（例如用户可以登录的时间段）？
1. `auth`
2. `account`
3. `password`
4. `policy`

### 129. 你需要在服务器上创建一个限制性的访问控制列表（ACL）。防火墙中 `INPUT` 链的默认策略应该是哪个？
1. `deny`
2. `permit`
3. `accept`
4. `discard`

### 130. `ls` 命令的哪个选项显示给定文件或目录的所有权，包括用户和组所有者？
1. `-o`
2. `-a`
3. `-l`
4. `-d`

### 131. 在创建一个将在本地服务器上使用的守护进程时，应该使用以下哪方法？
1. 本地主机/网络
2. Socket
3. 消息传递
4. RDP

### 132. 使用 `free` 命令确定内存使用情况时，哪一列显示内核用于缓冲区（buffers）的内存？
1. `used`
2. `shared`
3. `buffers`
4. `cache`

### 133. 下面哪个命令提供了进入 NetworkManager 的命令行界面？
1. `nmc`
2. `dmc`
3. `nmcli`
4. `netman`

### 134. 哪个命令在类似 `top` 的界面中显示网络流量？
1. `iftop`
2. `iptop`
3. `ptop`
4. `netcap`

### 135. 你怀疑饱和影响了你的 Linux 服务器的网络性能。哪个命令可以帮助确定通过给定接口的流量大小？
1. `netp`
2. `sat`
3. `iptraf`
4. `ipsat`

### 136. 你正在寻找优化 Linux 服务器 I/O 调度器的方法。哪个 I/O 调度算法是默认的？
1. `deadline`
2. `noop`
3. `cfq`
4. `ique`

### 137. 你想高效地管理防火墙规则，以便能够定义可以应用于单个规则的地址组。哪个命令允许你创建地址组？
1. `ipgroup`
2. `iptables -group`
3. `addrgroup`
4. `ipset`

### 138. 你收到用户尝试在服务器之间进行 SSH 连接时出现时的报告。应该使用哪个命令来协助这些报告？
1. `tcptroute`
2. `ping`
3. `telnet`
4. `ps`

### 139. 哪个命令可以以 `pcap` 格式捕捉网络流量，以便后续使用 Wireshark 等工具进行分析？
1. `tcpcap`
2. `pdump`
3. `tshark`
4. `pcapr`

### 140. 你需要确定地址的所有者。你尝试使用 `nslookup` 确定主机名，但该 IP 没有 PTR 记录。哪个命令可以用于确定谁拥有该 IP？
1. `iplookup`
2. `ipowner`
3. `whois`
4. `bg`

### 141. 哪个命令可以帮助诊断磁盘的延迟问题？
1. `diskstat`
2. `statd`
3. `fdisk`
4. `ioping`

### 142. 哪个命令可以触发内核更新分区表？
1. `ifdisk`
2. `partup`
3. `partprobe`
4. `uppart`

### 143. 下面哪个命令可以用于显示跨不同参数的历史性能数据？
1. `sar`
2. `kernperf`
3. `pkern`
4. `perfshow`

### 144. `sysctl` 的哪个选项显示所有可用参数？
1. `-a`
2. `-b`
3. `-c`
4. `-d`

### 145. 在检查 `ps` 命令输出的 `state` 列时，有一个状态为 `D` 的进程。该进程目前处于什么状态？
1. 调试 (Debug)
2. 可中断睡眠 (Interruptible sleep)
3. 不可中断睡眠 (Uninterruptible sleep)
4. 死亡 (Dead)

### 146. Debian 或 Ubuntu 系统上的键盘映射在哪个文件中设置？
1. `/etc/kbd.conf`
2. `/etc/default/keyboard`
3. `/etc/default/kbd.conf`
4. `/etc/keymap`

### 147. 你正在排查 Linux 上的打印访问问题。CUPS 守护进程默认在哪个端口上？
1. 25
2. 342
3. 631
4. 316

### 148. 你需要更改目录内文件的所有权，使其继承子目录和文件。`chown` 命令的哪个选项可以完成此任务？
1. `-o`
2. `-R`
3. `-r`
4. `-f`

### 149. 哪个工具可以查找 SELinux 违规？
1. `sestat`
2. `secv`
3. `convio`
4. `ausearch`

### 150. 你向系统添加了一个 RAID 适配器。哪个命令可以确保内核检测到了适配器？
1. `showraid`
2. `lsadapt`
3. `dmesg`
4. `raidlist`

### 151. 使用 `pkill` 时，哪个选项用于向进程发送信号？
1. `-<SIGNAL>`
2. `-s`
3. `-i`
4. `-h`

### 152. 你正在排查目录权限问题。目录和所有子目录都属于 root。在顶层目录内有一个权限为 755 的目录。然而，非 root 用户无法获取该目录的列表。以下哪项可能是问题所在？
1. 目录权限继承，因此顶层目录必须设置为禁止“其他”用户的执行权限。
2. 子目录需要 777 权限。
3. 子目录需要写入权限。
4. 子目录的其他权限需要设置为 7。





## 4. `/etc/default/ioscheduler`

155. `iftop` 的哪个选项可以防止发生主机查询？
1. `-d`
2. `-a`
3. `-t`
4. `-n`

156. 在 `nslookup` CLI 中可以使用哪个命令来更改查询发送到的服务器？
1. `dest`
2. `server`
3. `srv`
4. `auth`

157. 用户写入一个其不是其所有者也不属于该目录所在组的目录，所需的最小权限是什么？
1. 写 (Write)
2. 读/写/执行 (Read/Write/Execute)
3. 读/执行 (Read/Execute)
4. 写/执行 (Write/Execute)

158. 以下哪种协议提供了在 Linux 系统外部进行身份验证的方法？
1. SSL
2. SSH
3. LDAP
4. AD

159. 用户在创建文件时收到的错误。文件很大。用户可以执行哪个命令来确定文件大小限制？
1. `limit`
2. `ulimit`
3. `filelimit`
4. `flimit`

160. bash 脚本对所有人可执行需要什么权限？
1. 755
2. 644
3. 777
4. 222

161. 可以使用哪个命令设置文件属性（例如使文件变为不可变）？
1. `chr`
2. `fattr`
3. `chattr`
4. `fop`

162. 服务账户通常使用哪个范围的 UIDs？
1. 1 to 999
2. 1 to 100
3. 32,768 to 65,535
4. 1,000 to 1,999

163. 以下哪个命令可以获取用户当前的组成员关系列表？
1. `groupmem`
2. `groups`
3. `lsgr`
4. `getgr`

164. 你向 Linux 服务器添加了交换磁盘并执行了 `mkswap`。然而，在检查 `free` 命令的输出时，交换空间并未被使用。你需要执行哪个命令？
1. `swapon`
2. `swap-en`
3. `actswap`
4. `swpact`

165. `ioping` 的哪个选项设置请求的大小？
1. `-m`
2. `-n`
3. `-f`
4. `-s`

166. 在查找 SELinux 访问拒绝或违规时，应该查询哪些消息类型？
1. `AVC`
2. `DEN`
3. `AVC,USER_AVC`
4. `STOP,VIOL`

167. 哪个命令可以获取扩展硬件信息，包括关于主板的信息？
1. `mbhw`
2. `lsmb`
3. `dmidecode`
4. `lsallhw`

168. 你发现 RAID 阵列中的一个 SATA 磁盘坏了。`mdadm` 的哪个选项可以将磁盘从 RAID 阵列中移除并将其处于降级状态？
1. `rm`
2. `fail`
3. `rem`
4. `del`

169. `whois` 的哪个选项可以抑制某些注册局的法律免责信息？
1. `-L`
2. `-q`
3. `-H`
4. `-s`

170. `iftop` 的哪个选项设置 `iftop` 监听的接口？
1. `-m`
2. `-i`
3. `-l`
4. `-a`

171. 你向哪个文件 echo “- - -” 以导致对 SCSI 主机适配器的新磁盘扫描？
1. `/sys/bus/scsi/hostscan`
2. `/sys/class/scsi_host/hostN/scan`
3. `/sys/class/<host>/scan`
4. `/etc/scsiadm`

172. 在执行本地认证时，哪个文件提供了加密的密码信息？
1. `/etc/passwd`
2. `/etc/shadow`
3. `/etc/encrpass`
4. `/etc/passen`

173. 哪个选项用于显示当前文件属性的信息？
1. `lsfile`
2. `lsattr`
3. `showfile`
4. `exattr`

174. 内存溢出终止（OM killer）一直在杀死系统上的某些进程。`ps` 输出中的哪些列对于确定给定进程的内存使用有用？
1. `size` 和 `rss`
2. `mem` 和 `swap`
3. `free` 和 `cache`
4. `phy` 和 `vir`

175. 哪个信号号对应 `SIGKILL`？
1. 1
2. 5
3. 9
4. 12

176. 以下哪个类是 `host` 命令查询的默认类型？
1. `EX`
2. `HS`
3. `FO`
4. `IN`

177. `netstat` 的哪个选项显示路由表？
1. `-r`
2. `-t`
3. `-a`
4. `-l`

178. `du` 命令的哪个选项提供摘要输出？
1. `-o`
2. `-h`
3. `-s`
4. `-u`

179. 以下哪个命令可以用于查找僵尸进程？
1. `ps -Z`
2. `ps | grep Z`
3. `ps | grep zombie`
4. `ps -a -z`

180. 哪个命令可以列出系统内检测的所有硬件？
1. `lshw`
2. `showhw`
3. `lspic`
4. `slist`

181. `ioping` 命令的哪个选项设置要发送的请求数？
1. `-r`
2. `-c`
3. `-n`
4. `-a`

182. 哪个进程状态表示进程正在运行？
1. `C`
2. `R`
3. `T`
4. `V`

# 第 5 章：自动化与脚本

本章涵盖了以下 CompTIA LINUX+ 考试目标：

### 5.1 给定场景，部署并执行 bash 脚本
- Shell 环境和 shell 变量
    - `PATH`
    - 全局 (Global)
    - 局部 (Local)
    - `export`
    - `env`
    - `set`
    - `printenv`
    - `echo`
- `#!/bin/bash`
- 脚本源 (Sourcing scripts)
- 目录和文件权限
    - `chmod`
- 扩展名 (Extensions)
- 注释 (Commenting)
    - `#`
- 文件通配符 (File globbing)
- Shell 扩展 (Shell expansions)
    - `${}`
    - `$()`
- 重定向与管道 (Redirection and piping)
- 退出状态 (Exit codes)
    - `stderr`
    - `stdin`
    - `stdout`
- 元字符 (Metacharacters)
- 位置参数 (Positional parameters)
- 循环构造结构 (Looping constructs)
    - `while`
    - `for`
    - `until`
- 条件语句 (Conditional statements)
    - `if`
    - `case`
- 转义字符 (Escaping characters)

### 5.2 给定场景，使用 Git 进行版本控制
- 参数 (Arguments)
    - `clone`
    - `push`
    - `pull`
    - `commit`
    - `merge`
    - `branch`
    - `log`
    - `init`
    - `config`
- 文件：
    - `.gitignore`
    - `.git/`

## 5.3 总结编排过程和概念
- 代理 (Agent)
- 无代理 (Agentless)
- 过程 (Procedures)
- 属性 (Attributes)
- 基础设施自动化 (Infrastructure automation)
- 代码即基础设施 (Infrastructure as code)
- 清清单 (Inventory)
- 自动化配置管理
- 构建自动化

1. 你正在使用 bash 编写一个脚本并需要打印变量的内容。以下哪个命令可以实现？
1. `echo`
2. `lf`
3. `sp`
4. `varpt`

2. 以下哪个软件包以无代理的方式为 Linux 提供编排？
1. `Ansible`
2. `Puppet`
3. `Automat`
4. `vid`

3. 以下哪个命令可以用于使用自定义环境执行命令？
1. `set`
2. `env`
3. `run`
4. `crun`

4. 在使用 `git` 时，以下哪个命令从仓库检索最新对象并尝试将这些更改整合到本地工作副本中？
1. `fetch`
2. `pull`
3. `retr`
4. `get`

5. 以下哪项最能描述“代码即基础设施”的概念？
1. 使用编译程序管理交换机和路由器
2. 使用脚本、源码管理和自动化管理服务器和其他系统
3. 使用敏捷方法部署硬件
4. 为基础设施代码中的漏洞制定计划并留出修复时间

6. 以下哪个命令可以更改名为 `script.sh` 的文件，使其仅文件所有者可以执行，而其他人不行？
1. `chmod 700 script.sh`





2. `chown +x script.sh`
3. `chmod script.sh +x`
4. `chmod 777 script.sh`

7. 哪个命令可以向当前 shell 添加函数和变量？
1. `source`
2. `echo`
3. `en`
4. `src`

8. 下面哪项是调用 bash shell 运行脚本的正确方法，通常位于脚本的第一行？
1. `#!/BASH`
2. `#!bash`
3. `#!/bash`
4. `#!/bin/bash`

9. 你需要将命令的输出重定向到日志文件中。重写日志文件的内容是可以接受的。以下哪个字符用于重定向输出以满足此场景？
1. `|`
2. `<`
3. `>`
4. `&`

10. 你需要创建一个名为 `repo` 的新空 git 仓库。以下哪个序列可以完成此任务？
1. `mkdir repo; cd repo; git init --bare`
2. `mkdir repo; git init repo/`
3. `git init repo –md`
4. `git create repo/`

11. 在编排和自动化场景中，使用哪个术语指代被管理的设备集合？
1. 设备集合 (Device collection)
2. 清单 (Inventory)
3. 机器 (Machines)
4. 可用对象 (UsableObjects)

12. 你需要打印 bash 脚本的输出，使得输出字符串包含单引号。应该使用哪个字符作为转义序列将单引号引入输出？
1. `/`
2. `’`
3. `"`
4. `\`

13. 哪个退出代码表示 bash 脚本执行成功？
1. 0
2. 1
3. 2
4. EOF

14. 下面哪个命令产生输出 `sit sat set`？
1. `echo s{i,a,e}t`
2. `echo s(i,a,e)t`
3. `echo s[i,a,e]t`
4. `echo s/i,a,e/t`

15. 下面哪个字符或字符序列开始 bash 脚本中的注释？
1. `/*`
2. `//`
3. `#`
4. `’`

16. 为了让 bash 脚本执行，需要哪个文件扩展名？
1. `.sh`
2. `.bash`
3. `.bat`
4. 不需要特殊的扩展名。

17. 获取之前克隆的 git 仓库的变化后，使用哪个 git 命令将这些更改合并到本地副本？
1. `put`
2. `push`
3. `merge`
4. `inc`

18. 下面哪项最准确地描述软件编排中代理（agent）的角色？
1. 代理是监听并执行来自服务器命令的软件。
2. 代理用于从一个操作系统迁移到另一个操作系统。
3. 代理是用于身份的硬件令牌。
4. 代理不用于软件编排。

19. 能够根据高需求或负载部署额外的服务器是哪种类型自动化示例？
1. 构建 (Build)
2. 编译 (Compile)
3. 基础设施 (Infrastructure)
4. 配置 (Config)

20. 哪个命令可以指示 bash 脚本中的局部变量？
1. `localvar`
2. `ll`
3. `local`
4. `%local%`

21. 哪个 git 命令用于从远程服务器检索仓库？
1. `clone`
2. `checkout`
3. `co`
4. `retr`

22. 你需要将脚本名称返回给用户用于用法说明或帮助输出。哪个位置参数可以用于此目的？
1. `$me`
2. `$1`
3. `$myname`
4. `$0`

23. 下面哪个命令可以打印当前 shell 环境的内容？
1. `echoenv`
2. `printenv`
3. `showenv`
4. `env`

24. 你正在 bash 脚本中写一个 `while` 循环并需要比较两个值。使用哪个运算符实现此目的？
1. `-ne`
2. `=`
3. `equal`
4. `eq`

25. 你需要创建一个 bash 脚本，它将持续循环并在循环内执行某些命令。以下哪行可以完成此任务？
1. `if [ exit -eq "exit" ]`
2. `while true; do`
3. `for ($i = 0, $i++)`
4. `until ($exit)`

26. 下面哪个命令更改 `git` 中 `HEAD` 指向的位置？
1. `git point`
2. `git checkout`
3. `git change`
4. `git load`

27. 你在运行脚本之前需要将变量声明为环境变量的一部分。以下哪个命令可以此此？
1. `dec`
2. `create`
3. `export`
4. `get`

28. 下面哪个命令在 bash 中显示当前路径？
1. `echo PATH`
2. `echo $PATH`
3. `echo $CURPATH`
4. `echo $PATH`

29. 哪个字符序列用于在 bash 脚本的子 shell 中执行命令？
1. `$()`
2. `subs()`
3. `$%`
4. `$(~`

30. 你需要对整个基础设施中的 SSH 守护进程配置进行更改。能够从中央服务器这样做是哪种类型自动化示例？
1. 安全 (Security)
2. 自动化配置管理 (Automated configuration management)
3. 开发配置管理 (Development configuration management)
4. 可用性管理 (Usability management)

31. `env` 命令配合哪个选项用于从环境中删除变量？
1. `-r`
2. `-u`
3. `-n`
4. `-d`

32. 在 bash 脚本中，你需要运行两个命令，但当第一个命令成功时运行第二个命令。以下哪个元字符可以完成此任务？
1. `<>`
2. `&`
3. `&&`
4. `|`

33. 你需要重定向命令的输出并将该输出附加到文件中。以下哪个字符序列可以完成此？
1. `>`
2. `>>`
3. `|`
4. `^`

34. 你需要获取目录列表，但不包含以字母 `p` 开头的文件和目录。以下哪个命令可以完成任务？
1. `ls !p`
2. `ls [!p]`
3. `ls [^p]`
4. `ls [^p]*`

35. 在 git 仓库中使用以下哪个文件来指示不应版本化的文件模式？
1. `novers`
2. `.gitignore`
3. `gitignore.txt`
4. `gitover`

36. 你需要遍历目录并对其中的文件执行操作。为了完成此任务，你将使用 bash 脚本和循环结构。哪种循环结构最适合此目的？
1. `until`
2. `do`
3. `for`
4. `foreach`

37. 你正在调试另一个管理员编写的 bash 脚本。在脚本中，你看到命令被反引号包裹。使用反引号的结果是什么？
1. 命令执行并将输出发送到控制台。
2. 命令不执行。
3. 命令执行就像使用了 `$()` 命令替换。
4. 命令执行并将输出发送到 `/dev/null`。

38. 哪个 git 命令显示带有提交 ID 的短提交历史？
1. `showhist`
2. `list`
3. `log`
4. `hist`

39. 你向 git 仓库提交代码并需要在命令行中包含消息。哪个选项启用此行为？
1. `-m`
2. `-h`
3. `-f`
4. `-l`

40. 当开发者向仓库的某个分支提交代码时编译软件是哪种类型自动化示例？
1. 基础设施 (Infrastructure)
2. 构建 (Build)
3. 复杂 (Complex)
4. DevOps

41. 你正在处理 MySQL 数据库并需要从文件中读取多个 SQL 命令并发送到 MySQL CLI 执行。你将使用 STDIN 重定向来实现此操作。假设文件名为 `customers.sql`，以下哪个命令是正确的？
1. `mysql < customers.sql`
2. `mysql | customers.sql`
3. `mysql > customers.sql`
4. `mysql >< customers.sql`





42. 你正在使用 `git` 作为源代码管理工具协作一个代码项目。队友们说他们看不到你的代码，尽管你一直在定期提交代码（commit）。以下列哪项最可能是问题所在？

    1.  你没有添加提交信息（commit messages）。
    2.  你需要将提交 ID 发送给队友。
    3.  你没有执行 `git push` 将代码发送到服务器。
    4.  你正在使用 `-h` 标志进行提交。

43. `chmod` 命令的哪个选项可以执行递归更改？

    1.  `-re`
    2.  `-R`
    3.  `-c`
    4.  `-v`

44. bash 脚本中使用哪个字符序列来表示 `case` 语句中的默认情况？

    1.  `()`
    2.  `*.*`
    3.  `**`
    4.  `*)`

45. bash 脚本中使用哪个字符序列表示 `if` 条件语句的结束？

    1.  `}`
    2.  `fi`
    3.  `end`
    4.  `endif`

46. git 仓库中默认分支的名称是什么？

    1.  `source`
    2.  `main`
    3.  `primary`
    4.  `master`

47. 你需要将一个命令的输出作为另一个命令的输入。哪个字符有助于这种场景？

    1.  `>`
    2.  `|`
    3.  `!`
    4.  `` ` ``

48. 哪个 `git` 命令显示仓库工作副本的当前状态？

    1.  `git list`
    2.  `git status`
    3.  `git state`
    4.  `git view`

49. `echo` 命令的哪个选项会抑制通常包含的结束换行字符？

    1.  `-a`
    2.  `-n`
    3.  `-d`
    4.  `-y`

50. 确定每个节点上安装的软件版本是自动化基础设施中哪项收集信息的示例？

    1.  清单（Inventory）
    2.  组（Group）
    3.  过程（Procedure）
    4.  构建（Build）

51. 你需要将命令的标准错误输出（STDERR）重定向到文件中以捕捉错误。哪个字符序列可用于此？

    1.  `>`
    2.  `%2>`
    3.  `2>`
    4.  `%%>`

52. 你需要更改 git 环境，因为你的电子邮件地址发生了变化。以下哪条命令可以确保后续提交都使用你的新电子邮件地址？

    1.  `git config user.email`
    2.  `git change email`
    3.  `git config email.addr`
    4.  `git config email.address`

53. 使用哪个 shell 内置命令显示只读变量列表？

    1.  `ro`
    2.  `readonly`
    3.  `env-ro`
    4.  `ro-env`

54. 假设你正在使用 bash 壳，并想防止输出重定向意外覆盖现有文件。可以使用哪个命令和选项来调用此行为？

    1.  `setoutput -f`
    2.  `overwrite=no`
    3.  `overwrite -n`
    4.  `set -C`

55. 你收到一个没有文件扩展的文件。你可以运行哪个命令来帮助确定它可能是什么类型的文件？

    1.  `grep`
    2.  `telnet`
    3.  `file`
    4.  `export`

56. 使用 bash 时，以下哪个命令会显示命令历史的最后 50 行，包括当前会话的命令？

    1.  `bashhist 50`
    2.  `history 50`
    3.  `cat .bash_history`
    4.  `tail -f .bash_history`

57. 使用 bash 时，如何执行以特定字符串开头的最后一个命令，即使该命令不是你输入的最后一个？

    1.  在命令前加上 `!` 然后加上要搜索的字符串。
    2.  在历史中搜索该命令。
    3.  在命令前加上 `?` 然后加上要搜索的字符串。
    4.  这在 bash 中无法实现。

58. 哪个 shell 内置命令可以确定给定命令的运行位置？

    1.  `type`
    2.  `when`
    3.  `find`
    4.  `help`

59. 哪个命令用于在 bash shell 中读取并执行文件中的命令？

    1.  `run`
    2.  `execute`
    3.  `source`
    4.  `func`

60. 你需要一个所有用户注销时执行的命令。假设所有用户都使用 bash，这应该放在哪个文件中？

    1.  `~/.bash_logout`
    2.  `/etc/bash.bash_logout`
    3.  `/home/.bash_logout`
    4.  `/etc/bash_logout`

61. 以下哪个命令删除已设置的环境变量？

    1.  `profile --unset`
    2.  `env -u`
    3.  `set -u`
    4.  `import`

62. 在设置 shell 脚本的 shebang（bang）行时，以下哪条命令有助于自动确定解释器的位置？

    1.  `#!/usr/bin/env bash`
    2.  `#!/bin/bash`
    3.  `#!env`
    4.  `/bin/int bash`

63. 以下哪项最能描述 `PS1` 环境变量？

    1.  `PS1` 用于设置 `PostScript` 命令的位置。
    2.  `PS1` 用于定义 bash 的默认 shell 提示符。
    3.  `PS1` 作为系统变量使用。
    4.  `PS1` 没有值。

64. 脚本中的哪个变量用于访问第一个命令行参数？

    1.  `$ARG`
    2.  `$0`
    3.  `$1`
    4.  `$ARG`

65. 以下哪项将打印从 0 开始的数字列表？

    1.  `list 0`
    2.  `seq 0`
    3.  `echo 5`
    4.  `seq 1`

66. 以下哪项会执行脚本并退出 shell？

    1.  `run`
    2.  `source`
    3.  `./`
    4.  `exec`

67. 脚本中的哪个命令等待用户输入并将其放入变量？

    1.  `exec`
    2.  `get`
    3.  `read`
    4.  `prompt`

68. 使用什么字符将一系列命令标记为函数？

    1.  圆括号 `()` 和大括号 `{}`
    2.  大括号 `{}` 和圆括号 `()`
    3.  方括号 `[]` 和大括号 `{}`
    4.  引号 `""` 和圆括号

69. bash 脚本中使用哪个字符序列来终结一个 `case` 语句？

    1.  `end`
    2.  `done`
    3.  `esac`
    4.  `caseend`

70. `declare` 命令的哪个选项显示的输出方式可以随后作为另一个命令的输入？

    1.  `-o`
    2.  `-n`
    3.  `-p`
    4.  `-m`

71. 哪些字符用于表示 `while` 循环测试部分的开始和结束？

    1.  圆括号 `()`
    2.  大括号 `{}`
    3.  方括号 `[]`
    4.  双引号 `""`

72. 当带有一个参数使用 `test` 内置命令时，如果参数为空，返回值是什么？

    1.  `false`
    2.  `true`
    3.  `unknown`
    4.  `-1`

73. 使用波浪号（如 `cd ~`）切换目录时使用哪个环境变量？

    1.  `HOMEDIR`
    2.  `HOMEPATH`
    3.  `HOME`
    4.  `MAILPATH`

74. 你想通过 git 历史查看单个文件。假设文件名为 `nhl_scores.php`，应该使用哪个命令来实现目的？

    1.  `git log --history nhl_scores.php`
    2.  `git log --follow nhl_scores.php`
    3.  `git history nhl_scores.php`
    4.  `git commit-history nhl_scores.php`

75. 在自动化基础设施中，以下哪项最能描述清单的属性？

    1.  客户端 IP 地址和软件版本等参数
    2.  客户端节点数量
    3.  用于编排的服务器软件
    4.  部署架构模式

76. 在 bash 脚本中比较整数时，使用哪个运算符来判断一个是否与另一个相等？

    1.  `-ro`
    2.  `===`
    3.  `-eq`
    4.  `-fe`

77. 你想连续运行多个命令但不想将输出发送到下一个命令。以下哪个元字符可以完成此任务？

    1.  `&`





2. `>`
3. `;`
4. `|`

78. 哪一个转义序列用于表示警报或铃声？
1. `\a`
2. `\b`
3. `\c`
4. `\d`

79. 下列中哪项是 bash 脚本中有效的变量声明，将变量 `NUM` 设置为 1？
1. `NUM = 1`
2. `$NUM = 1`
3. `NUM= 1`
4. `NUM=1`

80. 下列哪一个命令可以获取自 epoch 来的秒数，并将其放入 shell 脚本中名为 `DATE` 的变量中？
1. `DATE="$(date +%s)"`
2. `DATE="date"`
3. `DATE="$(date);`
4. `DATE="$date %s"`

81. 哪个序列用于标记 shell 脚本中 `for` 循环内执行命令的开始和结束？
1. 大括号 `{ }`
2. 关键字 `do` 和 `done`
3. 分号 `;`
4. 制表符

82. `declare` 命令的哪个选项会创建一个只读变量？
1. `-r`
2. `-ro`
3. `-p`
4. `-x`

83. 哪一个环境变量控制日期和时间的格式，例如 12 小时制或 24 小时制的时钟？
1. `LOCALE_DATE`
2. `DATE_FORMAT`
3. `LC_TIME`
4. `LC_DATE`

84. `netstat` 的哪个选项以类表格格式显示接口信息，可能适用于脚本编写？
1. `-i`
2. `-r`
3. `-t`
4. `-l`

85. 你正在 SSH 会话中运行一个 shell 脚本。可以使用哪个组合组合来终止脚本？
1. Ctrl+X
2. Ctrl+-
3. Ctrl+C
4. Ctrl+Esc

86. bash 脚本下列哪一个条件判断将测试变量 `DAY` 是否等于 `SUNDAY`？
1. `if ($DAY == "SUNDAY")`
2. `if ($DAY -eq "SUNDAY")`
3. `if [[ $DAY == "SUNDAY" ]]`
4. `if [ DAY = "SUNDAY" ]`

87. 下列哪一个命令将 `~/code/bin` 添加到路径？
1. `PATH=~/code/bin:$PATH`
2. `PATH=/code/bin:$PATH`
3. `PATH=/home/code/bin:$PATH`
4. `PATH=PATH:~/code/bin`

88. `git merge` 的哪个选项可以尝试回滚发生冲突的合并？
1. `--rollback`
2. `--abort`
3. `--rewind`
4. `--restart`

89. 哪一个环境变量可以更改通过 `git init` 创建的新 git 仓库的默认路径？
1. `GIT_DIR`
2. `GIT_HOME`
3. `GIT_DEST`
4. `GIT_LOC`

90. 哪个字符序列用于在 bash 脚本中使用 `echo` 添加水平制表符？
1. `\h`
2. `\t`
3. `\a`
4. `\f`

91. 你需要排除名为 `build.o` 的构建文件被 git 跟踪。在 `.gitignore` 文件可以使用哪个字符序列来排除或忽略所有目录下的该文件？
1. `build.o`
2. `/build.o`
3. `**/build.o`
4. `build.*`

92. 哪个文件通配符序列将匹配所有大写 *A* 或大写 *F* 开头的文件？
1. `[AF]*`
2. `[af]*`
3. `*AF*`
4. `AF*`

93. 假设远程名称为 `origin`，可以使用哪个 `git` 命令获取关于远程的额外信息？
1. `git show origin`
2. `git remote show origin`
3. `git show remotes`
4. `git remote list`

94. 哪个字符序列显示传递给 bash 脚本的命令行参数的数量？
1. `$NUM`
2. `$CLA`
3. `$+`
4. `$#`

95. 如果你想在一段时间没有活动后自动注销 shell，可以设置哪一个环境变量？
1. `TIMEOUT`
2. `TMOUT`
3. `TO`
4. `IDLETIME`

96. 你正在调试一个 bash 脚本，注意到有一行包含：`echo $NUM #sending $NUM to output`。这一行的结果是什么？
1. 它不会输出任何内容，因为它被注释了。
2. 它会导致语法错误，因为它是无效的。
3. 它将输出 `NUM` 变量的内容。
4. 它将输出 `$NUM`。

97. 当使用 `git clone` 克隆仓库时，你需要更改远程名称，使其不为 `origin`。可以为 `git clone` 添加哪个选项来实现此？
1. `--origin`
2. `--remote`
3. `--name`
4. `--remote-name`

98. 在虚拟服务器环境中工作时，`iostat` 中的哪列显示了由于虚拟机花费的非自愿时间（百分比）？
1. `proc`
2. `wait`
3. `user`
4. `steal`

99. 如果你需要为特定会话临时重新配置所有的 locale 变量和设置，可以使用哪一个环境变量？
1. `LC_LIST`
2. `LC_GLOBAL`
3. `LC_ALL`
4. `ALL_LOCALE`

100. 在客户端节点执行的一组命令是哪种类型自动化的示例？
1. `Procedure`（过程）
2. `Subset`（子集）
3. `Agent`（代理）
4. `Collection`（集合）

101. 哪个字符序列用于表示 bash 脚本 `case` 语句中单独语句的结束？
1. `//`
2. `eol`
3. `;;`
4. `<`

102. 下列哪一个命令删除当前定义的命令？
1. `remove`
2. `rm`
3. `unalias`
4. `delete`

103. 下列哪一个测试将在 shell 脚本上下文中判断文件是否存在？
1. `-a`
2. `-e`
3. `-m`
4. `-i`

104. `LANG` 环境变量的下列哪些值将配置系统尽可能地跳过 locale 翻译？
1. `LANG=COMPAT`
2. `LANG=NONE`
3. `LANG=C`
4. `LANG=END`

105. `git config` 命令的哪个选项显示所有已设置的配置参数？
1. `--list`
2. `--show`
3. `-u`
4. `--display`

106. 如果你需要将 `STDERR` 重定向到文件并追加到文件，应该使用哪个字符序列？
1. `2>`
2. `2>>`
3. `&>>`
4. `1>>`

107. 在处理基础设施即代码（IaC）时，你收到一个 `.yml` 扩展的文件。该文件内容的可能格式是什么？
1. `YAML`
2. `XML`
3. `Tab-delimited`（制表符分隔）
4. `Text`（文本）

108. 下列哪项最描述命令 `cat /etc/passwd | cut -d: -f1 > users.txt` 的结果？
1. 从 passwd 文件中提取第一个字段并放入 `users.txt`。
2. 从 passwd 文件中提取第二个字段并放入 `users.txt`。
3. 根据冒号分割 passwd 文件并输出到 `users.txt`。
4. passwd 文件中以冒号开头的字段进入 `users.txt`。

109. 哪个 shell 内置命令用于移动位置参数，使得 `$2` 变成 `$1`, `$3` 变成 `$2` 以此类推？
1. `move`
2. `rev`
3. `shift`
4. `dec`

110. 你正在使用 `git pull` 获取共享仓库的更改。你应该向 `git pull` 添加哪个选项以防止自动提交，以便先查看合并结果？
1. `--pre-merge`
2. `--no-auto`
3. `--nc`
4. `--no-commit`

111. 下列哪对表示 bash 脚本中 `until` 循环的开始和结束？
1. `do`; `done`
2. `start`; `stop`
3. `beg`; `end`
4. `until`; `litnu`

112. 哪个退出代码用于表示 bash 脚本中的通用错误？
1. `0`
2. `1`
3. `255`
4. `-1`

113. 在编写构建自动化脚本时，你需要在运行 `make` 命令之前运行一个配置脚本。假设该脚本与调用它的脚本在同一目录下，下列哪一个可以执行该配置脚本？
1. `configure`
2. `./configure`
3. `../configure`
4. `/configure`





114. 假设一个文件已经被添加并提交到 git，`git commit` 命令的哪个选项可以自动添加并提交该文件？

1. `-a`
2. `-b`
3. `-c`
4. `-d`

115. 哪个与 locale 相关的环境变量用于与货币相关的本地化？

1. `LC_MONE`
2. `LC_CURRENCY`
3. `LC_MONETARY`
4. `LC_CURR`

116. 在用户主目录下的 `.profile` 中添加以下哪一行将将其时区设置为中央时间（Central time）？

1. `TZ=/Central ; export TZ`
2. `TIMEZONE='America/Chicago' ; export TIMEZONE`
3. `set TZ=/Central`
4. `TZ='America/Chicago’; export TZ`

117. 下面哪一项在 bash 脚本中创建一个数组？

1. `ARRAY=(val1 val2)`
2. `ARRAY = "val1 val2"`
3. `ARRAY_PUSH($ARRAY,"val1","val2");`
4. `ARRAY{0} = "val1"`

118. 壳脚本 `while` 循环中的哪个测试项将检查一个值是否小于另一个值？

1. `-less`
2. `-lessThan`
3. `-lt`
4. `-lthan`

119. 假设一个用空格分隔的值列表已定义为 `LIST="one two three four"`，下面哪种 `for` 循环结构可以遍历列表中的元素？

1. `for LIST`
2. `for VAR in LIST`
3. `for VAR in $LIST`
4. `for $LIST -> $VAR`

120. 哪个关键字用于启动 bash 脚本中的备选条件？

1. `if`
2. `else if`
3. `elif`
4. `elsif`

121. git 在哪个目录下存储存储元数据的本地副本？

1. `.gitmeta`
2. `gitlocalmeta`
3. `.git`
4. `git`

122. 你需要将 STDERR 和 STDOUT 都重定向到文件中。下面哪种字符序列可以完成此任务？

1. `2>`
2. `2>&1`
3. `2+1`
4. `+2+1`

123. 在 bash 脚本中，你需要运行两个命令，但只有在第一个命令失败时才运行第二个命令。下面哪个元字符可以完成此任务？

1. `<>`
2. `&`
3. `&&`
4. `||`

124. 下面哪条命令创建了一个名为 `project1` 的新分支并将 `HEAD` 指向该分支？

1. `git branch project1`
2. `git checkout project1`
3. `git checkout -b project1`
4. `git create project1 -H`

125. 下面哪项最符合 bash 脚本中 `while` 循环和 `until` 循环之间的差异？

1. `while` 循环总是执行一次；`until` 循环不执行。
2. `until` 循环总是执行一次；`while` 循环不执行。
3. `while` 循环在条件为真时一直执行；`until` 循环直到条件为假为止执行。
4. `until` 循环直到条件为真为止执行；`while` 循环直到条件为假为止执行。

126. 在 bash 脚本中可以使用哪条语句判断变量 `$num1` 是否大于 `$num2`，假设两个变量都包含整数？

1. `if [ "$num1" -gt "$num2" ]`
2. `if [ "$num1" > "$num2" ]`
3. `if ($num1 -gta $num2)`
4. `if [ $num1 gt $num2 ]`

127. 下面哪个协议通常用于无代理基础设施编排？

1. SMTP
2. ICMP
3. `SSH`
4. FTP

128. 下面哪种字符序列在 bash 脚本中展开或插值名为 `VAR` 的变量？

1. `VAR`
2. `$(VAR}`
3. `${VAR}`
4. `*VAR*`

# 第 6 章

## 模拟考试

1. 哪个命令允许你查看当前的 IRQ 分配？

1. `view /proc/irq`
2. `cat /proc/interrupts`
3. `cat /dev/irq`
4. `less /dev/irq`

2. udev 设备配置通过操作哪个目录下的文件完成？

1. `/udev/devices`
2. `/devices/`
3. `/udev/config`
4. `/etc/udev`

3. 哪个命令用于自动加载模块及其依赖项？

1. `modprobe`
2. `lsmod`
3. `insmod`
4. `rmmod`

4. 在带有 GRUB 的系统启动期间，可以按哪个键显示 GRUB 菜单？

1. `Shift`
2. `E`
3. `V`
4. `H`

5. 哪个命令可以查看内核环形缓冲区以排除进程故障？

1. `lsboot`
2. `boot-log`
3. `krblog`
4. `dmesg`

6. 哪条语句最符合使用 `-l` 命令显示的以下内容？
`lrwxrwxrwx 1 root root 35 Jul 20 .fetchrc -> .configs/mail/.fetchrc`

1. 这是一个名为 `.fetchrc` 的文件，通过符号链接连接。
2. 这是一个名为 `.configs/mail/.fetchrc` 的文件，由 root 所有。
3. 这是一个名为 `.fetchrc` 的目录，由用户所有。
4. 这是一个名为 `.configs/mail/.fetchrc` 的本地目录。

7. 使用 `systemd` 的哪个命令列出可用的服务单元？

1. `systemd list-units`
2. `systemctl list-units`
3. `systemd unit-list`
4. `systemctl show-units`

8. `lspci` 的哪个选项用于显示数字代码和设备名称？

1. `-numdev`
2. `-n`
3. `-nn`
4. `-devnum`

9. 哪个命令和选项可以用于判断给定服务是否已加载？

1. `systemctl --ls`
2. `telinit`
3. `systemctl status`
4. `sysctl -a`

10. 为邮件服务器划分磁盘分区时，哪个分区应该是最大的以允许存储？

1. `/etc`
2. `/usr/bin`
3. `/mail`
4. `/var`

11. 哪个 YUM 选项显示包的依赖关系？

1. `list`
2. `deplist`
3. `dependencies`
4. `listdeps`

12. `rpm` 命令的哪些选项将显示安装过程的详细输出以及安装进度？

1. `-ivh`
2. `-wvh`
3. `--avh`
4. `--ins-verbose`

13. 哪个命令将在 Debian 系统上搜索名为 `zsh` 的包？

1. `apt-cache search zsh`
2. `apt-get search zsh`
3. `apt-cache locate zsh`
4. `apt-search zsh`

14. 哪个 `rpm` 选项可以验证自安装以来没有文件被修改过？

1. `-V`
2. `-v`
3. `--verbose`
4. `--filesum`

15. 下面哪条命令行可以持续监控一个名为 nagios 的单个进程？

1. `top -n 1`
2. `top -p 23`
3. `ps -nagios`
4. `top -ppidof nagios`

16. `xfs_metadump` 的哪个选项显示进度指示？

1. `-g`
2. `-p`
3. `-f`
4. `-v`

17. SAN 再次崩溃，导致 Linux 服务器上的一个文件系统导致了严重损坏。可以使用哪个命令和选项尝试检查驱动器内容而不造成更多损坏？

1. `fdisk -f`
2. `mke2fs -c`
3. `debugfs -c`
4. `ls -a`

18. 下面哪条命令可以帮助你确定 X 会话中给定窗口的信息，包括窗口大小和位置信息？

1. `xkbinfo`
2. `xdspy`
3. `xwininfo`
4. `xver`

19. 哪个文件用于指示 Linux 服务器上的本地时区？

1. `/etc/timez`
2. `/etc/timezoneconfig`
3. `/etc/localtime`
4. `/etc/localtz`

20. 在哪个目录下你会找到与不同区域时区的文件？

1. `/etc/timezoneinfo`
2. `/etc/zoneinfo`
3. `/var/zoneinfo`
4. `/usr/share/zoneinfo`

21. 应该在哪个目录下放置文件，以便在创建用户时将这些文件复制到用户的主目录？

1. `/etc/skel`
2. `/etc/homedir`
3. `/home/usertemplate`
4. `/etc/template`

22. 哪个命令列出当前通过 `at` 调度的作业列表？

1. `atlist`
2. `atq`





### 3. `atl`
### 4. `at --jobs`

### 23. 下列编码中哪个提供了字符的多字节表示？
1. `ISO-8859`
2. `UTF-8`
3. `ISO-L`
4. `UFTMulti`

### 24. LDAP over SSL 运行在哪个端口？
1. 端口 53
2. 端口 389
3. 端口 636
4. 端口 443

### 25. 下列哪个命令可以根据自 1970 年 1 月 1 日以来的天数设置账户过期？
1. `passwd -e`
2. `chage -E`
3. `usermod -l`
4. `chguser`

### 26. SSH 的哪个选项允许使用密钥进行身份验证？
1. `-i`
2. `-k`
3. `-f`
4. `--key`

### 27. 在脚本场景中，你需要防止 `sudo` 提示凭据或出于其他任何原因进行提示。使用 `sudo` 的哪个选项来指示这一点？
1. `-n`
2. `--noprompt`
3. `-i`
4. `-q`

### 28. 根据 `/etc/inittab` 的指示，通常哪个运行级别用于单用户模式？
1. 1
2. 2
3. 5
4. 6

### 29. 下列哪个命令提供了当前内存使用情况以及交换空间及其利用率的概述？
1. `mem`
2. `free`
3. `pstat`
4. `swap`

### 30. 下列哪个命令可以显示当前的磁盘利用率（包括可用空间）？
1. `df`
2. `du`
3. `diskutil`
4. `diskuse`

### 31. 下列哪个命令显示 CPU 相关的性能信息，每秒采集一次，共 10 次？
1. `sar -u 2 10`
2. `sar -u 10 2`
3. `sar -u 2`
4. `uptime -t`

### 32. `iostat` 的哪个选项导致输出以兆字节为单位？
1. `-k`
2. `-l`
3. `-m`
4. `-o m`

### 33. 你正在使用一个旧的 CentOS 5 系统并需要重新创建初始内存磁盘（RAM disk）。哪个命令用于此目的？
1. `mkinitrd`
2. `mkramdisk`
3. `mkdisk --init`
4. `mkfs.init`

### 34. 创建 bzImage 使用哪种压缩方法？
1. zip
2. bzip3
3. gzip
4. 无法确定

### 35. `fsck` 命令的哪个选项会查找并自动假设应该修复发现的错误？
1. `-ry`
2. `-vy`
3. `-my`
4. `-xy`

### 36. `systemd` 系统启动到哪个单元名称以启动其他层级？
1. `default.target`
2. `init.target`
3. `initial.target`
4. `load.target`

### 37. 使用哪个命令格式化交换分区？
1. `mkfs -swap`
2. `mkswap`
3. `format -swap`
4. `mksw`

### 38. 你在 `/etc/fstab` 中看到了 `defaults`get。哪些选项包含在 `defaults` 中？
1. `ro`, `exec`, `auto`
2. `rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, `async`
3. `rw`, `exec`, `auto`, `nouser`, `async`
4. `rw`, `exec`, `nouser`, `async`, `noauto`, `suid`

### 39. 使用哪个命令从精简配置存储中删除未使用的文件系统块？
1. `thintrim`
2. `thtrim`
3. `fstrim`
4. `fsclean`

### 40. `mdadm` 的哪个选项用于创建新阵列？
1. `--create`
2. `--start`
3. `--begin`
4. `--construct`

### 41. 下列哪个命令使用 LVM 创建逻辑卷？
1. `lvc`
2. `lvcreate`
3. `lvlist`
4. `lvmake`

### 42. 下列哪个命令显示网络套接及其分配的内存？
1. `ss -m`
2. `mpas`
3. `mem`
4. `free`

### 43. 在排查潜在硬件问题时，你需要确定哪个接口用于某个地址。实现此点的方法之一是使用 `ping` 命令监控设备上的活动。`ping` 的哪个选项会向接口泛洪 `ECHO_REQUEST` 数据包？
1. `-e`
2. `-a`
3. `-c`
4. `-f`

### 44. 下列哪个 `dd` 命令一次读取并写入一兆字节？
1. `dd bs=1024M`
2. `dd size=1M`
3. `dd bs=1M`
4. `dd rw=1M`

### 45. `rsync` 命令的哪个选项仅检查文件大小作为判断是否应同步该文件的手段？
1. `--filesize`
2. `--size-only`
3. `--list-size`
4. `--file-size`

### 46. 为区域创建 MX 记录时，下列哪个是优先级最高的交换器？
1. 0
2. 10
3. 20
4. 100

### 47. 区域请求发送在哪个协议和端口上？
1. `UDP/53`
2. `ICMP/53`
3. `TCP/143`
4. `TCP/53`

### 48. `dig` 命令可以使用哪种类型来测试传输？
1. `xfr`
2. `transfer`
3. `zxfr`
4. `axfr`

### 49. 下列哪个文件用于定义 NFS 共享的文件系统？
1. `/etc/nfs.cfg`
2. `/etc/nfs.conf`
3. `/etc/export.nfs`
4. `/etc/exports`

### 50. `dhcpd.conf` 中的哪个选项指定了允许允许租约的最长时间？
1. `max-time`
2. `max-lease-time`
3. `lease-max`
4. `maximum-lease-duration`

### 51. 你正在为一个用户排除身份验证问题。你认为系统使用本地文件和 LDAP 进行身份验证。`/etc/nsswitch.conf` 中的下哪行显示了这些验证机制？
1. `passwd: files ldap`
2. `passwd [files ldap]`
3. `auth: local ldap`
4. `auth: localfiles ldap`

### 52. 下列哪个命令可以用于为 SSH 身份验证生成私公钥对？
1. `ssh-createkey`
2. `sshkey`
3. `ssh-key`
4. `keygen`

### 53. 哪个文件包含了用于身份验证的密钥列表？
1. `~/ssh/keys`
2. `~/.ssh/pubkeys`
3. `~/.ssh/auth`
4. `~/.ssh/authorized_keys`

### 54. 新添加的 SATA 磁盘在启动过程中未显示。你可以在哪里检查这个问题？
1. 使用系统日志
2. 使用 `debugfs`
3. 在 `fdisk` 工具中
4. 在计算机 BIOS 或固件中

### 55. 下列哪个命令使用 bash shell 将环境变量 `JAVA_PATH` 设置为 `/home/user/java2`？
1. `invoke JAVA_PATH=/home/user/java2`
2. `export JAVA_PATH=/home/user/java2`
3. `envvar JAVA_PATH=/home/user/java2`
4. `echo JAVA_PATH=/home/user/java2`

### 56. `.bashrc` 中的哪个选项设置了 `.bash_history` 中保留的命令数量？
1. `HISTLIMIT`
2. `HISTORYFILE`
3. `HISTSIZE`
4. `HISTNUM`

### 57. 你正在创建一个信息的脚本。下列哪个命令以制表符格式打印 `/etc/passwd` 中所有用户的用户名和真实名称？
1. `cut -d: -f 1,6 /etc/passwd`
2. `sed 's/://' /etc/passwd`
3. `awk -F: '{print $1,$5}' OFS="\t" /etc/passwd`
4. `cat -o "\t" /etc/passwd`

### 58. 哪个 `git clone` 命令会将名为 `portalutils` 的仓库克隆到名为 `utils` 的目录？
1. `git clone ssh://sourcehost/portalutils -d utils`
2. `git clone ssh://sourcehost:/portalutils utils`
3. `git clone ssh://sourcehost/:portalutils utils`
4. `git clone ssh://sourcehost::portalutils -d utils`

### 59. 哪个命令使得当前 shell 中定义的变量对子进程可用？
1. `export`
2. `source`
3. `let`
4. `def`

### 60. 你正在观察另一个管理员在服务器上执行工作。作为工作的一部分，管理员使用了以下命令：`. variables.sh`
* 下列哪个命令与 `. variables.sh` 等效？
1. `let variables.sh`
2. `set variables.sh`
3. `source variables.sh`
4. `var variables.sh`





# 61. 哪一项显示了有效的名为 `sayHello` 的 bash 函数？

1. `function sayHello() { echo "hello"; }`
2. `function sayHello{}`
3. `function sayHello() { echo Hello }`
4. `function sayHello() { echo Hello } ;`

# 62. `useradd` 命令的哪个选项设置密码过期到账户禁用之间的天数？

1. `-n`
2. `-f`
3. `-e`
4. `-g`

# 63. 使用 `crontab` 命令时，哪个选项可以删除指定用户的所有 cron 任务？

1. `-d`
2. `-e`
3. `-r`
4. `-l`

# 64. 哪个命令用于解析基于 `systemd` 的系统日志文件项？

1. `logger`
2. `journalentry`
3. `jrnctl`
4. `journalctl`

# 65. 下面哪个 syslog 设施捕获来自 `lp` 打印设施的消息？

1. `auth`
2. `messages`
3. `lpr`
4. `root`

# 66. 为了让服务器接收标准 LDAP 流量，需要通过防火墙哪个端口？

1. TCP 端口 25
2. TCP 端口 443
3. TCP 端口 143
4. TCP 端口 389

# 使用 SSH 通过端口 2200 连接到 `host.example.com` 的正确语法是哪个？

1. `ssh -l 2200 host.example.com`
2. `ssh host;example.com`
3. `ssh host.example.com:2200`
4. `ssh host:2200 -d example.com`

# 68. `tar` 命令的哪个选项保留权限？

1. `-x`
2. `-v`
3. `-z`
4. `-p`

# 69. 处理补丁文件时，哪个选项可以让补丁过程忽略空格？

1. `-w`
2. `-i`
3. `-e`
4. `-p`

# 70. 使用 `dm-crypt` 命令时，默认使用哪种加密类型？

1. `plain`
2. `SHA-256`
3. `LUKS`
4. `loop`

# `journalctl` 的哪个选项反向显示输出，并将最新的条目放在前面？

1. `-n`
2. `-r`
3. `-f`
4. `-b`

# 72. 当救援模式下无法恢复时，哪个 `systemd` 目标可以作为救援模式的替代？

1. `emerg`
2. `recover`
3. `control-recover`
4. `emergency`

# 73. 在跨设备执行 `rsync` 时，你收到无法保留文件所有权的错误，可能是由于目标系统缺少用户或组。应该从 `rsync` 选项中删除哪个选项以便保留用户和组所有权？

1. `-go`
2. `-o`
3. `-no-ownership`
4. `-remove-owners`

# 74. `ping` 命令的哪个选项启用绕过路由表？

1. `-q`
2. `-r`
3. `-b`
4. `-A`

# 75. `patch` 命令的哪个选项创建文件的备份？

1. `-d`
2. `-b`
3. `-s`
4. `-c`

# 76. 在编排中，客户端机器上监听连接并代表服务器执行命令的软件通常被称为以下哪一个？

1. `Executor`
2. `Runner`
3. `Agent`
4. `Host`

# 77. bash 中哪些转义字符代表回车和换行？

1. `\enter`
2. `\r\n`
3. `\n`
4. `\c\n`

# 78. bash 脚本中的哪个文件测试用于检查文件是否存在？

1. `-f`
2. `-o`
3. `-l`
4. `-p`

# 79. 下面哪项即使没有设置执行位，也会执行名为 `test.sh` 的 bash 脚本？

1. `./test.sh`
2. `test.sh --execute`
3. `bash test.sh`
4. `run test.sh`

# 80. 在测试 `.gitignore` 文件的排除模式时，可以使用哪个 `git` 命令和选项来查看将被忽略的结果？

1. `git ls-files -i --exclude-standard`
2. `git ls-files -v ignored`
3. `git show-ignored`
4. `git status --ignored`

# 81. 下面哪项即使没有设置执行位，也会执行名为 `test.sh` 的 bash 脚本？

1. `./test.sh`
2. `test.sh --execute`
3. `bash test.sh`
4. `run test.sh`

# 82. `tune2fs` 的哪个选项设置最大计数？

1. `-a`
2. `-b`
3. `-c`
4. `-e`

# 83. `mount` 的哪个选项显示挂载情况？

1. `-q`
2. `-v`
3. `-l`
4. `-f`

# 84. 下面哪个命令显示当前路由？

1. `netstat`
2. `ifconfig`
3. `ip route`
4. `ip addr`

# 85. 哪个工具可以测量内存占用？

1. `ps`
2. `iotop`
3. `iostat`
4. `ifconfig`

# 86. 使用 `vmstat` 时，哪个统计代表 CPU 等待 I/O 的时间？

1. `sy`
2. `us`
3. `wa`
4. `io`

# 87. `uptime` 中的三个数字代表什么时间间隔？

1. 1, 5 分钟
2. 5, 10 分钟
3. 10, 30 分钟
4. 1, 30 秒

# 88. `sysctl` 的哪个选项显示所有值？

1. `-a`
2. `-b`
3. `-d`
4. `-e`

# 89. 使用 `systemctl` 杀死进程时，默认信号是什么？

1. `SIGKILL`
2. `SIGTERM`
3. `SIGINT`
4. `SIGCALL`

# 90. 你在共享库方面遇到困难。下面哪个命令打印缓存？

1. `ldconfig -C`
2. `ldd -f`
3. `ldconfig -p`
4. `ldd -b`

## 答案与解析

### 第 1 章：硬件与系统配置

1. A. `modprobe` 命令加载模块及其依赖项（如果适用）。`lsmod` 命令用于列出已加载模块，因此答案 B 错误。`insmod` 命令将加载模块但不会加载依赖项。答案 D，`rmmod` 用于从内存中移除模块。
2. C. 在内核命令行上给出的关键字 `single` 将把系统启动到单用户模式。其他选项不是。
3. A. 如果在控制权首次交给 GRUB 时按下 Shift 键，将显示 GRUB 菜单。
4. D. `dmesg` 命令显示内核环缓冲区的内容。在许多 Linux 发行版中，此日志也保存到 `/var/log/dmesg`。此题显示的其他选项都不是有效命令。
5. D. `lsmod` 命令用于列出当前加载的模块，因此此题的答案 D 是正确的。`insmod` 命令（答案 A）用于加载模块。答案 C 是有效命令，但不是该命令的有效选项，答案 B 不存在。
6. D. LDAP 流量使用 TCP 端口 389。
7. C. 使用特定端口 SSH 的正确语法是 `ssh host:port`。
8. D. `tar` 中的 `-p` 选项保留权限。
9. A. `-w` 选项允许 `patch` 命令忽略空格。
10. C. `LUKS` 是 `dm-crypt` 的默认加密类型。
11. B. `journalctl` 的 `-r` 选项反向显示输出。
12. D. 当救援模式无法恢复时，`emergency` 目标可以作为救援模式的替代。
13. B. 为了保留用户所有权，应该从 `rsync` 选项中删除 `-o` 选项。
14. D. `ping` 的 `-A` 选项绕过路由表。
15. B. `patch` 的 `-b` 选项创建文件备份。
16. C. `Agent` 是监听连接并代表服务器执行命令的软件。
17. B. `\r\n` 代表回车和换行。
18. A. `-f` 文件测试检查文件是否存在（普通文件。
19. C. 使用 `bash test.sh` 即使没有执行位也会执行脚本。
20. A. `git ls-files -i --exclude-standard` 显示将被 `.gitignore` 忽略的内容。
21. C. 使用 `bash test.sh` 即使没有执行位也会执行脚本。
22. C. `tune2fs` 的 `-c` 选项设置最大计数。
23. C. `mount` 的 `-l` 选项列出挂载的文件系统。
24. C. `ip route` 是显示路由表的现代命令。
25. A. `ps` 提供进程相关的内存占用信息。
26. C. `wa` 代表 CPU 等待 I/O 的时间。
27. A. `uptime` 中的数字代表 1、5 和 15 分钟的平均负载。
28. A. `sysctl` 的 `-a` 选项显示所有变量。
29. B. `SIGTERM` 是 `systemctl kill` 发送的默认信号。
30. C. `ldconfig -p` 打印库缓存。




10. A. `update-grub` 命令将其输出发送到 `STDOUT`。因此，你必须使用 `>` 进行重定向并将输出发送到正确的文件。其他选项对于此目的均无效。答案 C 和 D 并不是有效命令，而答案 B 包含无效的选项和无效的目标文件位置。

11. B. 基于 MBR 的磁盘最多可以分为四个主分区，其中一个可以进一步分区或扩展为逻辑分区。

12. B. `0x82` 是 Linux 交换分区（swap），而 `0x83` 是 Linux。NTFS 是 `0x07`，FAT 是 `00c`。

13. A. `/etc/default/grub` 文件可用于此目的。你也可以编辑 `/boot/grub/grub.cfg`，但本题未提供该选项。

14. C. 使用 `-o` 选项可以指定目标文件，将输出发送到该文件而不是 `STDOUT`。本题列出的其他选项不存在。

15. A. `/boot` 分区通常远小于 500 MB，但不应设计过小。随着更多内核的添加（例如在升级过程中），`/boot` 内的占用空间将会增加。

16. B. `pvcreate` 命令初始化一个物理分区，以便将来以后作为 LVM 逻辑卷使用。

17. D. `grub2-install` 命令用于将 GRUB 安装到磁盘上。第二个 SATA 磁盘为 `/dev/sdb`，因此答案 D 是正确选项。

18. C. `lvcreate` 命令用于使用 LVM 创建逻辑卷。`pvcreate` 命令在创建逻辑卷之前初始化物理卷。本题另外两个选项中的命令不存在。

19. A. 首先初始化物理卷，然后创建卷组，最后创建逻辑卷。

20. B. 在修改了 `/etc/default/grub` 文件后，应运行 `grub-mkconfig` 命令，以便使用更改后的选项创建新的配置文件。

21. C. `lvmdiskscan` 命令查找已为供 LVM 使用而初始化的物理卷。

22. D. GRUB Legacy 从 0 开始计数，并用逗号分隔磁盘字母和分区，因此 `0,0` 是第一块磁盘上的第一个分区。答案 A 和 C 不是系统上的第一块磁盘，答案 B 包含一个不存在的分区。

23. B. 安装 GRUB 的命令是 `grub-install`，第一个 SATA 驱动器是 `/dev/sda`。列为 `hda` 的设备通常是 PATA 驱动器，因此这些选项是错误的。

24. C. `-y` 选项将尝试自动修复，实际上回答“y”或 yes 而不是提示。在其他选项中，只有 `-V` 是有效的且会产生详细输出。

25. D. 第一步是使用 `fdisk` 创建一个或多个分区。然后格式化分区，最后挂载分区使用。可以使用 `mkfs` 及其子命令创建各种文件系统类型。这些文件系统类型包括 `ext3`、`ext4`、`xfs` 和 `ntfs`。

26. B. `tune2fs` 命令可用于此目的，但应谨慎使用，因为它可能会导致数据损坏。

27. B. `ext3` 中日志增加了文件系统的可靠性和性能。

28. D. `/srv` 层次结构用于服务器程序的数据。`/etc` 层次结构是配置信息，而 `/var` 也是数据文件但是变量文件（如邮件文件）。`/tmp` 目录用于临时文件。由于每个路径都以 `/` 开头，因此被视为绝对路径。

29. C. `-a` 选项挂载 `/etc/fstab` 中所有当前可用的文件系统。在列出的其他选项中，只有 `-f` 选项可用，它是“fake”选项的快捷方式，除了执行挂载的模拟运行外，什么都不做。

30. A. `tune2fs` 命令显示关于文件系统的大量信息，包括文件系统挂载的次数。

31. A. `-g` 选项显示 dump 的进度。列出的其他选项不存在。

32. A. `du` 命令以递归方式报告磁盘使用情况，与此处显示的其他命令不同。

33. C. `/etc/fstab` 文件用于存储在系统中挂载的文件系统信息。

34. D. `/media` 挂载点用于可移动媒体。有关 FHS 的更多信息请参阅 [https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html]。

35. A. `/etc/mtab` 文件包含当前挂载的文件系统。注意 `/etc/fstab` 包含文件系统信息，但不包含哪些文件系统当前已挂载。

36. B. `-r` 选项导致 `umount` 尝试以只读模式重新挂载。`-v` 选项是详细模式，`-f` 选项强制操作。`-o` 选项不存在。

37. D. `gdisk` 中的 `c` 选项用于更改分区。`n` 选项创建新分区，`v` 选项验证磁盘。




55. C. 设置 `LANG=C` 是 POSIX 兼容的别名，将导致程序跳过本地化翻译。`LANG` 显示的其他选项都是无效的。

56. C. `LC_ALL` 变量可用于设置区域设置等环境变量，并会覆盖其他变量。这可以用于需要临时更改的情况。这里列出的其他变量不用于此目的，且默认不会创建。

57. A. `ln` 命令用于此目的，`-s` 选项创建符号链接，而 `-f` 强制或覆盖目标。其他选项和命令顺序都是无效的。

58. C. `LC_MONETARY` 变量被某些程序确定货币的本地化。

59. D. `hwclock` 命令用于查询和设置硬件时钟（例如由系统固件或 BIOS 维护的时钟）。`ntpdate` 命令用于设置本地系统时间但与硬件时钟无关。其他命令是无效的。

60. D. `-s` 选项按命令指定的日期和时间。如果有其他自动设置日期的方法，它可能会覆盖该更改。例如，如果 `ntpd` 正在运行，该进程在在使用 `date -s` 设置之后仍可能更改日期。

61. A. `-w` 选项将硬件时钟设置为当前系统时间。`-s` 选项执行相反操作，将系统时间设置为硬件时钟。`hwclock` 没有 `-a` 或 `-m` 功能。

62. A. `--systohc` 将根据当前系统时间设置硬件时钟。需要使用 `--utc` 以确保时间被设置为 UTC。如果省略了 `--utc`，时间将默认为上一次运行该命令时使用的值，这可能是 UTC，但也可能是本地时间。因此，最佳选项是 A。

63. A. `netstat` 命令可用于此目的，`-r` 选项显示当前路由。添加 `-n` 可以防止 DNS 查询，有助于提高性能。

64. D. 私有 IP 地址位于 `10.0.0.0/8`、`172.16.0.0/12` 和 `192.168.0.0/16` 范围内，因此 143 范围内的地址是公网 IP。

65. C. `route` 命令用于此目的，通过 `add` 选项添加路由。默认网关使用 `default gw` 关键字后跟网关和适配器的 IP 来添加。

66. A. `host` 命令允许 `-t` 选项更改查询类型。使用 `ns` 作为类型将查询给定域名的名称服务器。没有 `all` 类型，其他选项也是无效的。

67. B. `-I` 选项允许选择接口。小写的 `-i` 选项设置间隔，而 `-a` 表示有声的 ping。最后，`-t` 仅启用基于 TTL 的 ping。

68. A. 可以通过将类型设置为 `mx` 来使用 `host` 或 `dig` 命令实现此目的。`mx` 类型将查询给定域名的邮件交换器。没有 `smtp` 类型。

69. B. IPv6 的本地主机地址可以写为 `::1`。显示的 127 等地址代表 IPv4 本地主机范围，但没有正确地写入 IPv4 或 IPv6。

70. A. 带有 `monitor` 选项/子命令的 `ip` 命令将在 netlink 消息到达时显示它们。`ip` 没有 `netlink` 子命令，且 `route` 命令无法用于此目的。

71. A. 语法为 `database: databasename`，额外的数据库名称用空格分隔，如本题正确选项所示。

72. A. `@` 符号用于指示直接发送查询的服务器。这对于通过将查询直接发送到域名的权威名称服务器来排除解析问题非常有用。在其他选项中，`-t` 设置类型，其他选项均无效。

73. A. `getent` 命令用于处理 NSS 数据库，`getent hosts` 将显示使用 `/etc/nsswitch.conf` 中配置的数据库可用主机。

74. C. 配置选项是 `nameserver`，该选项的值是所需名称服务器的 IP 地址。多个选项影响域名解析的执行方式，例如尝试次数和超时。更多信息请参见 `resolv.conf(5)`。

75. A. `route` 命令可用于此目的，语法包括网络范围（用 `-net` 选项表示），随后是 `netmask` 单词和掩码位，最后是字母 `gw` 和网关的 IP。显示的其他选项由于各种原因（包括缺少关键字、选项和顺序）而无效。

76. A. `netstat` 命令用于此目的，`-a` 选项显示所有套接字（监听和非监听）。注意，经常添加 `-n` 选项或如 `netstat –an` 那样组合选项，以防止名称查找。这样做可以显著提高命令的性能。

77. A. 正确格式是 IP 地址，后跟规范主机名，然后是主机的任何别名。你可以使用 `/etc/hosts` 中的条目来覆盖 DNS 查询，这对于防止这些名称解析或提供不同的解析有用。

78. B. `ip route` 命令可用于此目的，其语法使用 `change` 命令和 `via` 关键字。相同的操作可以通过 `route` 命令完成，但需要先删除现有网关，然后重新添加新的默认网关。

79. A. `soa` 类型用于查询域的起始机构（SOA）记录。注意，在许多情况下，`dig` 会尝试在给定命令中查找域，看起来可能没有错误。例如，运行选项 D (`dig -t auth example.com`) 时，你将收到有关 `example.com` 的信息，输出中将有一行说明 `dig` 忽略了无效的类型 `auth`。

80. A. `search` 选项用于此目的，可以提供多个域名，每个域名用空格或制表符分隔。`domain` 选项在 `/etc/resolv.conf` 中有效，但不允许多个域名。

81. A. `route` 命令可用于此目的，在描述的场景中，路由使用了 `reject` 目标。显示的其他选项无效的，因为它们对 `route` 命令使用了无效的选项。

82. D. `-c` 选项提供发送的 ping 计数。`-n` 选项仅指定数字输出，而 `-p` 指定用于数据包内容的模式。最后，`-t` 选项设置 TTL。

83. D. 本题的最优选项是在 `/etc/hosts` 中为主机添加条目。这样做将导致 DNS 查询始终解析到 `127.0.0.1`。其他选项不够稳健，因为它们依赖于 `www.example.com` 始终具有相同的 IP 地址，或者如果 `www.example.com` 的 IP 地址更改，解决方案需要额外的维护来不断添加新的 IP 地址。

84. A. 在更改路由后应执行 `ip route flush cache` 命令。本题显示的其他命令都是无效的。

85. A. SPF 记录存储在 DNS 的 `txt` 记录类型中，因此 `-t txt` 是此目的的正确选项。在其他答案中，只有 `-t mx` 是有效的的；它返回给定域的邮件交换器。

86. C. `G` 表示路由表中的网关。

87. A. `axfr` 类型是区域传输，`@` 符号表示发送查询的服务器。没有 `xfer` 类型，选项 B 只是发送到指定服务器的域名的普通查询。

88. D. `iostat` 的 `-p` 选项显示设备和分区的信息。`-c` 选项显示 CPU 利用率，`-d` 显示设备利用率。没有 `-a` 选项。




89. A. `df` 命令显示磁盘使用信息，并可以帮助规划随时间变化的磁盘利用率。例如，如果你注意到磁盘利用率显著增加，可以准备上线更多磁盘，甚至更改日志轮转计划，使日志更快地轮转，从而释放空间。

90. A. `mkinitrd` 命令用于旧系统中创建初始 RAM 磁盘（initial RAM disk）。初始 RAM 磁盘用于加载（有些人可能说是预加载）用于磁盘和其他启动所需的其他关键组件的核心模块。

91. B. `lsmod` 命令用于显示当前加载的模块。这对于从标准内核或发行版提供的内核迁移到自定义内核的情况非常有用，因为你需要知道哪些模块需要编译到新内核中。

92. B. `depmod` 命令用于创建模块列表。该列表存储在名为 `modules.dep` 的文件中，其位置取决于所使用的 Linux Linux 发行版。

93. A. `-a` 选项显示 `sysctl` 的所有值及其当前设置。`-b` 选项是二进制格式，显示不带任何换行符的值。`-d` 选项是 `-h` 的别名，即帮助显示。没有 `-c` 选项。`sysctl` 选项可以在 `/etc/sysctl.conf` 中找到。

94. B. `modprobe` 命令检查给定模块的依赖关系，并同时加载依赖项和请求的模块。

95. A. `modinfo` 命令提供给定内核模块的信息。你可以使用 `modinfo` 查找给定模块所需的参数以及它依赖的模块等其他信息。`modprobe` 命令用于加载模块。没有 `tracemod` 或 `modlist` 命令。

96. C. `insmod` 命令将模块插入到运行的内核中。然而，它不会尝试解析依赖关系，如果不存在所需的依赖模块或内核符号，它将输出错误。

97. B. `-r` 选项移除指定的内核模块，并可能尝试移除该模块所依赖的任何模块。`-d` 选项设置模块的根目录，而 `-v` 是详细模式（verbose），`-f` 强制强制加载模块。

98. B. `/etc/modprobe.d` 目录用于存储与模块相关的配置信息，例如用于黑名单的配置，以及其他配置信息，如 `udev` 和模块选项。

99. B. `dracut` 命令用于为新系统创建初始 RAM 磁盘，它取代了用于相同目的的旧 `mkinitrd` 命令。

100. B. 放在 `/etc/sysctl.conf` 中的变量和值将在启动时生效。列出的其他文件无效。

101. B. `--show-depends` 选项显示给定模块的依赖关系。其他选项对于 `modprobe` 命令。

102. C. `mount` 命令的格式为 `[partition] [target]`，因此选项 C 是正确的。其他选项无效，因为参数顺序错误。

103. D. `-n` 选项仅更改下次启动的启动顺序，并从指定的分区启动。`-b` 配合 `-B` 会修改后删除该选项。`-o` 选项设置启动顺序。`-c` 选项创建启动编号。

104. A. ISOLINUX 为格式化为 ISO 9660 的 CD-ROM 提供了一种启动手段。使用 ISOLINUX 启动的活动 CD 或救援/恢复 CD 是非常常见的。其他引导程序对于此目的无效或不存在。

105. B. 由于微软 UEFI 设计中做出的显然不安全的决策，通常需要一个 shim 来使 Linux 能够在带有 UEFI 的系统上启动。`shim.efi` 文件可以作为此目的的初始引导器。

106. B. UEFI shell 中的 `bcfg` 命令用于配置基于 UEFI 的系统上的引导程序。该命令可以接受各种参数，以配置引导程序和内核在启动时的加载方式。在显示的其他命令中，`grub-install` 是有效的，但不在 UEFI shell 内部。

107. B. 主引导记录（MBR）是磁盘上的第一个扇区，包含关于磁盘结构的信息。如果 MBR 损坏，磁盘上的所有数据可能会丢失。此问题显示的其他选项无效。

108. D. `pxelinux.0` 文件必须存在于 TFTP 服务器的 `/tftpboot` 目录下，系统才能使用 PXELINUX 启动。其他文件对于 PXELINUX 无效或不必。启动后，PXE 启动可以使用 NFS 挂载的文件系统进行启动，该文件系统物理上托管在不同的计算机上。

109. D. `--boot-directory` 选项允许你指定 GRUB 镜像的替代位置而不是默认的 `/boot`。此问题显示的其他选项无效。

110. C. `shim.efi` 引导器加载另一个引导器，默认是 `grubx64.efi`。其他选项不是此类目的的文件名。

111. C. `-t` 选项将文件系统类型设置为 `ext2`、`ext3` 或 `ext4`。`mke2fs` 命令通常是 `/sbin/mkfs.ext2` `/sbin/mkfs.ext3` 和 `/sbin/mkfs.ext4` 的软链接。`-f` 选项强制 `mke2fs` 创建文件系统。`-a` 和 `-e` 选项不存在。

112. B. `/etc/crypttab` 文件包含加密的文件系统和设备。其他文件路径默认不存在，且与此问题无关。

113. C. `-b` 选项显示坏块（Bad blocks）。`-f` 选项强制 `dumpe2fs` 执行请求的操作，其他命令选项不存在。

114. C. `-f` 选项指定 `xfs_check` 应检查指定文件内容的一致性。`-v` 选项设置详细程度，没有 `-d` 或 `-a` 选项。

115. A. 导入或恢复的块大小必须与导出或转储使用的块大小匹配。块大小通过 `-b` 选项指定，因此 A 是正确的。其他选项对于 `xfsrestore` 无效。

116. B. 挂载选项为 `defaults` 的文件系统将 `rw`、`suid` 挂载，并具有执行权限（`exec`）。该文件系统将自动挂载（`auto`），但用户将无法挂载它（`nouser`）。字符和块设备将被解释（`dev`），对磁盘的操作将以异步方式进行（`async`）。

117. C. `-z` 选项设置包含转储的文件的最大大小。`-b` 选项设置块大小，但与此场景中的问题无关。`-s` 选项设置包含在转储中的路径，`-p` 设置进度指示器的时间间隔。

118. D. 分区类型 0xFD 用于软件 RAID 阵列。可以使用如 `fdisk` 等工具设置或查看。显示的其他选项不是有效的分区类型。

119. C. `/dev/disk/by-id` 目录包含指向 `/dev/sd` 的符号链接，例如 `/dev/sda`。因为 WWID 可以跨系统识别设备，因此它们经常用于 SAN 环境中。列出的其他目录不存在。

120. C. `pvdisplay` 命令显示给定物理卷（PV）的信息。你可以使用 `pvdisplay` 查看构建 PV 的设备以及 PV 的区大小。显示的其他命令无效。





122. C. `multipath` 命令用于管理 LUN 等设备，并可用于查找服务器到 LUN 的路径，例如在 SAN 配置中。其他命令都是无效的，`ls` 除外：`ls` 是有效的，但显示的选项与 LUN 无关，而是 `ls` 命令各种标志的组合。

123. C. `fstrim` 命令用于删除未使用的块。在 SAN 配置中，经常使用 `fstrim` 命令用以将未使用的存储空间还给 SAN。`fstrim` 命令也可以用于固态硬盘以达到相同的目的。显示的其他命令是无效的。

124. B. `-E` 选项表示后面跟着一个扩展选项，例如 `stripe_width`。`-f` 选项强制执行操作，但在本解决方案中没有必要，而 `-e` 选项设置错误时的行为。没有 `-extend` 选项。

125. A. `--create` 选项启用使用 `md` 创建 RAID 数组。典型的参数是 `/dev/mdN` 设备。列出的其他选项对 `mdadm` 都是无效的。

126. C. `/dev/mapper` 目录包含有关逻辑卷等多路径设备的信息。其他目录是无效的。

127. C. `--monitor` 选项用于主动监控数组是否存在如磁盘故障等问题。监控可以作为守护进程并在后台运行，从而在出现问题时发出警报。

128. B. `MAILADDR` 选项设置 `mdadm` 在监控模式下记录的 RAID 事件的邮件目的地址。

129. C. `ip` 命令在未使用 `-f` 选项进行指定的情况下，默认使用 `inet` 族。该命令将尝试猜测正确的族并回退到 `inet`。作为此命令选项列出的其他族对 `ip` 命令来说都是无效的。

130. B. `iwconfig` 命令与 `ifconfig` 命令类似，与单个无线接口工作，以设置和显示参数。在其他命令中，`ifconfig` 命令是有效的，但不用于无线网络。其他命令是无效的。

131. A. `ss` 命令提供了与 `netstat` 许多相同的功能，但可以显示一些扩展信息，例如给定套 的内存分配。`free` 命令显示内存使用情况但不是按套接的，另外两个命令不存在。

132. C. `-p` 选项在 `ss` 输出中显示与给定套接相关的进程 ID。`-a` 选项表示所有套接，而 `-l` 表示监听的套接。`-f` 选项用于指定协议族。

133. D. `/etc/network` 目录包含网络接口的信息，并包含目录，这些目录进一步包含在接口启动或关闭时要执行的脚本。列出的其他目录不存在。

134. B. 在 `/etc/hosts` 中，只有字母数字、减号（或连字符）和点是有效的主机。

135. B. `/etc/resolv.conf` 中的选项以 `options` 关键字开头，随后跟有一个或多个选项，如 `debug`。

136. C. `-f` 选项将强制执行 `umount`。`--fake` 选项本质上是干运行，因为它不会实际卸载文件系统。另外两个选项不存在。

137. A. `--output` 选项配置命令输出的位置，而不是 `STDOUT`。

138. A. 文件 `lpxelinux.0` 包含支持从 HTTP 和 FTP 启动所需的代码。

139. B. 文件 `/etc/grub2.cfg` 通常是 `/boot/grub2/grub.cfg` 的符号链接。

140. C. `vmlinuz` 文件经过压缩，因此比 `vmlinux` 占用磁盘空间。两者都包含二进制格式的 Linux 内核。

141. C. 模块存储在 `/usr/lib/modules/{kernel-version}` 中。

142. C. 文件 `/var/log/kern.log` 包含内核消息，可用于诊断内核崩溃（kernel panic）。

143. B. JSON 格式的文件是 JavaScript 对象表示。这些文件与 YAML 文件经常被用于提供模板和配置信息，因为这两种格式都是轻量级且具描述性的。在处理虚拟机模板或自动化时，你可能会遇到这些格式。

144. D. 持久卷在虚拟化环境的部署之间保留数据。容器镜像用于原始启动。

145. B. 双宿网络配置是指具有两个网络接口的配置。桥接网络（Bridged networking）是指在虚拟化场景中使用主机适配器。叠加网络（Overlay network）是指构建在另一个网络之上的网络。转发与此解决方案无关。

146. C. `localectl` 命令用于查看和配置针对特定区域的键盘布局等设置。列出的其他命令不存在。

147. D. 目录 `/etc/sysconfig/network-scripts` 包含与网络配置的文件。不再建议直接编辑这些文件，而是通过 Network Manager 使用 `nmcli` 和 `nmtui` 等命令。其他路径默认不存在。

148. A. `e2label` 命令更改文件系统标签。其他命令不存在。

149. B. OVF 采用 XML 格式。经常看到 YML 扩展名，通常包含 YAML 格式的数据，但这与此问题无关。HTML 是有效的文档标准，但不是用于 OVF 文件。没有 OVFMeta 文档标准。

150. A. 网络地址翻译 (NAT) 有效将虚拟机隐藏在主机 IP 地址之后。桥接允许虚拟机获取自己的 IP，从而让外部客户端也能访问它。

151. B. 文件 `/etc/modprobe.conf` 是一个旧文件，可能会在 Linux 的后续版本中删除，它包含系统模块配置的信息。其他文件不存在。

152. C. `active-backup` 模式用于创建“主备用”配置，当其中一个适配器故障时，另一个将接管。其他选项无效。

153. D. `kernel-install` 命令使用位于 `/usr/lib/kernel` 目录中的文件将内核及相关文件安装到 `/boot`。这里列出的其他命令均无效。

154. C. 相对路径以 `/` 以外的字符开头，而绝对路径始终以 `/` 开头，表示文件系统的根。其他选项——虚拟和符号不是描述路径的有效名称。

155. C. 原始设备（raw device）是指未分区的设备。原始设备有时用于虚拟化以及数据库场景，其中高层软件管理磁盘。显示的其他选项与此答案无关。高可用（Highly available）通常仅指冗磁盘或网络场景。

156. A. 值 1 启用调试日志。值 2 是信息（info），3 是警告（warn），4 是错误（error）。

157. B. Anaconda 是 Red Hat 和 CentOS 系统的安装程序名称。Kickstart 可用于脚本化和自动化安装过程。

158. A. `time` 命令包含计时信息，如系统时间、用户时间和实际时间。其他命令无效的。

159. D. Blob（或二进制大对象）是一种经常与云环境关联的存储格式。Blob 存储允许将单个对象作为独立对象存储。其他格式是有效的，但其他选项中没有适用于该场景的最合适机制。





### 163 C. `--list` 显示系统上可字符集。如果系统支持 `ASCII`、`UTF-8` 和 `UNICODE` 等字符集，将会被显示。此题提供的其他选项并不存在。

### 164 A. `/dev/` 文件系统用于存储连接设备的信息。`/etc/` 文件系统用于配置文件，且不存在用于开发或内核设备列表的禁止目录。

### 165 B. `/proc/mounts` 文件显示当前挂载的文件系统。`/etc/fstab` 文件用于挂载文件系统，但它不会随着文件系统挂载的变化而实时更新。列出的其他文件并不存在。

### 166 B. `CIFS` 是通用互联网文件系统，现在被认为是遗留文件系统，已被 `SMB3` 取代。`CIFS` 是 `SMB` 的实现，通常用于旧版本的 Microsoft Windows。

### 167 B. `YAML` 格式用于 `cloud-init` 的配置文件。`XML` 以及列出的其他格式均未用于 `cloud-init`。

### 168 C. `-g` 选项清除缓存以移除不存在的设备。`-p` 选项跳过缓存。`blkid` 没有 `-a` 或 `-m` 选项。

### 169 D. `/dev/disk/by-uuid` 文件显示系统上磁盘的 `UUID`。其他位置并不存在。

### 170 C. `/etc/sysconfig/network` 文件默认创建，但在 `RHEL7` 等系统上不再填充内容。对于依赖此位置的环境，可以使用它来替代 `Network Manager`。此题提供的其他选项并不存在。

### 171 B. 交换机应支持 `LACP` 聚合功能才能正常工作。`802.11` 协议用于无线网络，且不存在 `LinkAG` 或 `802.3ag` 协议规范。

### 172 A. `virt-install` 命令用于创建虚拟机。提供的其他答案并不存在。

### 173 C. 使用 `-A` 选项时，`-R` 选项会跳过根文件系统。`-M` 选项不检查挂载的文件系统。没有 `-S` 选项。

### 174 A. `Type 1` 虚拟机器也称为裸金属虚拟机器，可以在没有宿主操作系统的情况下进行安装。托管型虚拟机器有时被称为 `Type 2`。列出的其他选项既不是 `Type 1` 也不是 `Type 2`。

### 175 D. `/proc/partitions` 文件包含系统上的分区列表，以及它们的主设备号、次设备号和块数。`/dev/disk/` 选项是一个目录而非文件，因此对本题是不正确的。显示的其他选项并不存在。

### 176 C. `/sys/block/sda/stat` 文件包含关于 `sda` 设备的信息。`/sys/block` 层次结构包含了关于系统上块设备的信息。

### 177 A. `OVA` 文件是设备文件，意味着它包含了可以作为设备执行的信息和镜像，终端用户几乎或完全不需要配置。此题提供的其他选项未被使用，或未描述 `OVA` 文件。

### 178 B. `/etc/netplan` 中的文件用于较新版本 Ubuntu 系统的网络配置，应采用 `YAML` 格式格式化并以 `.yaml` 扩展命名。

### 179 D. `-s` 选项按目录汇总输出，而 `-h` 选项以更符合人类阅读习惯的方式呈现输出。

### 180 B. `WWID`（或全局标识符）是全局唯一的。`UUID` 和 `GUID` 不是多路径设备的有效缩写。`UUID` 通常用于普通块设备，而 `GUID` 是有时在应用程序使用的术语。没有与本题可能答案相关的 `DISKID` 名称。

### 181 D. `SFTP` 无法配合 `kickstart` 使用。其他选项以及 `FTP` 和本地驱动器（未列出）均适用于 `kickstart`。

### 182 C. `balance-rr` 模式用于提供轮询负载均衡。提供的其他选项不是模式。

### 183 B. `-D` 选项告诉 `dmesg` 停止向控制台显示消息。`-F` 选项有效，但用于从文件读取，因此与本题无关。没有 `-o` 或 `-Q` 选项。

### 184 A. `-f` 选项强制卸载模块。其他选项对 `rmmod` 无效。

### 185 A. `-A` 选项检查 `modules.dep` 以查找新模块，如果没有更改则不自动重新生成文件。`-C` 选项更改配置文件的位置。其他选项对 `depmod` 无效。

### 186 B. `lsblk` 命令以树形结构显示设备信息，并显示指定的其他信息、主次设备号以及分区是否为只读。在提供的其他选项中，`fsck` 是唯一的命令，且它不用于所述目的。

### 187 C. `-m` 选项以机器可读格式显示输出。`-v` 选项打印 `parted` 的版本。没有 `-p` 或 `-S` 选项。

### 188 B. `brctl` 命令用于创建以太网桥，也用于管理已创建的桥。显示的其他选项无效。

### 189 A. `/etc/dhcpd.conf` 文件用于 `DHCP` 配置。需要注意的是，该文件的位置在不同发行之间之间，有时也可以在 `/etc/dhcp/dhcpd.conf` 找到。此题提供的其他选项不是有效的文件位置。

### 190 C. 将使用 `ethtool` 命令用于此，`-i` 选项显示正在使用的驱动程序。其他命令对此目的无效。

### 191 B. `server` 命令更改当前会话中从 `nslookup` 发出的查询的目标地址。显示的其他选项无效。

# 第 2 章：系统操作与维护

### 1. B. 当前中断 (IRQ) 分配包含在 `/proc/interrupts` 文件中。因此使用 `cat` 等命令查看文件内容是有效的。没有 `view` 命令，因此答案 A 错误。同样，没有 `/dev/irq` 文件，因此答案 C 和 D 错误。

### 2. D. `udev` 的配置文件位于 `/etc/udev` 和相关的 `/etc/udev/rules.d` 中，这使得答案 D 正确。其他选项不存在。

### 3. B. `lsusb` 命令用于获取系统上 USB 设备的基本列表。其他命令无效。在答案 D 的情况下，`ls` 命令有效，但没有 `--usb` 选项。

### 4. C. 运行级别 1（有时显示为运行级别 `s` 或 `S`）是单用户模式，许多服务未启动。运行级别 5 和 6 用于其他用途，且运行级别 `SU` 不是有效选项。

### 5. D. 在使用 `SysVinit` 的系统中，脚本存储在 `/etc/init.d` 中。你有时也可以发现 `/etc/rc.d/init.d` 链接。其他选项对本题无效。

### 6. A. `init` 命令可以访问不同的运行级别。运行级别 6 用于重启系统。答案 B 将关闭系统而非重启。答案 C 将系统置于单用户模式。答案 D 不是有效选项。

### 7. B. `--list` 选项将显示系统上的所有服务以及它们在每个运行级别的状态。`on` 和 `off` 选项分别启用和禁用服务。

### 8. C. USB 设备通常被认为是热插拔设备。热插拔设备可以在系统“热运行”或开启时插入和拔出，而冷插拔设备是指在系统关机时必须插入或拔出的设备。

### 9. C. `ExecStart` 选项指示了 `systemd` 服务启动时执行的命令。

### 10. D. `systemctl get-default` 命令将显示默认目标。其他命令无效。

### 11. A. `enable` 选项配置服务在启动时运行。`start` 选项（答案 D）用于立即启动服务。其他选项对该命令无效。





### 12. C
`/proc` 文件系统包含当前运行进程的信息，以及关于内核和系统当前启动的额外信息。

### 13. D
`ldconfig` 命令更新当前的共享库缓存和列表。`ldconfig` 读取 `/etc/ld.so.conf` 并整合其中发现的更改。此问题中列出的其他选项并不存在。

### 14. B
`apt-get` 的 `upgrade` 选项将系统中已安装的软件包升级到最新版本。不存在 `apt-update` 命令，`dpkg` 也没有 `-U` 选项。`apt-cache` 命令用于处理软件包缓存。

### 15. C
`yum install` 命令将安装指定的软件包。`update` 选项将更新软件包。列出的其他选项并不存在。

### 16. A
`rpm2cpio` 默认将其输出发送到 `STDOUT`，因此在大多数情况下需要将该输出重定向到文件中。

### 17. D
`ldd` 命令将列出命令参数所依赖的库。

### 18. C
`lsusb` 的 `-t` 选项将以树状格式输出，以便查看哪些设备连接到哪些总线。`lsusb` 的其他参数是无效的，且 `usblist` 命令不存在。

### 19. A
根据 SCSI 类型的不同，每个总线支持 7 到 15 个设备。

### 20. C
在给出的选项中，`systemctl status` 命令和选项是最合适的。`telinit` 和 `sysctl` 命令不用于此目的。同样，`systemctl` 的 `--ls` 选项是无效的。

### 21. B
`isolate` 选项用于将系统移动到指定的目标，因此选项 B 是正确的。其他选项并不存在。

### 22. C
在对 `/etc/inittab` 进行更改后，可以使用 `telinit` 命令刷新系统。值得注意的是，答案 B 将重启系统，但根据题目要求这并不是一个给选项。答案 A 和 D 不是有效命令。

### 23. D
`runlevel` 命令显示系统的当前运行级别（runlevel）。答案 B 不是 `init` 命令的有效选项，而在此 `init` 命令前加上 `sudo` 没有区别。答案 A 不是有效命令。

### 24. C
单元配置文件存储在 `/lib/systemd/system` 中。此问题中的其他目录选项不相关，或者默认不存在。

### 25. A
列表显示了一个使用 `ln` 命令创建的符号链接文件，位于当前目录，链接到 `.configs/fetchmail/.fetchmailrc`。该文件属于 root 用户和 root 组，创建于 2014 年 7 月 8 日。

### 26. B
`systemctl` 命令用于处理服务和目标（targets）。`list-units` 命令用于列出目标。其他命令不用于此目的，或者在所需的选项下不存在。

### 27. C
`-nn` 选项同时显示数字和设备名称，因此答案 C 是正确的。`-n` 选项（答案 B）仅显示数字。另外两个选项不存在。

### 28. D
`/proc/bus/usb` 目录包含关于 USB 设备的信息。其他目录对于此目的无效的。对于基于 `udev` 的内核，`/proc/bus/usb` 可能默认不存在。该路径是旧版 `usbfs` 的一部分。

### 29. C
SATA 磁盘的地址为 `/dev/sdX`，就像 SCSI 磁盘一样。`/dev/hdX` 是传统的 ATA 磁盘。其他选项不存在。

### 30. D
包含 `/var` 的分区应该是邮件服务器最大的，因为邮件队列（mail spools）存储在该层次结构中。`/etc/` 层级通常很小，`/usr/bin` 也是如此。`/mail` 目录默认不存在。

### 31. B
`deplist` 选项显示指定软件包的依赖。`list` 选项显示特定软件包的信息，另外两个选项无效。

### 32. A
`-ivh` 选项将使用 `rpm` 安装文件，同时显示详细输出和进度哈希标记（hash marks）。呈现的其他选项不存在或无法完成指定任务。

### 33. A
`apt-cache` 命令用于处理软件包缓存，`search` 选项用于在缓存搜索提供的参数（在此例中为 `zsh`）。`apt-get` 命令用于处理软件包本身，而 `apt-search` 命令不存在。

### 34. D
`yum` 存储库的配置文件位于 `/etc/yum.repos.d`。在其他选项中，`/etc/yum.conf` 是文件而不是目录，其他目录不存在。

### 35. A
`-V` 或 `--verify` 选项将检查给定软件包中的文件与软件包数据库中的版本（或校验和）是否一致。如果没有文件被更改，则不产生输出。请注意，对于在安装期间或其他原因更改的文件，可能会产生输出。还要注意此选项使用的是大写的 `V`，而不是 `verbose*` 的小写 `v`。

### 36. B
`/etc/lib` 目录通常不与库文件关联，除非手动创建，否则 Linux 系统上通常不存在。其他选项要么包含系统库，要么可以用于该目的。

### 37. C
`apt-get update` 命令通过从软件包源检索最新的软件包列表来更新软件包缓存。不存在 `cache-update` 选项或 `apt-cache` 的 `update` 选项。`upgrade` 选项用于更新系统的软件包，而不是缓存。

### 38. C
位于 `/etc/apt` 的 `sources.list` 文件包含 Debian 软件包的存储库列表。其他文件位置默认不存在。

### 39. A
`dpkg-reconfigure` 程序将导致已安装的软件包被重新配置或更改。`dpkg` 的 `-r` 选项移除软件包，因此答案 B 是错误的。`dpkg` 没有 `reconf` 选项，`apt-get` 也没有 `reinstall` 选项。

### 40. D
`search` 选项对软件包名和描述等各种字段进行搜索。

### 41. B
`rpm -q kernel` 将显示内核版本。你也可以使用 `uname -r` 实现相同目的。

### 42. A
`exclude` 选项可排除某些软件包。该参数接受通配符，因此排除 `kernel*` 将产生所需的行为。

### 43. B
`dpkg` 的 `-s` 搜索软件包并提供其当前状态的信息。`apt-cache` 命令不用于此目的，`dpkg` 的 `-i` 选项安装软件包。`apt-info` 命令不存在。

### 44. A
`dpkg` 的 `-i` 选项将安装之前下载的 `.deb` Debian 软件包。其他命令不存在，`dpkg` 的 `-U` 选项不存在。

### 45. C
`.tgz` 文件通常表示压缩过的 tar 文件。`-z` 选项用于表示文件应该解压缩，`-x` 表示文件应该解包。`-v` 选项不是必须的，但会提供详细输出。最后，`-f` 选项指定要使用的文件。如果文件没有压缩（可能通过具有 `.tar` 后名看出），则可以省略 `-z` 选项。

### 46. C
`info` 选项在运行 `zypper` 工具的系统上显示关于给定软件包的信息。

### 47. A
`search` 选项通过命令行提供的名称查找软件包。其他选项对于 `dnf` 命令无效。

### 48. A
`g` 选项（也称为 `global` 或 `greedy`）将匹配项的操作应用于整行，而不仅仅是匹配项的第一个实例。其他选项的应用方式与 Perl 兼容正则表达式（PCRE）相同。

### 49. C
`-l` 选项提供输入的输入行数。例如，`wc -l /etc/passwd` 将打印 `/etc/passwd` 文件的行数。此问题中提供的其他选项对于 `wc` 命令无效。

### 50. C
`head` 和 `tail` 默认都输出 10 行。





51. B. `rm` 的 `-rf` 选项将递归删除目录的内容，包括其他目录。在这种情况下，单独使用 `-f` 选项将不起作用，因为存在额外的目录。`rmdir` 提供的其他选项并不存在。

52. D. `-type` 选项使 `find` 将搜索限制在目录上，而 `-name` 选项限制了返回元素的名称。注意由于问句的表述方式，这里使用了通配符。还要注意使用 `./` 表示从当前目录开始搜索。

53. A. `cat` 命令将显示 `/etc/passwd` 文件的内容，然后将该输出管道给 `awk` 命令。`awk` 命令随后解析其输入，按照 `/etc/passwd` 指定的分隔符（即冒号 `:`）进行分割。输出随后被打印并管道到 `sort` 命令。选项 B 中的 `sort` 命令将不起作用，因为 `cut` 命令需要一个参数。同样，选项 C 中的 `echo` 命令只会向 `STDOUT`（标准输出）输出 `echo /etc/passwd`。

54. C. `ls` 的 `-l` 选项产生长格式或列表输出，而 `-t` 按时间戳排序。`-r` 选项反转顺序，而 `-a` 需要包含隐藏（点开头）文件，因此答案 C 是确的。

55. A. 当对已存在的文件运行 `touch` 时，该文件的时间戳将会改变。

56. D. `-i` 选项将使 `cp` 和 `mv` 都变为交互模式；即在覆盖之前进行提示。`-f` 选项将强制命令运行，而 `-r` 是递归的。

57. C. `tee` 命令将输出同时发送到 `STDOUT` 和指定的文件，因此答案 C 是确的。选项 A 将将输出重定向到正确的文件，但不会同时重定向到 `STDOUT`。其他答案不适用于此问题。

58. A. `-p` 选项允许 `mkdir` 创建额外的目录层级而不报错。在这种情况下，不带选项运行 `mkdir` 将不起作用。`mkdir` 的 `-r` 和 `-f` 选项并不存在。

59. B. `-R` 选项将递归复制目录。注意，如果没有启用 `-i` 选项，递归复制将覆盖目标位置的文件。`-v` 选项增加了详细性，但不会导致任何递归，而 `-Z` 选项不存在。

60. B. `cut` 命令使用 Tab 键作为默认分隔符。可以通过 `-d` 选项进行更改。

61. D. 如果一个命令通过 `&` 或 `bg` 命令置于后台，`fg` 命令将将其带回前台。

62. A. 你需要将更改写入文件，因此你需要 `:w`。加上 `q` 也会退出。注意你也可以使用 `ZZ` 写入并退出。Vi 中的 `dd` 命令删除一行，而 `x` 删除单个字符。

63. D. `-n` 选项将 `head` 和 `tail` 的输出行数更改为指定的数字。此问题中列出的其他选项对 `head` 无效，而 `tail` 的 `-f` 选项会在文件增长时跟踪该文件。

64. C. `-9` 选项调用 `SIGKILL`，这将强制进程结束。信号 `15` 是默认信号。`-f` 和 `-stop` 选项不存在。

65. C. 在 bash 中，数字 1 代表 `STDOUT`，2 代表 `STDERR`。重定向两者意味着按照选项 C 所示的方式合并它们。

66. D. 在正则表达式中，`*` 代表 0 个或多个字符，在这种情况下，问题不在于用户是否使用 `/bin/bash` 或 `/usr/bin/zsh`。同样，`.` 匹配单个字符。但在 bash 和 zsh 的情况下，你需要同时查看第一个字符和可选的第二个字符：因此使用 `?`，它使得第二个 `.` 变为可选。最后，`$` 将模式锚定在字符串末尾，这是该正则表达式的关键。

67. C. `o` 命令在当前光标位置下方打开新行。`a` 命令在光标后的字符处开始插入模式，而不是行。

68. A. `-p` 选项允许 `mkdir` 创建额外的目录层级而不报错。在这种情况下，不带选项运行 `mkdir` 将不起作用。`mkdir` 的 `-r` 和 `-f` 选项不存在。

69. B. `-R` 选项将递归复制目录。注意，如果没有启用 `-i` 选项，递归复制将覆盖目标位置的文件。`-v` 选项增加了详细性，但不会导致任何递归，而 `-Z` 选项不存在。

70. B. `cut` 命令使用 Tab 键作为默认分隔符。可以通过 `-d` 选项进行更改。

71. D. 如果一个命令通过 `&` 或 `bg` 命令置于后台，`fg` 命令将将其带回前台。

72. A. 你需要将更改写入文件，因此你需要 `:w`。加上 `q` 也会退出。注意你也可以使用 `ZZ` 写入并退出。Vi 中的 `dd` 命令删除一行，而 `x` 删除单个字符。

73. D. `-n` 选项将 `head` 和 `tail` 的输出行数更改为指定的数字。此问题中列出的其他选项对 `head` 无效，而 `tail` 的 `-f` 选项会在文件增长时跟踪该文件。

74. C. `-9` 选项调用 `SIGKILL`，这将强制进程结束。信号 `15` 是默认信号。`-f` 和 `-stop` 选项不存在。

75. C. 在 bash 中，数字 1 代表 `STDOUT`，2 代表 `STDERR`。重定向两者意味着按照选项 C 所示的方式合并它们。

76. D. 在正则表达式中，`*` 代表 0 个或多个字符，在这种情况下，问题不在于用户是否使用 `/bin/bash` 或 `/usr/bin/zsh`。同样，`.` 匹配单个字符。但在 bash 和 zsh 的情况下，你需要同时查看第一个字符和可选的第二个字符：因此使用 `?`，它使得第二个 `.` 变为可选。最后，`$` 将模式锚定在字符串末尾，这是该正则表达式的关键。

77. C. `o` 命令在当前光标位置下方打开新行。`a` 命令在光标后的字符处开始插入模式，而不是行。

78. A. `-p` 选项允许 `mkdir` 创建额外的目录层级而不报错。在这种情况下，不带选项运行 `mkdir` 将不起作用。`mkdir` 的 `-r` 和 `-f` 选项并不存在。

79. B. `-R` 选项将递归复制目录。注意，如果没有启用 `-i` 选项，递归复制将覆盖目标位置的文件。`-v` 选项增加了详细性，但不会导致任何递归，而 `-Z` 选项不存在。

80. B. `cut` 命令使用 Tab 键作为默认分隔符。可以通过 `-d` 选项进行更改。

81. D. `fg` 命令将把一个命令带回前台，如果它已经通过 `&` 或 `bg` 命令置于后台。

82. A. 你需要将更改写入文件，因此你需要 `:w`。加上 `q` 也会退出。注意你也可以使用 `ZZ` 写入并退出。Vi 中的 `dd` 命令删除一行，而 `x` 删除单个字符。

83. D. `-n` 选项将 `head` 和 `tail` 的输出行数更改为指定的数字。此问题中列出的其他选项对 `head` 无效，而 `tail` 的 `-f` 选项会在文件增长时跟踪该文件。

84. C. `-9` 选项调用 `SIGKILL`，这将强制进程结束。信号 `15` 是默认信号。`-f` 和 `-stop` 选项不存在。

85. C. 在 bash 中，数字 1 代表 `STDOUT`，2 代表 `STDERR`。重定向两者意味着按照选项 C 所示的方式合并它们。

86. D. 在正则表达式中，`*` 代表 0 个或多个字符，在这种情况下，问题不在于用户是否使用 `/bin/bash` 或 `/usr/bin/zsh`。同样，`.` 匹配单个字符。但在 bash 和 zsh 的情况下，你需要同时查看第一个字符和可选的第二个字符：因此使用 `?`，它使得第二个 `.` 变为可选。最后，`$` 将模式锚定在字符串末尾，这是该正则表达式的关键。

87. C. `o` 命令在当前光标位置下方打开新行。`a` 命令在光标后的字符处开始插入模式，而不是行。

88. A. `-p` 选项允许 `mkdir` 创建额外的目录层级而不报错。在这种情况下，不带选项运行 `mkdir` 将不起作用。`mkdir` 的 `-r` 和 `-f` 选项并不存在。

89. B. `-R` 选项将递归复制目录。注意，如果没有启用 `-i` 选项，递归复制将覆盖目标位置的文件。`-v` 选项增加了详细性，但不会导致任何递归，而 `-Z` 选项不存在。

90. B. `cut` 命令使用 Tab 键作为默认分隔符。可以通过 `-d` 选项进行更改。

91. D. `fg` 命令将把一个命令带回前台，如果它已经通过 `&` 或 `bg` 命令置于后台。

92. A. 你需要将更改写入文件，因此你需要 `:w`。加上 `q` 也会退出。注意你也可以使用 `ZZ` 写入并退出。Vi 中的 `dd` 命令删除一行，而 `x` 删除单个字符。

93. D. `-n` 选项将 `head` 和 `tail` 的输出行数更改为指定的数字。此问题中列出的其他选项对 `head` 无效，而 `tail` 的 `-f` 选项会在文件增长时跟踪该文件。

94. C. `-9` 选项调用 `SIGKILL`，这将强制进程结束。信号 `15` 是默认信号。`-f` 和 `-stop` 选项不存在。

95. C. 在 bash 中，数字 1 代表 `STDOUT`，2 代表 `STDERR`。重定向两者意味着按照选项 C 所示的方式合并它们。

96. D. 在正则表达式中，`*` 代表 0 个或多个字符，在这种情况下，问题不在于用户是否使用 `/bin/bash` 或 `/usr/bin/zsh`。同样，`.` 匹配单个字符。但在 bash 和 zsh 的情况下，你需要同时查看第一个字符和可选的第二个字符：因此使用 `?`，它使得第二个 `.` 变为可选。最后，`$` 将模式锚定在字符串末尾，这是该正则表达式的关键。

97. C. `o` 命令在当前光标位置下方打开新行。`a` 命令在光标后的字符处开始插入模式，而不是行。





88. A. 如果你的家目录存在存在 `.bash_profile` 文件，它将在登录时被执行。请注意，将函数放在 `/etc/profile` 中在技术上是行的，但这样该函数将对所有用户可用，这并不是题目所要求的。

89. B. `xorg.conf` 中的 `Screen` 部分用于逻辑上绑定给定的显卡和显示器，其中每个设备都会在配置文件的各自对应的部分中定义。此题显示的其他选项都不存在。

90. A. 当使用 `SSH` 等协议时，可以使用 `DISPLAY` 变量将 X 会话的窗口远程发送到另一台计算机。不存在 `XTERMINAL` 或 `XDISP` 环境变量，`XTERM` 通常是一个终端窗口而不是环境变量。

91. D. `Welcome` 选项用于设置用户登录时在显示管理器中向用户显示的消息。对于远程用户，可以使用 `RemoteWelcome` 消息来实现相同的目的。

92. C. Shift 键可用于 Gnome 等其他图形界面中启用或禁用粘滞键（sticky keys），以实现辅助功能。

93. A. Orca 项目为 Gnome 提供了辅助屏幕阅读功能。在给出的其他选项中，`screen` 命令是有效的，但并非用于此目的。

94. D. `kmag` 程序用于放大桌面上的项目，并用作辅助技术。通常，`kmag` 也可以与其他窗口管理器配合使用。

95. B. 必须启用 `X11Forwarding` 选项，以便从 X 服务器生成的 X 连接或窗口通过 `SSH` 连接发送。

96. C. `/etc/passwd` 文件包含了有关系统中用户的各种信息，如用户名和真实姓名，以及用户 ID (UID) 和登录 shell。该文件是所有人可读的。

97. B. `cron` 的格式为 `[minute hour day-of-month month-of-year day-of-week]`，因此选项 B 是此题的正确答案。

98. B. `/etc/cron.allow` 文件是有权限创建和删除自己的 `cron` 任务的用户列表。`/etc/crontab` 文件用于存储 `cron` 任务。其他文件不存在。

99. B. `at` 命令用于运行输入的一系列命令。与 `cron` 不同，你可以从命令行调度命令，并按照输入的顺序执行执行，而无需为命令创建特定的脚本。选项 B 显示的语法将时间设置为现在一小时后。

100. B. `userdel` 命令用于此目的，`-r` 选项（小写）会同时删除家目录和邮件池文件。`-R` 选项（大写）则告知 `userdel` 命令使用一个 `chroot` 目录。

101. A. `groupmod` 命令用于此目的，`-n` 选项用于更改组名。列出的其他命令不存在。

102. A. `/var/spool/cron/crontabs` 目录包含每个当前拥有一个或多个 `cron` 任务或目的的用户的文件。请注意，此处列出的其他文件对于此目的是的。

103. C. `atrm` 命令根据 ID 删除任务。可以通过 `atq` 命令获取 ID。所示 `atq` 和 `at -l` 命令将列出任务而不会删除它们。`rmat` 命令无效的。

104. C. `/etc/crontab` 文件是一个纯文本文件，被视为系统范围内的 `cron` 文件。因此，该文件通常与任何单一用户关联，编辑此文件后无需运行特殊命令。

105. A. `/etc/cron.daily` 目录包含每天执行的脚本文件。相应的 `cron.hourly`、`cron.weekly` 和 `cron.monthly` 目录会根据目录名称按照各自的调度运行。

106. B. `-m` 选项会导致创建用户的 `home` 目录。默认情况下，如果没有指定此选项且未设置 `CREATE_HOME`，则不会创建 `home` 目录。`-h` 选项显示帮助文本，所示其他选项无效。

107. A. `usermod -L` 命令通过在加密密码中放置 `!` 来锁定账户。如果用户有其他登录方式（例如使用 `SSH` 密钥），使用 `usermod -L` 将无法阻止其登录。

108. A. 添加用户名时的格式将用户名放在调度时间和要执行的命令之间，因此选项 A 是正确的。此题显示的其他选项均无效。在选项 B 的情况下，没有调度时间。在选项 C 和 D 的情况下，调度时间格式不正确。

109. C. `passwd` 命令将用于此目的。`-a` 选项显示所有用户，但需要使用 `-S` 来指示状态。仅 `-S` 选项不会产生所有用户的报告，且 `--all` 选项是 `-a` 的别名。

110. B. `/etc/shadow` 文件包含用户名、UID 和加密密码，由于加密密码的敏感性，系统上的任何非 root 用户都无法读取。`/etc/passwd` 文件包含用户名和 UID，但不包含加密密码。此题列出的另外两个文件不存在。

111. D. 系统的 UID 和 GID 之间没有直接关系。UID 代表用户，而 GID 代表组 ID。在某些系统中，普通用户的 UID 和 GID 编号会匹配，但这并非强制要求，更多是一种巧合。

112. A. `usermod` 命令用于此目的。`-d` 选项更改家目录，而 `-m` 移动内容。此题显示的其他命令无效的。

113. D. `-G` 选项是用户将被的附加组列表。小写的 `-g` 选项提供主 GID。`-l` 选项导致用户不会添加到 `lastlog` 和 `faillog` 数据库中。不存在 `-x` 选项。

114. D. `chage` 命令用于此目的。`-d` 选项设置自上次更改密码以来的天数，自 1970 年 1 月 1 日起。`-W` 选项是更改密码的警告天数，`-l` 选项显示账户相关的各种设置列表。

115. A. `crontab` 命令可用于此目的，`-l` 选项用于列出 `crontab` 条目。需要 `-u` 选项指定当前用户以外的用户。

116. A. `-r` 选项创建一个系统用户，通常意味着没有过期、没有家目录且 UID 低于 1000。`-s` 选项定义 shell，通常不用于此目的。`-a` 和 `-S` 选项不存在。

117. B. `/etc/gshadow` 文件包含安全信息，如可能的组加密密码。`/etc/group` 文件包含组的一般信息。作为选项列出的另外两个文件不存在。

118. B. `groupdel` 命令无法删除组，除非没有用户将该组作为其主 GID。因此，选项 B 最符合场景。不存在 `-f` 或 `-r` 选项，使得选项 A 和 D 错误。

119. A. `id` 命令显示用户名、UID、主组和 GID 以及附加组。`passwd` 和 `chage` 命令不用于此目的。不存在 `getid` 命令。

120. D. `-c` 选项更改 `/etc/passwd` 中的注释字段。注释字段通常与账户的真实相关。`-R` 选项表示 `chroot` 目录，而 `-d` 表示更改家目录。不存在 `-n` 选项。

121. D. `find` 命令将用于此目的。正确的语法在选项 D 中。`group` 命令仅会在指定文件中查找数字 1501；而 `grep` 的 `-u` 选项包含字节偏移量，这不适用于本题。




122. A. 将地址设置为 `127.0.0.1` 将使用本地回环接口。其他本地 NTP 客户端将通过其正常的 IP 地址连接此服务器。

123. B. `newaliases` 命令用于在运行 Postfix、Sendmail 和 qmail 的服务器上重新创建别名数据库。运行 `newaliases` 后不需要重启邮件服务器。选项 C 所示的 `alias` 命令会为命令 shell 创建别名，但它与 Postfix 无关。

124. D. CUPS 的配置文件位于 `/etc/cups`。然而，通过其 Web 界面管理 CUPS 也是常见的。列出的其他目录都是无效的。

125. B. Qmail 目录默认包含 `/var/qmail` 中。队列目录是 `/var/qmail/queue`。其他目录在 Qmail 的默认配置中是的。

126. D. `info` 严重级别为特定的设施（facility）提供信息消息。在给出的选项中，`emerg` 用于紧急消息通常不用于应用程序；而 `debug` 是通过 `syslog` 可用的最高或最详细的日志级别。

127. C. `ntpq` 命令为 NTP 服务器提供了一个交互式的、菜单式的界面。例如，你可以使用 `ntpq` 检查对的统计信息。选项 B 所示的 `ntpdate` 命令用于设置时间的命令行工具。选项 A 所示的 `ntpd` 命令将执行 NTP 守护进程本身。

128. A. `lpr` 命令将文件（或标准输入）放入打印队列以供 `lpd` 处理。`lpq` 命令打印当前队列。没有 `lpx` 命令。

129. D. TCP 端口 631 用作进入 CUPS 的管理接口。访问该端口上的活动 CUPS 服务器将显示管理网站，用于处理打印队列和其他与 CUPS 相关的其他配置项。

130. A. 显示的 URL 将显示本地 CUPS 服务器的任务区域，其查询字符串名称为 `which_jobs`，值为 `completed`。列出的其他 URL 都是无效的。

131. A. `postqueue -f` 命令用于刷新队列。该命令将处理所有等待交付的电子邮件。其他命令对于此目的无效。

132. C. 应用程序理论上可以使用任何日志设施，取决于正在开发的应用程序类型。然而，记录到自定义日志文件的要求意味着日志将具有与标准日志不同的名称，可能还有不同的位置。因此，将日志记录到任何标准或系统级设施都不适用于此场景，因此使用本地设施（`local0` 到 `local7`）之一是合适的。

133. B. 带有 `-aG` 选项的 `usermod` 用于将组添加到用户的组列表中。在这种情况下，用户需要是 `lpadmin` 组的成员。

134. B. `mailstats` 命令用于描述的目的。在其他选项中，`mailq` 命令将显示当前邮件队列，但不会显示已处理邮件的统计信息。另外两个选项无效命令。

135. A. `systemctl` 命令用于控制服务。在这种情况下，应该向 CUPS 服务发送 `restart` 命令，如名称 `cups.service` 所示。

136. D. SNMP 流量发生在端口 161 和 162 上。虽然流量通常在 UDP 上，但 TCP 端口也预留给了 SNMP。端口 110 和 143 分别用于 POP3 和 IMAP，而 23 和 25 分别是 telnet 和 SMTP。最后，端口 80 和 443 是 HTTP 和 HTTPS。

137. D. 使用 `-f` 选项加载备用文件。这样做恰恰有助于描述的场景：能够从旧日志文件中检查登录情况。`-a` 选项控制主机显示的位置，而 `-t` 选项控制显示截至指定日期的登录情况。没有 `-e` 选项。

138. D. `w` 命令显示当前登录的用户以及如系统运行时间和平均负载负载等信息。`fuser` 命令用于显示打开的文件，`ls` 的 `-u` 选项控制文件列表的显示。没有 `listuser` 命令。

139. A. `usermod` 命令的正确格式是 `YYYY-MM-DD`。

140. A. 将为此目的使用 `systemctl` 命令，子命令是 `disable`。有一个 `stop` 子命令，但它只会停止给定的服务，而不是防止其在开机时启动。其他选项由于各种原因无效，包括它们使用 `systemd` 作为命令名称而不是 `systemctl`。

141. C. 最后更改密码的日期（自 1970 年 1 月 1 日起的天数）包含在 `shadow` 条目的第三字段中。过期日期将是冒号分隔的第八字段。

142. D. Nagios 提供了适用于描述场景的高级监控能力。Nagios 使用各种插件工作，监控设备和系统的许多方面。Ntop 和 mrtg 都提供图形统计数据，但没有指定的告警功能。

143. B. `make oldconfig` 命令将现有现有文件集成到内核的新配置中。对于新内核中移动或更改的项目，仍需要小心，以确保配置正确。

144. D. `udevadm` 命令用于处理内核中的 `udev` 接口，`monitor` 子命令实时显示内核 `uevent` 和其他 `udev` 事件。

145. C. 将为此目的使用 `systemctl` 命令，带有 `daemon-reload` 子命令。`reboot` 选项可以用于重载 `systemd` 配置，但它是错误的，因为它需要整个服务器重启，这并不是题目所要求的。

146. B. `/etc/inittab` 文件包含各种运行级别以及在给定运行级别要运行的内容。例如，运行级别 1 是单用户，运行级别 6 是重启，此类此类。列出的其他文件不存在。

147. D. `/etc/rc.d` 层次结构包含指向 `/etc/init.d` 内部文件的符号链接。这些符号链接随后用于在适当的运行级别执行脚本。例如，在启动时，系统将为启动时执行的每个运行级别执行 `runlevel` 目录中的脚本。

148. B. `/etc/auto.master` 文件包含 `autofs` 的配置。选项列出的其他文件对于此场景无效。

149. B. 支持 NVMe 的驱动器命名为 `/dev/nvme*`。除了现代系统中内核自带的驱动程序外，不需要特殊驱动程序。其他答案默认不存在路径。

150. B. `/sys/class/fc_host` 目录包含基于可用光纤通道的其他目录。在这些主机目录中，将在一个名为 `port_name` 的文件中找到 WWN（全球标识符）。其他目录层次结构是无效的。

151. C. `/dev/mapper` 目录包含关于多路径设备等逻辑卷的信息。其他目录是无效的。

152. A. 将为此目的使用 `iw` 命令。当配合特定设备使用 `iw` 时，会出现 `dev` 关键字，后面是设备名称，然后是在该设备上执行的命令。在这种情况下，使用了 `link` 命令。

153. A. 应使用 `grep` 命令，并应使用 `-i` 选项使 `grep` 不区分大小写。当配合 `-v` 使用时，`grep` 将排除参数，从而与此处的需求相反。内核环形缓冲区可能不包含有关 DHCP 的信息，因此 `dmesg` 不是正确选项。

154. B. `-c` 选项在首次读取后清除内核环形缓冲区。`-C` 选项立即清除。`-e` 选项显示相对时间和本地时间。没有 `-a` 选项。





155. C. `-a` 选项提供归档模式，它是其他几个选项的替代方案。`-r` 选项表示递归，`-o` 选项表示保留所有者，而 `-f` 选项启用过滤器。

156. A. 根据 `make` 命令的 `man(1)` 页面，文件名 `Makefile`（大写 M）是推荐的文件名。`makefile` 作为默认是有效的，但不是推荐选项。其他文件作为默认名称无效的。

157. B. `gunzip` 命令用于解压使用 `gzip` 压缩的文件。

158. D. `install` 目标将最终编译后的文件安装到适当的位置，并在适用时使其变为可执行。在其他选项中，`distclean` 有时被包含，并将源文件恢复到原始状态。列出的其他目标均无效。

159. D. `baseurl` 选项用于设置 URL 且必须是完全限定的，这意味着必须包含协议，例如 `http://` 或 `file://`。

160. A. `/boot` 目录几乎肯定存在，但尚未分区到独立空间中。如果 `/boot` 确实是一个独立分区，那么它不会在 `lsblk` 中隐藏。

161. A. 将使用 `grep` 命令实现此目的。注意 `grep -r` 和 `grep -ri` 之间的区别。问题没有要求忽略大小写，因此选项 B 使用 `-i` 导致它是错误的。

162. C. `-f` 选项将强制执行卸载。`--fake` 选项本质上是一个空运行，因为它不会实际卸载文件系统。另外两个选项不存在。

163. C. `<<<` 字符组合从 `STDIN` 或标准输入读取输入，并将其作为 `mail` 命令的消息正文。

164. B. `who` 命令显示当前登录的用户及其登录日期时间。`whois` 命令显示有关域名的信息。其他命令均无效。

165. A. 位于 `/etc/` 或 `/etc/bind/` 的 `named.conf` 文件是 BIND 服务器的默认配置文件。该文件通常加载或包含其他特定的配置文件以实现特定配置。

166. A. 将使用 `openssl` 命令实现此目的，并配合 `genrsa` 选项。使用 `-out` 指定输出文件。其他包含 `openssl` 的命令都包含无效选项。最后一个命令是 `openssh`，它不用于此场景。

167. B. `acl` 配置指令创建访问控制列表。访问控制列表是 Squid 代理设置中的强大功能，可以包含网络、MAC 地址、端口、浏览器等。

168. B. `http_access` 指令与 ACL 指令结合用以定义使用 Squid 代理的访问。其他指令在 Squid 中均无效。

169. B. `nmbd` 守护进程负责 NetBIOS 名称服务请求的处理。`smbd` 守护进程负责文件和打印共享，而 `winbindd` 提供用户和组信息。没有名为 `samba` 的守护进程。

170. A. `PermitRootLogin` 指令设置为 `yes` 或 `no`，决定 root 用户是否可以直接登录。显示的其他选项均无效。

171. B. `push` 指令用于在连接时向客户端发送路由。在这种情况下，发送了网络和子网掩码，`255.255.255.0` 对于 `/24` 是适当的。其他选项均无效。

172. A. 如果你使用 Wayland，会设置 `WAYLAND_DISPLAY` 环境变量。你可以通过以下查看

173. A. 将使用 `grep` 命令实现此目的。注意 `grep -r` 和 `grep -ri` 之间的区别。问题没有要求忽略大小写，因此选项 B 使用 `-i` 导致它是错误的。

174. C. `-f` 选项将强制执行卸载。`--fake` 选项本质上是一个空运行，因为它不会实际卸载文件系统。另外两个选项不存在。

175. C. `<<<` 字符组合从 `STDIN` 或标准输入读取输入，并将其作为 `mail` 命令的消息正文。

176. B. `who` 命令显示当前登录的用户及其登录日期时间。`whois` 命令显示有关域名的信息。其他命令均无效。

177. A. 位于 `/etc/` 或 `/etc/bind/` 的 `named.conf` 文件是 BIND 服务器的默认配置文件。该文件通常加载或包含其他特定的配置文件以实现特定配置。

178. A. 将使用 `openssl` 命令实现此目的，并配合 `genrsa` 选项。使用 `-out` 指定输出文件。其他包含 `openssl` 的命令都包含无效选项。最后一个命令是 `openssh`，它不用于此场景。

179. B. `acl` 配置指令创建访问控制列表。访问控制列表是 Squid 代理设置中的强大功能，可以包含网络、MAC 地址、端口、浏览器等。

180. B. `http_access` 指令与 ACL 指令结合用以定义使用 Squid 代理的访问。其他指令在 Squid 中均无效。

181. B. `nmbd` 守护进程负责 NetBIOS 名称服务请求的处理。`smbd` 守护进程负责文件和打印共享，而 `winbindd` 提供用户和组信息。没有名为 `samba` 的守护进程。

182. A. `PermitRootLogin` 指令设置为 `yes` 或 `no`，决定 root 用户是否可以直接登录。显示的其他选项均无效。

183. B. `push` 指令用于在连接时向客户端发送路由。在这种情况下，发送了网络和子网掩码，`255.255.255.0` 对于 `/24` 是适当的。其他选项均无效。

184. A. 如果你使用 Wayland，会设置 `WAYLAND_DISPLAY` 环境变量。你可以通过以下查看





194. C. 自动错误报告工具 `abrt` 在 CentOS 7 上使用 `/var/tmp/abrt`。在 CentOS 6 中使用的是 `/var/spool/abrt`。

195. B. `trigger` 命令用于重放或触发事件。显示的其他选项不适用于 `udevadm`。

196. D. `set-chassis` 命令用于配置运行 `hostnamectl` 命令的机器类型。这对于某些类型的应用程序非常有用。显示的其他命令是无效的。

197. C. 文件 `/etc/rc.local` 可用于此目的。`/etc/rc.local` 内部命令将在计算机进入多用户模式后执行。显示的其他选项不是用于此目的的有效文件。

198. C. `rndc` 命令用于控制 BIND 服务器，包括通过远程连接。显示的其他命令是无效。

199. B. 在此场景中，全局文件系统 (GFS)，特别是 GFS2，可能会被用作集群或共享文件系统。ext2 文件系统不会用于此目的。可能可以使用 CIFS 实现此目的，但 GFS2 是 Red Hat 首选的集群文件系统。FAT 文件系统不会用于此目的。

200. B. `<video>` 节用于配置 Spice 时添加视频设备。显示的其他选项不适用于 Spice。

201. B. `<<` 运算符用于此目的，它将从 `STDIN` 读取，直到遇到指定的字符或字符组合。这有时被称为 Here Document 或 HEREDOC。在它的其他选项中，只有 `>` 是有效的，且它会导致 `STDOUT` 被重定向。

202. A. `--level` 选项启用设置运行级别。给出的其他选项不适用于 `chkconfig`。

203. B. `-o` 选项设置本地文件名。`-O` 选项保留远程文件名。`-f` 选项导致 `curl` 静默失败，`-l` 选项用于 FTP 以产生仅文件名列表。

204. A. `groupadd` 命令用于向系统添加用户组。显示的其他选项是无效。

205. C. `whoami` 命令显示当前有效用户 ID 的用户名。在显示的其他命令中，只有 `w` 命令是有效的，它显示谁登录了系统，但不会显示用户 ID 到用户名的关联。

206. D. `/etc/profile.d` 目录可用于存储登录时执行的文件和脚本。在其他答案中，`/etc/profile` 确实存在，但它是一个文件而不是目录。其他答案都不是无效的目录。

207. A. Unity 桌面与 Ubuntu 关联最为密切。其他发行版使用不同的桌面管理器。

208. B. `/etc/rcS.d` 目录包含一个在 Debian 启动时配置 `udev` 的脚本。其他目录不用于所描述的场景。

209. B. 正确的命令和顺序是 `systemctl stop <service>`。这与 `service` 命令不同，后者的格式为 `service <service> stop`。其他命令不适用于所描述的场景。

210. C. `Monitor` 部分是 X11 配置中放置特定显示器配置的地方。显示的其他选项不适用于此场景。

211. B. 当输出重定向到 `/dev/null` 位置时，它会接受输入且不会消耗额外的磁盘空间。`/dev/random` 设备存在，但不适用于此场景。同样，重定向到网络接口或普通文件也不符合此场景的准则。

212. B. `-d` 选项设置用于 `paste` 的分隔符。显示的其他选项不适用于 `paste` 命令。

213. D. `reload` 目标或命令作为 `service` 命令的一部分使用，会导致守护进程重新加载或重新读取配置文件。

214. B. `Environment` 键用于为 `systemd` 单元文件配置环境参数或变量。

215. B. `<` 运算符将输入从文件重定向到命令，以便该命令从文件中读取。`>` 运算符重定向 `STDOUT`，其他运算符不适用于此场景。

216. B. `NAME` 参数设置设备名称。显示的其他选项不是无效的 `udev` 参数。

217. D. `/etc/X11` 目录通常用于 X Window 系统的配置，包括 Xorg 的主配置文件 `xorg.conf`。其他路径均无效。

218. C. `alsamixer` 命令显示一个基于 ncurses 的界面，看起来像调音器，用于设置各种音频设备的音量。其他所有选项均不适用于此目的。

219. B. `xrdp` 软件包是远程桌面协议 (RDP) 的开源实现。此问题的其他其他选项不是该场景的有效包。

220. D. 端口 3306 是 MySQL 的默认端口。在其他选项中，25 是 SMTP，389 通常用于 LDAP。

221. A. `dmesg` 命令将查看内核消息，例如显卡检测消息。当通过 `-i`（不区分大小写）管道传递给 `grep` 时，你可以轻松搜索检测到的 VGA 卡。

222. C. Ctrl+Z 键组合将挂起进程。其他选项不适用于此目的。Ctrl+C 键组合会杀死进程。

223. C. `SSLCertificateKeyFile` 指令指向 SSL 配置的私钥位置。显示的其他选项不是有效指令。

224. B. `iwconfig` 命令与 `ifconfig` 命令类似，与单个无线接口配合设置并显示参数。在其他命令中，`ifconfig` 命令是有效的，但不用于无线网络。其他命令均无效。

225. D. `tr` 命令可用于描述的操作。`tr` 命令在文本转换方面非常强大。显示的其他命令不存在。

226. B. Nano 编辑器适用于此场景。虽然 Vi 确实是一个文本编辑器，但初学者通常难以对付。`nc` 命令不用于文本编辑，也没有 ShellRedirect 文本编辑器。

227. C. `mask` 命令将单元文件链接到 `/dev/null`，从而确保无法运行。`disable` 命令删除 `/etc/systemd` 和 `/lib/systemd` 之间的符号链接，但服务仍然可以运行。显示的其他选项均无效。

228. A. `more` 命令提供简单的分页功能。与在许多系统中需要安装的 `less` 命令不同，`more` 即使在基础安装中通常可用。`grep` 命令不是分页器，其他命令均无效。

229. A. `&>` 运算符用于重定向 `STDOUT` 和 `STDERR`。`>` 运算符重定向 `STDOUT`，显示的其他选项不适用于此场景。

230. C. `/dev/tty` 设备是 Linux 系统上的特殊文件，是当前进程的终端。其他位置均无效。

231. A. `printf` 命令可用于为字符串添加特殊格式以便打印。`echo` 命令在某种程度上用于此目的，但在特殊格式化方面不如 `printf` 命令强大。其他命令不适用于此目的。

232. C. `unlink` 命令可用于删除文件，在简单使用场景下有时比 `rm` 快。其他选项均无效。

233. A. `scp` 命令通过 SSH 复制或传输文件。`ncftp` 命令不能用于此目的。其他命令均无效。

234. A. 当 TraceEnable 关闭时，将发送“405, Method not allowed”响应。100 状态表示继续，而 302 是重定向，200 是 OK。

235. C. `nohup` 命令忽略 `SIGHUP` 信号，从而实现本题所需的场景。其他命令均无效。

236. D. `lsusb` 命令显示 USB 设备。与 `grep -i`（不区分大小写）结合时，你可以搜索蓝牙设备。显示的其他选项均无效。




## 第 3 章：安全

1. C. `dd` 命令用于创建磁盘镜像等。在这种情况下，输入文件为 `/dev/sda1`，输出文件为 `output.img`。通常还会通过 `bs` 参数添加 `blocksize`（块大小）选项，例如 `bs=1M`。

2. C. `tail` 命令提供作为参数的文件的末尾部分。添加 `-f` 选项将导致当被跟踪的文件添加新行时，输出将随之更新。

3. A. `xz` 命令可以压缩和解压缩多种格式的文件，其中一种是 LZMA。

4. A. `chgrp` 命令用于更改文件的组所有权。顺序为 `chgrp <groupname> <target>`。

5. C. `-S` 选项以 `u=rwx,g=rx,o=rx` 等格式显示输出。列出的其他选项不存在。

6. D. `/srv` 层次结构用于服务器程序的数据。`/etc` 层次结构是配置信息，而 `/var` 也是数据文件，但是变化文件，如邮件池文件。`/tmp` 目录用于临时文件。将数据保留在单独的分区上有于操作系统分区出现问题时最大限度地提高系统可用性。

7. C. `chmod` 命令用于此目的，`u+s` 选项为指定目标的用户设置粘滞位（sticky bit）。

8. C. 022 `umask` 将将新的非可执行文件转换为 644 权限。

9. C. `-R` 选项将以递归方式执行所有权更改。

10. C. `-R` 选项设置递归选项，这意味着 `chgrp` 将遍历给定目录并在指定的层次结构中执行组所有权更改操作。

11. A. `suid` 位允许程序以文件所有者的身份运行，无论是谁执行了该程序。出于安全考虑，通常不建议使用 SUID。其他权限允许文件所有者读取（`r`）和写入（`w`）。组和“其他”权限包含读取（`r`）和执行（`x`），但不写入。

12. D. 你至少需要能够读取被源的文件，因此 `chmod 400` 将正确设置权限。任何赋予额外权限的 `chmod` 都是必要的。当使用八进制符号授予权限时，数字 4 表示读取，2 表示写入，1 表示执行。三种权限：用户（所有者）、组和其他（或世界）。因此，`chmod 400` 授予所有者“读取”权限，而不给组和其他/世界授予任何权限。

13. B. `chage` 命令用于此目的，特别是带有 `-E` 选项。当提供日期时，`chage` 将在该日期过期账户。当提供 `-1` 时，将移除过期设置，从而移除用户锁定。

14. B. `getent` 命令根据 `/etc/nsswitch.conf` 文件显示条目。`getent` 的用例之一是在与 Microsoft Active Directory 或另一个 LDAP 服务集成时，检查是否可以连接到 LDAP 服务器。`usermod` 命令是有效的，但不用于此目的，问题中显示的其他命令是无效的。

15. B. `/etc/cron.deny` 文件包含无法创建 `cron` 计划任务的用户列表。`/etc/cron.allow` 文件用于提供允许创建 `cron` 作业的用户列表。另外两个文件默认不存在。

16. C. `kern` 设施接收来自内核的消息用于日志记录。在其他选项中，`syslog` 用于记录有关 `syslog` 本身的消息。显示的另外两个选项不是有效的 `syslog` 设施。内核消息有时存放在名为 `/var/log/kern.log` 的单独日志中。

17. C. `journalctl` 命令用于处理 `systemd` 日志。在基于 `systemd` 的系统上，`journalctl` 是调试和故障排除的中央命令。

18. A. `systemd` 管理的计算机上用于日志的服务被称为 `systemd-journald`。你使用 `journalctl` 查看日志项，而不是标准的 Linux 工具集。

19. A. `mail` 选项将在 `logrotate` 完成后将日志发送到指定的电子邮件地址。显示的其他选项在 `/etc/logrotate.conf` 中并不存在。

20. B. `$UDPServerRun` 选项用于描述的目的。服务器应该监听的端口将作为该选项的值提供。显示的其他选项不是 `rsyslogd` 的有效配置项。

21. A. `SystemMaxFileSize` 选项控制日志文件的大小，以确保日志不会引起磁盘使用相关问题。`SystemMaxUse` 选项控制日志文件的总大小，`SystemMaxFileSize` 的默认值是 `SystemMaxUse` 设置的八分之一，以便文件轮转。

22. B. SMTP 运行在 TCP 端口 25 上，如果其他服务器正在连接你的 SMTP 服务器，你需要监听此端口并允许流量通过它。端口 23 用于 telnet，端口 110 用于 POP3，端口 143 用于 IMAP，这些对于 SMTP 流量都不是必要的。

23. D. `nocompress` 选项用于防止日志文件在轮转过程中被压缩或压缩包。这在压缩会对性能产生负面影响或需要额外处理的系统上可能是需要的。

24. B. 传统上，`udp/53` 用于 DNS 查询，但由于主备服务器，假设可能会发生区域传输。DNS 区域传输通常发生在 `tcp/53` 上。

25. D. `/etc/services` 文件包含了基于 IANA 知名端口和分配端口的标准端口到协议信息。如果你想为服务提供自定义名称，可以通过编辑此文件来实现。默认没有 `/etc/ports` 或 `/etc/p2p` 文件，且 `/etc/ppp` 通常是点对点协议守护程序相关服务的目录。

26. D. ICMP 是一个三层协议，意味着它不使用端口进行通信。TCP/43 用于 whois，而端口 111 用于 sunrpc。UDP/69 用于 TFTP 协议。

27. B. TCP 是一种面向连接的协议，使用三次握手建立连接并提供有状态的协议。ICMP 不使用端口通信，而 UDP 是无连接的或无状态的。IP 是核心互联网协议，不使用握手。

28. D. `chage` 命令用于处理账户老化信息，如过期日期、密码更改、密码更改之间的天数等。`-l` 命令列出给定账户的信息。`usermod` 命令用于修改账户，另外两个命令是无效的。

29. B. `ssh-keygen` 命令用于创建密钥对，以用于 SSH 而不是密码。在其他选项中，`ssh` 命令确实存在，但 `-k` 选项用于禁用 GSSAPI 凭证转发，而不是用于所述目的。

30. A. 存储在 `home` 目录下 `.ssh` 目录中的 `authorized_keys` 文件包含了授权使用相应私钥登录服务器的公钥。

31. A. `-u` 选项用于此目的是正确的。大写的 `-U` 选项设置列出权限的用户上下文。`-s` 选项设置 shell，`-H` 选项设置主目录。

32. B. `NOPASSWD` 选项导致 `sudo` 在执行指定的 sudo 命令时不提示密码。这对于密码提示会引起问题的脚本场景非常有用。

33. C. `ulimit` 命令显示此类限制，`-a` 选项显示当前登录用户的所有限制。其他命令是无效的。




34. C. 阻止所有服务的访问的语法使用 `ALL` 关键字，后跟策略将要应用的地址或网络。这非常重要，因为你可能会注意到来自某些 IP 段的攻击，而使用 TCP wrappers 进行拦截提供了一种快速且有效的拦截方法。

35. A. 文件默认名为 `id_rsa`，公钥文件名为 `id_rsa.pub`。对于 DSA 密钥，名称为 `id_dsa` 和 `id_dsa.pub`。

36. C. `-c` 选项执行单条命令但不通过交互式会话执行。`-s` 选项指定要使用的 shell。`su` 命令没有 `-u` 或 `-e` 选项。

37. C. `send-key` 选项后跟密钥名称会将密钥发送到由 `keyserver` 选项指定的密钥服务器。这是将本地生成的公钥发送到公共服务器以供他人使用的典型场景。所示的其他潜在选项并不存在。

38. C. 虽然可以使用任何文本编辑器，但强烈建议使用 `visudo` 命令编辑 `/etc/sudoers`。使用 `visudo` 可以启用语法检查，这有助于防止无效配置给依赖 `sudo` 的用户带来问题。

39. B. 文件 `ssh_known_hosts` 通常保存在 `/etc/` 或 `/etc/ssh/` 中，用于上述目的。请注意，在某些系统上，此文件和其他 SSH 相关配置可能位于 `/etc/sshd/` 中。指向 `~` 或 `/root` 内的答案是错误的，因为问题指定的是全服务器范围的列表。在 `~/.ssh` 中找到的 `known_hosts` 文件表示用户的 `home` 目录。

40. C. 该选项名为 `X11Forwarding`，并且必须设置为 `yes`，以便让目标服务器将基于 X 的窗口转发到本地客户端计算机。所示的其他选项均无效。注意，在某些发行版中，配置文件位于 `/etc/sshd/`，而在另一些发行版中，配置文件位于 `/etc/ssh/`。

41. A. `--gen-key` 子命令用于上述描述的目的，并在 PKI 场景中生成一对自签的私钥和公钥。所示的其他选项并不存在。

42. B. `/etc/inetd.conf` 中的行可以使用井号或哈希标记（`#`）注释。修改 `/etc/inetd.conf` 后，应当重启服务。

43. B. 位于 `~/.gnupg` 中的文件 `pubring.gpg` 包含公钥圈。

44. C. `-` 选项是传递给 `su` 进行登录的典型选项。没有 `-u` 或 `-U` 选项，也没有 `-login` 选项。有一个双杠 `--login` 选项，但不是图中显示的。

45. A. 基于密码的密钥派生函数 2 (PBKDF2) 用于 LUKS 密码学的密钥派生。SSL 是安全套接层，通常用于 HTTP 流量的加密。RSA 和 DSA 都是加密算法，但与此无关。

46. A. `cryptsetup` 命令用于设置和帮助配置 `dm-crypt` 卷。此问题所示的其他命令均无效。

47. C. `PARANOID` 通配符指定主机名和 IP 必须匹配。`ALL` 关键字也是 TCP wrappers 中有效的配符，可用于 `/etc/hosts.allow` 和 `/etc/hosts.deny`。

48. A. `-c` 选项表示创建一个 `tar` 文件。`-d` 选项用于两个 `tar` 文件之间的差异比较，`-b` 选项提供块大小，`-f` 选项指定文件名。

49. C. `--remove-files` 选项在向文件系统添加文件后删除它们。`-r` 选项将文件追加到文件末尾。`-f` 选项指定文件名。

50. C. `/etc/hosts` 文件用于上述目的。注意，在某些系统上，该文件和 SSH 相关配置是无效的。

51. A. `--delete` 选项在 `rsync` 中删除不存在的文件。所示的其他选项均无效。

52. B. `--exclude` 选项在 `rsync` 中排除匹配模式的文件。

53. C. `etc/issue`（登录信息，缩写 motd）在用户登录时显示。`-e` 选项表示 SSH 传输。

54. A. `-z` 选项用于解压缩 `tar` 文件。`-x` 选项解提取，`-f` 选项指定文件名。

55. B. `-c` 选项创建 `tar` 文件。所示的其他选项均无效。

56. D. `--modify-window` 选项修改窗口。

57. B. `-c` 选项输出到 STDOUT。`-d` 选项解压缩，`-f` 选项指定文件名。

58. B. `-q` 选项抑制所有警告。`-v` 选项为详细模式，`-r` 选项表示递归。

59. C. `-rsh=ssh` 使用 SSH 作为传输手段，确保通过隧道进行。

60. C. `home` 目录应设置为 `/etc/passwd`。

61. D. `rndc` 可用的算法为 `hmac-md5`，密钥可以使用 `dnssec-keygen` 生成。所示的其他选项是加密或哈希算法，但未用于此问题。




68. C. `pam_unix.so` 模块用于标准登录。`pam_unix.so` 的帮助页指出它用于“传统的密码身份验证”。列出的其他模块不是标准的 PAM 模块，尽管 Squid 有一个类似的 `pam_auth` 或 `squid_pam_auth` 模块。

69. B. `pam_cracklib.so` 模块强制密码强度选项。列出的其他文件不是有效的 PAM 模块。

70. B. PEM 格式用于 Postfix TLS 配置中的公钥和钥。列出的其他方法是有效的加密算法或系统，但不适用于描述的场景。与 Sendmail 类似，系统管理员应采取措施保护邮件服务器，防止服务器被用于发送垃圾邮件。对于许多场景，仅仅从服务器中继邮件不需要像 Postfix 或 Sendmail 这样完整的邮件服务器。

71. B. `PREROUTING` 链是 `nat` 表的一部分，包含在数据包到达时应用的规则。该链的常见用途是应用重定向规则。在其他答案中，`REDIRECT` 看起来可能是有效的，但它实际上是一个目标（target）而不是链（chain）。显示的其他选项均无效。

72. C. `iptables-save` 命令将当前的 `iptables` 规则发送到 `STDOUT`。输出可以保存到文件中，并在下次重启服务器时应用。显示的其他命令无效。

73. D. `iptables -n` 选项导致 `iptables` 不解析主机名或端口名。`-L` 选项列出当前规则。没有 `-a` 选项。

74. D. `/etc/fail2ban` 目录包含与 `fail2ban` 相关的配置文件。显示的其他目录无效。其他类似的软件（如 DenyHosts）也可以使用，但在许多环境中已很大程度上被 Fail2ban 取代了。

75. B. `PermitEmptyPasswords` 指令指定是否可以使用空密码进行身份验证。启用空密码是一种特殊的用例，通常不建议这样做。显示的其他选项均无效。

76. C. `-P` 选项设置 `iptables` 中给定链的策略。在这种情况下，链是 `INPUT`，所需的策略是 `DROP`。

77. B. OpenVPN 默认监听 UDP 端口 1194。其他组合不是有效的 OpenVPN 配置。

78. B. `DROP` 目标静默丢弃匹配规则的数据包。对于 `REJECT`，会回发 ICMP 不可到达消息。通常，优选 `DROP`，以减少拒绝服务（DoS）或其他信息收集问题的发生。

79. B. `-m` 限制匹配配合包括 `LOG` 目标在内的所示配置选项，创建了描述的场景。每分钟将产生三个日志记录。这有助于防止由于日志文件满或在进行其他攻击时阻塞服务器 I/O 导致的拒绝服务。

80. A. 将使用 `INPUT` 链。当与 `-A` 选项一起使用时，它将向链中追加规则。`-p` 选项指定协议（在此情况下为 ICMP）；`-j` 选项指定目标（在此情况下为 `ACCEPT`）。`-P` 选项指定策略，在此场景中不会使用。

81. B. 将使用 `INPUT` 链，并且需要用 `-A` 追加规则。当在指定协议时，`ALL` 选项意味着所有协议都包含在规则中。`-s` 选项指定源，在此情况下是单个 IP。最后，`DROP` 目标静默丢弃数据包。没有 `BLOCK` 或 `DISCARD` 目标，`ACCEPT` 目标不会拦截而是接受所有流量。

82. A. 将用 `-A` 在 `INPUT` 链中追加规则。在这种情况下，应用 `-p` 指定协议为 TCP，目标端口为 2222。指定的源地址 `0/0` 将规则应用于所有主机。将使用 `ACCEPT` 目标。

83. B. 向 `/proc/sys/net/ipv4/ip_forward` 文件写入 `1` 可启用 IP 数据包的转发。这对于利用 NAT 和其他用途是必须的。IPv6 有一个类似的文件位于 `/proc/sys/net/ipv6/ip_forward`。不存在 `/proc/sys/net/ipv4/nat` 文件。

84. A. `logpath` 指令决定 `fail2ban` 监控失败情况的日志文件。该文件被视为特定 jail（监狱）较大配置的一部分。其他指令对 `fail2ban` 无效。

85. D. `ssh-copy-id` 命令将身份发送到远程服务器，然后可用于基于密钥的验证。显示的其他命令无效。

86. B. `mailto` 配置选项设置了 `sudo` 相关邮件的目标地址。列出的其他选项对 `sudo` 无效。

87. C. 端口 123 默认用于 NTP 通信。端口 161 是 SNMP，139 是 NetBIOS，194 是 IRC。

88. D. 用 `-a` 调用的存档选项等于 `rsync` 的其他几个选项，如递归、保留组和所有权等。该选项在创建备份时经常使用。

89. C. 与 SSL 相关的文件通常存储在 `/etc/ssl`（或其子目录）或 `/etc/pki` 层次中。不存在 `/etc/private` 或 `/usr/share/ssl` 目录。

90. A. `AllowUsers` 指令用于指定允许登录服务器的用户。显示的其他选项无效。

91. A. `--log-prefix` 选项指定当 `iptables` 创建日志条目时前置的字符串。显示的其他选项对 `iptables` 无效。

92. B. `SELINUXTYPE` 选项可以设置为 targeted 或 strict（严格的）。设置为 targeted 时，只有特定的网络守护进程受到保护。

93. A. 当返回 `Permissive` 时，SELinux 未强制执行规则，而是使用 DAC 规则。其他返回输出为 `Enforcing` 和 `Disabled`。

94. B. `sshd.conf` 文件用于服务器配置。在某些发行版中，该文件名为 `sshd_config`。`ssh.conf` 文件用于系统的客户端配置。

95. D. 当必需模块返回失败时，其他模块将继续处理，但身份验证最终会失败。这样做是为了产生日志记录并让其他模块有机会处理该身份验证尝试。如果应该立即失败而不处理其他模块，则应使用 `requisite` 选项而不是 `required`。

96. B. Linux 系统上的 root 账户 UID 为 `0`。通常，服务账户的 UID 低于 1000，许多低于 100。普通用户账户通常从 UID 1000 开始。

97. B. 虽然可以使用硬件令牌，但默认选项是基于软件的。还要注意，生成一次性密码的 OTP 解决方案在功能上类似于提供多因素身份验证。

98. D. `/etc/inittab` 文件包含一行类似于 `ca:12345:ctrlaltdel:/sbin/shutdown -t1 -a -r now` 的内容。使用井号 (`#`) 注释此行将在重启系统后禁用此组合键。

99. B. `/usr/lib/firewalld/zones/` 目录包含用于 `firewalld` 的预定义区域。文件在修改后会被复制到 `/etc/firewalld/zones/`。

100. D. `password` 配置选项设置在 `/boot/grub/grub.conf` 中。问题显示的其他选项对该场景无效。

101. B. `setenforce` 命令用于此目的，可以赋予数字 `1` 或单词 `Enforcing` 作为参数来启用 `Enforcing` 模式。可以通过 `sestatus` 命令验证。

102. C. `ssh-add` 命令用于此目的。显示的其他命令不存在。

103. A. `getfacl` 命令用于显示文件的访问控制列表信息。`setfacl` 命令用于设置此信息。显示的其他命令均不是 Linux 命令。




### 104. A. 通过用空的 `echo` 命令覆盖 `/etc/securetty`，root 用户将无法直接从控制台登录。在其他潜在选项中，选项 C 删除了 `/etc/securetty`，其效果是允许 root 从任何地方登录。

### 105. C. `~/.ssh/config` 文件是此类此类配置信息的合适位置。在其他答案中，只有 `~/.ssh/known_hosts` 存在，并且它包含你连接过的主机的公钥信息。

### 106. A. `-R` 选项用于指示递归行为。在其他选项中，只有 `-v` 是有效的，且提供详细输出。

### 107. C. 可以使用 `gdisk` 命令查看给定分区的 GUID。所示其他命令都是无效的。

### 108. B. `-P` 选项使得值在重启后依然有效。其他选项在 `setsebool` 中是无效的。

### 109. B. `/etc/apparmor.d/` 是配置文件（profiles）所在的位置。

### 110. C. DTLS，即数据报传输层安全，用于数据报流量。列出的其他协议都是无效的。

### 111. B. `lastb` 命令查看 `/var/log/btmp` 以记录错误或失败的登录。所示其他命令都是无效的。

### 112. D. `klist` 命令在使用 Kerberos 认证时显示当前票据。在其他答案中，`kinit` 命令用于获取初始票据授予票据。其余答案均为无效命令。

### 113. A. 可以使用 `ps` 命令帮助排除此类故障。在其他命令中，`uptime` 命令是有效的，但它只会报告基础的 CPU 使用信息。

### 114. B. `-l` 选项提供文件和目录的长格式或详细列表，包括所有者和权限。`-m`、`-b` 和 `-f` 选项与描述场景无关。

### 115. A. `-a` 选项返回所有布尔值。其他选项在 `getsebool` 中是无效的。

### 116. C. `aa-unconfined` 命令显示提供网络端口但没有 AppArmor 配置文件的进程。其他命令都是无效的。

### 117. C. `wheel` 组可用于限制只有该组成员账户才能使用 `su` 命令。其他组默认不存在。

### 118. C. `chcon` 命令用于更改安全上下文。

### 119. A. SSL VPN 有时可以绕过会阻止 VPN 流量的防火墙。基于 SSL 的 VPN 通常不是 Linux 的默认选项。

### 120. A. 当选择 RSA 作为密钥类型时，`SHA256withRSA` 是默认选项。其他选项包括 `SHA1withRSA`、`SHA512withRSA`、`MD5withRSA` 和 `MD2withRSA`，其中 `MD5` 和 `MD2` 提供消息摘要格式。所示其他答案均不是有效的 RSA 哈希算法。值得注意的是，当选择 `ECC` 作为密钥类型时，`SHA1withEC` 是一个可用选项。

### 121. C. 增量备份仅捕获自备份以来的更改，可用于节省空间。其他答案都是常用的备份类型。全备创建所有文件的备份。镜像通常指磁盘分区的底层位对位复制。最后，快照克隆通过克隆或复制快照来获取磁盘镜像并将其放置在安全位置。值得注意的是，增量备份有时也被称为差异备份。

### 122. C. 在可用答案中，账户是共享的这一事实意味着它违反了共享 ID 的最佳实践。这通常不会影响完整性或可用性，而密码策略指的是密码长度和过期时间等内容。

### 123. B. 在 BIOS 中设置密码可用于防止系统启动或将启动过程移交给引导加载程序。由于存在物理访问权限，`GRUB` 密码或 root 对这种场景均不起帮助。

### 124. B. 可以使用 `fprint` 包来提供生物识别认证（如指纹认证）。在其他答案中，存在 `finger` 命令，但它通常应该被禁用，因为它可以提供有关系统账户的信息。

### 125. A. `restorecon` 的 `-n` 选项显示当前上下文而不进行更改。在其他有效的选项中，`-r` 改变递归更改，`-p` 显示进度。

### 126. C. `sudoedit` 命令允许用户选择自定义的编辑器来编辑文件。在其他答案中，`vim` 和 `nano` 都是有效的编辑器，但通过 `sudo` 允许可能会带来额外的安全影响。`visudo` 程序用于编辑 `/etc/sudoers` 文件本身，这在该场景中并未指定。

### 127. D. `ps` 命令显示进程。当给定 `-Z` 选项时，会显示 SELinux 上下文。

### 128. B. `pam_tally2` 模块跟踪失败的登录，并可以在尝试一定次数后锁定账户。请注意 `pam_faillock` 提供类似的功能。

### 129. B. 虽然 Tunnel 模式可用于客户端流量，但它最常用于站点到点的流量，因此 Transport 是此题的正确答案。Tunnel 和 Transport 模式都使用 IPSec 进行封装。

### 130. C. Linux 中的伪终端以 `/dev/pty` 开头。标准终端是 `/dev/tty`，串口控制台以 `/dev/ttyS` 开头。

### 131. A. 命令 `aa-complain` 用于将配置文件放入投诉模式。配置文件位于 `/etc/apparmor.d/`，因此所示命令将所有配置文件放入投诉模式。

### 132. D. `/var/log/secure` 日志文件显示有关认证和授权的信息。在其他选项中，`/var/log/messages` 和 `/var/log/kern.log` 存在，但通常不包含认证或授权信息。

### 133. B. `PermitRootLogin` 选项用于确定 root 是否可以使用 SSH 直接登录。通常禁用 SSH  root 登录是最佳实践。

### 134. D. RADIUS 常指的 AAA 是认证（Authentication）、授权（Authorization）和计费（Accounting），其中计费是对拨号尝试的记录。

### 135. C. `--runtime-to-permanent` 选项将当前的运行时设置为永久并在下次启动时可用。

### 136. D. SFTP 是首选，因为它比传统的 FTP 提供了额外的安全性。总而言，通常应该禁用 FTP，因为凭据和其他流量没有加密。在其他选项中，由 Sendmail 和 Postfix 提供的电子邮件（SMTP）不提供加密，如果未使用则应禁用。SSL 本身不传输文件。因为场景未包含传输是否为远距离传输的细节，很难判断 USB 是否合适。然而，服务器上经常不建议使用 USB 设备，因为它可以可能是另一个攻击向量。




142. C. `cpio` 实用可以处理多种归档格式，其中一种就是 HPUX 创建的归档。`gzip` 或 `bzip2` 命令可能无法打开或从文件中提取内容；它们通常用于压缩而非归档。

143. B. `scp` 实用使用 SSH 作为传输，因此需要 TCP 端口 22。TCP 端口 20 和 21 用于旧版 FTP，而 `UDP/53` 用于 DNS 查询。

144. A. `-a` 选项显示以点（.）开头的文件和目录。显示的其他选项与此场景无关。

145. A. 使用 `dd` 对分区进行位级镜像是一个好主意，以便保留任何入侵证据。使用 `tar` 创建备份是一个较不优的选项。使用 `fdisk` 检查分区不会显示任何相关信息，而且在未了解攻击范围之前，通常不应该重新格式化分区。

146. B. `-i` 选项指定了用于连接的身份文件。显示的其他选项对 SSH 是有效的，但不满足此场景的要求。

147. A. `sha1sum` 实用可用于创建和验证文件的校验和，以确保文件内容没有更改。由于对碰撞以及 MD5 其他安全问题的担忧，SHA1 优于 MD5。

148. C. `-r` 选项告诉 `zip` 命令在创建归档时遍历目录。其他选项对于此目的无效。

149. A. `ps` 命令在带有如 `auwx` 等参数时，将显示所有进程以及这些进程的所有者。结合 `grep` 命令结合可以显示出包含 `apache` 单词的进程。在其他系统上，这可能被称为 `httpd` 而不是 `apache`，但题目指定了 Debian 系统。

150. A. `chown` 命令更改文件或目录的所有者，题目中指定了 `www-data` 用户，因此该选项是此场景的唯一正确选项。

151. C. `sudo` 的非交互模式通过 `-n` 选项触发。其他选项对此场景无效。

152. D. Telnet 运行在 TCP 端口 23 上。在几乎所有环境中都应该禁用 Telnet，因为它对密码或 telnet 会话内的其他流量不提供安全性。如果旧版应用需要 telnet，那么防火墙将是下一个最佳选择，并且仅限制来自应用程序本身的连接。

153. A. `aa-disable` 命令用于关闭与 AppArmor 使用的配置文件。显示的其他命令无效。

154. C. `ls` 的 `-Z` 选项用于查看 SELinux 安全上下文。`file` 命令是一个有效命令，但它没有 `-Z` 选项。

155. B. GnuPG 可以通过其 `gpg` 命令提供数字签名。显示的其他答案无效。

156. D. 目录 `/etc/apparmor.d/tunables` 包含了经常更改的参数和配置。

157. C. 目录 `/etc/ufw` 通常包含 UFW 的配置信息。在许多系统上，`/etc/default/ufw` 也会包含经常更改的默认配置项。

158. B. `ipset` 项目和软件通过帮助创建 IP 地址集（通用规则适用于这些集合），从而有助于更有效的规则管理。

159. A. 公钥应该被复制到远程主机。当它被复制并将内容放入 `~/.ssh/authorized_keys` 时，任何提供相应私钥的人都将被允许身份验证。

160. C. 使用八进制表示法时，数字 4 表示读，2 表示写，1 表示执行。用户、组和其他权限按此顺序出现在八进制中。因此，7 授予用户读写-执行权限，5 授予组和其他的读-执行权限。

161. C. 文件 `/etc/rsyslog.conf` 包含系统日志的配置信息。在某些系统上，该文件可能被称为 `rsyslogd.conf`。你会发现如哪些日志项进入 `/var/log/messages` 以及系统上的其他日志。

162. B. `-v` 选项显示 `/etc/sestatus.conf` 中列出的文件的上下文。其他选项对于 `sestatus`无效。

163. C. `-M` 选项设置密码有效的最大天数，而 `-m` 设置密码更改之间的最小天数。其他选项与此场景无关。

164. B. `KerberosAuthentication` 是 SSH 服务器配置中的选项，用于控制用户是否可以使用 Kerberos 进行身份验证。

165. A. `-t` 选项结合表名，将输出限制为指定的表而不是所有表。其他选项对于 `iptables-save` 无效。

166. C. 常用端口有时被称为特权端口，被认为是 1024 以下的端口。这些端口通常由系统守护进程和系统级服务提供。

167. C. 各种日志文件轮转策略的单独配置文件位于 `/etc/logrotate.d` 中。该目录被主配置文件 `/etc/logrotate.conf` 包含。

168. C. 正 `tail -f` 命令在添加新内容时持续更新显示一样，`-f` 选项也会为 `journalctl` 显示新条目。`-t` 选项显示指定的 `syslog` 标识符的消息。没有 `-tail` 或 `-l` 选项。

169. D. `pam_limits.so` 模块负责执行题目中提到的限制以及其他若干项限制，如文件最大大小、内存使用等。列出的其他模块均无效。

170. D. 指定 `slapd` 的日志级别和调试有多种方法，包括通过关键字、整数，或者如题目所示，通过十六进制。显示的所有值对于 `loglevel` 都是有效的。无调试为 0，跟踪为 1，统计日志根据类型为 256 或 512，发送和接收的数据包为整数 16 或十六进制 0x10。

171. C. LDAPS 或通过 SSL 的 LDAP 端口是 636。端口 389 是标准的、非 SSL 的 LDAP。端口 443 用于 HTTPS，3128 用于 Squid 代理。

172. B. `pam_listfiles.so` 模块用于创建场景，通过这些场景你可以通过 PAM 系统创建控制身份验证和授权的文件。其他文件对于描述的场景无效。

173. B. `-t` 选项为 `ssh-keygen` 设置密钥类型。其他选项不设置密钥类型，但可能用于其他用途。

# 第 4 章：Linux 故障排除与诊断

1.  C. SATA 磁盘的地址为 `/dev/sdX`，与 SCSI 磁盘一样。`/dev/hdX` 是传统的 ATA 磁盘。其他选项不存在。

2.  B. `lsusb` 命令用于获取系统上 USB 设备的基本列表。其他命令无效。在答案 D 的情况下，`ls` 命令是有效的，但没有 `--usb` 选项。

3.  C. 在 Linux 内核命令行上给出 `single` 关键字将系统引导到单用户模式。其他选项无效。

4.  B. 检查磁盘是否在 BIOS 中被检测到是故障排除良好的第一步。答案 A 拔掉磁盘无法帮助检测。重启 Web 服务器不会帮助检测磁盘，且 `disk-detect` 命令不存在。

5.  A. 在 `grub >` 提示符下的 `ls` 命令将以如 `(hd0,1)` 的格式显示可用分区。

6.  A. 使用线缆选择（cable select）时，ATA 驱动器将按照它们在主板线缆上的插入顺序被检测。可能需要在物理上交换线缆上的驱动器位置。





### 7. D. 在给出的选项中，运行 `dmesg` 是查找内核分配驱动器位置的常用方法。重启系统不是一个好的选项，尽管它可以生效。并没有 `/var/log/usb.log` 这种文件；而且驱动器的位置可能会随端口变化，取决于系统如何检测该驱动器。

### 8. A. SCSI 每个总线支持 7 到 15 个设备，取决于 SCSI 的类型。

### 9. D. `ldconfig` 命令更新当前的共享库缓存和列表。`ldconfig` 读取 `/etc/ld.so.conf` 并整合其中发现的任何更改。此问题列出的其他选项并不存在。

### 10. B. `apt-get` 的 `upgrade` 选项将系统已安装的软件包升级到最新版本。不存在 `apt-update` 命令，`dpkg` 也没有 `-U` 选项。`apt-cache` 命令用于软件包缓存。

### 11. C. `yum install` 命令将安装指定的软件包。`update` 选项将更新软件包。列出的其他选项并不存在。

### 12. B. `export` 命令用于在 bash 中设置环境变量。其他命令不适用于此种目的。

### 13. C. 与 Yum 仓库相关的配置文件位于 `/etc/yum.repos.d`。在其他选项中，`/etc/yum.conf` 是一个文件而不是目录，其他目录不存在。

### 14. D. `ldd` 命令将列出命令参数依赖的库，对于解决 GCC 兼容性问题很有帮助。

### 15. B. 当系统内存不足时，使用交换空间（Swap space）。

### 16. B. `/etc/lib` 目录通常与库文件关联，除非手动创建，否则 Linux 系统上通常不存在。其他选项包含系统库或可用于该目的。

### 17. C. `apt-get update` 命令通过从软件包源获取最新的软件包列表来更新软件包缓存。`apt-cache` 并没有 `cache-update` 选项或 `update` 选项。`upgrade` 选项用于更新系统软件包而非缓存。

### 18. C. 位于 `/etc/apt` 的 `sources.list` 文件包含 Debian 软件包仓库列表。其他文件位置默认不存在。

### 19. B. `pvcreate` 命令初始化物理分区，以便将来作为 LVM 逻辑卷使用。

### 20. C. `lvcreate` 命令用于使用 LVM 创建逻辑卷。`pvcreate` 命令在创建逻辑卷之前初始化物理卷。此问题中另外两个选项中的命令并不存在。

### 21. A. 首先初始化物理卷，然后创建卷组，最后创建逻辑卷。

### 22. D. `search` 选项对软件包名称和描述等各种字段进行搜索。

### 23. B. `rpm -q kernel` 命令将显示内核版本。你也可以使用 `uname -r` 实现相同的目的。

### 24. A. `exclude` 选项可用于排除某些软件包。该参数接受通配符，因此排除所有 `kernel*` 更新将实现所需的行为。

### 25. B. 正常的 Linux 分区应创建类型为 0x83。类型 82 用于交换分区（swap），而 84 用于 OS/2 分区。没有 L 类型。

### 26. B. `dpkg` 的 `-s` 选项搜索指定的软件包并提供其在系统上当前状态的信息。`apt-cache` 命令不用于此目的，`dpkg` 的 `-i` 选项用于安装软件包。`apt-info` 命令不存在。

### 27. C. `lvmdiskscan` 命令查找已初始化用于 LVM 的物理卷。

### 28. A. `dpkg` 的 `-i` 选项将安装之前下载的软件包。其他命令不存在，`dpkg` 也没有 `-U` 选项。

### 29. B. `env` 命令将打印 Bash 的当前环境变量。`printenv` 命令也会执行相同的操作。此问题中列出的其他命令不存在。

### 30. B. 虽然 `ps auwx` 命令结合 `grep` 可以提供运行中的 Apache 实例的信息，但它提供的信息比解决此问题所需或有用的多得多。`pgrep` 命令仅提供进程，因此符合问题中提出的标准。

### 31. D. `free` 命令显示 RAM 和交换 的整体内存使用情况，可用于判断何时可能需要额外内存。

### 32. A. `uptime` 命令显示基本信息，如所述内容，连同登录系统的用户数和当前时间。`bash` 命令是一个 shell 环境，`ls` 命令不会显示所需信息。

### 33. D. `screen` 命令启动一个新的按需要断开和重新连接的终端。在 `screen` 会话中运行的进程不知道自己正在 `screen` 会话中运行，因此满足此题所需的标准。`fg` 和 `bg` 命令不符合标准，`kill` 命令将停止进程。

### 34. B. `nice` 命令在不带参数运行时，将输出当前登录用户的优先级（通常为 0）。`renice` 命令可更改运行进程的优先级。此问题选项中显示的另外两个命令不存在。

### 35. C. `jobs` 内置命令显示后台运行的任务列表。它的输出包含任务编号和任务状态。

### 36. C. `killall` 命令用于通过名称终止进程。

### 37. A. `df` 的 `-i` 选项产生所有文件系统的索引节点（inodes）信息。`ls -i` 选项会产生 inode 列表，但仅针对当前目录。`-i` 选项对 `du` 无效，且 `dm` 作为命令不存在。

### 38. C. `-y` 选项将尝试自动修复，本质上回答 `y` 或 `yes` 而不是提示。在其他选项中，只有 `-V` 是有效的且会产生详细输出。

### 39. B. `tune2fs` 命令可用于此目的，但应谨慎使用，因为它可能导致数据损坏。

### 40. B. `mkswap` 命令格式化交换分区。`fdisk` 用于创建分区而非格式化。另外两个选项不存在。

### 41. A. `du` 命令以递归方式报告磁盘使用情况，与此处显示的命令不同。

### 42. C. `usrquota` 选项将在指定的挂载点启用用户级配额。这通常在 `/etc/fstab` 中设置。

### 43. D. `-c` 选项首次创建文件。`-f` 选项用于强制检查，`-u` 用于用户配额，`-m` 用于尝试重新挂载为只读。

### 44. D. `-r` 测试确定给定文件是否存在并可被当前用户读取。`-e` 测试仅检查文件`是否`存在，而 `-s` 确定文件是否`存在且大小大于零。没有 `-a` 文件测试。

### 45. D. `allow-guest` 选项改变 LightDM 访客登录的行为。禁止访客登录通常会使计算机稍微安全一些，尽管如果有人拥有设备的物理访问权限，他们可能通过其他方式访问。

### 46. C. `xhost` 命令用于控制对 X  服务器的访问。使用 `+` 号添加主机，通过在主机名前加 `-` 号移除。

### 47. D. 将用户的 shell 设置为 `/bin/false` 将防止他们交互式登录系统（例如通过 SSH）。此问题所示其他选项都是有效的 shell，并将允许交互式登录。

### 48. C. `journalctl` 命令用于此目的；`--disk-usage` 选项显示日志文件占用的磁盘空间，这些文件通常存储在 `/var/log/journal`。




49. A. 使用 `ifconfig` 命令实现此目的，并需要添加 `-a` 选项，因为适配器目前处于关闭状态。`ifup` 命令可用于启动接口，但默认不显示信息。`netstat` 命令可以显示网络信息，但不是使用 `-n` 选项。

50. D. 私有 IP 地址位于 `10.0.0.0/8`、`172.16.0.0/12` 和 `192.168.0.0/16` 范围内，因此 143 范围内的地址是公网 IP。

51. C. 使用 `route` 命令实现此目的，通过 `add` 选项添加路由。使用 `default gw` 关键字后跟网关 IP 和适配器来添加默认网关。

52. A. `host` 命令通过 `-t` 选项允许更改查询类型。使用 `ns` 作为类型将查询给定域名的名称服务器。没有 `all` 类型，其他选项也是无效的。

53. B. `-I` 选项允许选择接口。小写的 `-i` 选项设置间隔，而 `-a` 表示可听性 ping。最后，`-t` 选项仅启用基于 TTL 的 `ping`。

54. A. 使用 `host` 或 `dig` 命令并将类型设置为 `mx` 可以此目的。`mx` 类型将查询给定域的邮件交换器。没有 `smtp` 类型。

55. A. `-T` 选项导致 `traceroute` 使用 TCP 数据包。该选项需要 root 权限，对于防火墙可能拦截 `traceroute` 流量的情况很有帮助。`-i` 选项选择接口，而 `-s` 选项选择源地址。小写的 `-t` 选项设置服务类型 (ToS) 标志位。

56. A. 带有 `monitor` 选项/子命令的 `ip` 命令将在消息到达时显示 netlink 消息。`ip` 命令没有 `netlink` 子命令，且 `route` 命令无法用于此目的。

57. A. `@` 符号用于指示直接向服务器发送查询。这对于通过将查询直接发送到域名的权威名称服务器来排除解析故障非常有用。在其他选项中，`-t` 设置类型，其余选项均无效。

58. A. `getent` 命令用于处理 NSS 数据库，`getent hosts` 将显示使用 `/etc/nsswitch.conf` 中配置的数据库可用主机。

59. C. 配置选项名为 `nameserver`，该选项的值为所需名称服务器的 IP 地址。有多个影响解析执行的选项，例如尝试次数和超时。更多信息请参见 `resolv.conf(5)`。

60. A. 可以使用 `route` 命令实现此；语法包括由 `-net` 选项表示的网络范围，随后是 `netmask` 单词和掩码位，然后是 `gw` 单词和网关 IP。显示的其他选项由于多种原因无效，包括缺少关键字、选项以及顺序错误。

61. A. 使用 `netstat` 命令实现此目的，`-a` 选项显示所有套接字（监听和非监听）。注意，经常添加 `-n` 选项非常有帮助，或者如 `netstat –an` 那样组合使用，以防止名称查找。这样做可以显著提高命令的性能。

62. A. 正确格式是 IP 地址，后跟规范主机名，然后是该主机的任何别名。你可以使用 `/etc/hosts` 中的项目来覆盖 DNS 查询，这对于防止这些名称解析或提供不同的解析有用。

63. C. 配置接口的 `ifconfig` 命令以设备开始，后跟 IP 地址，然后是 `netmask` 关键字和要添加的掩码。由于这是 /24，因此掩码是 255.255.255.0。

64. B. 使用 `ip route` 命令实现此目的，其语法使用 `change` 命令和 `via` 关键字。可以使用 `route` 命令完成相同操作，但需要先删除现有网关然后重新添加新的默认网关。

65. C. Secure Shell（或 SSH）默认在 TCP 端口 22 上运行。TCP/23 用于 telnet，TCP/25 用于 SMTP，TCP/2200 未与任何已知服务关联。

66. B. 使用 `nc` 命令启动 `netcat`，`-l` 选项使其处于监听状态。`-p` 选项用于指定 `netcat` 监听的端口。`-s` 选项指定本地源地址，在此场景中未使用。

67. A. `soa` 类型用于查询域的起始权威（Start of Authority）记录。注意，在许多情况下，`dig` 会尝试在给定命令中查找域，看起来可能没有发生错误。例如，运行选项 D (`dig -t auth example.com`) 时，你将收到关于 `example.com` 的信息，输出中有一行显示 `dig` 忽略了无效的类型 `auth`。

68. A. `search` 选项用于此目的，可以提供多个域名，每个域名用空格或制表符分隔。`domain` 选项在 `/etc/resolv.conf` 中有效，但不允许多个域名。

69. A. 可以使用 `route` 命令实现此；在描述的场景中，路由使用了 `reject` 目标。显示的其他选项无效的，因为它们对 `route` 命令使用了无效的选项。

70. B. `tracepath` 命令提供可能的跳数最大传输单元 (MTU)。`traceroute` 和 `tracepath` 均可从内部或外部使用，且都提供 IPv6 能力。`traceroute` 命令的某些选项可能需要 root 权限，但问题中提供的信息不足以使其成为正确选项。

71. D. `-c` 选项提供发送 ping 的数量计数。`-n` 选项仅指定数字输出，而 `-p` 指定用于数据包内容的填充模式。最后，`-t` 选项设置 TTL。

72. B. NXDOMAIN 是不存在的域或主机的状态：基本上就是发送查询的主机不存在。在没有错误时，正常状态为“NOERROR”。

73. A. 在更改路由后应执行 `ip route flush cache` 命令。此问题中显示的其他命令均无效。

74. A. SPF 记录存储在 DNS 的 `txt` 记录类型中，因此 `-t txt` 是此目的的正确选项。在其他答案中，只有 `-t mx` 有效并返回给定域的邮件交换器。

75. C. 列出的选项中唯一可能的是 ICMP 流量被拦截。因为可以使用 HTTP 到达，所以 TCP 流量显然通过了，且 DNS 也必须正常。

76. C. `G` 表示路由表中的网关。

77. A. `axfr` 类型是区域传输，`@` 符号表示发送查询的服务器。没有 `xfer` 类型。选项 B 只是发送到指定服务器的域普通查询。

78. A. 如果 `/etc/nologin` 存在，用户将被阻止登录系统。假设 SSH 配置中启用了 root 登录，root 用户仍可以登录。

79. B. 使用 `find` 命令实现此目的，权限可以描述为 `4000` 以表示存在 `setuid` 位。`-type` 选项可用于更改返回的对象类型，但与描述的场景无关。

80. A. 使用 `nmap` 命令扫描开放端口。它将扫描指定地址或多个地址的开放 TCP 端口。显示的其他命令不扫描外部（主机外）IP 地址的开放端口。

81. B. 格式为用户名（或其他指定符），后跟 hard 或 soft（取决于限制类型），然后是关键字，最后是该给定关键字的值。




82. B. `lsof` 命令可用于此目的；通过 `-i` 选项，它将显示网络端口及其进程。`netstat` 命令通过 `-a` 选项可以显示网络端口，但不会显示进程。`ps` 命令用于进程，而不是网络端口。最后，没有 `netlist` 命令。

83. A. 设置 `-P0` 将导致在扫描之前不发送 ping 请求，这对于所描述场景非常有用。有一个 `-s` 选项，但它不是用于此目的。其他选项均无效。

84. C. `maxlogins` 参数用于控制给定账户的并发登录数。

85. A. `-s` 选项设置扫描类型，当后面跟大写字母 `S` 时，会将选项设置为 `SYN`。`T` 选项是 `Connect()` 扫描。`nmap` 没有 `Y` 选项或 `-type` 选项。

86. D. 此目的将使用 `find` 命令，并且需要 `-p`erm 选项，具体为使用 `2000` 权限以表示 `setgid`。注意使用 `/` 表示将搜索整个服务器。所示的 `grep` 命令无法用于此目的，因为它仅在当前目录下的文件中查找是否存在 `setgid` 字符串。

87. D. `iostat` 的 `-p` 选项显示设备和分区的信息。`-c` 选项显示 CPU 利用率，`-d` 显示设备利用率。没有 `-a` 选项。

88. D. `vmstat` 命令用于显示有关性能的扩展信息，包括块入和块。`iptraf` 命令用于提供网络级监控，列出的另外两个命令无效。

89. B. `w` 命令显示各种有用信息，包括平均负载、已登录用户和其他运行时间信息。`uptime` 命令不显示当前登录了谁。没有 `swap` 或 `sysinfo` 命令。

90. B. 在 `top` 中按下 Shift+F 允许你选择显示哪些列以及这些列的排序顺序。在所描述的场景中，你可以查看使用内存最高的进程。

91. C. Cacti 是一种绘图工具，它使用脚本以及 SNMP 来收集性能数据。图表可以帮助网络和系统的可视化。`pstree` 命令用于显示进程的树状结构。

92. B. `-e` 选项导致 `swapon` 跳过那些不存在的分区。其他选项对此场景无效。

93. A. `-f` 选项强制 `fsck` 在原本干净的文件系统上运行。这对于当你怀疑文件系统存在错误并需要在排故障过程中进行验证时很有帮助。这也有助于为转换准备文件系统，例如使用 `btrfs-convert` 等工具时的情况。

94. A. `swapoff` 命令禁用交换空间，从而使其无法作为系统的虚拟内存。作为选项所示的其他命令均无效。

95. C. `--show` 选项显示关于计算机上交换空间的信息，包括当前使用了多少交换空间。`-a` 选项激活所有交换空间。没有 `--list` 选项，`-h` 显示帮助信息。

96. C. `pvdisplay` 命令显示有关给定物理卷的信息。你可以使用 `pvdisplay` 查看构建 PV 的设备以及 PV 的物理区大小。所示的其他命令无效。

97. A. `vgscan` 命令查找与 LVM 配置相关的物理卷和卷组。`vgscan` 命令在系统启动时运行，也可以手动运行。其他命令无效。

98. C. `pvscan` 命令显示给定服务器上的物理卷列表。显示的 PV 是那些已通过 `pvcreate` 初始化以供 LVM 使用的。

99. C. `ip` 命令在未通过 `-f` 选项指定指定的情况下默认使用 `inet` 族。该命令将尝试猜测正确的族并回退到 `inet`。该命令选项列出的其他族对 `ip` 命令无效。

100. D. `-n` 选项导致 `route` 仅使用数值，不进行名称解析。该选项对于所描述的场景很有用。`-e` 选项导致输出采用 `netstat` 格式。`route` 命令没有 `-d` 或 `-f` 选项。

101. A. 因为你正在处理 MAC 地址，将将使用 `arp` 命令。`-d` 选项移除或删除 ARP 条目，这在这里是合适的，以便再次进行 MAC 地址解析。`netstat` 命令不会用于此目的。`hostname` 和 `dig` 命令用于名称解析，但不用于 MAC 地址或 ARP 表。

102. B. `-o` 选项从输出中删除换行符，从而使输出更适用于 `grep` 命令。`-l` 选项指定 `ip addr flush` 命令的循环次数。`-f` 选项指定协议族。没有 `-n` 选项。

103. A. `-s` 选项创建 ARP 表条目。`-d` 选项移除条目。不存在 `-c` 和 `--a` 选项。

104. C. `-D` 选项列出计算机上的接口。`-d` 选项转储编译后的匹配代码，`-i` 选择接口。没有 `-a` 选项。

105. B. `-R` 选项要求尝试执行名称解析。`-n` 选项则相反：它禁用名称解析。没有 `-b` 或 `-a` 选项。

106. B. `mtr` 命令提供了一种独特的方法来查看主机间路由中每个跳数的实时信息。`traceroute` 和 `route` 命令都是有效的，但它们各自显示的选项是无效的。没有 `liveroute` 命令。

107. A. `--delay` 选项设置检查数组健康之间的间隔。参数值单位为秒。所示的其他选项无效。

108. C. `!H` 序列表示主机不可达。网络不可达是 `!N`。

109. A. `-m` 选项指定如何标记或标记数据。`-a` 选项是发声 ping，`-p` 允许指定自定义填充。没有 `-k` 选项。

110. B. `-r` 选项显示关于刚完成的 `fsck` 操作的报告，包括 CPU 时间和退出状态。`-f` 选项强制执行请求的操作，`-s` 序列化 `fsck` 操作，`-l` 创建排斥 `flock`。

111. D. 文件 `/proc/meminfo` 提供了关于内存使用和利用率的丰富信息。其中许多信息由各种命令显示，但这些命令的规范源通常可以在此文件中找到。其他选项中，只有 `/proc/cpuinfo` 是有效的，该文件提供有关计算机 CPU 的信息。

112. D. 使用 `nmap` 的 `-sX` 模式可以使用 Xmas 扫描。`-sT` 模式是 TCP 连接，`-sS` 是 TCP SYN。没有 `-sP` 选项。





119. C. `itop` 命令实时显示中断使用情况，其显示方式与 `top` 命令类似。此问题中显示的其他选项均为无效命令。

120. B. `ibstat` 命令显示 Infiniband 设备的信息。其他命令均无效。

121. A. `renice` 命令用于更改优先级。数字越小，优先级越高。正确的语法如选项 A 所示。选项 B 将降低优先级。选项 C 和 D 的语法无效。

122. D. `-n` 选项与 `netstat` 配合使用，防止主机名查找，这可以提高输出速度。其他选项无法执行所需任务。

123. B. `pidof` 命令显示与给定参数相关的所有进程。在这种情况下，选项 B 显示了正确的语法。其他选项中显示的 `ps` 命令是有效命令，但使用的语法并非所示语法。

124. A. 数字 1 或 `SIGHUP` 是向进程发送挂断信号（hangup）的信号。显示的其他选项是有效信号，但不是用于所述目的。

125. D. `sysctl` 命令可用于更改运行内核中的参数。然而，这些更改在重启之间不会保存，如果系统重启则需要重新应用。显示的其他命令无效。

126. C. `-i` 选项设置字节与 inode 的比例。`-b` 选项设置块大小，`-r` 设置文件系统版本，而 `mke2fs` 没有 `-u` 选项。

127. C. `/sys/class/fc_host` 目录包含系统中 HBA 适配器端口的信息。其他选项不是有效目录。

128. B. `account` 模块接口是访问验证的地方。在其他选项中，`auth` 和 `password` 接口用于不同的目的，且没有 `policy` 接口。

129. A. 默认策略应为 `deny`。默认拒绝（deny-by-default）策略会丢弃数据包。值得注意的是，也可以使用 `reject` 策略，它会向发送者发送一个拒绝响应。其他选项不适用于所述任务。

130. C. `-l` 选项显示所有权信息，包括文件或目录的用户所有和组所有。`-o` 选项仅显示用户但不显示组。显示的其他选项对此目的无效。

131. B. 应该创建一个创建一个使用本地 socket 进行通信的程序。基于 socket 的程序不需要包含网络或协议信息，因此对于所述目的，它们优于基于网络的程序。如果程序需要网络连接，则选项 A 将是合适的。其他选项不适用于此场景。

132. C. `buffers` 列显示分配给内核缓冲区的 RAM 数量。`Cache` 表示页缓存使用情况，`shared` 通常表示 `tmpfs` 使用情况。

133. C. `nmcli` 命令提供了进入 NetworkManager 的命令行界面。显示的其他选项均为无效命令。

134. A. `iftop` 命令用于通过类似于 `top` 命令的接口显示实时网络使用情况。给出的其他选项均为无效命令。

135. C. `iptraf` 命令实时显示给定接口的累积网络使用情况。显示的其他选项无效。

136. C. `cfq` 调度器是 Linux 系统的默认值。在显示的其他选项中，`deadline` 和 `noop` 是有效的但不是默认的。没有 `iqueue` I/O 调度器。

137. D. `ipset` 命令可用于所述目的。值得注意的是，你可以为每个 IP 和规则创建单独的 `iptables` 规则，但这样做的效率低于使用 `ipset` 组并对该组应用单个规则。

138. A. 应使用 `tcptraceroute` 命令实现此目的。该命令尝试在指定的 TCP 端口上连接到目标。这种方法比简单的 ping 优，因为 ICMP 可能会被过滤，从而导致诊断不准确。其他命令不会用于此目的。

139. C. `tshark` 命令允许将网络流量捕获到文件中。显示的其他命令无效。

140. C. `whois` 命令用于查询域名和 IP 地址等，并可用于此目的。其他命令对此目的无效。

141. D. `ioping` 命令向给定磁盘发送请求并记录请求所需的时间。在其他命令中，`fdisk` 是有效的，但不会用于确定性能相关问题。其他命令无效。

142. C. `partprobe` 命令导致内核更新分区。其他选项不是有效命令。

143. A. `sar` 命令可用于显示各种性能相关信息，包括随时间捕获的信息。其他命令无效。

144. A. `-a` 选项显示所有可用参数。显示的其他选项对 `sysctl` 无效。

145. C. 状态 `D` 意味着不可中断睡眠。没有调试或死锁进程的状态，可中断睡眠的状态为 `S`。

146. B. 文件 `/etc/default/keyboard` 包含键盘映射信息。显示的其他选项无效。

147. C. 默认端口是 `631`。选项列出的其他端口未用于 CUPS。

148. B. `-R` 选项以递归方式更改所有权。其他选项对此目的无效。`chown` 有 `-f` 选项，但它会将输出变为静默。

149. D. `ausearch` 命令可用于查找最近违反 SELinux 策略的情况。其他命令无效。

150. C. `dmesg` 命令显示内核环缓冲区，是判断系统是否检测到新硬件的主要工具。其他选项无效。

151. A. 可以使用信号数字或符号名称，并如选项 A 所示前加单个连字符（`-`）。其他选项不符合问题要求。

152. A. 目录的执行权限是继承的，因此顶级目录不能允许“其他”执行权限，这是子目录内列出目录所需的。

153. B. `ioping` 的默认大小为 4 KB。

154. A. 使用的 I/O 调度器位于 `/sys/block/<device>/queue/scheduler` 中。其他选项不是此场景的有效位置。

155. D. `-n` 选项防止 `iftop` 进行主机名查找。这有助于减少 `iftop` 输出中显示的噪声或不必要信息。其他选项无法完成所需任务。

156. B. 在 `nslookup` 界面内运行 `server` 命令时，将设置查询发送到的服务器。显示的其他选项对此目的无效。

157. D. 用户为了向其不是所有者且没有组所有权的目录写入，需要写入和执行权限。

158. C. LDAP 可用于 Linux 的外部认证场景，并经常用于与 Microsoft Windows 和 Active Directory 的集成环境中提供认证。在其他选项中，SSL 和 SSH 均不提供外部认证，尽管 SSH 可能与其他认证手段集成。

159. B. `ulimit` 命令显示适用于给定用户的各种限制，包括文件大小限制。其他选项无效。

160. A. 权限应为 755，以便用户执行脚本。其他选项对于所述目的将不起作用，或者权限过于宽松。

161. C. `chattr` 命令用于更改文件属性，包括将其设置为不可变。其他命令无效。




162. A. 小于 1000 的 `UIDs`（不包括 0）通常用于服务账户。这并非强制要求，但是惯例俗成。

163. B. `groups` 命令用于检索组列表。其他命令均无效。

164. A. `swapon` 命令激活交换空间使用。其他命令均无效。

165. D. 使用 `ioping` 的 `-s` 选项可以设置请求大小。其他选项在 `ioping` 中均无效。

166. C. 在 `ausearch` 命令中查找访问向量缓存 (AVC) 消息可以揭示有关策略违规的信息。通常也会查询中包含 `USER_AVC`。显示的其他选项均无效。

167. C. `dmidecode` 命令显示 Linux 系统内硬件的扩展信息。显示的其他选项不是有效的命令。

168. B. `mdadm` 的 `fail` 选项表示磁盘已损坏。显示的其他选项均无效。

169. C. `-H` 选项在可能的情况下抑制免责声明。其他选项无法完成此场景中描述的任务。

170. B. `-i` 选项设置 `iftop` 的接口。显示的其他选项对于所需的任务均无效。

171. B. 文件 `/sys/class/scsi_host/hostN/scan` 用于此目的，其中 `N` 是适配器编号。其他路径对于此场景中描述的目的无效。

172. B. `/etc/shadow` 文件存储加密密码。`/etc/passwd` 文件不存储加密密码，其他选项均无效。

173. B. `lsattr` 命令可用于显示文件的扩展属性信息，例如文件是否为不可变。显示的其他选项均无效。

174. A. `ps` 输出中的 `size` 和 `rss` 列有助于确定给定进程的内存使用情况。其他选项对于进程级排排除无效。

175. C. `SIGKILL` 对应信号数 9。显示的其他数字是有效的信号数，但不是 `SIGKILL`。

176. D. `IN` 类（或 Internet 类）是使用 `host` 命令查询的默认类型。可以通过使用 `host` 命令的 `-c` 选项进行更改。

177. A. 使用 `-r` 选项显示路由表。其他选项不显示路由表。

178. C. `-s` 选项对给参数显示摘要输出。显示的其他选项未能完成所需任务。

179. B. `ps` 命令列出进程，使用 `grep` 查找状态为 `Z` 将显示僵尸进程。在其他选项中，`ps` 虽然有 `-Z` 选项，但它不用于此处描述的目的。

180. A. `lshw` 命令显示系统内的所有硬件，提供关于该硬件许多方面的详细信息。显示的其他命令无效。

181. B. `-c` 选项设置通过 `ioping` 发送的请求数。给出的其他选项对于 `ioping` 无效。

182. B. `R` 状态表示进程正在运行。其他选项不表示运行状态。

## 第 5 章：自动化与脚本

1. A. `echo` 命令用于从 Bash 脚本发送输出。其他选项不是有效命令。

2. A. Ansible 是无代理的，使用 SSH 和 Python 进行编排。Puppet 确有无代理模式但通常使用代理进行编排。其他不是有效的编排包。

3. B. `env` 命令执行命令并为该命令执行启用自定义环境。`set` 命令更改环境变量，但不会像场景中指定的那样为单个命令执行更改变量。其他选项不是有效命令。

4. B. git 中的 `pull` 命令获取更改并合并到当前工作副本中。`fetch` 命令仅检索但不合并更改。其他选项不是有效的 `git` 子命令。

5. B. 基础设施即代码通常意味着使用开发者使用的一些相同工具来管理基础设施组件，例如源码管理以及程序或脚本，以及用于部署和配置更改的自动化。

6. A. 此方案将使用 `chmod` 命令。答案授予 700 是为所有者开启了执行权限。其他选项具有错误的语法，或对于描述的场景具有不适当的权限。

7. A. `source` 命令将文件参数找到的函数添加到当前 shell 中。`source` 命令经常用于软件安装，以确保在执行安装脚本之前正确设置环境。

8. D. 字符序列 `#!/bin/bash` 将随后的命令作为 Bash 脚本调用。

9. C. 大于符号 `>` 用于将输出重定向到文件，如果文件已存在将覆盖它。其他字符不满足此场景的要求。

10. A. 创建 git 仓库需要创建目录，将当前工作目录更改到新目录，然后运行 `git init --bare`。其他命令不会创建空的 git 仓库。

11. B. `inventory`（库存清单）术语通常用于编排，指代受管理的设备集合。

12. D. 反斜杠 `\` 用于转义 Bash 脚本中的单引号等字符。其他字符无法达到预期的结果。

13. A. 退出代码 `0` 表示脚本未遇到错误。此退出代码在 Linux 中通常与程序的成功执行相关。

14. A. Shell 扩展，或更准确地说，大括号扩展（brace expansion），可用于创建所示的输出。其他选项不会产生所示输出。

15. C. 符号 `#` 用于指示后面是注释，不会执行该行的剩余部分。其他选项在其他语言中是有效的注释样式，但对于 Bash 脚本不是。

16. D. 执行 Bash 脚本不需要特殊的扩展名。选项中显示的 `.sh` 是一种常见的扩展，适用于各种类型的 shell 脚本，但扩展并非必须的。

17. C. `merge` 命令合并对之前克隆的 git 仓库的更改。`push` 命令有效但未用于此目的。其他命令无效。

18. A. 代理（Agent）是运行在客户端并在编排架构中监听服务器命令的软件。

19. C. 基础设施自动化是与负载和需求增加（及删除）服务器最相关的术语。

20. C. 当作为函数的一部分执行时，`local` 命令用于在 Bash 脚本中创建局部变量。

21. A. `clone` 命令获取仓库副本供本地使用。`checkout` 和 `co` 命令用于 Subversion 而不用于 git。

22. D. 参数 `$0` 包含被调用脚本的名称。其他答案不符合此场景的要求。

23. B. `printenv` 命令可打印当前 shell 环境的内容（如环境变量）。显示的其他选项不是有效命令。

24. B. 单个等号 `=` 在 Bash 脚本中用于字符串比较。在其他答案中，`-ne` 是有效的，但用于比较整数。字符串 `eq` 如果前面跟一个单连字符（如 `-eq`），则将是一个运算符。在这种情况下，`-eq` 用于整数比较。

25. B. 评估布尔 `true` 的 `while` 循环将完成描述的任务。给出的其他选项在各种方面语法上都是错误的。

26. B. `git checkout` 命令将工作副本切换到指定分支，并将 `HEAD` 指向该分支。显示的其他选项在 git 中无效。




27. C. `export` 命令将变量添加到当前环境中，并经常用于所描述的场景。其他选项不是有效的命令。

28. B. 使用 `echo` 命令可以显示 `PATH` 变量或其他任何 shell 环境变量当前的内容。Bash 中的变量使用 `$` 作为标识符的一部分。因此，任何不带 `$` 的选项都无效。

29. A. `$()` 序列在子壳（subshell）中执行命令，这有助于确保 Bash 脚本中的全局变量不会被修改。显示的其他序列对于所描述的场景无效。

30. B. 该场景描述了通过编排管理配置，因此选项 B 是最接近的答案。

31. B. `-u` 选项或 `--unset` 将从环境中删除变量。其他选项对于 `env` 命令是无效的。

32. C. 双 am 符号元字符 `&&` 仅在第一个命令以成功退出码退出时才执行右侧的命令。单个 am 符号 `&` 会将命令放入后台运行，因此选项 B 是错误的。管道符 `|` 会执行第二个命令，但无论第一个命令的成功与失败都会执行，因此选项 D 是错误的。

33. B. 两个大于号 `>>` 将输出追加到指定的目标。选项 A 仅包含一个大于号，它会覆盖而非追加输出。选项 C 中的管道符 `|` 不会将输出发送到文件，且选项 D 无法实现所述目的。

34. D. 文件通配符（File globbing）是特殊字符扩展的过程，这是该场景所必需的。在这种情况下，否定字符是脱字符 `^`，因此选项 D 是正确的。

35. B. `.gitignore` 文件用于存储不会被版本控制的文件。

36. C. 此目的应使用 `for` 循环，因为它会遍历列表。`until` 循环需要额外的代码，因此对于所描述的目的来说，它是不优的结构。Bash 中没有 `do` 循环或 `foreach` 循环，因此这些选项是错误的。

37. C. 命令替换可以使用反引号（backquotes）或 `$()` 完成。这两种方法在实质上等价，但并非完全相同。

38. C. `git log` 命令用于显示提交历史。显示的其他命令对 `git` 都是无效的。

39. A. `-m` 选项允许在提交中包含消息，从而减少了进入编辑器创建提交消息的需要。显示的其他选项无法完成所需任务。

40. B. 构建自动化（Build automation）是触发提交时启动软件编译最合适的名称。

41. A. 在此场景中，STDIN 重定向是通过小于号 `<` 实现的，获取 `customers.sql` 的内容并将其发送到 `mysql` 命令中。`mysql` 命令可能包含像 `-u` 用于用户名、`-p` 用于提示密码等内容，但这些与该场景无关，且在所有情况下都不是必须的。显示的其他选项对于所述目的无效。选项 B 和 C 接收 `mysql` 命令的输出，而选项 D 是无效的字符序列。

42. C. 很有可能你没有执行 `git push` 将代码发送到服务器。在其他选项中，你不需要向同事发送提交 ID，也没有迹象表明你在提交代码本身时遇到了问题。

43. B. `-R` 选项对 `chmod` 命令识别出的目标执行递归更改。其他选项对 `chmod` 不执行递归更改。

44. D. 右括号用于表示一种情况（case）；当前面有星号 `*` 时，表示默认情况。

45. B. 字符序列 `fi` 是 `if` 语句的反过来写，表示脚本中 `if` 条件的结束。作为选项显示的其他序列可能用于其他语言。

46. D. `master` 分支是 git 仓库中默认创建的分支。显示的其他名称可以使用，但不是默认的。

47. B. 管道符 `|` 将一个命令的输出发送或管道到另一个命令，在 Linux 环境中常用于创建复杂的命令序列，无论是通过脚本还是直接在命令行中。显示的其他选项未用于场景中描述的目的。

48. B. `git status` 命令用于显示工作区的状态，显示如未跟踪的文件、已暂存提交的文件等。显示的其他选项对于该场景无效。

49. B. `-n` 选项抑制了 `echo` 命令末尾的换行符，这在脚本场景中非常有用。其他选项对该命令无效。

50. A. 基础设施的清单包含客户端上安装的软件版本等内容。

51. C. 重定向 STDERR 是通过字符序列 `2>` 完成的。普通的大于号 `>` 重定向 STDOUT。作为选项显示的其他字符序列对于所述目的无效。

52. A. 此目的将使用 `git config` 命令，参数是 `user.email`。

53. B. `readonly` 命令显示当前会话中定义的只读变量列表。列出的其他命令不存在。

54. D. `set` 命令可以用于多种目的来更改 shell 环境的工作方式。其中一个选项是 `–C`，它可以防止像使用 `>` 那样的输出重定向在文件已存在时覆盖文件。

55. C. `file` 命令可确定正在使用的文件类型。这对于没有扩展名的文件特别有用，此时你可能不确定应该查看文件内容。选项 A `grep` 用于在文件内部查找，但在这种情况下没有帮助。`telnet` 和 `export` 命令不用于此目的。

56. B. `history` 命令将显示你的命令历史，包括当前会话的命令。你可以指定显示多少行历史，如本题答案所示。请注意 `.bash_history` 不会显示当前会话的历史。

57. A. 在命令前加一个 `!` 将搜索历史并执行指定的命令。例如，`!vi` 将启动你的上一次 vi 会话。

58. A. 内置命令 `type` 返回 shell 将用于运行给定命令的位置。`find` 命令不能用于此目的，其他命令不存在。

59. C. `source` 命令用于执行来自文件中的命令。一个典型的用例是创建函数或变量，然后这些内容可以在当前会话中使用。列出的其他命令不存在。

60. B. 虽然每个用户都有 `.bash_logout`，但该文件存在于他们的家目录下，因此用户可以编辑它。因此，为了确保在注销时执行所需的命令，必须使用 `/etc/bash.bash_logout` 文件。

61. B. `env -u` 命令将取消当前会话的环境变量。`unset` 命令也可以用于此目的。

62. A. `env` 命令当用 `#!/usr/bin/env bash` 使用时，将自动确定 bash 解释器的位置。这使得生成的脚本对于 bash 可能不在 `/bin/` 下的系统具有更好的移植性。

63. B. `PS1` 变量通常默认设置在 `/etc/profile` 中，并作为 shell 提示符使用。用户可以自定义提示符以包含主机名、工作目录和其他元素。




## 64
C. `$1` 变量在 bash 脚本中自动可用，代表第一个命令行参数。`$0` 变量代表脚本本身。本题列出的其他变量默认不存在。

## 65
B. `seq` 命令用于以各种格式打印数字序列。该题的答案提供了一个起始值 (0)、一个增量 (1) 和最后一个数字 (5)，因此输出六个数字。

## 66
D. `exec` 命令执行作为参数给出的命令，然后将退出 shell。`source` 命令不会退出 shell。

## 67
C. `read` 命令等待用户输入并将该输入放入指定的变量中。`exec` 命令用于执行命令，其他选项对于描述的用途无效。

## 68
A. 括号用于表示函数，例如 `myFunction()`。括号是可选的，但后面紧跟着大括号，大括号中包含调用函数时要执行的命令。

## 69
C. 序列 `esac` 是 `case` 的反写，用于表示 `case` 语句的结束。在其他选项中，`done` 语句用于终止 Bash 中的某些循环。

## 70
C. `-p` 选项以完全限定的形式显示 `declare` 语句，这样这些命令可以通过管道或重定向到脚本来作为另一个命令的输入。

## 71
C. 方括号用于表示 shell 脚本中 `while` 循环测试部分的开始和结束。其他语言通常使用括号用于此目的。

## 72
B. `test` 内置命令将返回真，并可测试变量是否存在且为空。请注意，`test` 内置命令的行为取决于参数的数量。

## 73
C. 当输入命令 `cd ~` 时，系统会查询自动设置为用户主目录的 `HOME` 环境变量。以 `HOME` 开头的其他路径默认不存在，而显示的 `MAILPATH` 环境变量包含了在交互式使用 shell 时检查邮件的路径列表。

## 74
B. 将使用 `git log` 命令实现此目的，并带有 `--follow` 选项以及要跟踪历史记录的文件名/路径。

## 75
A. 客户端的参数和其他事实在编排中也被称为 `attributes`（属性）。

## 76
C. 整数比较运算符 `-eq` 用于 Bash 脚本中的整数比较。其他答案对于 Bash 脚本比较无效。

## 77
C. 分号元字符将多个命令连接在一起，但不会将一个命令的输出作为下一个命令的输入。如果需要将输出发送到下一个命令，则使用管道字符（选项 D）。单个符号 符号会将任务置于后台运行，因此选项 A 是错误的；大于号重定向标准输出，使得选项 B 也是错误的。

## 78
A. `\a` 转义序列与 `echo` 命令配合使用时会发出警报声或铃声。`\b` 选项是退格。`\c` 选项表示 `echo` 不产生任何额外的输出。`echo` 没有 `\d` 选项。

## 79
D. 注意，变量名和等号之间不能有任何空格。同样，等号和变量内容之间不能有任何空格。这使得答案 D 唯一的正确选项。

## 80
A. 提供的答案执行了命令替换，并将结果命令的值放入变量中。注意日期上使用了 `+%s` 格式，然后按照问题要求的将输出格式化为自 epoch 来的秒数。选项 C 提供 `DATE` 变量中的日期，但不会按指定格式格式化。

## 81
B. 在 shell 脚本中，执行命令从 `do` 关键字开始，到 `done` 关键字结束。其他语言通常使用大括号或标签。

## 82
A. `declare` 的 `-r` 选项将创建或标记变量为只读。`-p` 选项以可以重用的格式打印输出。`-x` 选项声明导出变量。

## 83
C. 环境变量 `LC_TIME` 用于控制时间的显示和行为，可以更改为不同的区域（locale），以实现所需的日期时间格式显示和行为。本题列出的其他选项不存在。

## 84
A. `-i` 选项以表格格式显示接口信息。会显示发送和接收字节以及接口的 MTU 等其他信息。`-r` 选项显示路由，而 `-l` 显示监听套字。没有 `-t` 选项。

## 85
C. Ctrl+C 键组合会杀死正在交互式运行的 shell 脚本。其他键组合可能有影响，但在此语境下或对于预期的行为无效。

## 86
C. Shell 脚本语法使用所示格式，在测试条件周围使用方括号，并使用双等号进行字符串测试。变量前如所示带有美元符号。

## 87
A. 设置 `PATH` 的语法用冒号分隔新路径，如正确选项所示。本题正确选项与错误选项之间的主要区别在于实际指定路径的显示方式。

## 88
B. `--abort` 选项尝试回滚有问题的合并。所示其他选项作为 `git merge` 命令的选项不存在。

## 89
A. 环境变量 `GIT_DIR` 可以更改默认位置，使其偏离 `./.git` 目录（通常在此创建新仓库）。其他选项未被 git 作为环境变量使用。

## 90
B. `\t` 转义序列添加水平制表符。其他可能有可能有含义，因此对本题无效。例如，`\a` 是警报或铃声。

## 91
C. 双星序列 `**` 具有特殊含义，表示该文件将在所有目录中被忽略。

## 92
A. 该场景需要交替。因此，将使用方括号表示序列的开始。括号之后，单个星号表示通配符。其他选项不适用于描述的场景。

## 93
B. 将使用 `git remote` 命令实现此目的；当给定 `show` 选项和远程名称（在此情况下为 `origin`）时，将显示关于该远程的附加信息。该命令对于显示推送代码的目的地有用。

## 94
D. `$#` 序列包含传递给 shell 脚本的命令行参数个数。所示其他选项均非 Bash 预定义。

## 95
B. `TMOUT` 变量可以在给定用户的 shell 中设置，用户将在空闲达到给定值（秒）后被注销。此地列出的其他环境变量均不存在。

## 96
C. 该行将输出 `NUM` 变量的内容。注释出现在行的命令之后，只有 `#` 之后的代码会被忽略。

## 97
A. 使用 `--origin` 或 `-o` 选项可以更改名称，而不是使用默认的 `origin`。其他选择不是 `git clone` 的选项。

## 98
D. `steal` 列显示了由于虚拟机管理程序为另一个虚拟处理器获取周期而导致等待的时间百分比，可用于自动化以指示需要部署额外的 CPU 资源。

## 99
C. `LC_ALL` 变量可设置区域环境变量，并会覆盖其他变量。这可以在需要临时更改时使用。此处列出的其他变量未用于此目的，且默认不存在。

## 100
A. 过程是指作为自动化的一部分在客户端节点上执行的一个或多个命令。





101. C. 双分号 `;;` 用于表示 `Bash` 脚本中单个子句的结束。所示的其他序列无法完成所描述的任务。

102. C. `unalias` 命令用于删除之前定义的别名。`rm` 命令会删除普通文件，但不会删除别名。其他命令不存在。

103. B. `-e` 选项检查文件是否存在，通常用于 shell 脚本中的条件语句中。其他选项可能在 shell 脚本中有效，但它们不是用于文件存在性的测试。

104. C. 设置 `LANG=C` 是 POSIX 兼容性的别名，将导致程序跳过本地化翻译。显示的 `LANG` 的其他选项均无效。

105. A. `--list` 选项显示 `git` 的当前配置参数。其他选项作为 `git config` 命令的选项并不存在。

106. B. 数字 2 表示 `STDERR` 重定向，双大于号 `>>` 表示输出将是追加而不是覆盖。

107. A. 扩展名为 `.yml`的文件通常包含 YAML。问题还提到了“基础设施即代码”（infrastructure as code），许多工具使用 YAML 进行配置和过程。

108. A. `passwd` 文件将被发送到 `STDOUT`，在那里捕获并发送到 `cut` 命令。`cut` 命令将使用冒号作为分隔符逐行分离文件内容。第一个字段将发送到 `STDOUT` 并置于名为 `users.txt` 的文件中。

109. C. `shift` 命令将位置参数向下移动一位。这对于具有多个命令行参数（每个参数包含一个选项）的复杂场景很有帮助。

110. D. 应该在 `git pull` 中添加 `--no-commit` 选项，以防止合并自动提交。

111. A. 与 `for` 循环一样，`until` 循环内的命令用 `do` 和 `done` 隔开。

112. B. 退出码 1 表示通用错误。退出码 0 表示成功，255 是超出范围的。`Bash` 没有 -1 退出码。

113. B. `./configure` 模式通常用于调用配置脚本。选项 A 可能有效，但 `build` 目录通常不在路径中。

114. A. 在 `git commit` 中添加 `-a` 选项会自动提交之前已知的文件。`-c` 选项会调用编辑器进行提交，而其他选项不存在。

115. C. `LC_MONETARY` 变量被某些程序用于确定货币的本地化设置。

116. D. `TZ` 环境变量用于此目的，通用格式如所示，因此选项 D 是正确答案。

117. A. 在 shell 脚本中，数组创建在这样方式使用时涉及括号。你也可以使用方括号来定义单个元素，例如 `ARRAY[0] = "val1"`。

118. C. `-lt` 运算符用于测试脚本中的“小于”条件。其他运算符在 shell 脚本中无效。

119. C. 在这种情况下，`for` 循环结构要求在变量名 `LIST` 前面加上美元符号（`$`），因此选项 C 是正确的。其他选项将无法实现描述的目的。

120. C. `elif` 关键字用于在 shell 脚本中创建备选执行路径。其他结构（如 `else if` 和 `elsif`）用于其他语言。

121. C. `.git` 目录用于存储仓库的元数据。

122. B. 选项 B 所示的字符序列是重定向 `STDERR` 和 `STDOUT` 的正确序列。在所示其他选项中，选项 A 只重定向 `STDERR`。所示的其他选项均无效。

123. D. 双管道元字符 `||` 仅在第一个命令失败时才执行右侧命令。单个安符 `&` 将命令放入后台运行，因此选项 B 是错误的。双安符元字符 `&&` 仅在第一个命令成功时才执行第二个命令，因此选项 C 是错误的。

124. C. `git checkout` 命令切换 `HEAD` 指向的位置。通过添加 `-b` 选项，还会创建该分支。

125. D. `while` 和 `until` 循环都会执行到条件发生变化。`while` 循环在条件不再为真时停止，而 `until` 循环一直执行到条件为真为止。

126. A. 整数比较通常使用二元比较运算符，如 `-gt`、`-eq` 等。选项 B 是错误的，因为 `>` 运算符用于方括号中。没有 `-gta` 运算符或 `gt` 运算符，因此选项 C 和选项 D 都是错误的。

127. C. SSH 通常用于无代理编排中节点之间的通信。不常见的是如 HTTPS 这样的协议。选项中所示的其他协议将不会用于无代理编排。

128. C. 变量或参数扩展通过包裹在参数名周围的 `${ }` 完成。

# 第 6 章：模拟考试

1. B. 当前中断 (IRQ) 分配包含在 `/proc/interrupts` 文件中。因此，使用 `cat` 等命令查看文件内容是可行的。没有 `view` 命令，因此答案 A 错误。同样，没有 `/dev/irq` 文件，因此答案 C 和 D 错误。

2. D. udev 的配置文件可以在 `/etc/udev` 中找到，这使得答案 D 正确。其他选项不存在。

3. A. `modprobe` 命令加载模块及其依赖项（如果适用）。`lsmod` 命令用于列出当前加载的模块，因此答案 B 错误。`insmod` 命令将加载指定的模块但不加载其依赖项。答案 D，`rmmod` 用于从内存中删除模块。

4. A. 如果在控制权移交给 GRUB 时按下 Shift 键，将显示 GRUB 菜单。

5. D. `dmesg` 命令显示内核环形缓冲区的内容。在许多 Linux 发行版中，此日志也保存到 `/var/log/dmesg`。此问题所示的其他选项均为无效命令。

6. A. 列表显示位于当前目录下的符号链接文件，链接到 `.configs/fetchmail/.fetchmailrc`。该文件属于 root 用户和 root 组，创建于 2014 年 7 月 8 日。

7. B. `systemctl` 命令用于处理服务和目标。`list-units` 命令用于列出目标。其他命令未用于此目的，或者其所需的选项不存在。

8. C. `-nn` 选项同时显示数字和设备名称，因此答案 C 正确。`-n` 选项（答案 B）只显示数字。另外两个选项不存在。

9. C. 在给出的选项中，`systemctl status` 命令和选项最合适。`telinit` 和 `sysctl` 命令不用于此目的。同样，`--ls` 选项对 `systemctl` 无效。

10. D. 包含 `/var` 的分区应该是邮件服务器最大的，因为邮件队列存储在该层次结构中。`/etc/` 目录通常较小，`/usr/bin` 也是如此。默认不存在 `/mail` 目录。

11. B. `plist` 选项显示给定软件包的依赖项。`list` 选项显示特定软件包的信息，而另外两个选项无效。

12. A. `-ivh` 选项将使用 `rpm` 安装文件，显示详细输出和用于进的哈希标记。所示的其他选项不存在或无法完成指定任务。

13. A. `apt-cache` 命令用于处理包缓存，`search` 选项用于在缓存中搜索提供的参数（在此例中 `zsh`）。`apt-get` 命令用于处理包本身，而 `apt-search` 命令不存在。




### 14. A
`-V` 或 `--verify` 选项将检查给定软件包中的文件是否与软件包数据库中的版本（或校验和）相符。如果没有文件被修改，则不会产生任何输出。请注意，对于在安装期间或其他原因更改的文件，可能会产生输出。另请注意，此选项使用的是大写的 `V`，而不是表示详细模式的写写 `v`。

### 15. D
`top` 命令用于持续监控 CPU 和内存使用等情况，`-p` 选项监控单个进程。通过配合 `pidof` 命令使用运行引号，可以将进程 ID 作为输入提供给 `-p` 选项。值得注意的是，这只有当进程只有一个实例时才有效。

### 16. A
`-g` 选项显示转储的进度。列出的其他选项均不存在。

### 17. C
`debugfs` 命令可用于此目的。当使用 `-c` 打开文件系统时，它将以灾难模式（catastrophic mode）打开，这意味着它是只读的，并且打开时不会读取 inode。

### 18. C
`xwininfo` 命令显示 X 会话中给定窗口的信息。此答案中列出的其他命令均无效。

### 19. C
文件 `/etc/localtime`（可以是实际文件或符号链接）被用于指示本地时区。列出的其他文件均不存在。

### 20. D
在 `/usr/share/zoneinfo` 层次结构中，你将找到有关可用区域和时区的信息。该层次结构中的文件可以符号链接到 `/etc/localtime`。

### 21. A
`/etc/skel` 目录包含在创建用户时会自动复制到该用户家目录的文件。此问题列出的其他目录默认不存在。

### 22. B
`atq` 命令显示用 `at` 命令调度的任务列表。其他命令均不存在，但选项 D 除外，该选项显示了 `at` 命令但带了一个无效的选项（`--jobs`）。

### 23. B
UTF-8 提供多字节字符编码，并被广泛认为是未来的编码标准。ISO-8859 是单字节编码。其他答案均无效。

### 24. C
基于 SSL 的 LDAP (LDAPS) 运行在端口 636 上。端口 53 用于 DNS；端口 389 用于普通的非 SSL LDAP；端口 443 用于基于 SSL 的 HTTP。

### 25. B
`chage` 命令可用于此目的，`-E` 选项接受自 1970/1/1 起的天数。`passwd` 没有 `-e` 选项，`usermod` 的 `-l` 不会执行描述的操作。没有 `chguser` 命令。

### 26. A
SSH 的 `-i` 选项后跟随用于身份验证的私钥。这意味着公钥位于远程主机上的 `authorized_keys` 文件中。`-k` 选项禁用 GSSAPI 凭据，而 `-f` 用于请求 SSH 后台运行。没有 `--key` 选项。

### 27. A
`-n` 选项有助于描述的场景，并将以非零退出而不是提示。`-i` 选项设置登录名称，在此场景下无效。`-q` 和 `--noprompt` 选项不存在。

### 28. A
单用户模式通常是运行级别 1。在运行级别 1 中，不会启动网络服务。运行级别 2 有网络，但通常没有服务。运行级别 5 是带网络的完整多用户模式，运行级别 6 是重启。

### 29. B
`free` 命令显示 RAM 和交换区的当前内存使用情况，包括总可用量、当前使用量和当前空闲量。列出的其他选项命令均不存在。

### 30. A
`df` 命令显示磁盘使用信息，并可以帮助规划长期磁盘利用率。例如，如果你注意到磁盘利用率正在显著增加，可以准备上线更多磁盘，甚至可以更改日志轮转计划，使日志轮转更快，从而释放空间。

### 31. A
`sar` 命令可用于此目的，当提供显示格式的数字时，它将每隔 X 秒更新一次 Y 次。

### 32. C
`-m` 选项导致磁盘统计数据使用兆字节作为单位，而不是默认的千字节。

### 33. A
`mkinitrd` 命令在旧系统中用于创建初始 RAM 磁盘。初始 RAM 磁盘用于加载（有人可能会说是预加载）磁盘和其他启动所需的其他关键组件的必需模块。

### 34. D
`bzImage` 可能意味着使用了 bzip 压缩镜像，但也可以仅仅意味着“Big zImage”并使用 gzip 压缩。`bzImage` 通常用于可以超过适用于 zImage 的 512 K 限制的内核镜像。

### 35. A
`-r` 选项修复文件系统，而 `-y` 选项导致 `fsck` 假设为是而不是进行提示。`-v` 选项是详细模式。`fsck` 没有 `-m` 或 `-x` 选项。

### 36. A
`default.target` 是 `systemd` 在启动时激活的默认目标单元。默认目标根据依赖关系启动其他服务。

### 37. B
`mkswap` 命令用于格式化交换分区。其他命令无效。

### 38. B
挂载选项带有 `defaults` 的文件系统将被挂载为读写 (`rw`)、`suid`，并具有执行可执行文件 (`exec`)。文件系统将自动挂载 (`auto`)，但用户将无法挂载它 (`nouser`)。字符和块特殊设备将被解释 (`dev`)，对磁盘的操作将以异步方式执行 (`async`)。

### 39. C
`fstrim` 命令用于删除未使用的块。`fstrim` 命令经常用于 SAN 配置，以将未使用的存储空间归给 SAN。`fstrim` 命令也可以用于固态硬盘以达到相同目的。列出的其他命令无效。

### 40. A
`--create` 选项启用使用 `md` 创建 RAID 阵列。典型参数是 `/dev/mdN` 设备。列出的其他选项对 `mdadm` 无效。

### 41. B
`lvcreate` 命令用于从之前创建的物理设备卷卷创建逻辑卷。使用 `lvcreate` 是实际使用逻辑卷之前 LVM 三步骤中的最后一步。

### 42. A
`ss` 命令提供了许多 `netstat` 相同的功能，但可以显示一些扩展信息，例如给定套接字的内存分配。`free` 命令显示内存使用情况但不是按套接字划分，另外两个命令不存在。

### 43. D
`-f` 选项是洪水泛洪（flood ping）。这将有效地导致接口发送和接收大量流量，通常使其更容易在交换机上找到。`-a` 选项是听觉 ping，在 `ping` 时发出声音。`-c` 选项发送指定数量的 ping，没有 `-e` 选项。

### 44. C
`bs` 选项用于指定块大小。可以是各种后缀，例如 `M` 等于兆字节，`K` 等于千字节。

### 45. B
`--size-only` 选项检查正在同步的文件大小是否相同。这对于可能存在显著时间偏斜或其他问题，导致正常差异机制无法正常工作的情况很有帮助。列出的其他选项对 `rsync` 无效。

### 46. A
MX 记录优先级最低的数字获胜，从而使 0 成为该域优先级最高的 MX 记录。

### 47. D
DNS 通常使用 UDP 端口 53，区域传输除外，由于大多数区域请求的大小，区域传输使用 TCP 端口 53。

### 48. D
`axfr` 类型可以配合 `dig` 使用来请求区域传输。请求区域传输的客户端需要获得授权才能发起传输。

### 49. D
文件 `/etc/exports` 包含了使用 NFS 共享的文件系统的定义。其他文件均不可用于 NFS。




**50. B.** `max-lease-time` 指令后接秒数，指定了给定主机在被清除之前可以拥有的租约时间。显示的其他选项在 `dhcpd.conf` 配置文件中是的。

**51. A.** 在 `nsswitch.conf` 中，`passwd` 行包含有关身份验证的信息。其格式如正确答案所示。本地验证使用 `files` 关键字针对普通的 `passwd` 文件完成。通常有一行名为 `shadow` 的类似行，假设服务器使用影子密码（shadow passwords）。`shadow` 行遵循类似的格式。

**52. D.** `ssh-keygen` 命令生成一对公钥和私钥，该密钥对可用于客户端和服务器之间的用户身份验证。显示的其他命令均无效。

**53. D.** `authorized_keys` 文件包含密钥，当客户端发送相应的私钥时，这些密钥可用于身份验证。其他文件均的。

**54. D.** 开始故障排除的逻辑位置是在系统 BIOS 或固件内部，以确保计算机检测到了驱动器。

**55. B.** `export` 命令用于此目的，并接受如答案所示的 `name=value` 对。其他命令均无效，`echo` 命令除外，它只会将参数回到控制台。

**56. C.** `HISTFILESIZE` 选项配置在历史文件中保留的命令数。其他变量在 bash 中均无效。

**57. C.** 显示的 `awk` 命令可以用于此目的。`-F` 选项设置字段分隔符，`OFS` 选项设置输出字段分隔符。

**58. B.** 如果在命令行中传递不同的目录，`git clone` 命令将克隆到该目录，如选项 B 所示。显示的其他选项不是有效的 `git clone` 语法。

**59. A.** 必要的 `export` 命令以便在当前会话中手动定义的任何变量都可以对子进程可用。`source` 命令执行文件并可用于描述的目的，但需要额外的参数。`let` 和 `def` 命令均无效。

**60. C.** `source` 命令的功能上等同于单个点 (`.`)。`set` 命令存在但未用于此目的。其他命令均无效。

**61. A.** 正确的语法如所示。注意，当命令包含在一行时，需要一个分号，如答案所示。

**62. B.** `-f` 选项设置账户过期与禁用之间的天数。`-g` 选项用于设置组 ID，而 `-e` 用于设置总过期日期。

**63. C.** `crontab` 命令的 `-r` 选项删除指定用户的所有 cron 条目。`-l` 选项列出 cron 作业，而 `-e` 编辑 `crontab`。没有 `-d` 选项。

**64. D.** `journalctl` 命令用于查看和解析基于 systemd 的系统上以特殊格式维护的日志文件。`logger` 命令可创建日志条目，显示的其他命令均不存在。

**65. C.** `lpr` syslog 设施将消息从 `lp` 子系统发送到 syslog。`auth` 设施用于安全消息。列出的其他选项不是 syslog 设施。

**66. D.** 标准 LDAP 流量是服务器上的 TCP 端口 389。TCP 端口 25 是 SMTP，443 是 HTTPS，143 是 IMAP。

**67. C.** 连接到备用端口时，可以使用 `-p` 选项设置端口，或使用冒号将主机与端口分开。

**68. D.** `-p` 选项保留权限。`-x` 选项提取，而 `-z` 使用 gzip 解压缩。`-v` 选项是 `verbose`（详细）。

**69. B.** `-i` 选项告诉 `patch` 忽略空格。当补丁文件与所需的完全完全匹配时，这可能是必要的。`-p` 选项设置补丁的目录级别，而 `-e` 通知 `patch` 解释为 ed 脚本。`patch` 没有 `-w` 选项。

**70. C.** LUKS 加密是 `dm-crypt` 命令的默认模式。其他模式包括 plain、loopaes 和 tcrypt。

**71. B.** `-r` 选项反转日志，首先显示最新条目。`-n` 选项显示最近的 N 个事件，`-f` 是 `follow`（跟踪），`-b` 告诉 `journalctl` 显示来自特定启动 ID 的消息。

**72. D.** `emergency` 目标用于救援模式无法恢复系统的情况。其他目标均无效。

**73. A.** 如问题所示，你需要同时移除组所有权用户所有权，因此都需要 `-g` 和 `-o`。其他选项均无效，尽管你可以在归档过程中通过 `--no-g` 和 `--no-o` 移除单个选项，这等同于从命令中移除 `-g` 和 `-o` 选项。

**74. B.** `-r` 选项绕过路由表并允许使用接口直接发送数据。`-A` 选项是自适应 `ping`，而 `-b` 允许向广播地址发送 ping。`-q` 选项是静默输出。

**75. B.** `-b` 选项在补丁之前创建原始文件的副本。这在连续补丁多个文件的脚本化场景中特别有用。`-d` 选项导致在补丁之前更改目录，而 `-c` 告诉 `patch` 将补丁文件解释为普通 diff 文件。`-s` 选项导致 `patch` 在静默模式下工作。

**76. C.** 编排软件可以使用代理（问题中描述的部分），编排软件也可以是无代理的，不需要在每个客户端机器上安装特殊软件。

**77. B.** `\r` 转义序列是回车符，`\n` 是换行符。`\c` 序列调用控制字符与此问题无关。

**78. A.** `-f` 文件测试检查文件是否存在，在描述的脚本场景中很有用。

**79. C.** 通过专门为脚本中的命令调用 shell，你可以执行脚本的内容。选项 A 需要设置执行位。其他选项将不起作用。

**80. A.** 将使用 `ls-files` 命令用于此目的，并使用 `-i` 或 `--ignored` 同一个必需的排除模式，因此选项 A 是确的。选项 B 缺少必需的排除模式。

**81. A.** 从文件重定向输入使用小于号。选项 B 获取 `script.sh` 的输出并将其发送到 `file.txt`。选项 C 尝试使用 `file.txt` 作为输入，但没有方法将内容发送到 `STDOUT`。选项 D 执行 `script.sh`并将内容发送到 `file.txt`，这与场景相反。

**82. B.** `-c` 选项设置最大挂载次数。`-C` 选项设置当前挂载次数。`-b` 和 `-a` 选项不存在。

**83. D.** `-f` 选项也称为 `fake`，有助于调试挂载过程或需要为以前挂载的文件系统向 `/etc/mtab` 添加条目的情况。`-l` 选项显示标签，`-v` 是 `verbose`。没有 `-q` 选项。

**84. A.** 可以使用 `netstat` 命令用于此目的，`-r` 选项显示当前路由。添加 `-n` 可以防止 DNS 查找，这有助于性能。

**85. A.** `ps` 命令提供单个进程的处理器和内存使用信息。你可以使用这些信息来预测容量。

**86. C.** `wa` 统计显示等待 I/O 的时间，可用于测量或寻找与磁盘相关的瓶颈。`us` 统计是花费在用户态进程上的时间，而 `sy` 是花费在内核进程上的时间。`vmstat` 中没有名为 `io` 的统计数据。

**87. A.** 使用 `uptime` 命令显示的平均负载以 1 分钟、5 分钟和 15 分钟为增量显示。





88. A. `-a` 选项显示 `sysctl` 的所有值及其当前设置。`-b` 选项为 `binary`（二进制），在不任何换行的情况下显示值。`-d` 选项是 `-h` 的别名，用于显示帮助。没有 `-c` 选项。

89. B. `SIGTERM` 信号是使用 `systemctl kill` 命令发送的默认信号。

90. C. `ldconfig` 命令用于处理库缓存，`-p` 选项打印缓存中的目录和库。`-C` 选项告知 `ldconfig` 使用不同的缓存。`ldd` 命令打印给定命令的库依赖，但给出的选项并不适用于 `ldd`。

# 索引

## A

* `\a` 转义序列，174
* `aa-complain` 命令，115
* `aa-disable` 命令，119
* `aa-unconfined` 命令，113
* `AAA`（认证、授权、审计）服务，116
* 用于合并冲突的 `--abort` 选项，176
* 访问控制列表
    * 文件，111
    * 策略，149
    * Squid，73–74
* 账户
    * 禁用，196
    * 过期，69, 96, 190
    * 相关信息，98
    * 锁定，115
    * PAM，149
* `acl` 命令，73
* 网络绑定的活动-备用模式（active-backup），30
* 网络绑定的活动/被动模式（active/passive），30
* 地址。另见 IP 地址
* 密码年龄限制，121
* 代理编排，164, 198
* 无代理编排，183
* 警告的转义序列，174
* 别名命令，178
* 邮件别名，66
* `allow-guest=false` 选项，135
* `AllowUsers` 指令，108
* `alsamixer` 命令，82
* anaconda 和 kickstart，31
* Ansible 包，162
* Apache 服务器
    * 配置文件，77
    * 重启，75
    * SSL 私钥，83
* AppArmor
    * 进程，113
    * 配置文件，115, 119
    * 设置，119
* 追加输出
    * 追加到文件，167
    * 追加到标准输出（STDOUT），78
* `apt-cache search` 命令，51, 188
* `apt-get update` 命令，52, 130
* `apt-get upgrade` 命令，48, 129
* `rsync` 命令的归档模式，71
* 参数，数量，177
* `arp` 命令，144–145
* 数组
    * 创建，25, 181, 192
    * RAID，24, 26, 156
* `at now` 命令，62
* `atq` 命令，189
* `atrm` 命令，63
* 文件属性，154, 156
* 音频，混音器量，82
* `auditd` 守护进程，117
* `ausearch` 命令，152
* 认证
    * 生物识别，114
    * Kerberos，104, 112, 121
    * 密钥，190, 194
    * LDAP，122, 154
    * 日志，115
    * 机制，194
    * 网络组件，117
    * PAM，122
    * `rndc`，103
    * 服务器 UID 和 GID，64
* 认证、授权、审计（AAA）服务，116
* 权威名称服务器，查询，16
* 授权
    * 日志，115
    * PAM，122
    * authorized_keys 文件，98
* `autofs` 自动挂载，70
* 自动注销，177
* 自动化
    * 构建，168, 180
    * 配置，166
    * 基础架构，165, 178
    * 清单，174
* 自动挂载选项，70
* AVC 消息，155
* `awk` 命令，195

## B

* 后台任务，查看，133
* 反引号，168
* 反斜杠，163
* 备份
    * 提取，17
    * 增量，114
    * 补丁，198
* 反向搜索，58
* 块
    * 检查，147
    * 显示，23
* 负载均衡 rr 模式，35
* 裸金属虚拟机，34
* 软件包 URL，72
* `.bash_history` 文件，195
* `.bash_profile` 文件，60
* 调用 Bash 壳，63
* `bcfg` 命令，22
* 警报声转义序列，174
* `/bin/false` shell，135
* BIND
    * chroot，103
    * 重载，77
    * 服务器配置，73
    * 服务器控制，79
* 生物识别认证，114
* BIOS
    * 密码，114
    * SATA 磁盘，194
* 模块黑名单，21
* `blkid` 命令
    * 缓存，33
    * UUID，11, 33
* 块存储，31
* 块设备信息，142
* 块
    * 移除，25, 192
    * 预留，12
* 蓝牙设备，检测，85
* 绑定链路聚合，33
* 绑定场景，负载均衡在，35
* `/boot/efi` 分区，5
* `/boot/grub/grub.conf` 文件，110
* `/boot` 分区
    * 挂载在，22
    * 大小，7
* 服务启动时间，76
* 启动
    * 更改顺序，22
    * 配置，22
    * 设备检查顺序，12
    * 从 HTTP 和 FTP，28
    * 内核环形缓冲区，5
    * kickstart，35
    * 位置，27
    * `lsblk` 命令，72
    * 防止，114





- 单用户模式，5
- 故障排除，129
- 引导加载程序
    - ISO, 22
    - 密码，110
    - UEFI, 22
- `echo` 命令中的大括号扩展，164
- `brctl` 命令，36
- 桥接 vs. NAT，30
- btrfs 文件系统，11
- 内存使用的 `buffers` 列，150
- 自动化构建，168, 180
- 构建文件，排除，176
- 绕过
    - 语言区域翻译，14, 179
    - 路由表，198
- 字节与索引节点比例，149
- 创建 `bzImage`，191
- `bzip2` 命令，103

## C
- 缓存
    - Kerberos 认证，112
    - 软件包，52
    - 清理，33
    - 共享库，48, 129
- Cacti 工具，143
- `caja` 文件管理器，76
- 回车符的转义字符，198
- case 语句 (case statements)
    - 子句结束，178
    - 默认情况 (default case)，169
    - 终止，173
- `cat /etc/passwd` 命令
    - 内容输出，55
    - 描述，179
    - 用户名，54
- `cat /proc/interrupts` 命令，46, 186
- CentOS 7 错误报告工具，78
- 证书权威服务器，73
- 证书签名请求 (CSRs)，77
- Postfix TLS 中的证书，105
- `cfq` 调度程序，150
- `chage` 命令
    - 账户，96, 98
    - 密码，64, 121
- 命令链式，169, 174
- 修改密码过期日期，64, 69
- 字符大小转换，83
- 字符
    - 属性，189
    - 多字节表示，13
    - 支持的字符集，32
- `chattr` 命令，154
- `chcon` 命令，113
- 文件的校验和，118
- `chgrp` 命令
    - 组所有权，94–95
    - Web 服务器，59
- `chkconfig` --level 命令，79
- `chkconfig` --list 命令，47
- `chmod` 命令
    - 权限，111
    - 特权，95
    - 递归更改，95, 169
    - 脚本执行，162
    - 粘滞位，95
- `chown` 命令，118, 152
- 使用 `BIND` 的 `chroot` 场景，103
- `CIFS` (通用互联网系统)，32
- 时钟
    - 设置，15
    - UTC 时间，15
    - 操作，14
- 仓库克隆，165, 177, 195
- `cloud-init` 命令，32
- 集群服务器，79
- 设备集，163
- 命令执行
    - 自定义环境，162
    - 注销时，171
    - 在非交互式会话中，99
    - source 命令，171
    - 子 shell，166
- Network Manager 的命令行界面，150
- 命令
    - 别名，178
    - 参数，177
    - 反引号，168
    - 链式，169, 174
    - 注销时执行，171
    - 退出 shell，172
    - 来自文件，171
    - 历史，171, 195
    - 内核模块，30
    - 位置，171
    - 多个，167, 182
    - 参数，172
    - 路径，176
    - 调度，62
    - SQL，168
    - 执行，31
    - 用户输入，172
- 注释
    - `/etc/inetd.conf` 文件，100
    - 脚本，164
- 提交
    - 自动，180
    - 历史，174, 171
- `CIFS` (通用互联网系统)，32
- 比较
    - 文件，77
    - 整数，174, 182
    - 模块，35
    - 字符串，165
    - 变量，176
- AppArmor 模式，115
- 完成的 CUPS 任务，67
- 压缩
    - `.gz` 文件，72
    - 日志，97
    - `lzma` 文件，94
    - `tar` 命令，102
- 配置自动化管理，166
- 磁盘连接，129
- 连接
    - 虚拟机，32
    - `SSH`，197
    - 故障排除，140
    - 设备，48
    - 服务器，135
- root 用户登录，111
- 容器，75
- 上下文
    - 显示，114
    - 文件，120
    - `SELinux`，113, 115, 119, 152
- 字符大小转换，83
- 复制
    - 目录，55
    - 文件，60, 85, 117, 189
    - 密钥，120
    - 仓库，169
- `cp` 命令
    - 目录，55
    - 覆盖文件，55
- `cpio` 实用，117
- `cron`
    - 目录，63
    - 条目列表，65
    - 执行，62
    - 计划任务，96
    - 系统级文件，63
    - 用户，62
- `crontab` 命令
    - 条目列表，65
    - 删除任务，196
- `cryptsetup` 命令，101
- CSRs (证书签名请求)，77
- `Ctrl+Alt+Del` 键，禁用，110
- `Ctrl+C` 键
- 终止守护进程，77





* 终止脚本，175
* 用于挂起进程的 `Ctrl+Z` 键，83
* CUPS 系统
    * 已完成的打印作业，67
    * 配置，66
    * 默认端口，67, 152
    * 重启，68
* `curl` 命令，80
* 与货币相关的本地化，14, 181
* 当前默认路由，199
* 当前挂载的文件系统，10
* 内内核模块的自定义命令，30
* 自定义日志，67
* 在自定义环境中的命令执行，162
* `cut` 命令，55
* 用于安全公告的 CVE 流程，116

# D

* 守护进程 (daemons)
    * 配置文件，81
    * 本地服务器，149
    * 停止，81
    * 挂起，83
    * 终止，77
* 数据报安全，112
* 数据报传输层安全协议 (DTLS)，112
* `date` 命令，15
* 日期
    * 格式，13, 175
    * 获取，175
    * 设置，15
* `dd` 命令
    * 兆字节 IO，193
    * 分区镜像，94, 118
* Debian 系统，更新，48, 129
* `debugfs` 命令，188
* 调试，启用，27
* libvirt 的调试日志，31
* `declare` 命令，173, 175
* 声明变量，166
* VNC 中的默认基端口，78
* 仓库中的默认分支，169
* BIND 服务器的默认配置，73
* 默认分隔符，55
* 默认网关
    * 添加，15, 136
    * 更改，18, 138
* 默认路径，176
* 默认端口
    * CUPS，67, 152
    * MySQL，82
    * VNC，78
* 默认路由，显示，15, 199
* default.target 单元，191
* 默认目标，显示，47
* `/etc/fstab` 文件中的 `defaults` 行，24, 192
* 分隔符，设置，81
* 访问控制列表的拒绝策略，149
* 依赖关系
    * 显示，21, 51, 186–187
    * 库，48, 130
    * 已载的模块，20
    * 加载，5
* `depmod` 命令
    * 依赖关系，20
    * 模块比较，35
* 已检测到的硬件列表，157
* `/dev/disk/by-id` 目录，24
* `/dev/disk/by-multipath` 目录，35
* `/dev/disk/by-path` 目录，25
* `/dev/disk/by-uuid` 目录，33
* `/dev` 文件系统，32
* `/dev/mapper` 目录，26, 71
* `/dev/null` 目录，81
* `/dev/nvme*` 目录，70
* `/dev/pty` 设备，115
* `/dev/sda1` 分区，8, 94
* `/dev/sdX` 设备，50, 128
* `/dev/tty` 设备，84
* 设备
    * 启动检查顺序，12
    * 集合，163
    * 显示名称，50, 187
    * 信息，74
    * `lsmod` 驱动，6
    * 伪终端，115
* `df` 命令
    * 磁盘利用率，19, 190
    * 节点，134
    * 报告，147
* DHCP
    * 配置，36
    * 租期，194
    * 服务器日志，71
* `dhcp.conf` 文件，194
* `diff` 命令，77
* `dig` 命令
    * 查询，16, 137
    * 服务器查询，17, 139
    * 区域传输，18, 193
* 数字目录
    * 复制，55
    * 创建，55
    * 查找，54, 134
    * 列出，167
    * 权限，153
    * 删除，54
    * 遍历，118
* 磁盘
    * 禁用，96
    * 账户，110
    * 日志，35
    * GRUB 配置，8
    * 准备，9
    * 内存，20, 191
    * SATA，50
    * USB 磁盘，129
    * 显卡，83
* `dmidecode` 命令，155
* `dnf` 命令，53
* DNS
    * 覆盖，18
    * 服务器设置，17, 137
    * SPF 记录，19, 140
    * 故障排除，140
* `dnssec-keygen` 命令，103
* `do` 关键字
    * for 循环，175
    * until 循环，180
* 美元符号 ($)





- `command execution`,166
- `command-line arguments`,177
- `domains`，信息，13
- `dominfo` 命令，13
- `done` 关键字
    - for 循环，175
    - until 循环，180
- `dot (.)` 文件，显示，117
- `dpkg` 命令
    - 软件包更改，52
    - 软件包信息，53, 132
- `dracut` 命令，21
- `drivers`
    - 显示，36
    - 网络接口，36
- `iptables` 的 `DROP` 目标，106
- `DTLS`（数据 agram 传输层安全），112
- `du` 命令
    - 人类读格式，34
    - 目录上的大文件，10, 134
    - 总结输出，157
- 双宿主网络，29
- `dumpe2fs` 命令，12, 23

## E
- 用于文件存在的 `-e` ，178
- `e2label` 命令，29
- `EC2` 实例，32
- `echo` 命令
    - 大括号扩展，164
    - 转发，107
    - 换行符，169
    - 路径，166
    - 变量显示，162
- `ECHO_REQUEST` 数据包，193
- ICMP 中的 echo 请求，147
- 回显脚本名称，165
- 编辑
    - `/etc/sudoers` 文件，100
    - 文件，114
- `EFI` 启动分区，5
- `efibootmgr` 命令，22
- 用于查找用户的 `egrep` 命令，56
- `elif` 关键字，181
- 电子邮件
    - 地址更改，170
    - 别名，66
    - 目的地，26, 108
    - 统计，68
- 邮件发送日志，97
- 紧急目标，197
- 空密码，106
- 加密设备，列出，23
- 加密
    - 身份验证密码，156
    - `dm-crypt` 命令，197
    - 组密码，65
- SELinux 中的强制模式（Enforcing mode），110
- 遍历主机数据库，17, 137
- `env` 命令
    - 自定义环境，162
    - 显示，132
    - 环境变量，167, 171
- 环境密钥，81
- 环境，打印，165
- 环境变量
    - 创建，81
    - 显示，132
    - `env` 命令，167
    - `HOME`，173
    - `PS1`，172
    - ，171
- 用于整数比较的 `-eq` 运算符，174
- 等号（`=`）
    - 字符串比较，165
    - 变量比较，176
- 错误修正
    - 自动，134
    - 交换分区，134
- 使用 `fsck` 命令修复错误，8, 191
- `esac` 序列，173
- 转义序列
    - 警报，174
    - 回车和换行，198
    - 引号，163
- `/etc/apparmor.d` 目录，112
- `/etc/apparmor.d/tunables` 目录，119
- `/etc/apt/sources.list` 文件，52, 131
- `/etc/auto.master` 文件，70
- `/etc/bash.bash_logout` 文件，171
- `/etc/cron.allow` 文件，71
- `/etc/cron.daily` 目录，62
- `/etc/cron.deny` 文件，96
- `/etc/crontab` 文件，63
- `/etc/crypttab` 文件，23
- `/etc/cups` 目录，66
- `/etc/default/grub` 文件，8
- `/etc/default/keyboard` 文件，152
- `/etc/dhcp.conf` 文件，36
- `/etc/exports` 文件，194
- `/etc/fail2ban` 目录，106
- `/etc/fstab` 信息，12, 192
- `/etc/mount` 命令，10
- `/etc/grub.cfg`，28
- `/etc/shadow` 文件，65
- `/etc/issue` 文件，101
- `/etc/issue.net` 文件，99
- `/etc/hosts` 文件，17, 137
- `/etc/hosts` 文件，16
- `/etc/inetd.conf` 文件，100
- `/etc/init.d` 目录，70
- `/etc/init.d` 脚本，46
- `/etc/inittab` 文件，49
- `/etc/nsswitch` 文件，110
- `/etc/pam.d` 目录，104
- `/etc/passwd` 文件，103, 55, 61, 54
- `/etc/pki` 目录，108
- `/etc/profile.d` 目录，80
- `/etc/rc.d` 目录，70
- `/etc/rc.local` 文件，79
- `/etc/rcS.d` 目录，80
- `/etc/resolv.conf` 文件，27, 17, 137, 18, 139
- `/etc/rsyslog.conf` 文件，120
- `/etc/securetty` 文件，111





* `/etc/security/limits.conf` 文件
    * 进程限制, 141
    * 同时登录, 142
* `/etc/services` 文件, 98
* `/etc/shadow` 文件
    * 加密密码, 156
    * 密码更改日期, 69
    * 密码、用户名和 UUID 中的, 64
* `/etc/skel` 目录, 60, 189
* `/etc/ssh_known_hosts` 文件, 100
* `/etc/sshd/sshd.conf` 文件, 100
* `/etc/sudoers` 文件
    * 编辑, 100
    * 邮件目标, 108
    * 密码, 99
* `/etc/sysconfig/network` 文件, 33
* `/etc/sysconfig/network-scripts/` 目录, 29
* `/etc/sysctl.conf` 文件, 21
* `/etc/timezone` 文件, 13
* `/etc/udev` 目录, 46, 186
* `/etc/ufw` 目录, 120
* `/etc/X11` 目录, 82
* `/etc/X11/xorg.conf` 文件, 60
* `/etc/yum.conf.d` 目录, 51, 130
* `/etc/yum.conf` 文件, 52, 131
* `/etc/yum.repos.d` 目录, 72
* 以太网桥接, 创建, 36
* `ethtool` 命令, 36
* 事件, 重放, 78
* `git` 命令中的排除模式, 199
* `ExecStart` , 47
* 可执行文件
    * 位置, 58
    * 权限, 95
* 脚本的执行位, 199
* 执行
    * 命令. *参见*命令执行
    * 脚本, 162, 164
    * 启动时执行服务, 79
* 文件的存在性, 135, 178, 198
* 使用 `touch` 命令处理现有文件, 55
* 退出码
    * 一般错误, 180
    * 成功, 164
* 变量展开, 183
* 账户过期, 69, 96, 190
* `export` 命令
    * 环境变量, 195
    * 库, 130
    * 变量, 166, 195
* ext2 文件系统, 9
* ext3 文件系统
    * 对比 ext2 文件系统, 9
    * 调整大小, 31
* 扩展硬件信息, 关于, 155
* 扩展
    * 确定, 170
    * 脚本执行, 164
* 从备份中提取文件, 117

## F
* RAID 列的 `fail` 选项, 156
* fail2ban 系统
    * 配置, 106
    * 日志文件位置, 107
* 失败登录尝试
    * 账户锁定, 115
    * 列出, 112
* 集群服务器的 FAT 文件系统, 79
* `fdisk` 命令, 9
* `fg` 命令, 56
* FHS (文件系统层次结构标准)
    * 可移动媒体的挂载点, 10
    * 站点特定数据, 9
* `fi` 关键字, 169
* 光纤 HBA, 149
* `file` 命令, 170
* 文件扩展名
    * 确定, 170
    * 脚本执行, 164
* 文件
    * 访问控制, 111
    * 向追加输出, 167
    * 属性, 154, 156
    * 备份, 198
    * 校验和, 118
    * 来自命令, 171
    * 提交, 180
    * 比较, 77
    * 内容, 72
    * 上下文, 120
    * 拷贝, 60, 85, 117, 189
    * 创建, 135
    * 编辑, 114
    * 存在性, 135, 178, 198
    * inode 节点, 58
    * 链接, 70
    * 列出, 54, 67
    * 匹配, 77
    * 修改, 103
    * 移动, 57
    * 输出到, 7
    * 覆盖, 55
    * 用户所有, 66
    * 所有权, 112, 118, 152
    * 权限, 112
    * 队列, 67
    * 相对路径, 30
    * 删除, 84, 102
    * 搜索, 141
    * 大小, 154, 193
    * 符号链接, 58
    * 传输, 116
    * 解压缩, 72, 94, 102
* 文件系统层次结构标准 (FHS)
    * 可移动媒体的挂载点, 10
    * 站点特定数据, 9
* 文件系统
    * 检查, 12
    * 集群服务器, 79
    * 关于信息, 155
    * 标签, 29
    * 重新挂载, 11
    * NFS 共享, 94
    * 大小, 31
    * 类型设置, 23
    * 卸载, 73
    * 不可访问, 27
    * 验证, 24
* `find` 命令
    * 目录, 54
    * 文件, 141
    * 用户所有, 66
    * inode 节点, 59
    * 修改过的文件, 57
    * 用户调用 `sudo` 命令, 57
* 查找僵尸进程, 157
* `firewall-cmd` 命令, 116
* `firewalld` 区域用于, 110
* 防火墙
    * LDAP, 196
    * Netfilter, 117
    * NTP, 108
    * SNMP 流量, 68
* for 循环
    * 列表迭代, 167, 181
    * 标记, 175
* 前台, 将命令置前台, 56
* 日期和时间格式, 13, 175
* 格式化打印, 84
* 转发, 启用, 107
* `fprint` 软件包, 114
* `free` 命令用于内存使用, 133, 150, 190
* `fsck` 命令




* 清理的文件系统，143
* 磁盘统计信息，146
* 错误修复，8, 191
* 文件系统检查，12
* 节点 (inodes)，134
* 跳过 root 检查，33
* `fstrim` 命令，25, 192
* FTP，从...启动，28
* 函数
* 添加，163
* 登录时可用，60
* 示例，196
* 括号用于，173

## G
* 用于路由表的 `G` 标志，140
* 默认关，默认
* 添加，15, 136
* 修改，18, 138
* `gdisk` 命令
* GUID 分区表，111
* 分区名称，12
* 通用错误，退出码，180
* `getenforce` 命令，109
* `getent` 命令
* hosts 数据库，17, 137
* 用户，96
* `getfacl` 命令，111
* `getsebool` 命令，113
* GIDs 和 UIDs，64
* `git checkout` 命令，166, 182
* `git clone` 命令，195
* `git commit` 命令，180
* `git config` 命令
* 配置参数，179
* 邮箱地址，170
* `GIT_DIR` 环境变量，176
* 用于存储元数据的 `.git` 目录，182
* `git log` 命令，168, 174
* `git ls-files` 命令，199
* `git merge` 命令，176
* `git pull` 命令
* 位置参数，180
* 共享仓库，180
* `git push` 命令，168
* `git remote show origin` 命令，177
* `git status` 命令，169
* `.gitignore` 文件，167
* GnuPG 密钥对，100
* `gpg` 命令
* 数字签名，119
* 密钥对，100
* 公钥环，101
* GPIO 接口，76
* 显卡配置信息，60
* `grep` 命令
* 文件内容，72
* 系统日志，71
* `groupadd` 命令，80
* `groupdel` 命令，65
* `groupmod` 命令，62
* 组
* 添加，80
* 加密密码信息，65
* IP 地址，150
* 查询信息，16
* 成员列表，155
* 名字，62
* 所有权，94–95
* 打印机，68
* 删除，65
* `su` 命令访问，113
* 用于用户，64
* `grub-install` 命令
* 备用目录，23
* MBR，8
* 安装在 MBR 的 GRUB，7–8
* GRUB Legacy 配置文件，8
* GRUB 菜单，5, 186
* `grub-mkconfig` 命令，8
* GRUB2 配置文件
* 新的，6
* 超时，7
* `grub2-install` 命令，7
* `grub2-mkconfig`
* 位置，27
* 输出到文件，7
* `grubx64.efi` 文件，23
* 客户登录，防止，135
* GUID 分区表信息，111
* `gunzip` 命令，72
* `.gz` 文件，72
* `gzip` 命令，103

## H
* 进程挂起信号，148
* HAProxy 400 响应，76
* 硬盘，检测，128
* 准备工作，9
* 硬链接，58
* 硬件配置，155
* 列出，157
* 硬件时钟，设置，15
* UTC 时间，15
* 用于，14
* 用于 PKI 的算法，113
* `head` 命令，54, 56
* `HEAD` 位置，166
* `HISTFILE` 大小，195
* `history` 命令，171, 195
* 提交，168, 174
* 性能数据，1
* `hmac-md5` 算法，103
* `home` 目录，64
* chroot，103
* 复制，60
* 创建，63
* `HOME` 环境变量，176
* `host` 名字，17
* 授权名称，136
* 类类型，157
* `hostname` 字符，27
* 禁用，148
* 防止，153
* `hostnamectl` 设置，78
* `hosts` 缓存，100, 137
* 举举，111
* 不可用，146
* `hotplug` 设备，USB，47
* HTTP 405 状态，85
* `http_access` 指令，74
* HTTP，从...启动，28
* `hwclock` 硬件时钟设置，15
* UTC 时间，15
* 用于，14
* 虚拟机
* 连接，32
* 类型 1，34

## I
* `ibstat` 命令，148
* `ICMP` 回请求，147
* 接口，16, 136
* `iptables` 规则，107
* 端口，98
* `iconv` 命令，32
* `id` 命令，65
* `id_rsa` 文件，99
* `IDs`
* 进程，27, 132, 148
* SATA 磁盘，128
* 共享，114
* 用户名，80
* `if` 条件语句
* 结束字符，169
* 文件是否存在，135
* `ifconfig` 命令，136
* `iftop` 命令
* 主机名查找，153
* 接口设置，156




` block` 块是一个**索引**（关键词和页码的列表），而不是包含变量、函数或逻辑的散文文本。

根据您的指令，我应该对 `varName`、`funcName()` 和 `commands` 等技术元素进行格式化。由于索引主要由术语组成，我侧重于维护结构、清理列表，并在适用的情况下对命令进行格式化。

以下是您的索引文本的格式化版本：

[content]
* 网络使用，150
* 分区镜像，94, 118
* 用于主机命令的 `IN` 类，157
* 增量备份，114
* inet 协议
    * 默认，26
    * `ip` 命令，144
* InfiniBand 设备，信息，148
* 信息性消息，66
* 基础代码，162
* 基础架构自动化，165, 178
* 继承权限，111
* `init` 命令，46
* 初始化文件，无 shell 执行的情况下，60
* 初始化分区，7, 131
* inode 索引节点
    * 打印，58
    * 通过...搜索文件，59
* inodes
    * 字节到 inode 的比例，149
    * 分区，134
* 输入，用户，172
* `INPUT` 链策略，106
* Vi 编辑器的插入模式，57
* `insmod` 命令，21
* `install` 命令，make 命令目标，72
* 安装
    * 内核，20, 30
    * 软件包，48, 53, 129, 132
    * 虚拟机，33
* 整数，比较，174, 182
* 交互式登录，135
* NTP 服务器的交互模式，67
* 接口
    * 显示，145
    * ICMP 数据包，16
    * `iftop`,156
    * 信息，136
    * `netstat` 的显示，175
    * 树莓派，76
* 解释器位置，171
* 中断，监控，147
* 清单
    * 自动化基础架构，174
    * 设备集合，163
* 调用 Bash 壳，163
* IO，调度，150, 153
* `ioping` 命令
    * 延迟，151
    * 请求设置，158
    * 请求大小，153, 155
* `iostat` 命令
    * 非自愿等待场景，178
    * 兆字节显示，191
    * 分区信息，19, 142
* IP 地址
    * 组，150
    * NTP 服务器，66
    * 所有权，151
    * 私有，136
* `ip` 命令
    * 默认协议，26
    * 换行，145
    * 协议族，144
* `ip monitor` 命令，16, 137
* `ip route change` 命令
    * 随后的命令，19
    * 默认网关，18, 138
* `ip route flush cache` 命令，19, 140
* `iperf` 命令，147
* `ipset` 命令
    * 组，150
    * `iptables`,120
* `iptables`
    * ICMP 流量，107
    * `INPUT` 链，106
    * `ipset` 软件，120
    * 日志条限制，106
    * Netfilter，117
    * `PREROUTING` 链，105
    * 规则，105–107
    * 目标，106, 108
    * UFW 配置，120
* `iptables-save` 命令
    * 规则，105
    * 表名，121
* `iptraf` 命令，150
* IPv6 地址，16
* IRQ 分配，46, 186
* ISOLUX 启动程序，22
* `itop` 命令，147
* `iw` 命令，71
* `iwconfig` 命令，26, 83
* JAVA_PATH，195
* JavaScript (JSON) 格式，28
* 
    * 后台任务，133
    * 移除，63, 196
    * 调度
* `journalctl` 命令
    * 磁盘空间，136
    * 日志条，96, 121
    * 日志条，196
    * 反向输出，197
* `journal.conf` 文件，97
* `journaling` 在文件系统中
    * 启用，104
    * 令牌，121
    * 缓存，112
* Kerberos 认证，121
* Kerberos ，96
* 内核
    * 安装，30
    * 消息，96
    * 参数，148
    * udev，70
    * 升级，52, 131
    * 版本，69
* 内核-install 命令
* 内核模块
    * 自定义命令，30
    * 安装，20
    * 位置，28
* 内核环形缓冲区
    * 清理，71
    * 崩溃，28
    * 查看，5, 186
* gpg 中的密钥环，101
* 密钥和密钥对
    * Apache 服务器，83
    * 认证，190, 194
    * 证书机构，73
    * GnuPG，100
    * 布局，29
    * LUKS，101
    * 映射，152
    * Postfix TLS，105
    * 发送，100
    * SSH，98–99, 107, 118, 120, 194
    * `ssh-agent`,110
* kickstart
    * 和 anaconda，31
    * 启动，35
* `kill` 命令
    * BIND 重载，77
    * 进程，56–57, 148
* `killall` 命令，133
* 杀死进程，133, 200
* `klist` 命令，112
* `kmag` 命令，61

## L

* 文件系统的标签，29





- `LACP` 协议, 33
- `LANG` 环境变量, 14, 179
- 目录上的大文件, 10, 134
- 用于日志的最后命令, 68
- 用于失败登录尝试的 `lastb` 命令, 112
- 延迟
    - 诊断, 151
    - `ping` 命令, 147
- `LC_ALL` 环境变量, 14, 178
- `LC_MONETARY` 环境变量, 14, 181
- `LC_TIME` 环境变量, 13, 175
- LDAP
    - 认证, 122, 154
    - 端口, 122, 189, 196
- `ldconfig` 命令, 48, 129, 200
- `ldd` 命令, 48
- 租约, DHCP, 194
- 法律免责声明信息，抑制, 156
- `less` 命令, 58
- `/lib/systemd/system` 文件夹, 49
- 库
    - 依赖, 48, 130
    - 打印, 200
    - 共享, 48, 51, 129, 200
    - 存储, 130
- `LIBVIRT_DEBUG`, 31
- 用于调试日志的 libvirt, 31
- 限制
    - PAM, 122
    - 密码年龄, 121
    - 进程, 141
    - 同时登录, 142
    - 用户, 99
- 行, 打印, 54
- 链接文件, 70
- 链接缓存无线设备状态, 71
- 共享库的链接, 48, 129
- 用于配置参数的 `--list` 选项, 179
- `ln` 命令
    - 软链接, 58
    - 时区, 14
- 负载平均, 133, 142, 200
- 绑定场景下的负载均衡, 35
- 已加载模块，显示
    - 当前已加载的, 20
    - 内核, 5
- 加载模块及依赖项, 5
- 加密密码的本地认证, 156
- 本地客户端服务，启用, 18, 139
- 变量的本地命令, 165
- 本地服务器，守护进程运行, 149
- 本地时区, 13
- 本地变量，指示, 165
- 用于自定义日志的 local# facilities, 67
- 区域 (locale)
    - 货币, 181
    - 绕过翻译, 14, 179
    - 变量重配置, 14, 178
- `localectl` 命令, 29
- IPv6 中的 localhost, 16
- 用于数据库更新的 `locate` 命令, 59
- 锁定账户, 115
- 锁定基于密码的登录, 63
- 用于 iptables 的 `--log-prefix` 选项, 108
- 已登录用户, 68–69, 142
- 逻辑卷
    - 创建, 7, 131, 192
    - 目录, 71
    - 信息, 26
    - 逻辑创建顺序, 8
- 登录
    - 3D 加加速, 75
    - 控制台, 111
    - 环境, 101
    - 交互式, 135
    - 防止, 104, 141
    - 同时, 142
    - 用户信息, 73
- 注销
    - 在其执行的命令, 171
    - 退出后, 85
    - 用户, 177
- `log-prefix` 选项, 107
- `logrotate` 命令, 121
- `logrotate` 配置
    - 认证与授权, 115
    - 压缩, 97
    - 自定义, 67
    - 禁用, 35
    - 邮件, 179
    - 条目, 120
    - 条目限制, 106
    - 解析, 196
    - 日志, 97
    - 内核消息, 96
    - 最后命令, 68
    - 路径, 107
    - 输出自, 76
    - 输出到, 163
    - 数据包, 122
    - systemd 服务, 96
    - 监控, 94
- 日志
    - 循环, 166
    - 用于, 71
    - px, 28
- `lattr` 命令
    - 点文件, 54
    - 示例, 50
    - 过滤器, 67
    - 硬链接, 58
    - inode 节点号, 58
    - 所有者, 149
    - 分区, 128
    - 权限, 59
    - SELinux, 119
    - 符号链接, 186
- `lsblk` 命令
    - 引导分区, 72
    - 分区信息, 36
- `lsdev` 命令, 74
- `lshw` 命令, 157
- `lsmod` 命令
    - 设备驱动, 6
    - 已加载模块, 20
- `lsof` 命令, 141
- `lspci` 命令
    - 列出数字代码和设备名称, 50, 187
- `lsusb` 命令
    - 蓝牙设备, 85
    - USB 连接, 48
    - USB 设备, 46, 128
- `-lt` 运算符, 181
- `LUKS`
    - 加密, 197
    - 派生函数, 101
- `LUNs`
    - 来自光纤, 25
    - 路径, 25
- `lvcreate` 命令, 7, 131, 192
- `LVM`
    - 逻辑卷, 7, 131





* `partitions`（分区）, 7, 131
* `lvmdiskscan` 命令, 8, 132
* `lzma` 扩展, 94

# M

* MAC 地址
    * 新条目, 145
    * 删除, 144
* 机器类型设置, 78
* 放大功能, 61
* 用于 STDIN 消息的 `mail` 命令, 73
* 用于发送日志的 `mail` 选项, 97
* 邮件队列
    * 目录, 66
    * Postfix 服务器, 67
* 邮件服务器
    * 邮件别名, 66
    * 查询, 16, 137
* 邮件存储, 187
* `MAILADDR` 选项, 26
* `mailstats` 命令, 68
* `mailto` 选项, 108
* `make` 命令
    * 与之使用的命令和关系, 72
    * 目标, 72
* `make oldconfig` 命令, 69
* `Makefile` 名称, 72
* 主引导记录 (MBR)
    * 在 MBR 上 GRUB, 7–8
    * 分区信息, 22
    * 主分区, 6
* 仓库中的主分支, 169
* 匹配文件, 177
* MATE 桌面环境, 76
* max-lease-time 选项, 194
* 最大挂载次数, 199
* maxlogins 选项, 142
* MBR (主引导记录)
    * 在 MBR 上 GRUB, 7–8
    * 分区信息, 22
    * 主分区, 6
* `mdadm` 命令
    * 阵列, 25, 192
    * 邮件, 26
    * 轮询间隔, 145
    * RAID 阵列, 26
* `/media` 文件, 10
* 组成员列表, 155
* 内存使用情况
    * 显示, 146
    * `free` 命令, 133, 150, 190
    * 进程, 157, 200
* 用于仓库的 `merge` 命令, 164
* 合并冲突，回滚, 176
* 消息
    * 捕获, 196
    * 信息性, 66
    * 内核日志, 96
    * netlink, 16, 137
    * 仓库, 168
    * 面向, 102
    * 警告, 103
    * 欢迎, 61
* 仓库中的元数据, 182
* 调音器音, 82
* `mkdir` 命令
    * 目录, 55
    * 仓库, 163
* `mke2fs` 命令
    * 坏块, 147
    * 修改, 149
    * 文件系统类型, 23
* `mkfs.btrfs` 命令, 11
* `mkinitrd` 命令, 20, 191
* `mkswap` 命令, 134, 192
* 修改过的文件，查找, 57
* 修改文件, 103
* `modinfo` 命令, 20
* `modprobe` 命令, 5
    * 依赖关系, 21, 186
    * 内核模块, 20
    * 删除模块, 21
* 模块
    * 黑名单信息, 21
    * 对比, 35
    * 依赖关系, 21, 186
    * 插入, 21
    * 加载, 5
    * 删除, 21
    * 卸载, 6, 35
* 监控
    * 中断使用情况, 147
    * 性能, 69
    * 进程, 188
* 监控器
    * 配置, 60, 81
    * X, 81
* `more` 命令, 84
* `mount` 命令
    * `/etc/fstab`, 9
    * 挂载过程, 199
    * 分区, 22
    * USB 设备, 12
    * USB 磁盘, 6
    * 最大挂载次数, 199
    * 挂载可移动介质, 10
* 挂载的文件系统
    * 显示, 32
    * `/etc/mtab`, 10
    * 移动, 57
    * 位置, 180
* `mtr` 命令, 145
* `multath` 命令, 25, 189
* 多路命令, 167, 182
* `mv` 命令
    * 文件, 55
    * 文本, 57
* MX 记录, 82
# N

* nagios 软件, 69
* 网络适配器的 NAME 选项, 82
* 名称
    * 映射, 145
    * 路由, 144
* 名称服务器
    * 端口, 97
    * 查询, 16
* `named.conf`, 73
* 名称
    * 修改, 65
    * 组, 62
    * 网络适配器, 82
    * 分区, 12
* 名称服务器行, 17
* `Nano` 编辑器, 83
* `NAT` 与, 30
* `nc` 命令, 139
* `net` 命令, 104
* NetBIOS 请求, 74
* `netcat` 命令, 139
* Netfilter 防火墙, 117
* netlink 消息, 16, 137
* `netstat` 命令
    * 当前默认路由, 15, 199
    * 主机查找, 148
    * 接口信息, 175
    * 路由表, 157
    * 服务和套字, 17, 138
* 网络适配器名称, 82
* 网络绑定, 30
* 网络接口，驱动, 36
* Network 管理器, 150
* 网络
    * 组件身份验证, 117
    * 配置, 29
    * 配置保存, 33
    * 吞吐量测量, 147
    * 使用显示, 150
* 新文件的权限, 95
* `newaliases` 命令, 66
* 换行符
    * `echo` 命令, 169
    * 转义字符, 198
    * 删除, 145





* `nice` 命令, 133
* `nmap` 命令
    * 域名解析, 145
    * 开放端口, 141–142
    * Xmas 扫描, 146
* `nmbd` 守护进程, 74
* `nmcli` 命令, 150
* 共享仓库的 `--no-commit` 选项, 180
* 日志的 `nocompress` 选项, 97
* `nohup` 命令, 85
* 非交互模式
    * 在...中执行命令, 99
    * `sudo` 命令, 119
* 非交换分区, 132
* `NOPASSWD` 选项, 99
* 不使用初始化文件的 shell 执行的 `--norc` 选项, 60
* `nslookup` 命令, 36, 154
* NTP
    * 交互模式, 67
    * IP 地址, 66
    * 端口, 108
* `ntpq` 命令, 67
* 数字代码, 显示, 50, 187
* `NXDOMAIN` 消息, 140

## O

* Vi 编辑器中的 `o` 命令, 57
* 权限的八进制表示, 120
* 开放端口, 扫描, 141–142
* 远程桌面协议的开源包, 82
* OpenSSH (注：原文应为 OpenSSH，此处保留原文)
    * 空密码, 106
    * 允许登录的, 108
    * SSH 客户端登录, 74
* `openssl` 命令
    * 证书授权服务器, 73
    * 证书签名请求 (CSR), 77
* OpenVPN
    * 网络访问, 74
    * 端口, 106
* Orca 屏幕阅读器, 61
* 排排
    * 无代理基础设施, 183
    * 代理, 164, 198
    * Ansible 包, 162
* 仓库的 `--origin` 选项, 177
* 输出
    * 转义字符, 163
    * 输出到日志文件, 163
    * 日志记录, 76
    * 重定向, 7, 81, 170
    * 变量, 177
* 输出文件设置, 80
* OVA 文件, 34
* 覆盖文件, 55
* OVF 模板, 29
* 所有权
    * 修改, 95, 118
    * 删除的账户, 66
    * 显示, 112, 149
    * 组, 94–95
    * 继承, 152
    * IP 地址, 151

## P

* 包
    * 可用的, 53
    * 缓存, 52
    * 更改, 52
    * 信息, 53, 132
    * 安装, 48, 53, 129, 132
    * 仓库, 52, 72, 131
    * 搜索, 51, 188
    * .tgz 文件扩展名, 53
    * 更新, 130
* 数据包
    * ICMP, 16
    * 日志记录, 122
    * 快照, 146
* 分页器, more 命令, 84
* `pam_cracklib.so` 模块, 105
* `pam_limits.so` 模块, 122
* `pam_listfiles.so` 模块, 122
* `pam_nologin.so` 模块, 104
* `pam_tally2` 模块, 115
* `pam_unix.so` 模块, 105
* 参数, 位的, 180
* 用于函数的括号 `()`, 173
* 解析日志文件条, 196
* `parted` 命令, 12
* `/partition/` 目录, 50, 187
* 分区表, 更新, 151
* 分区
    * 修改, 12
    * 显示, 128
    * EFI 系统, 5
    * GRUB 配置文件, 6
    * 识别, 94, 118
    * 信息, 34, 36
    * 初始化, 131
    * Inodes, 134
    * 列出, 36
    * LUN, 25
    * 非交换, 132
    * RAID 阵列, 24
    * 交换, 143, 192
    * UUID, 1
* `passwd` 命令, 151
* 基于密码的, 63
* 密码
    * 年龄, 21
    * 引导器, 4
    * 空, 106
    * 文件, 64
    * 本地认证, 156
    * PAM, 105
    * 恢复, 128
    * 大小, 99
    * 强度, 105
* `paste` 命令, 81
* 用于备份的 `patch` 命令, 198
    * 空格, 197
    * 默认, 176
    * 显示, 166
    * 文件, 30
* `PBKDF2` 函数, 101
* 用于流量的 `pcap` 格式, 151
* `pci-0000` 文件, 25
* `PEM` 格式, 105
* 性能
    * CPU, 191
    * 绘图, 143
    * 历史数据, 151
    * 监控, 69
    * 轮询间隔, 145
* 权限
    * bash 脚本, 154
    * 目录, 153
    * 显示, 94
    * 文件, 112
    * 继承, 111
    * 新文件, 95
    * 八进制, 120
    * `rsync` 命令, 198
    * suid 位, 95
    * 软链接, 59
    * `tar` 命令, 197
    * 写入, 154
* SELinux 中的 `Permissive` 模式, 109
* `PermitEmptyPasswords` 选项, 106
* `PermitRootLogin` 选项, 74
* 持久化卷, 29
* `pgrep` 命令, 132
* 物理卷





# 索引

* 信息，144
* 逻辑卷来自，8
* 搜索，8, 132
* `pidof sshd` 命令，148
* `ping` 命令
    * 绕过路由表，198
    * `ECHO_REQUEST` 数据包，193
    * 模拟，18, 139
    * ICMP 回显请求，147
    * ICMP 数据包，136
    * 延迟，147
    * 数据包策略，146
    * 查询，16
* PKI 哈希算法，113
* `pkill` 命令，153
* 可插式认证模块 (PAM)
    * 授权与认证，122
    * 配置，104
    * 登录尝试失败，115
    * 预防登录，104
    * 密码认证，105
    * 密码强度，105
    * 策略，149
    * 强制，109
    * 用户限制，122
* 策略
    * `INPUT` 链，106
    * PAM，149
    * SELinux 配置，109
* 性能轮询间隔，145
* SSH 中的端口转发，76
* 端口到协议的转换，98
* 端口
    * 配置，97
    * CUPS 管理 Web 界面，67
    * CUPS 打印进程，152
    * 光纤通道 HBA，149
    * 防火墙，68
    * ICMP，98
    * LDAP，122, 189, 196
    * MySQL，82
    * 名称服务器，97
    * NTP，108
    * 开放，141–142
    * OpenVPN，106
    * slapd 进程，104
    * SMTP 流量，97
    * Squid，104
    * SSH，122, 138
    * telnet，119
    * VNC，78
    * 用端口，121
* 位置参数，移动，180
* Postfix
    * 邮件队列，67
    * TLS 配置格式，105
* `postqueue` 命令，67
* 井号 (#)
    * 命令行参数，177
    * 脚本中的注释，164
* `PREROUTING` 链，105
* 主分区，6
* `printenv` 命令，165
* 打印机组，68
* `printf` 命令，84
* 打印
    * `awk` 命令，195
    * 已完成的打印作业，67
    * 环境，165
    * 格式化，84
    * inode 索引节点，58
    * 库，200
    * 行，54
    * 列表，172
    * 端口，152
    * 打印队列，67
* 优先级
    * MX 记录，193
    * 进程，133, 148
* 私有地址，15, 136
* 私钥
    * Apache 服务器，83
    * 证书授权服务器，73
    * SSH，18, 120
    * `ssh-agent`,110
    * 权限，95
    * `/proc/bus/usb` 目录，50
    * `/proc` 文件系统，47
    * `/proc/meminfo` 文件，146
    * `/proc/mounts` 文件，32
    * `/proc/partitions` 文件，34
    * 过程自动化，178
    * 进程，158
    * AppArmor，113
    * hangups，148
    * ID，27, 132, 148
    * 杀死，133, 200
    * 限制，141
    * 注出后，85
    * 内存使用，157, 200
    * 监控，188
    * 优先级，133, 148
    * 重启，57, 133
    * 运行，158
    * 停止，56
    * 终端，84
    * 可中断睡眠，152
* 用于时区的 `.profile` 文件，14, 181
* 配置文件
    * AppArmor，15, 19
    * 目录，112
    * 进度指示，10, 188
    * `ps auwx` 命令，118
    * `ps aux` 命令，112
* `ps` 命令
    * 内存使用，157, 200
    * SELinux 上文，115
    * 可中断睡眠，152
    * 僵尸进程，157
* `PS1` 环境变量，172
* 伪终端设备，115
* 用于 gpg 的公钥环，101
* SSH 中的公钥，98, 107, 120
* `pubring.gpg` 文件，101
* 用于存储的 `pull` 命令，162
* 清理缓存，33
* 用于网络访问的 `push` 命令，74
* `pvcreate` 命令，7, 131
* `pvdisplay` 命令，25, 144
* `pvscan` 命令，144
* PXE 启动，23
* `pxelinux.0` 文件，23

# Q
* 查询目的地，更改，154
* 使用 `less` 命令的问号 (?)，58
* `quotacheck` 命令
    * 文件创建，135
    * 用户配额，59
* 配额
    * 启用，135
    * 用量显示，59

# R
* `\r\n` 转义字符，198
* RAID 阵
    * 适配器检测，153
    * `mdadm` 命令，26
    * 分区，24
    * 从中移除磁盘，156
* RAM 磁盘，20–21, 191
* 树莓派接口，76
* 原始设备，30
* `rc` 文件运行级别，70
* 用于用户输入的 `read` 命令，172
* `read` I/O 请求，显示，34





* 显示，170
* `readonly` 命令，170
* 重启，46
* 重新配置 `locale variables`，178
* 恢复密码，128
* `chmod` 命令的递归更改，169
* 重定向
    * 重到日志文件，163
    * 输出，7, 81, 170
    * `STDERR`，56, 84, 170, 179
    * `STDIN`，79, 82, 182, 199
    * `STDOUT`，56, 84, 103, 182
* 时区区域，13, 189
* `iptables` 的 `REJECT` 目标，106
* 相对路径，30
* 重新加载 `BIND`，77
* 远程桌面协议，82
* 远程名称，获取，177
* 重新挂载文件系统，11
* 可移动介质的挂载点，10
* 
    * 块，25, 192
    * cron 任务，196
    * 目录，54
    * 环境变量，171
    * 文件，84, 102
    * 组，65
    * 任务，63
    * MAC 地址，144
    * 模块，21
    * 换行符，145
    * 用户，62
* `renice` 命令，148
* 重放事件，78
* 报告规模，147
* 存储
    * 更改，164
    * 克隆，177, 195
    * 复制，169
    * 创建，163
    * 默认分支，169
    * 文件版本，167
    * 消息，168
    * 元数据，182
    * 软件包，131
    * 获取，165
    * 从...获取对象，162
    * 共享，180
    * URL，72
    * `Yum`，130
* `repquota` 命令，59
* 请求
    * 数量，158
    * 尺寸，153, 155
* 预留块，显示，12
* `resize2fs` 命令，31
* 调整文件系统大小，31
* 重启
    * Apache 服务器，75
    * `CUPS`，68
    * 进程，57, 133
* `restorecon` 命令，114
* `rm` 命令，54
* `rmmod` 命令，6, 35
* `rndc` 命令
    * 认证，103
    * `BIND` 服务器，79
* 回滚合并，176
* root 用户
    * 控制台登录，111
    * SSH 登录，16
    * UIDs，109
* `route add`
    * DNS 服务器，17, 138
    * 网关，136
    * 流量，18
* `route` 命令
    * 标志，19
    * 解析，144
* 路由
    * 添加，17, 138
    * 默认，191, 199
* 路由表
    * 跳过，198
    * 显示，157
    * 标志，140
* `rpm` 命令
    * 更改的文件，51, 188
    * 详细输出，51, 187
* `rpm` 软件包位置，52, 131
* `rpm2cp` 输出，48
* `RSA` 哈希算法，13
* `rsync` 命令
    * 归档模式，71
    * 修改的文件，103
    * 移除，102
    * 文件尺寸，193
    * 权限，108, 198
    * 同步进程，120
* `rsyslog` 命令
    * `iptables` 规则，105
    * 重新加载，75
* `runlevel` 命令
    * 显示，49, 47
    * 文件，70
    * 设置，79
    * 单用户模式，46, 190
* 客人登录的 `SeatDefaults`，135
* `SCSI` 设备
    * 主机适配器扫描，156
    * 每总线支持，49, 129
* 本地客户端服务的 `search` 行，18, 139
* 搜索
    * 文件，141–142
    * 软件包缓存，52, 131
    * 软件包，51, 188
    * 物理卷，8, 132
* 安全公告，116
* `sed` 命令，53
* `SELinux`
    * 拒绝访问，155





- 布尔值列表，113
- 配置策略，109
- 上上下文，113, 115, 119, 152
- 强制模式 (Enforcing mode)，110
- 允许模式 (Permissive mode)，109
- `SELINUXTYPE` 选项，109
- 分号 (;)
    - case 语句，178
    - 命令链链，77, 174
- `seq` 命令，172
- 串行 ATA (SATA) 磁盘
    - BIOS，194
    - 标识符，50, 128
- 用于查询目的地的服务器命令，36, 154
- 服务器
    - 容器，75
    - 查询，17
    - 站点特定数据，94
- 服务账户 UID，155
- `service apache2 restart` 命令，75
- `service reload` 命令，81
- `service status` 命令，77
- 服务单元，列表，50, 187
- 服务
    - 启动时间，76
    - 显示，17, 47, 84, 100, 138
    - 启动时执行，79
    - 已加载，49, 187
    - 脚本，46
    - 关闭，78
    - 停止，69
- `sestatus` 命令，120
- 用于输出重定向的 `set` 命令，170
- `setenforce` 命令，110
- `setsebool` 命令，111
- SFTP
    - 文件传输，116
    - kickstart 启动，35
- `sha1sum` 实用程序，118
- SHA256withRSA 选项，113
- 共享 ID，114
- 共享库
    - 链接与缓存，48, 129, 200
    - 存储，51
- 共享仓库的更改，180
- 用于解释器位置的 shebang 行，171
- 不带初始化文件执行的 shell，60
- 用于位置参数的 `shift` 命令，180
- Shift 键
    - GRUB 菜单，5, 186
    - 粘滞键 (sticky keys)，61
- `shim.efi` 启动加载器，22–23
- 用于 UEFI 的 shims，23
- 关闭服务，78
- `SIGKILL` 信号，157
- `SIGTERM` 信号，200
- 同时登录限制，142
- 单用户模式
    - 启动，5
    - 密码，128
    - 运行级别，46, 190
    - 设置，49
- 站点特定数据
    - FHS，9
    - 服务器，94
- 大小
    - `/boot` 分区，7
    - 储储，24
    - 文件，154, 193
    - 文件系统，31
    - 日志日志，97
    - 分区，12
    - 请求，155
- 内存使用的大小列，157
- `slapd.conf` 文件，122
- `slapd` 守护进程，104
- SMTP 流量端口，97
- 数据包快照，146
- SNMP 服务器防火墙端口，68
- 套接字显示，17, 26, 138, 192
-get
    - 更新，129
    - 版本，170
- 双因素认证中的软件令牌，110
- 用于唯一项目的 `sort` 命令，57
- `sort` 命令中的排序顺序，143
- `source` 代码的提交，168
- `source` 命令
    - 函数，163
    - 脚本执行，171
    - 变量，163, 195
- SSH 中启动的 SPF 记录，19, 140
- SSH 远程访问，79
- SQL 命令，168
- `while` 循环，177
- Squid 访问，73, 104
- `/srv` 目录，94
- `ss` 命令，27, 192
- SSD 磁盘，70
- SSH 基础设施，183, 190, 197
- SSH 身份验证，111
- SSH 密钥，41, 98, 120
- SSH 登录，76
- SSH 端口，122, 138
- SSH 私钥，118
- SSH 用户，74, 116
- SSH 启动的窗口，60
- SSH 同步进程，103
- ufw 流量，116
- `ssh-add` 命令，110
- `ssh-agent` 命令，110
- `ssh.conf` 文件，109
- `ssh-copy-id` 命令，107
- `ssh-keygen` 命令，98, 122, 194
- `sshd.conf` 文件，109
- `sshd_config` 文件，116
- SSL
    - 证书机构服务器，73
    - 配置，108
    - 私钥，83
    - VPN 客户端，113
- `SSLCertificateKeyFile` 指令
    - Apache 服务器，83
    - 配置，104
- `SSLEngine` 选项，104
- 权威信息起始，18, 139
- udev 设备启动命令，80
- `STDERR` 重定向，56, 84, 170, 179
- `STDIN`
    - mail 命令，73
    - 重定向，79, 82, 182, 199
- `STDOUT` 输出输出到，78





- 重定向，56, 84, 103, 182
- `rpm2cpio`,48
- 非自愿等待场景下的窃取列（steal column），178
- 粘滞位（sticky bits），启用，95
- 粘滞键（sticky keys），启用，61
- 停止
    - 守护进程，81
    - 进程，56
    - 服务，69, 78
- 存储
    - 二进制大对象（blob），31
    - 主机缓存，100
    - 库，130
    - 邮件，187
    - 网络配置，33
- 存储区域网络 (SANs)，9
- 字符串，比较，165
- `su` 命令
    - 访问限制，113
    - 登录环境，101
    - 非交互式话，99
- 在子 Shell 中执行命令，166
- 替换操作，53
- `sudo` 命令
    - 账户，96
    - 凭据，190
    - 非交互模式模式，119
    - 特定用户，99
- `sudoedit` 命令，114
- 用于权限的 suid 位，95
- 使用 `du` 命令的摘要输出，157
- 挂起守护进程，83
- 交换分区
    - 创建，192
    - 错误修正，134
    - 识别，6
    - 跳过，143
- 交换空间
    - 激活，155
    - 取消，143
    - 描述，130
    - 显示，133, 190
    - 相关信息，143
- `swapoff` 命令，143
- `swapon` 命令，143, 155
- 绑定链路聚合中的交换器支持，33
- 符号链接
    - 显示，186
    - 文件，28, 58
    - 权限，59
    - 全局标识符 (WWID)，24
- SSH 中的同步过程，103
- `/sys/block` 文件，153
- `/sys/class/fc_host` 目录
    - 光纤 HBA，149
    - 光纤的 WWN，71
- `/sys/class/scsi_host/hostN/scan` 文件，156
- `sysctl` 命令
    - 启动值，21
    - 内核，148
    - 参数，152
    - 设置显示，20, 200
- 用于信息消息 `syslog` 级别，66
- 用于硬盘检测的系统 BIOS，128
- 系统文件的更改，117
- DHCP 服务器的系统日志，71
- 系统用户，创建，65
- 全级 cron 文件，63
- 用于杀死进程的 `systemctl` 命令，200
- `systemctl daemon-reload` 命令，70
- `systemctl disable` 命令，69
- `systemctl enable` 命令，47
- `systemctl get-default` 命令，47
- `systemctl isolate` 命令，49
- `systemctl list-units` 命令，50
- `systemctl mask` 命令，84
- `systemctl restart` 命令，68
- `systemctl status` 命令，49, 77, 187
- `systemctl stop` 命令，81
- `systemd-analyze` 命令，76
- `systemd-journald` 服务，96
- systemd 系统
    - 配置更改，70
    - 配置文件，49
    - 环境变量，81
    - 日志，96
    - 要执行的程序，47
    - 服务单元，187
    - 目标，197
- systemd 时间，97
- SysV 脚本，46
- 标签
    - cut 命令，55
    - 水平，176
- TACACS+ 认证，117
- tail 命令
    - 行，54, 56
- tar 命令
    - 排除文件，102
    - 软件包，53
    - 权限，197
    - 创建，101
    - 解压缩文件，102
- 目标
    - iptables，106
    - 管理界面，67
    - SMTP 流量，97
    - 三次握手，98
- TCP SYN 数据包和开放端口，142
- `tcpdump`
    - 接口，145
    - 数据包快照，146
- `tcoute` 命令，151
- `telctl` 命令，49
- `telnet` 端口，119
- 终止进程，84
- `test` 参数，173
- `/tftp` 目录，23
- `.tgz` 扩展名，53
- 第三方日志代理，112
- 双因子认证中的令牌，110
- 用于主目录的波浪号 (`~`)，173
- 时区
    - 显示，13
    - 本地，13, 189
    - 区域，13, 189
    - 设置，14, 181
    - 全系统，14
- `timedatectl` 命令，13
- 超时
    - GRUB2 配置文件，7
    - 故障排除，151
- 时间
    - 命令执行时间，31
    - 格式，13, 175
    - 设置，14
- 时间戳，更改，55
- `TMOUT` 环境变量，177
- `top` 命令
    - 进程监控，188
    - 排序顺序，143
- `touch` 命令
    - 现有文件，55
    - 登录预防，141
- `tr` 命令，83
- `TraceEnable` 设置，85





* `tracepath` 命令, 139
* `traceroute` 命令
    * 实时更新, 145
    * 传入 TCP SYN 报包, 137
    * 对比 tracepath, 139
    * 不可达主机, 146
* 流量
    * 确定, 150
    * pcap 格式, 151
    * 防止, 18, 139
* 传输文件, 116
* VPN 的传输模式, 115
* 目录遍历, 118
* 故障排除
    * 连接, 140
    * 第三方日志代理, 112
* `tshark` 命令, 151
* `tune2fs` 命令
    * 错误修正, 9, 134
    * 扩展选项, 25
    * 最大挂载计数, 199
    * 文件系统挂载次数, 10–11
* 二因素身份验证令牌, 110
* 1 型虚拟机监控程序, 34
* `type` 命令, 171
* `TZ` 行, 14, 181

## U
* Ubuntu 发行版 Unity 桌面, 80
* `udev` 设备
    * 配置, 46, 186
    * 网络适配器名称, 82
    * 启动命令, 80
* `udev` 事件, 70
* `udevadm control` 命令, 75
* `udevadm monitor` 命令, 70
* `udevadm trigger` 命令, 78
* OpenVPN 的 UDP, 106
* `$UDPListen` 选项, 97
* UEFI
    * 引导程序, 22
    * 密码, 114
    * 垫程序, 23
* `ufw allow` 命令, 116
* UFW 配置, 120
* UIDs
    * 身份验证服务器, 64
    * root 账户, 109
    * 服务账户, 155
* `ulimit` 命令
    * 文件, 154
    * 用户, 99
* `umask` 命令, 94
* `umount` 命令
    * 重新挂载文件系统, 11
    * 卸载文件系统, 73
    * 不可达的文件系统, 27
* `unalias` 命令, 178
* 未分配的磁盘空间, 30
* 解压文件
    * `.gz` 文件, 72
    * lzma 文件, 94
    * `tar` 命令, 102
* 不可中断睡眠进程状态, 152
* Unity 桌面, 80
* `unlink` 命令, 84
* 卸载模块, 6, 35
* 使用 `traceroute` 命令的不可达主机, 146
* `until` 循环
    * 开始与结束, 180
    * 对比 while, 182
* `update-grub` 命令, 6
* `updatedb` 命令, 59
* 更新
    * Debian 系统, 48
    * 内核, 52, 131
    * 包缓存, 52
    * 软件包, 130
    * 分区表, 151
    * 软件, 129
    * traceroute, 145
* 升级内核, 69
* 用于查看平均负载的 `uptime` 命令, 133, 200
* 软件包仓库的 URL, 72
* USB 设备
    * 蓝牙, 85
    * 连接点, 129
    * 连接, 48
    * 热插拔, 47
    * 列出, 46, 128, 186
    * 挂载, 6, 12
    * 存储, 50
* 用户账户
* `useradd` 命令
    * 禁用, 196
    * 分组, 64
    * 家目录, 63
    * 系统, 65
* `userdel` 命令
    * 期, 69
    * 家目录, 64
    * 登录密码, 63
    * 分组, 68
* `usermod` 命令
    * 修改, 65
    * ID, 80
    * 用户名, 65
* `usernames`, 54
* `users`
    * 自动注销, 177
    * 配置, 60
    * 可用性, 62
    * 任务, 96
    * 拥有, 66
    * 分组, 64
    * 信息, 75
    * 输入, 72
    * 限制, 99
    * 列出, 96
    * 登录, 141
    * 登录, 108
    * 登录, 73
    * 登录, 102
    * 分组, 68
    * 进程, 141
    * 配额, [135], 135
    * 可读, 61
    * 删除, 62
    * 系统, 65
* `/usr/lib/zones`, 110
* `/usr/lib/modules`, 28
* `/usr/share/zoneinfo`, [139], 189
* `usrquota` 命令, 135
* `UTC` 时间时钟, 15
* `UTF-8` 字节字节表示, [139], 189
* `UUIDs`
    * 获取, 33
    * 分区, 11

## V
* 值, 显示, 20
* `/var/log/kern.log` 文件, 28
* `/var/log/secure` 文件, 116
* `/var/qmail/queue` 目录, 66
* `/var/spool/cron/crontabs` 目录, 62
* `/var/tmp/abrt` 目录, 78
* `variables`
    * 添加, 163
    * 可用性, 195
    * 比较, 176
    * 声明, 166
    * 显示内容, 162
    * 环境。*参见* 环境变量
    * 扩展, 183
    * 本地, 165
    * 输出, 177
    * 只读, [170, 175], 175
    * 设置, 174
* 安装过程中的详细输出, [51, 187], 187
* `versions`
    * 内核, [52, 131], 131
    * 软件, 170





* `VFS` (虚拟文件系统), 31
* `vgscan` 命令, 144
* `Vi` 编辑
    * 插入模式, 57
    * 保存工作, 56
* 视频卡，确定, 83
* 视频设备 Spice 远程访问, 79
* 用于 Spice 远程访问的 `<video>` 节, 79
* `virsh` 命令
    * 域信息, 13
    * 虚拟机程序, 32
* `virt-install` 工具, 33
* 虚拟文件系统 (VFS), 31
* 虚拟机，安装, 33
* `<VirtualHost>` 指令, 77
* `visudo` 编辑器, 100
* `vmlinux`, 28
* `vmlinuz`, 28
* `vmstat` 命令
    * 块, 142
    * IO 等待统计, 200
* VNC
    * 默认基础端口, 78
    * 服务, 78
* 卷
    * 创建顺序, 8
    * 信息, 25, 144
    * 逻辑, 71, 131
    * 持久, 29
    * 搜索, 132
* VPNs
    * 基于 SSL 的客户端, 113
    * 传输模式, 115

## W
* 用于登录用户的 `w` 命令, 68–69, 142
* 用于 IO 等待时间的 `wa` 统计数据, 200
* 警告消息，抑制, 103
* 监控日志, 94
* `WAYLAND_DISPLAY` 环境变量, 74
* Wayland 会话, 74
* `wc` 命令, 54
* Web 服务器，启用, 59
* 欢迎消息，设置, 61
* 欢迎部分, 61
* 常用端口, 121
* `wget` 命令, 76
* 用于 `su` 命令访问的 wheel 组, 113
* `whereis` 命令, 58
* `which` 命令, 58
* while 循环
    * 描述, 166
    * 测试部分, 173, 181
    * 对比 until, 182
* 补丁文件中的空格, 197
* `who` 命令, 73
* `whoami` 命令, 80
* `whois` 命令
    * IP 地址所有权, 151
    * 法律免责声明信息, 156
* `/etc/hosts.allow` 文件中的通配符匹配, 101
* Windows，信息, 188
* 无线设备
    * 链接状态, 71
    * 参数, 26, 83
* 世界标识符 (WWIDs)
    * `/dev/disk/by-multipath` 目录, 35
    * 符号链接, 24
* `Vi` 编辑器中的 `:wq` 命令, 56
* 光纤通道的 WWN, 71

## X
* X 服务连接, 135
* X 会话，通过 SSH 连接, 61
* X11Forwarding 选项
    * SSH 连接, 61
    * X11 转发, 100
* `xfs_check` 命令, 24
* `xfs_growfs` 命令, 11
* `xfs_info` 命令, 11
* `xfs_metadump` 命令, 10, 188
* `xfsdump` 命令, 24
* `xfsrestore` 命令, 24
* `xhost` 命令, 135
* Xmas 扫描, 146
* OVF 模板的 XML 标准, 29
* `xorg.c` 文件, 82
* `xrdp` 包, 82
* `xwininfo` 命令, 188
* `xz` 命令, 94

## Y
* YAML 格式
    * EC2 实例, 32
    * `/etc/netplan` 目录, 34
    * 扩展, 179
* `.yml` 扩展, 179
* `yum deplist` 命令, 32
* `yum install` 命令, 48, 129
* `yum search` 命令
    * 包缓存, 52
    * 分区, 131
* 用于 RAID 列的卷, 24

## Z
* `zip` 命令, 118
* 僵尸进程，查找, 157
* firewalld 区域, 110, 140, 193
* `zypper info` 命令, 53

# 综合学习环境

注册即可获得免费访问在线学习环境和测试库，帮助您准备 CompTIA Linux+ 认证——购买本书即可获得！

在线测试库包含：

* 用于强化所学知识的**练习题**
* 用于测试知识的**额外模拟考试**

访问 [`www.wiley.com/go/sybextprep`](http://www.wiley.com/go/sybextprep) 注册并访问此学习工具。

## 注册并访问测试库

注册书籍并访问测试库请按照以下步骤操作：

1. 访问 `bit.ly/SybexTest`。
2. 从列表中选择您的书籍。
3. 完成所需的注册信息，包括回答安全验证以证明拥有书籍。您将收到一个 PIN 码。
4. 按照邮件中的说明操作，或访问 [`https://www.wiley.com/go/sybextprep`](https://www.wiley.com/go/sybextprep)。
5. 输入您收到的 PIN 码，并点击“激活 PIN”按钮。
6. 在创建账户或登录页面，输入您的用户名和密码，然后点击“登录”。将显示“感谢激活您的 PIN!”。如果您还没有账户，请创建一个新账户。
7. 点击“进入我的账户”按钮将新书籍添加到“我的产品”页面。

![](img/b03001.png)

# **WILEY 用户许可协议**

访问 [www.wiley.com/go/eula](http://www.wiley.com/go/eula) 获取 Wiley 电子书 EULA。

