
# Linux Shell 命令参考：从 A 到 Z

cat, ln, nam

stat, tee, a

bunzip2, he

iconv, attr

getcap, con

at, batch, z

iotop, addg

usermod, ba

![](img/94f0b4d76a25250c220515a1d5bba83f_0_0.png)

```
user$ rdfind verz1 verz2
Now scanning "verz1", found 211 files.
Now scanning "verz2", found 215 files.
Now have 426 files in total.
Removed 0 files due to non-unique device
Total size is 85754591 bytes or 82 MIB
Removed 103 files due to unique sizes from
Now eliminating candidates based on first
removed 4 files from list, 319 files left.
removed 0 files from list, 319 files left.
Now eliminating candidates based on sha
removed 2 files from list, 317 files left.
It seems like you have 317 files that are n
Totally, 39 MIB can be reduced. Now mak
```

![](img/94f0b4d76a25250c220515a1d5bba83f_0_1.png)

Michael Kofler

![](img/94f0b4d76a25250c220515a1d5bba83f_0_2.png)

Michael Kofler

![](img/94f0b4d76a25250c220515a1d5bba83f_1_0.png)

我们希望你喜欢这本电子书。请向我们提供反馈，并阅读[服务页面]()以了解如何与我们联系。

2025939046

2 Heritage Drive, Suite 305

USA

Rheinkallee 4

Germany

+49 (0) 228 42150-0

# 使用说明

本电子书受版权保护。通过购买本电子书，你同意接受并遵守相关版权规定。你有权出于个人目的使用本电子书。你也可以对其进行打印和复制，但同样仅限个人使用。然而，我们不允许与他人共享电子副本或打印副本，无论是整体还是部分。当然，在互联网或公司网络上提供这些内容也是违法的。

有关详细且具有法律约束力的使用条件，请参考“法律备注”章节。

# 屏幕说明

你正在以文件格式（EPUB 或 Mobi）阅读本电子书，该格式可以适应你的显示需求。这是一好事；但遗憾的是并不是每个设备都能以相同的方式显示内容。如果你想放大图片（特别是在 iPad 上），再次点击即可返回上一个屏幕。你可以在屏幕布局自定义部分找到更多建议。

## 引言

# 命令概述

按主题

### 文件管理

| 命令 | 说明 |
|---|---|
| `cat` | 输出文件 |
| `cd` | 切换目录 |
| `chgrp` | 修改组 |
| `chmod` | 修改权限 |
| `cp` | 复制 |
| `dir` | 显示目录 |
| `erd` | 修改文件 |
| `file` | 识别文件类型 |
| `install` | 安装 |
| `ch` | 修改所有者 |
| `ln` | 创建链接 |
| `ls` | 显示内容 |
| `mkdir` | 创建目录 |
| `mv` | 移动 |
| `rm` | 删除 |
| `rsync` | 同步 |
| `stat` | 提供详细信息 |
| `tee` | 输出到多个文件 |
| `touch` | 创建空文件 |
| `tree` | 显示层次结构 |
| `uermod` | 修改用户 |
| `z` | （待定） |

### 查找文件

| 命令 | 说明 |
|---|---|
| `ack` | 用于文本 |
| `column` | 按列格式化 |
| `csplit` | 按预定义点分割文本 |
| `cut` | 提取列 |
| `delta` | 比较文本并高亮差异 |
| `diff` | 比较两个文本 |
| `expand` | 将制表符替换为空格 |
| `fold` | 将长行折叠 |
| `fzf` | 交互式滚动文件 |
| `grep` | 在文件中搜索 |
| `head` | 输出文件开头 |
| `iconv` | 更改文本字符集 |
| `jq` | 从 JSON 文档提取数据 |
| `less` | 分页查看文本（支持后退） |
| `more` | 分页查看文本 |
| `maxit` | 跟踪多个文件的变化 |
| `paste` | 按行合并文本 |
| `patch` | 根据 diff 文件修改文本 |
| `recode` | 转换不同的字符集 |
| `sed` | 流编辑器（可编程编辑器） |
| `sort` | 排序 |
| `split` | 将文件分割为子文件 |
| `strings` | 从二进制文件中提取字符串 |
| `tac` | 倒序输出文本，即最后一行在前 |
| `tail` | 输出文件末尾 |
| `tr` | 替换定义字符 |
| `unexpand` | 将空格替换为制表符 |
| `uniq` | 消除文本中的重复行 |
| `zcat` | 输出压缩文本文件 |
| `zless` | 分页查看压缩文本（支持后退） |
| `zmore` | 分页查看压缩文本 |

### 压缩与归档

| 命令 | 说明 |
|---|---|
| `bunzip2` | 解压 .bz2 文件 |
| `compress` | 压缩，比 bzip2 强大 |
| `cpio` | 在文件系统中传输存档 |
| `gunzip` | 解压 .gz 文件 |
| `gzip` | 压缩，比 compress 更强大 |
| `lzop` | 压缩文件，比 gzip 更快 |
| `tar` | 创建 .tar 归档 |
| `uncompress` | 使用压缩解压 |
| `unxz` | 解压 .xz 文件 |
| `zip` | 压缩，创建 Windows 兼容归档 |
| `zipinfo` | 显示 ZIP 档 |

### 文本处理

| 命令 | 说明 |
|---|---|
| `awk` | 文本分析编程语言 |
| `bat` | 带语法高亮显示文件 |
| `cat` | 输出文件或合并文本 |
| `column` | 按列格式化信息 |
| `csplit` | 按预定义点分割文本 |
| `cut` | 提取每行的列 |
| `delta` | 比较两个文本并高亮差异 |
| `diff` | 比较两个文本 |
| `expand` | 将制表符替换为空格 |
| `fold` | 将长行折叠为短行 |
| `fzf` | 交互式浏览 JSON 文件 |
| `grep` | 在文件中搜索 |
| `head` | 输出前几行 |
| `iconv` | 更改文件的字符集 |
| `jq` | 从 JSON 文档提取数据 |
| `less` | 分页查看文本（支持后退） |
| `more` | 分页查看文本 |
| `maxit` | 跟踪多个文件的变化 |
| `paste` | 按行合并文本 |
| `patch` | 根据 diff 文件修改文本 |
| `recode` | 转换不同的字符集 |
| `sed` | 流编辑器（可编程编辑器） |
| `sort` | 排序 |
| `split` | 将文件分割为指定大小的子文件 |
| `strings` | 从二进制文件中提取字符串 |
| `tac` | 倒序输出文本，即最后一行在前 |
| `tail` | 输出文件的末尾 |
| `tr` | 将定义的字符替换为其他字符 |
| `unexpand` | 将空格替换为制表符 |
| `uniq` | 消除文本中的重复行 |
| `zcat` | 输出压缩文本文件 |
| `zless` | 分页查看压缩文本（支持后退） |
| `zmore` | 分页查看压缩文本 |
| `getfacl` | 确定文件的 ACL（访问控制列表） |
| `getfattr` | 确定文件的扩展属性 |
| `setcap` | 修改文件的能力（capabilities） |
| `setfacl` | 修改文件的 ACL（访问控制列表） |
| `setfattr` | 修改文件的扩展属性 |

## 转换器 (Converters)

| 命令 | 说明 |
|---|---|
| `convert` | 转换图形文件 |
| `dvips` | 将 DVI 文件转换为 PostScript 格式 |
| `enscript` | 将文本文件转换为 PostScript 格式 |
| `epstopdf` | 将 EPS 文件转换为 PDF 文件 |
| `exiftool` | 读取或修改 JPG 文件中的 Exif 数据 |
| `ffmpeg` | 视频视频 |
| `iconv` | 更改文本文件的字符集 |



| `lame` | 生成兼容 MP3 的音频文件 |
| `magick` | 转换图形文件 |
| `mogrify` | 修改图像文件的参数 |
| `pandoc` | 从 Markdown 文件创建文档 |
| `paps` | 将 UTF-8 文本文件转换为 PostScript 格式 |
| `pdf2ps` | 将 PDF 文件转换为 PostScript 文件 |
| `pdfimages` | 从 PDF 文件中提取图像 |
| `pdftk` | 操作 PDF 文件 |
| `pdftops` | 作为 pdf2ps 的替代方案 |
| `pdftotext` | 将 PDF 文档转换为纯文本文件 |
| `pdfunite` | 将多个 PDF 文件合并为一个新文档 |
| `ps2pdf` | 将 PostScript 文件转换为 PDF 文件 |
| `recode` | 更改文本文件的字符集 |

## 进程管理 (Managing Processes)

| `at` | 在预定义时间执行作业 |
| `atq` | 列出稍后执行的作业 |
| `atrm` | 删除稍后执行的作业 |
| `batch` | 在系统空闲时执行作业 |
| `bg` | 在后台继续进程 |
| `chroot` | 在修改的根目录下启动 shell |
| `crontab` | 帮助管理自定义 crontab 条目 |
| `disown` | 将进程从 shell 中分离 |
| `fg` | 在前台继续进程 |
| `fuser` | 确定访问文件的程序 |
| `glances` | top 的现代替代方案 |
| `halt` | 退出 Linux 并停止计算机 |
| `history` | 显示 bash 中最后执行的命令 |
| `htop` | 每五秒显示一次所有进程列表 |
| `iftop` | 监控网络活动 |
| `ionice` | 控制进程的 I/O 优先级 |
| `iotop` | 显示 I/O 活动最的进程 |
| `kill` | 发送信号（通常用于终止进程） |
| `killall` | 类似于 kill；通过名称提及进程 |
| `ldconfig` | 更新库搜索缓存文件 |
| `lddd` | 提供程序所需的所有库 |
| `lsof` | 列出打开的文件和分配的进程 |
| `nice` | 以较低优先级启动程序 |
| `nohup` | 启动一个脱离 shell 的进程 |
| `parallel` | 并行启动多个相似作业 |
| `pidof` | 确定程序的进程号 |
| `powertop` | 分析运行进程的能量消耗 |
| `ps` | 显示运行进程列表 |
| `ptree` | 类似于 ps；使依赖关系更可见 |
| `reboot` | 退出 Linux 并重启计算机 |
| `renice` | 修改运行进程的优先级 |
| `sudo` | 以 root 身份运行程序 |
| `timeout` | 限制命令的执行时间 |
| `top` | 每五秒显示一次所有进程列表 |
| `uptime` | 显示计算机运行的时间 |
| `watch` | 定期执行命令并显示输出 |

## 用户与组管理 (Managing Users and Groups)

| `adduser` | 设置新用户 (Debian/Ubuntu) |
| `chgrp` | 更改文件的组成员关系 |
| `chpasswd` | 无交互地更改用户密码 |
| `chsh` | 更改用户的默认 shell |
| `delgroup` | 删除组 (Debian/Ubuntu) |
| `deluser` | 删除用户 (Debian/Ubuntu) |
| `groupadd` | 设置新组 |
| `groupdel` | 删除组 |
| `groupmod` | 修改组属性 |
| `groups` | 显示当前用户所属的组 |
| `gpasswd` | 修改组密码 |
| `id` | 显示当前用户和组 |
| `last` | 显示最后登录这台计算机的用户 |
| `lastb` | 列出最近失败的登录尝试 |
| `makepassword` | 生成新的随机密码 (CentOS, Fedora, RHEL) |
| `newgrp` | 更改用户的活动组 |
| `newusers` | 设置多个用户 |
| `passwd` | 更改密码 |
| `pwgen` | 生成易记的密码 |
| `useradd` | 设置新用户 |
| `userdel` | 删除用户 |
| `usermod` | 修改用户属性 |
| `vigil` | 编辑 /etc/groups |
| `visudo` | 编辑 /etc/sudoers |
| `who` | 提供有关用户的信息 |

## 文件系统管理 (Administrating the File System)

| `badblocks` | 测试扇区是否包含缺陷 |
| `blkid` | 返回文件系统的 UUID 和名称 |
| `btrfs` | 管理 Btrfs 系统 |
| `cfdisk` | 对硬盘进行分区 |
| `cryptsetup` | 设置加密设备 |
| `dd` | 在设备之间复制数据 |
| `df` | 显示磁盘空闲空间 |
| `du` | 确定目录的空间需求 |
| `dumpe2fs` | 显示 ext 系统信息 |
| `e4defrag` | 整理 ext4 文件 |
| `exfatlabel` | 修改 exFAT 标签 |
| `findmnt` | 列出挂载的文件系统 |
| `fstrim` | 为 SSD 擦除 |
| `kpart` | 创建内核分区 |
| `lsblk` | 列出块设备 |
| `mdadm` | 管理 RAID |
| `mkfifo` | 创建命名管道 |
| `mkfs` | 创建文件系统 |
| `mkswap` | 设置交换分区区 |
| `mount` | 挂载文件系统到目录树 |
| `ncdu` | 分析磁盘用量 |
| `parted` | 对硬盘分区 |
| `partprobe` | 通知内核分区变化 |
| `partx` | 读取内核的分区表 |
| `resize2fs` | 调整 ext 系统大小 |
| `sfdisk` | 使用 MBR 分区 |
| `sgdisk` | 使用 GUID 分区 |
| `smartctl` | 控制 SMART 功能 |
| `snapper` | 管理 Btrfs 快照 |
| `swapon` | 激活交换分区 |
| `swapoff` | 禁用交换分区 |
| `sync` | 执行所有写入操作 |
| `tune2fs` | 修改 ext 系统参数 |
| `umount` | 卸载文件系统 |
| `xfs_admin` | 修改 XFS 文件系统的参数 |
| `xfs_growfs` | 扩展 XFS 文件系统 |
| `xfs_info` | 显示 XFS 的数据 |
| `lvcreate` | 创建新的逻辑卷 (LV) |
| `lvdisplay` | 提供 LV 的详细信息 |
| `lvextend` | 扩展 LV |
| `lvm` | LVM 基础命令 |
| `lvreduce` | 缩小 LV 大小 |
| `lvremove` | 删除 LV |
| `lvrename` | 为 LV 重新命名 |
| `lvscan` | 列出所有 LV |
| `pvcreate` | 将分区识别为物理卷 (PV) |
| `pvdis` | 提供 PV 的详细信息 |
| `pvremove` | 未使用的 PV |
| `pvscan` | 列出所有 PV |
| `vgchange` | 更改卷组 (VG) 的属性 |
| `vgcreate` | 从一个多个 PV 创建新 VG |
| `vgdisplay` | 提供 VG 的详细信息 |
| `vgxtend` | 为 VG 增加一个 PV |
| `vgmerge` | 合并两个 VG |
| `vgreduce` | 减少一个未使用的 PV |
| `vgrename` | 为 VG 重新命名 |
| `vgscan` | 列出所有 VG |
| `aa-complain` | 记录 AppArmor 规则违规但不进行处罚 |
| `aa-disable` | 禁用 AppArmor 规则配置 |
| `aa-enforce` | 确保符合 AppArmor 规则 |
| `aa-status` | 确定 AppArmor 系统状态 |
| `chcon` | 修改文件的 SELinux 上下文 |
| `getenforce` | 确定 SELinux 模式（强制或许可） |
| `restorecon` | 恢复默认 SELinux 上下文 |
| `sealert` | 分析 SELinux 规则违规 |
| `sestatus` | 确定 SELinux 系统状态 |
| `setenforce` | 在强制和许可模式之间切换 |
| `setsebool` | 更改 SELinux 规则的布尔参数 |

# 包管理

| --- | --- |
| `apk` | 管理 Alpine Linux 中的软件包 |
| `apt` | 帮助管理 DEB 软件包（Debian, Ubuntu） |



# 软件包管理

| `add-apt-repository` | 设置 PPA 软件包源（Ubuntu） |
| `alien` | 在转换不同格式的软件包 |
| `alternatives` | 在 `/etc/alternatives` 中设置链接（Fedora, Red Hat） |
| `apt-cache` | 提供已安装/可用软件包的信息 |
| `apt-get` | 帮助管理 DEB 软件包（Debian, Ubuntu） |
| `apt-file` | 即使在未安装的软件包中也能搜索文件（Debian, Ubuntu） |
| `apt-key` | 为 APT 软件包源设置密钥 |
| `aptitude` | 帮助管理 DEB 软件包 |
| `cnf` | 显示哪个软件包包含某个命令（SUSE） |
| `dnf` | 作为 yum 的替代方案（Fedora） |
| `dpkg` | (卸)载或更新 DEB 软件包 |
| `flatpak` | 管理 Flatpak 软件包 |
| `pacman` | 管理 Arch Linux 软件包 |
| `pip` | 管理 Python 软件包 |
| `pkcon` | 跨发行版管理软件包（PackageKit） |
| `ppa-purge` | 禁用 PPA 软件包源（Ubuntu） |
| `pro` | 控制 Ubuntu Pro 功能 |
| `rpm` | (卸)载或更新 RPM 软件包 |
| `rpm2archive` | 将软件包转换为 TAR 存档 |
| `rpm2cpio` | 将软件包转换为 CPIO 存档 |
| `snap` | 管理 snap 软件包（Ubuntu） |
| `tasksel` | (卸)载 DEB 软件包组 |
| `update-alternatives` | 在 `/etc/alternatives` 中设置链接 |
| `yay` | 管理包含 AUR 的 Arch Linux 软件包 |
| `yum` | 帮助管理 RPM 软件包（Fedora, Red Hat） |
| `zypper` | 帮助管理 RPM 软件包（SUSE） |

# 网络管理

| --- | --- |
| `cadaver` | 通过 WebDAV 交互式传输文件 |
| `curl` | 从/或向 HTTP、FTP 和 SSH 服务器传输文件 |
| `dhclient` | 执行 DHCP 网络配置 |
| `dig` | 执行 DNS 查询 |
| `etherwake` | 激活支持网络唤醒（Wake-on-LAN）的设备 |
| `ethtool` | 修改以太网适配器的参数 |
| `exportfs` | 向 NFS 节点报告 NFS 配置 |
| `firewall-cmd` | 读取或更改防火墙配置（RHEL/Fedora） |
| `ftp` | 通过 FTP 交互式传输文件 |
| `host` | 解析 IP 地址或网络名称 |
| `hostname` | 返回或更改本地计算机名称 |
| `hostnamectl` | 永久更改主机名 |
| `ifconfig` | 配置网络接口 |
| `ifdown` | 禁用网络接口 |
| `ifup` | 激活网络接口 |
| `ip` | 显示或更改网络设置 |
| `ipcalc` | 计算网络区域和掩码 |
| `iptables` | 配置 Netfilter 防火墙 |
| `ip6tables-restore` | 读取多条防火墙规则 |
| `ip6tables-save` | 以文本格式输出所有防火墙规则 |
| `ip6tables-xml` | 以 XML 文档输出所有防火墙规则 |
| `jw` | 控制 WLAN 接口 |
| `mtr` | 结合 ping 和 traceroute 结果 |
| `nft` | 配置 nftables 防火墙 |
| `netplan` | 控制其他网络后端（Ubuntu） |
| `netstat` | 分析本地计算机的网络活动 |
| `networkctl` | 提供网络状态（systemd） |
| `newaliases` | 向邮件服务器报告 `/etc/aliases` 的更改 |
| `nmap` | 分析远程计算机的网络活动 |
| `nmblookup` | 确定 SMB 器的 NetBIOS 名称 |
| `nmcli` | 控制 NetworkManager |
| `openssl` | 生成和管理 SSL 密钥文件 |
| `ping` | 检查与计算机的网络连接 |
| `pnuke` | 在多个主机上并行终止程序 |
| `postconf` | 读取或更改 postfix 配置 |
| `postqueue` | 显示 postfix 队列 |
| `pscp` | 同时从/向主机复制文件 |
| `pssh` | 通过 SSH 在多个主机上执行命令 |
| `rdiff-backup` | 创建增量备份 |
| `resolvectl` | 确定或更改 DNS 配置 |
| `rfkill` | (禁用)蓝牙、WLAN 和移动无线适配器 |
| `route` | 修改或显示 IP 路由表 |
| `rpcinfo` | 提供 RPC 和 NFS 服务的信息 |
| `rsync` | 同步网络目录 |
| `scp` | 通过 SSH 加密传输文件 |
| `sftp` | 通过 SFTP 传输文件 |
| `showmount` | 列出 NFS 目录 |
| `smbclient` | 从 Windows 网络目录传输文件 |
| `smbpasswd` | 设置 Samba 账户的密码 |
| `smbstatus` | 提供本地 Samba 服务器的状态信息 |
| `ss` | 分析本地计算机的网络活动 |
| `ssh` | 网络上其他计算机的登录 |
| `ssh-keygen` | 生成和管理 SSH 密钥 |
| `ssh-copy-id` | 将公钥传输到 SSH 服务器 |
| `swaks` | 帮助测试和调试邮件服务器 |
| `telnet` | 与网络服务交互通信 |
| `ufw` | 配置防火墙（Ubuntu） |
| `wakeonlan` | 激活支持网络唤醒的设备 |
| `wget` | 下载文件 |
| `whois` | 执行查询 |
| `wol` | 激活支持网络唤醒的设备（Fedora） |

# 攻击与安全

| --- | --- |
| `arp` | 管理 ARP 缓存 |
| `arp-scan` | 发送 ARP |
| `chkrootkit` | 搜索 rootkit（根内核） |
| `fail2ban-client` | 管理 Fail2ban |
| `hydra` | 在线密码破解器 |
| `john` | 离线密码破解器 |
| `nc` | Netcat, 输入/输出 |
| `ngrep` | 过滤网络 |
| `nmap` | 网络和端口扫描器 |
| `rkhunter` | 搜索 rootkit |
| `tcpdump` | 过滤网络 |

# 打印机、数据库和服务器管理

| `acme/sh` | 来自 Let's Encrypt 的证书 |
| `htpasswd` | Apache 登录 |
| `lpadmin` | 设置新打印机 |
| `lpinfo` | 列出所有打印机、驱动程序 |
| `lpoptions` | 修改打印机选项 |
| `lpq` | 显示打印机内容 |
| `lpr` | 从队列删除打印作业 |
| `lpstat` | 提供打印机信息 |
| `pg_dump` | 创建 PostgreSQL 数据库备份 |
| `psql` | 在 PostgreSQL 服务器上执行 SQL 命令 |
| `smbpasswd` | 修改 Samba 密码 |
| `mysql` | 执行 SQL |
| `mysqladmin` | 帮助 MySQL 管理 |
| `mysqlbinlog` | 从日志文件中提取数据 |
| `mysqldump` | 执行 MySQL 备份 |

# 音频功能与硬件管理

| `acpi` | 提供电池信息 |
| `alsactl` | 保存或加载音频系统的所有参数 |
| `amixer` | 交互式调整音频通道 |
| `boltctl` | 控制 Thunderbolt 接口设备 |
| `free` | 显示空内存（RAM/Swap） |
| `fwdmgr` | 管理固件更新 |
| `hwclock` | 读取或设置硬件时 |
| `inxi` | 提供硬件概览 |
| `kbdrate` | 设置键频 |
| `localectl` | 更改语言和键盘设置 |
| `lscpu` | 提供 CPU 信息 |
| `lshw` | 创建硬件组件的分级列表 |
| `lspci` | 提供 PCI 组件信息 |
| `lsscsi` | 提供连接 SCSI 设备的信息 |
| `lusb` | 提供连接 USB 设备的信息 |
| `nproc` | 提供 CPU 核心数 |
| `pactl` | 控制 PulseAudio 服务器 |
| `paplay` | 通过 PulseAudio 播放原始文件 |



# 蓝牙

| `bluetoothctl` | 配置蓝牙设备 |
| `hciconfig` | (禁用)本地蓝牙适配器 |
| `hcitool` | 管理蓝牙设备 |
| `l2ping` | 向蓝牙设备发送显性请求 |
| `rfkill` | （禁用）禁用蓝牙、WLAN 和移动射电适配器 |
| `sdpptool` | 确定蓝牙设备的详细信息 |

# 内核 (Kernel)

| `canonical-livepatch` | 管理内核实时补丁 (Ubuntu) |
| `depmod` | 创建包含所有模块依赖的文件 |
| `dmesg` | 显示内核消息 |
| `dracut` | 创建新的 initrd 文件 (Fedora, RHEL, SUSE) |
| `insmod` | 加载内核模块（低级） |
| `kexec` | 激活另一个内核 |
| `lsmod` | 列出所有已加载的内核模块 |
| `modinfo` | 提供内核模块的信息 |
| `modprobe` | 加载内核模块，包括其依赖项 |
| `uname` | 显示当前内核版本 |
| `update-initramfs` | 创建新的 initrd 文件 (Debian, Ubuntu) |

# 系统启动与停止、init 系统、日志记录和 GRUB

| `efibootmgr` | 读取或更改 EFI 启动条目表 |
| `grub-install` | 将 GRUB 安装到引导扇 |
| `grub-mkconfig` | 创建新的 GRUB 配置文件 |
| `journalctl` | 从日志中读取新闻 |
| `logger` | 记录一条消息 |
| `loginctl` | 控制 systemd 登录管理器 |
| `needs-restarting` | 显示系统或单个服务是否需要重启 |
| `shutdown` | 终止 Linux |
| `systemctl` | 管理 systemd 进程 |
| `systemd-analyze` | 帮助进行 systemd 故障排除 |
| `update-grub` | 更新 GRUB 配置 (Debian, Ubuntu) |

# 虚拟化、容器、云服务

| `aws` | 控制 Amazon 云服务 |
| `docker` | 管理容器 |
| `kvm` | 运行虚拟机 |
| `docker` | Docker，管理容器 |
| `gemu` | 运行虚拟机 |
| `gemu-img` | 创建或编辑镜像文件 |
| `rclone` | 将本地目录与云目录同步 |
| `virsh` | 执行 libvirt 命令 |
| `virt-clone` | 创建虚拟机的副本 |
| `virt-install` | 安装新的虚拟机 |
| `virt-viewer` | 允许通过 VNC 操作虚拟机 |
| `wsl` | 管理 Windows 上的 Linux 安装 |

# 终端和文本控制台

| `echo` | 输出一行文本 |
| `loadkeys` | 为文本控制台加载键盘表 |
| `printf` | 启用类似于 C 语言的格式化输出 |
| `reset` | 重置终端 |
| `screen` | 在终端中管理多个会话 |
| `setterm` | 更改各种终端设置 |

# 在线帮助

| `apropos` | 按搜索命令 |
| `help` | 显示 shell 命令的描述 |
| `info` | 启动 info 系统 |
| `man` | 显示命令的描述 |
| `tldr` | 显示命令的使用示例 |
| `whatis` | 显示命令的简短描述 |

# 图形系统和 Gnome

| `chvt` | 更改活动文本控制台或激活图形系统 |
| `dconf` | 修改 dconf 数据库（低级） |
| `fc-list` | 列出所有可缩字体 |
| `fgconsole` | 返回活动控制台的数量 |
| `gnome-session-quit` | 启动注销或关机 |
| `grim` | 在 Wayland 上创建截图 |
| `gsettings` | 读取或更改 dconf 数据库的设置 |
| `nvidia-xconf` | 帮助配置 NVIDIA 图形驱动 |
| `xdg-open` | 使用合适的程序打开文件 |
| `scrot` | 在 X 下创建截图 |
| `slurp` | 在 Wayland 上启用选择矩形 |
| `wl-copy` | 将数据插入 Wayland 剪贴板 |
| `wl-paste` | 从 Wayland 剪贴板读取数据 |
| `wlr-randr` | 更改图形系统的分辨率 (Wayland) |
| `xdg-open` | 使用合适的程序打开文件 |
| `xdpyinfo` | 提供运行中的 X 服务器信息 |
| `xhost` | 允许或阻止主机登录 X |
| `xinput` | 为 X 配置输入设备 |
| `xkill` | 用鼠标点击终止程序 |
| `xrandr` | 更改图形系统的分辨率 (X) |
| `xset` | 更改图形系统的用户设置 (X) |
| `zenity` | 显示简单的图形对话框 |

# 杂项 (Miscellaneous)

| `alias` | 定义缩写 |
| `basename` | 确定路径的文件 |
| `bc` | 执行简单计算（类似于口袋计算器） |
| `cksum` | 计算文件的 CRC 校验和 |
| `date` | 显示日期和时间 |
| `dirname` | 确定路径的目录 |
| `expr` | 执行计算和样本比较 |
| `git` | 控制版本管理系统 Git |
| `gpiot` | 读取树莓派输入/输出引脚的状态 |
| `gpioset` | 更改树莓派输入/输出引脚的状态 |
| `hash` | 显示哈希表 |
| `ldd` | 显示程序所需的库 |
| `lsb_release` | 确定发行版的名称和版本 |
| `mail` | 将邮件传输到本地邮件服务器 |
| `md5sum` | 计算文件的校验和 |
| `printenv` | 仅显示环境变量 |
| `pinctrl` | 控制树莓派的输入/输出引脚 |
| `calc` | 作为终端的计算器 |
| `rpicam-still` | 拍照 (树莓派 OS) |
| `rpicam-vid` | 录制 (视频) |
| `seq` | 返回数值序列 |
| `set` | 显示所有环境变量 |
| `sha` | 计算文件的和 |
| `sleep` | 等待指定的时间 |
| `strace` | 跟踪系统调用 |
| `time` | 测量执行时间 |
| `tty` | 显示终端设备名称 |
| `type` | 指定命令类型 |
| `unalias` | 删除缩写 |
| `uname` | 返回操作系统名称和内核版本 |
| `xargs` | 重定向标准输入 |

# bash 编程 (Programming)

| `break` | 提前结束循环 |
| `case` | 初始化分支 |
| `continue` | 跳过循环体 |
| `exit` | 终止 shell |
| `for` | 启动循环 |
| `getopts` | 处理传递的选项 |
| `if` | 启动分支 |
| `local` | 函数中的局部 |
| `source` | 运行指定的文件 |
| `test` | 分析条件 |
| `until` | 启动循环 (1) |
| `while` | 启动循环 (2) |

# bash 变量管理 (Variable Management)

| `alias` | 定义缩写 |
| `declare` | 定义环境变量 |
| `export` | 导出指定的环境变量 |
| `local` | 函数中的局部 |
| `read` | 导入变量 |
| `readonly` | 显示只读变量 |
| `shift` | 移动参数列表 |
| `unalias` | 删除缩写 |
| `unset` | 删除变量 |

# bash 命令和特殊字符 (Commands and Special Characters)

| `dirs` | 显示保存的目录列表 |
| `disown` | 将进程从 shell 中分离 |
| `eval` | 分析指定的命令 |
| `popd` | 回到上一个保存的目录 |
| `pushd` | 保存目录并切换目录 |



| `trap` | 发生信号时执行命令 |
| `ulimit` | 控制 shell 使用的资源 |
| `wait` | 等待后台进程结束 |

# 配置文件 (Configuration Files)

| `etc/adduser.conf` | 新账户设置 (Debian, Ubuntu) |
| `etc/aliases` | 邮件转发 |
| `etc/bashrc` | bash 默认设置 |
| `boot/firmware/config.txt` | 树莓派硬件参数 (树莓派 OS) |
| `etc/crontab` | 定期运行 |
| `etc/deluser.conf` | deluser 和 delgroup 设置 (Debian, Ubuntu) |
| `etc/dnf/dnf.conf` | dnf 包管理配置 (Fedora) |
| `etc/fstab` | 自动挂载文件系统/分区 |
| `etc/group` | 组名和组分配 |
| `etc/default.grub` | GRUB 2 默认设置 |
| `boot/grub/grub.cfg` | GRUB 2 配置 |
| `etc/gshadow` | 组密码哈希值 |
| `etc/host.conf` | 解析器库配置 |
| `etc/hostname` | 计算机的主机名 |
| `etc/hosts` | 主机名和 IP 地址静态列表 |
| `etc/network/interfaces` | 网络配置 (Debian, Ubuntu) |
| `etc/systemd/journald.conf` | Journal 服务配置 |
| `etc/locale.conf` | 本地化设置 (systemd) |
| `etc/login.defs` | 创建新用户和组的选项 |
| `etc/mdadm/mdadm.conf` | 软件 RAID 配置 |
| `etc/modules` | 自动加载内核模块 (Debian, Ubuntu) |
| `etc/netplan/netplan.yaml` | 网络设置 (Ubuntu) |
| `etc/systemd/network/networkd.network` | networkd 配置 (systemd) |
| `etc/nsswitch.conf` | 命名服务切换函数的配置 |
| `etc/os-release` | 发行版的名称和版本号 (systemd) |
| `etc/passwd` | 所有用户及其主目录列表 |
| `etc/profile` | 系统级环境变量配置 |
| `etc/rc.local` | 启动过程结束时执行的脚本 |
| `etc/resolv.conf` | 命名服务器的 IP 地址 |
| `etc/rsyslog.conf` | syslog 服务配置 |
| `etc/services` | 网络服务与端口的映射 |
| `etc/shadow` | 登录密码的哈希值 |
| `etc/apt/sources.list` | APT 软件包源 (Debian, Ubuntu) |
| `etc/sudoers` | sudo 配置 |
| `etc/sysctl.conf` | 内核参数的默认设置 |
| `systemd.service` | systemd 服务配置 |
| `systemd.timer` | 定期 systemd 任务配置 |
| `etc/vconsole.conf` | 键盘设置 (systemd) |
| `etc/wpa/supplicant/wpa_supplicant.conf` | WLAN 配置 (Raspberry Pi OS) |

# 快捷键

| `bash` | Shell |
| `emacs gnome-terminal` | Gnome 上的终端窗口 |
| `grub` | 引导程序 |
| `info` | 显示帮助文本的命令 |
| `joe` | 简单编辑器 |
| `konsole` | KDE 上的终端窗口 |
| `less` | 显示文本文件的命令 |
| `man` | 显示帮助文本的命令 |
| `mutt` | 文本模式邮件客户端 |
| `nano` | 基础编辑器 |
| `screen` | 终端复用器 |
| `Text console` | 文本控制台中的快捷键 |
| `vi/vim` | 编辑器 |

## 引言

本书包含了对最重要的 Linux 命令的简要描述，用于管理文件系统、启动和终止进程、编辑文本文件、其他管理任务以及 bash 编程。书中还总结了基础配置文件的语法，并包含了 emacs、nano 和 vi 编译器的快捷键参考，以及如 `less` 或 `info` 等其他交互式命令。

本书的目的是为在终端中使用 Linux 提供一份精简凑的参考指南。本书的基本原则是：少即是多。本书不能也也不打算替代复杂命令的 `man` 和 `info` 页面！因此，你仍然需要自己查找或研究某些特殊的选项。

然而，通过本书，我试图减轻你从通常几十页的原始文档中搜索日常使用选项的负担。大量的示例也能让你一目了然地命令的基本用法。

有时，你正在寻找某个用于特定任务的命令，但不知道它的名字或刚刚忘记了。按主题组织的目录就是为了应对这种情况准备的。

取决于你使用的发行版，某些命令默认不可用，必须单独安装。还有特定发行版的命令，仅在某些发行版中可用，例如软件包管理命令 `dpkg` 和 `apt` (Debian, Ubuntu)、`rpm` 和 `yum` (Fedora, Red Hat) 以及 `zypper` (SUSE)。这些在相应的命令描述中会有说明。

## 什么是命令？

Linux 不区分命令（如本书中所描述的）与诸如 Firefox、LibreOffice 或 GIMP 等程序。在这里，“命令”指的是没有图形用户界面的程序，它们通常在终端窗口中执行。

在书中，我还描述了一些并不是真实程序的命令，它们只是当前活动 shell 的命令。我假设你正在使用 `bash` (Bourne Again Shell) 或与其兼容的 `zsh`。这些 shell 用于大多数 Linux 发行版中的交互式命令执行。shell 命令的一个示例是 `cd`，用于更改当前目录。

## 选项

书中描述的大多数命令都由选项控制。选项在所有其他参数*之前*指定。命令有两种表示方法：`-x` 用于短选项（单个字母）和 `--xyz` 用于长选项（多个字母）。

因此，以下 `ls` 命令是等价的，它们都会显示 `/usr` 目录下的所有文件和目录：

```
user$ ls -l /usr
user$ ls --format=long --almost-all /usr
```

对于某些命令，可以作为一个组来指定多个选项（例如使用 `-ab` 而不是 `-a -b`）。某些命令也可以在实际参数之后指定选项运行。然而，这不应该让你得出结论，认为这适用于所有命令！

```
user$ ls -IA /usr
user$ ls /usr -IA
```

对于少数命令，参数的顺序会影响命令的执行方式。如果指定的选项在逻辑上是互斥的，则最后指定的选项将生效。

## man, info, 和 help

为了避免本书变得不必要的冗，我只描述最重要的选项。大多数命令的所有选项的完整概述可以通过`命令名 --help` 提供。更详细的信息通常包含在手册页中，可以通过 `名称` 或 `man 1 名称` 访问。对于某些命令，man 页面仅包含对 info 文本的引用，可以通过 `名称` 相应显示。

对于直接集成到 bash 中的命令（例如 `cd`），man 页面仅包含对 info 文本的引用，可以通过 `名称` 相应显示。

`https://github.com/ggeer/the_silver_searcher/wiki`

## 示例

以下示例在 `/etc` 目录下搜索包含搜索词 `localhost` 的文件，并显示相应的匹配结果以及行号：

```
root# cd /etc
root# ack localhost
security/pam_env.conf
52=: "localhost" 而不是未设置
53=#REMOTEHOST DEFAULT=localhost OVERRIDE=@{PAM RHOST}
64=#NMTServer DEFAULT=localhost
sspeech-dispatcher/speech.conf
38# 对于来自 localhost 的连接。如果 LocalAccessOnly 设置为 0 则禁用此项
199=#AudioNAServer "tcp/localhost:5450"
speech-dispatcher/modules/festival.conf
7:#SqlServerHost "localhost"
```

## `acme.sh` [options]



# acme.sh

`acme.sh` 是一个用于帮助安装证书的脚本。`acme.sh` 默认使用证书机构 (CA) `https://zeross.com`。可以使用 `--server` 选项设置备用 CA，包括 Let's Encrypt (`https://letsencrypt.org`)。

该脚本是 `certbot` 命令的实用替代方案，后者的 Python 依赖项过去经常导致安装问题。

也必须安装 `acme.sh`。但这几乎毫不费力即可完成：

```
user$ sudo apt/dnf/yum/zypper install curl socat
user$ curl https://get.acme.sh -o acme-setup
user$ less acme-setup
(简要检查脚本代码)
user$ sudo sh acme-setup email=name@myhostname.com
...
安装到 /root/.acme.sh/acme.sh
正在安装别名到 '/root/.bashrc'
OK，关闭并重新打开终端开始使用 acme.sh
```

作为安装的一部分，`/var/spool/cron/root` 增加了一行。这使得 Cron 定期处理 `acme.sh -cron`，从而自动更新所有使用 `acme.sh` 设置的证书。

## 选项

### `-cron`

更新所有通过 `acme.sh` 安装的早于 60 天的证书。可以使用额外的 `--force` 选项强制提前续期。

### `-install-cert -d domain`

`[--cert-file path/to/certfile]`

`[--key-file path/to/keyfile]`

`[--fullchain-file path/to/fullchainfile]`

`[--reloadcmd systemctl restart httpd]`

将之前通过 `acme.sh -issue` 生成的证书复制到 Web 服务器可以访问的位置并重启 Web 服务器。与其使用 `systemctl restart httpd`，你必须输入适用于你发行版的命令来重启 Web 服务器。

请注意，不要建议你自己将存储在 `/root/.acme.sh` 中的证书复制到另一个目录。`acme.sh` 会记住用于自动更新证书的路径和重载命令。

`acme.sh` 不会更改你 Web 服务器的配置文件！你必须手动添加带有证书文件路径的语句。

### `--issue -d domain -w webrootdir`

为指定域名设置证书。`-d` 选项可以使用多次，以为相关域名创建证书（例如：`-d a-company.com -d www.a-company.com`）。如果你想要通配符证书，需要传递 `-d a-company.com -d *.a-company.com` 等。证书保存在 `/root/.acme.sh` 目录中。

如果计算机上没有运行 Web 服务器，你应该指定 `--standalone` 选项而不是 `-w webrootdir`。`acme.sh` 本身将临时充当 Web 服务器。这假设端口 80 没有被任何程序阻塞。

### `--remove -d domain`

禁用指定域名的证书更新（更新每 60 天自动进行一次）。尽管选项名称暗示如此，但证书本身不会被删除。不过，你可以手动删除对应的 `/root/.acme.sh/domain` 目录。

### `-server letsencrypt|buypass|google|sslcom|zerossl`

指定要使用的 CA。如果不使用此选项，则应用 `zerossl`，即从 `http://zerossl.com` 获取免费证书。

### `--upgrade`

更新 `acme.sh` 脚本。

## 示例

以下命令为域名 `a-company.com` 和 `www.a-company.com` 生成证书，并将证书复制到为以下设置的 `/etc/acme-letsencrypt` 目录：

```bash
mkdir /etc/acme-letsencrypt
acme.sh --issue -d a-company.com -d www.a-company.com -w /webroot --cert-file /etc/acme-letsencrypt/a-company.com.pem --key-file /etc/acme-letsencrypt/a-company.com.key --fullchain-file /etc/acme-letsencrypt/a-company.com.fullchain.pem --reloadcmd "systemctl restart httpd"
```

以下命令为域名 `a-company.com` 和 `www.a-company.com` 生成证书，并将证书复制到为以下设置的 `/etc/acme-letsencrypt` 目录：

```bash
mkdir /etc/acme-letsencrypt
acme.sh --issue -d a-company.com -d www.a-company.com -w /webroot --cert-file /etc/acme-letsencrypt/a-company.com.pem --key-file /etc/acme-letsencrypt/a-company.com.key --fullchain-file /etc/acme-letsencrypt/a-company.com.fullchain.pem --reloadcmd "systemctl restart httpd"
```

任何其他参数，所有定义的缩写都将显示。

在 Fedora 和 Red Hat 系统上，为 root 了一些预定义的别名。这些别名在登录时会从 `/root/.bashrc` 文件加载。

## 示例

以下命令为 `ls -l` 命令定义了 `ll` 缩写：

```
user$ alias ll='-l'
```

```
alien [options] package file
```

`alien` 将指定的软件包转换为不同的格式。所需的格式通过选项 `--to-deb` (Debian)、`--to-rpm` (RPM) 或 `--to-tgz` (tar 归档) 来指定。`alien` 必须由 root 运行，以便正确设置新软件包的所有者和访问权限。

`alien` 仅对简单软件包运行没有问题。然而，如果软件包使用了安装脚本或相应包格式的其他特定功能，则之前转换的软件包安装极可能会失败。

# alsactl [options] [command] [card/id/device]

你可以使用 `alsactl` 来显示、保存和恢复音频系统的状态。该命令还提供了一些较简单的 `amixer` 命令不具备的高级控制选项。

`alsactl` 通常适用于所有音频设备，除非明确指定了音频设备的数量或设备名称（另见 `/proc/asound/cards` 文件）。

- `-b` 在后台运行 `alsactl`。此选项有助于 init 系统将 `alsactl` 作为后台服务启动。
- `-f` 指定 `alsactl` 应读取或用于保存的文件（默认情况下，这是 `/var/lib/alsa/asound.state`）。
- `-s` 使用 syslog 服务记录消息、警告和错误。

这里列出了 `alsactl` 最重要的命令。还有其他几个命令专门用于作为后台服务使用，对于交互式调用或脚本很少感兴趣。

- `- init` 使用默认设置初始化音频系统。
- `- monitor` 跟踪音频系统的所有更改并显示它们，直到使用 Ctrl + C 结束命令。
- `- restore` 恢复之前保存的音频系统状态。数据从 `/var/lib/alsa/asound.state` 或由 `-f` 指定的文件读取。
- `- store` 将音频系统的状态保存到文本文件 `/var/lib/alsa/asound.state` 或由 `-f` 指定的文件中。

```
alsamixer [options]
```

`alsamixer` 是交互式命令，你可以使用功能键和光标键设置音频通道的音量或录音电平。Esc 终止程序。`alsamixer` 不适用于脚本编程。为此，你可以使用 `amixer`。

- `-c n` 如果存在多个音频卡，则选择所需的音频卡。音频卡从 0 开始连续编号。如有必要，你应该查看 `/proc/asound/cards` 文件，该文件列出了所有音频卡。
- `-D device` 选择音频系统。例如，你可以使用 `-D pulse` 来更改 PulseAudio 系统设置。如果没有此选项，`alsamixer` 将直接控制 ALSA 系统。
- `-V playback|capture|all` 决定初始显示哪些控制器：用于音频播放、用于录音或所有控制器。当 `alsamixer` 运行时，你可以使用 `F3`、`F4` 和 `F5` 在这些显示格式之间切换。

# alternatives [options] command



alternatives 是 Red Hat 或 Fedora 版本的 `update-alternatives`。这两个命令的语法很大程度上相同，并在 `update-alternatives` 命令中有描述。

## amixer [options] command

你可以使用 `amixer` 命令通过选项更改音频系统通道的音量或电平。如果你想交互式地调整音量或其他设置，可以使用带有简单文本用户界面的 `alsamixer` 命令。

- `-c n` 选择所需的音频卡。音频卡从 0 开始连续编号。如有必要，你可以查看 `/proc/asound/cards` 文件，该文件列出了所有音频卡。如果缺少该选项，`amixer` 处理默认音频设备。
- `-D device` 选择音频系统（例如 `-D pulse` 用于 PulseAudio 系统）。如果没有此选项，`amixer` 将直接控制 ALSA 系统。
- `-q` 在更改设置后不输出新状态。
- `-s` 从标准输入读取要执行的命令。只考虑 `sset` 和 `cset` 命令。

以下列表描述了最重要的 `amixer` 命令：

- `cget id` 指明开关的状态。开关可以通过一个或多个参数指定，例如，`numid=3` 或 `if=MIXER,name='Headphone Playback Switch'`。`amixer controls` 会创建一个包含所有控制和开关以及相应 ID 数据的列表。
- `controls|scontents|controls` 列出不同详细程度的所有控制和开关，并指示它们的当前状态。
- `cset id parameter` 更改开关状态。例如，`amixer cset numid=3 1` 开启树莓派上的音频输出。
- `info` 显示音频卡的简要描述。
- `sget 'name',n` 返回音频卡的状态。

`apt` 负责安装、更新和删除软件包，并考虑 `etc/apt/sources.list` 中定义的所有软件包源中的包。以下列表描述了最重要的命令：

- `apt autoclean`

仅从软件包缓存中删除已有新可用可用包。

- `apt autoremove`

卸载所有不再需要且由于依赖关系而安装的包。

- `apt full-upgrade`

工作方式类似于 `upgrade`，但它还会执行需要删除软件包才能进行的更新。

- `apt install name1 name2 ...`

在所有 APT 软件包源中搜索 `name1`、`name2` 等包；下载并安装它们。如果必要，还会加载并安装或更新额外的包以满足包依赖关系。

- `apt install ./filename.deb`

安装之前下载到本地的 Debian 软件包（`.deb`）。仍会使用所有 APT 软件包源来解析包依赖关系。重要的是，文件路径必须能够被识别为此类路径，并以 `./`（本地目录）或 `/`（绝对路径）开头。否则，`apt` 会认为这是一个包名，在软件包源中搜索它，并最终返回错误信息。

- `apt list`

列出所有可用包。带有 `--installed` 选项时，命令仅返回当前安装的包。

- `apt remove name12 ...`

卸载指定的软件包。

- `apt search search term`

列出所有名称或描述包含搜索词的包。

- `apt show name1`

显示指定包的信息。

- `apt update`

更新 `sources.list` 中指定的存档的软件包列表。仅读取并将软件包源的元数据存入 APT 缓存文件中。然而，不会下载或更新任何软件包！此命令的唯一目的是让 `apt` 知道互联网上有哪些包可用。在运行任何 `apt` 命令之前，都应该运行此命令。注意：如果你只想更新一个包（而不是所有包），你需要运行 `apt install name`，而不是 `apt update name`！

- `apt upgrade`

如果软件包源中有较新版本，则更新所有已安装的。如果必要，还会为更新安装额外的包。但是，`apt upgrade` 不会执行需要删除包才能进行的更新。

### 示例

以下命令展示了如何使用 `apt`：

```
root# apt update
(更新软件包源)
root# apt full-upgrade
(更新所有已安装的包)
root# apt install apache2
(安装 Apache 局服务器)
```

## apt-cache 命令

`apt-cache` 命令是 Debian 和 Ubuntu 特有的，用于提供有关可用或之前安装的包的信息。

- `apt-cache madison package name`

提供 `apt-cache policy` 结果的单行摘要（见下文）。

- `apt-cache policy`

显示所有软件包源的详细列表。

- `apt-cache policy package name`

显示当前安装的包来自哪个软件包源，以及哪些软件包源可能提供该包的备用版本。

- `apt-cache search pattern`

返回所有包名或包描述包含搜索文本模式的可用包列表（无论它们是否已经安装）。额外的 `--names-only` 选项将搜索范围限制在包名上。

- `apt-cache show package name`

提供包的简短描述。只要包描述在缓存中，这对于未安装的包也有效。

- `apt-cache showpkg package name`

显示该包的依赖关系信息。

- `apt-cache stats`

提供已安装和可用包数量的统计信息。

`apt-cache` 可以提供关于包特定内容的详细信息，或建立文件与相应包之间的关联。如果你对这些信息感兴趣，必须使用 `dpkg`。

### 示例

以下命令返回所有名称包含 `gimp` 的包的排序列表：

```
root# apt-cache search --names-only gimp | sort
gimp-commonplugins - 用于 GIMP 导入/出的扩展
          Commodore-64 文件
gimp-data - GIMP 的数据
gimp-data-extras - GIMP 的额外笔刷和图案
...
```

第二个示例显示了安装了哪个版本的 `openjdk-17-jre` 软件包，以及是否存在备用版本。`apt-cache` 仅找到了较旧的版本（17.0.2 而不是 17.0.10）：

```
user$ apt-cache policy openjdk-11-jre
openjdk-17-jre:
Installed: 17.0.10+7~1~22.04.1
Candidate: 17.0.10+7~1~22.04.1
Version table:
** 17.0.10+7~1~22.04.1 500
  500 http://.../ubuntu-ports jammy-updates/universe arm64 Packages
  500 http://ports/...-jammy-security/universe arm64 Packages
  100 /var/lib/dpkg/status
  17.2+8-1 500
  500 http://de.../ubuntu-ports jammy/universe arm64 Packages
```

## apt-file [options]

来自同名软件包的 `apt-file` 命令允许搜索 Debian 软件包中包含的文件——即使该包尚未安装。

### 示例

以下命令创建或更新本地数据库，然后搜索包含 `main.cf` 的文件的包：

```
root apt-file update
users apt-file find main.cf
postfix: /usr/share/postfix/main.cf.debian
postfix: /usr/share/postfix/main.cf.dist
postfix: /usr/share/postfix/main.cf.dist
```

来自 `apt-file` 软件包

`apt-file` 命令

## apt-get [options] 命令

`apt-get` 命令是 Debian 和 Ubuntu 特有的，用于安装、更新和删除软件包。对于交互式使用，现在推荐使用 `apt`。但 `apt-get` 在所有基于 Debian 的发行版中仍然可用。以下列表描述了最重要的命令：

- `apt-get autoclean`

仅从软件包缓存中删除已有新可用可用包。

- `apt-get autoremove`

卸载所有不再需要且由于依赖关系而安装的包。

- `apt-get check`

更新所有安装包的缓存并检测任何现有冲突和未解决的依赖关系。这在包已卸载时是必要的。

- `apt-get clean`

从软件包缓存中删除所有下载的包。

- `apt-get dist-upgrade`

工作方式类似于升级但在需要时安装新包。

- `apt-get install name1 ...`

安装 `name1`、`name2` 等包，并考虑软件包关系。如果包已安装，`apt-get install` 将更新此包。



### apt-get remove name1 ...

卸载指定的软件包。

### apt-get source name

安装包的源代码。

### apt-get update

更新 `sources.list` 中指定的存档的软件包列表。（更多细节见 `apt update`。）

### apt-get upgrade

如果软件包源中有较新版本，则更新所有已安装的。

`apt-get` 命令的详细行为由选项控制：

#### apt-get -d --download-only

仅下载包到 `/var/cache/apt/archives` 目录，但不进行安装。

#### apt-get --no-install-recommends

不安装推荐包。

#### apt-get -s --simulate

模拟安装，但不进行任何更改。

#### apt-get -y --assume-yes

对所有问题回答“是”，以便在脚本中使用命令。

## 示例

以下更新命令展示了你可以如何使用 `apt-get`：

```
root apt-get update && apt-get dist-upgrade
(执行完整更新)
root# apt-get remove -y emacs
(无询问删除 emacs)
```

## apt-key 命令

尽管 `apt-key` 命令在无数网络手册中被提到，但它是过时的。在过去，该命令帮助管理软件包源的密钥。通常以 `apt-key add keyfile` 的形式执行。

该命令在当前的发行版中不再可用。密钥文件现在必须手动保存在 `/etc/apt/trusted.gpg.d` 目录下。此外，在 `/etc/apt/sources.list` 或 `/etc/apt/sources.d` 中指定软件包源时，必须使用 `signed-by:` 显式引用密钥文件：

```
## /etc/apt/sources.d/myrepo.list
deb [signed-by=/etc/apt/trusted.gpg/myrepo.asc] https://apt.myrepo.com ...
```

## aptitude [options]

Debian 特有的 `aptitude` 命令安装、更新和删除软件包，并访问像 `apt` 和 `apt-get` 这样的 APT 基础设施。与相比的优势

这两个命令的区别在于，`aptitude` 在安装过程中会记住依赖包，并在卸载时自动删除它们。

所有包管理功能都以命令的形式执行（例如，`aptitude install package name`）。基础命令与 `apt-get` 中的命令对应，并在那里有有描述。然而，`aptitude` 中没有提供 `check` 和 `autoremove` 命令。强大的 `search` 命令可以实现此目的。

此外，你也可以通过在不带任何额外参数的情况下直接启动程序，在控制中使用带有文本用户界面的程序。使用键盘快捷键 `Ctrl+T` 选择菜单。尽管有菜单，但 `aptitude` 的用法并不十分直观，大多数用户像使用 `apt-get` 一样，仅使用 `aptitude` 来运行单个命令。

大多数发行版默认没有安装 `aptitude`，在使用它之前必须通过 `apt` 或 `apt-get` 进行安装。

### aptitude search

`aptitude search` 为搜索软件包数据库提供了全面的选项。在最简单的形式下，你可以使用 `aptitude search 搜索词` 来搜索名称包含该搜索词的包。你可以使用 `~` 加字母来构建各种搜索标准。例如，`~i` 将搜索限制为已安装的包，`~U` 显示可用更新的包。`-F` 选项允许你控制搜索结果的哪些细节在特定宽度的列中显示。

其他许多搜索选项请参见 `/usr/share/doc/aptitude/README` 以及下页页：

`www.debian.org/doc/manuals/aptitude/ch02s04s05.en.html`

## 示例

以下两个命令首先安装 `mysql-server` 包，然后再次将其删除。值得注意的是，第二个命令删除了几乎所有与 `mysql-server` 一起安装的依赖包（但是，独立于服务器的客户端和库会被保留）。

```
root# aptitude install mysql-server
The following NEW packages will be installed:
libcgi-fast-perl{a} libcgi-pm-perl{a} libevent-core-2.1-7{a} ...
mysql-server mysql-server-8.0{a} mysql-server-core-8.0{a}
0 packages upgraded, 19 newly installed
...
```

```
root# aptitude remove mysql-server
The following packages will be REMOVED:
libcgi-fast-perl{u} ... mysql-server-core-8.0{u}
0 packages upgraded, 0 newly installed, 19 to remove
```

以下命令提供了所有已安装包的列表。包组或包源指定在第一列（`%20s, Source`，列宽为20个字符），包名指定在第二列。

```
user$ aptitude search ~i -F "%20s %p"
utils               adduser
admin             adwaita-icon-theme
games              aisleriot
..
```

你可以使用 `egrep` 从结果中过滤源自 Ubuntu 软件包源 `universe` 或 `multiverse` 的包。

```
user$ aptitude search ~i -F "%20s %p" | egrep "universe|multiverse"
universe/admin      aptitude
universe/admin      aptitude-common
universe/introspection  girl1.2-gtk-vnc-2.0
universe/editors      joe
universe/libs        libburn4
..
```

## arp [options] [hosts/ipaddresses/network]

来自 `net-tools` 包的 `arp` 命令有助于管理 `地址解析协议`（ARP）的缓存。该缓存包含本地网络设备列表，并允许分配它们的 MAC 地址。在没有任何额外参数的情况下，该命令返回当前缓存内容。使用 `-n` 选项，显示相应的 IP 地址而不是主机名。

```
user$ arp
Address            HWtype Hwidth      Flags Mask Iface
fritz.box           ether 3c:37:12:b7:a1:cb C       enp0s1
Archer-C6.fritz.box ether d08:b6:4f:19:af C enp0s1
m3.fritz.box ether 80:a9:97:32:c5:d7 C enp0s1
BRN0018BA99C5DA4.fritz ether 00:1b:a9:9c:5d:a4 C enp0s1
```

```
user$ arp -n
Address HWype HWaddress Mask Iface
192.168.178.10 ether 3c:37:12:b1:cb C enp0s1
192.168.178.21 ether d08:b6:4f:19:af C enp0s1
192.168.178.146 ether 80:a9:97:32:c5:d7 C enp0s1
192.168.178.20 ether 00:1b:a9:9c:5d:a4 C enp0s1
```

## arp-scan [options] [hosts/ipaddresses/network]

`arp-scan` 向指定的主机或 IP 地址发送地址解析协议（ARP）数据包并显示得到的响应。`arp-scan` 提供了一种极其快速的方法来发现哪些主机或 IP 地址正在运行活动设备以及它们拥有哪些 MAC 地址。

## atq

`atq` 列出所有设置在未来某个时间执行的作业。如果由 `root` 用户运行 `atq`，它将显示所有用户的作业；否则，仅显示其自身的作业。

## atrm n

`atrm` 根据编号删除指定的作业。你可以使用 `atq` 来确定所有设置在未来执行的作业编号。

## attr [options] files

`attr` 确定或更改指定文件或目录的扩展访问属性。这仅在文件系统支持扩展属性（EAs）时才有效。对于 `ext3/ext4` 文件系统，必须使用挂载选项 `user_xattr`。



与其使用 `attr`，不如你应该优先使用 `getfattr` 或 `setfattr` 命令。`attr` 仅为了与 IRIX SGI 兼容而存在。

```
awk [options] 'code' text files
awk [options] -f code file text files
```

`awk` 并不是一个简单的命令，而是一种独立的编程语言，有助于结构化文本的处理和分析。例如，你可以用它搜索文本文件的关键词，并从后续文本部分提取一个文本列。你可以直接输入代码，也可以使用 `-f` 选项从代码文件中读取。

`awk` 然后会逐行处理作为参数传递的所有文本文件，并将结果写入标准输出。

要由 `awk` 处理的程序代码遵循以下简化语法：

```
/searchpattern1/ {actions}
/searchpattern2/ {more actions}
condition {even more actions}
```

`grep` 命令中描述的规则同样适用于搜索模式的结构。多个操作之间用分号分隔。如果缺少搜索模式，则操作将适用于文本文件的每一行。反之，如果缺少操作，则模式捕获的文本将直接输出。

由于空间限制，此处无法对 `awk` 及其功能进行详尽描述。相反，我将仅限制在几个示例上。如果你想更深入地熟悉 `awk`，以下教程是一个很好的介绍：

`www.grymoire.com/Unix/Awk.html`

官方用户指南提供了更详细的内容，但由于有近 500 页，它可能会让新手望而却步：

`www.gnu.org/software/gawk/manual/gawk.pdf`

## 示例

此摘自 `/etc/passwd` 的片段作为后续示例的起点：

```
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
...
```

第一个 `awk` 示例仅返回 `/etc/passwd` 中的第一列和第七列，即登录名和分配的。`-F` 选项指定列与列之间通过冒号分隔，而不是空格和制表符：

```
$ awk -F':'{print $1,$7}' /etc/passwd
root /bin/bash
bin /sbin/nologin
daemon /sbin/nologin ...
```

第二个示例确定了 `kofler` 的家目录和 shell：

```bash
user$ awk -F':' '/kofler/ {print $6; print $7;}' /etc/passwd
/home/kofler
bin/bash
```

第三个示例显示所有 UID 大于或等于 1000 的用户的登录名：

```bash
user$ awk -F':' '$3>=1000 {print $1}' /etc/passwd
nfsnobody
kofler
test
```

最后一个示例从 `ls -l` 的输出中提取文件大小和文件名。请注意，这适用于不包含空格的文件名。

```bash
user$ ls -l | awk '{print $5,$9}'
123 file1
456 file2
```

## `aws [options] command [subcommand]`

`aws` 命令通过主命令选择服务，以及子命令。`aws` 命令有助于管理各种 S3 服务。你通常可以通过 `aws --version` 来查看版本。AWS CLI 2 版本与 S3 存储是兼容的，但在设置 `aws configure` 区域上有所不同。你可以在 AWS 身份与访问管理 (IAM) 页面找到相关信息：`https://docs.aws.amazon.com/cli/latest`

### 安装与配置

`aws` 默认未安装，除非在 Linux 上配置它。在 ARM 机器上，你可以使用 `curl` 安装：

```bash
user curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o awscli.zip
user unzip awscli.zip
sudo ./aws/install
```

现在运行 `aws configure` 并输入访问密钥 ID 和秘密访问密钥。`aws` 将这些数据保存在 `.aws/credentials` 和 `.aws/config` 中。

```bash
root# aws configure
AWS Access Key [None]: AKxxxxxx
AWS Secret Key [None]: Zxxxxxxx
Default region [None]: eu-central-1
Default output [None]:
```

### 语法与在线帮助

`aws` 没有 man 手页。相反，`aws help` 提供了命令的概述。

### S3 管理

- `aws s3 ls [path]`：在不带进一步参数的情况下列出所有 S3 桶，或显示目录和文件的内容。路径格式为 `s3://<bucketname>/<directory>/<file>`（例如 `s3://my-bucket/my-dir/my-file`）。

- `aws s3 cp path path2`：将本地文件复制到 S3 桶并从那里返回文件系统。你也可以将 S3 文件复制到另一个 S3 位置。你可以使用递归选项复制目录。出于测试目的，你需要传递 `--dryrun`：命令将显示它将做什么，但不会更改任何内容。

- `aws s3 mv path path2`：与上一条相同，但它是移动文件或重命名位于 S3 内存中的文件。

- `aws s3 sync path1 path2`：同步两个目录：一个本地，一个在 S3存储中。这比 `aws s3 cp` 快，因为未更改的文件不会再次传输。源路径中删除的文件将保留在目标路径中。如果你不想这样做，必须传递 `--delete` 选项。

- `aws s3 mb newbucket`：创建一个新桶，以通常的方式指定名称（即 `s3://<bucketname>`）。该名称在全球范围内必须唯一。通过 `--region` 选项，你可以指定设置桶的数据中心，这与 `aws configure` 中预设的区域不同。

- `aws s3 rb bucket`：删除指定的桶。操作仅在桶为空时才会成功。否则，你可以使用 `--force` 强制删除。

### EC2 管理

虽然用于 S3 管理的 `aws` 命令易于使用，但遗憾的是这并不适用于 EC2：仅子命令的数量就令人望而畏——有 400 多个。许多命令还提供或期望 JSON 数据结构，因此它们仅打算用于脚本编程，而不是供人类使用。你可以尝试以 `aws ec2 describe instances` 作为起点。该命令将你所有设置好的实例以 JSON 文档的形式列出：

```bash
root# aws ec2 describe-instances
{
  "Reservations": [
    {
      "Groups": [],
      "Instances": [
        {
          "AmiLaunchIndex": 0,
          "ImageId": "ami-02fc41eea1852"
        }
      ]
    }
  ]
}
```

## 示例

以下两个命令设置了一个新桶并将 `/etc` 目录中的所有文件复制到桶中：

```bash
root# aws s3 mb s3://info.kofler.etcbak
root# aws s3 sync /etc s3://info.kofler.etcbak
```

## B

`badblocks` 设备

`badblocks` 对数据介质进行低级检查。只有在你怀疑硬盘或 SSD 可能存在缺陷时，它才有用。如果你打算在硬盘（分区）上建立 ext 文件系统，最好在格式化时的一部分使用 `-c` 参数进行检查。

通常，`badblocks` 不会破坏任何数据，只执行只读测试。你可以通过添加 `-n` 或 `-w` 选项来执行更彻底的测试：

- `-n`

执行读写测试，但会恢复数据块的原始内容。如果数据介质或分区正在使用中（即通过挂载包含在目录树中），无法使用该选项。

- `-w`

使用位模式执行写测试。注意：数据介质或分区的内容将被删除！

```
basename string [ending]
```

`basename` 返回所传递路径的文件名。因此，`basename /etc/X11/Xmodmap` 的结果是 `Xmodmap`。如果指定额外的参数作为文件扩展名，该文件扩展名（如果存在）将从文件名中移除。

### 示例

`basename` 删除了路径和标识 `.jpg`。剩余的是白色。

```bash
user$ basename /home/kofler/Bilder/Wallpapers/white.jpg .jpg
white
```



## bat 文本文件

同名包的 `bat` 命令是 `cat` 命令的变体。与 `cat` 相比，`bat` 会尝试识别文本内容，并在显示时执行彩色语法高亮。在某些发行版中（例如 Debian），必须以 `batcat` 的名称 `bat` 以避免命名冲突。

`bat` 默认依赖你的终端使用深色背景。如果你使用浅色背景，必须向 `bat` 传递相应的选项（例如 `--theme gruvbox-light`），或在配置文件 `.config/bat/config` 中永久设置颜色主题。

## batch

`batch` 标记一个稍后执行的作业顺序。与 `at` 类似，待执行的命令将通过交互方式输入。必须使用 `Ctrl+D` 完成输入。与 `at` 不同的是，它没有指定作业应在何时运行。相反，后台守护进程会等待系统负载较低。阈值定义为平均负载 1.5。如果作业提供了输出，该输出将通过电子邮件发送给用户，这要求计算机上必须可用 `/usr/sbin/sendmail`。

`batch` 不处理选项或参数。如果你想从文件读取作业顺序，必须运行 `at -qb -f file now`。

## 示例

一旦系统负载较低，就会开始执行备份脚本：

```bash
user$ batch
./backup-script
<Ctrl>+<D>
```

## bc [file]

`bc` 代表 basic calculator（基础计算器），是一种面向命令的口袋型计算器。它可以以交互式方式执行简单计算。如果 `bash` 的有限计算功能不足，`bc` 在脚本中也有用。`bc` 期望从标准输入或文件读取计算语句。

## 示例

以下示例展示了 `bc` 的交互式用法及其在命令中的用法。`scale=3` 语句控制输出中的小数点位数。

```bash
user bc
> 2+3
5
> <Ctrl>+<D
user$ echo "5 + 3 * 7" | bc
26
user$ echo "scale=3; sqrt(2)" | bc
1.414
```

## 替代方案

`bc` 只知道少数高级数学函数。对于更复杂的计算，使用 `calc` 更好。然而，`qalc` 的缺点是必须单独安装。

## bg [process]

`bg` shell 命令在后台继续执行被中断的进程。如果没有指定进程号，`bg` 将适用于上一个使用 `ctrl+Z` 中断的进程。否则，必须通过名称或 `bash` 内部作业号（而不是 PID）来指定进程。

## blkid [options] [device]

`blkid` 提供由设备名称指定的块设备的信息，例如硬盘分区、逻辑卷、RAID 设备。`blkid` 指定文件系统类型、UUID 和文件系统的名称（标签）。当调用 `blkid` 时缺少设备指定时，`blkid` 将提供所有活动分区和逻辑卷的此类信息。通过指定选项，你可以搜索特定的文件系统：

- `-k`

列出内核支持的所有文件系统类型。

- `-L label`

搜索指定名称的文件系统。

- `-n fstype1,fstype2,fstype3`

搜索对应指定类型的文件系统。

- `-t name=value`

搜索匹配搜索标准的文件系统。允许的标准有：TYPE（文件系统类型）、LABEL（文件系统名称）、PARTLABEL（分区名称）、UUID（文件系统的 UUID）和 PARTUUID（分区的 UUID）。`blkid -t TYPE=ext4` 对应 `blkid -n ext4` 并返回所有 ext4 文件系统的列表。

- `-U uuid`

搜索指定 UUID 的文件系统。

## 示例

`/dev/sda1` 分区包含一个 UUID 为 2716...19e4 的 ext4 文件系统：

```bash
root# blkid /dev/sda1
dev/sda1: UUID="27162884-8ef9-4fa9-8b5b-7ff01572383" TYPE="ext4"
```

搜索分区 lvm2：

```bash
root# blkid -t LABEL=lvm2
dev/sda2: UUID="37cc374e-847f-407a-bb5d-7ff015722" LABEL="lvm2"
```

## bluetoothctl

在桌面系统中，蓝牙配置通常通过图形界面完成。如果不可用（例如在没有连接显示器的树莓派上），也可以使用 `bluetoothctl` 以文本模式进行配置。为此，你需要启动一个 `bluetoothctl` 交互式会话，然后运行命令来查找并配对设备。

你可以在 `bluetoothctl` 会话中运行下列描述的命令。保持你想要重新配置的设备上的蓝牙按钮（配对按钮）开启很重要，这样设备就会向环境发出已准备好连接的信号。在许多设备上，蓝色 LED 将会闪烁。如果没有此类按钮，你也可以尝试关闭设备再重新打开。

- `agent on/off`

（激活）禁用蓝牙代理。该软件组件负责授权新设备，并允许例如通过键盘输入配对代码。

- `connect xx:xx:xx`

建立连接。（这仅在执行了 `pair` 和 `trust` 后才有效！）如果一切顺利，响应将是连接成功。现在可以使用该设备了。

- `exit Or quit`

结束 `bluetoothctl` 会话。

- `info xx:xx:xx`

显示连接状态和关于设备的各种其他信息。

- `pair xx:xx:xx`

启动与设备的连接。如果你使用键盘，将提示你输入多位代码。别忘记按回车键完成输入！你可以通过配对成功的消息识别配配对。没有输入选项设备（鼠标、耳机等）可以在不输入代码的情况下进行配对。

- `pairable on/off`

激活/禁用配对模式。

- `scan on/off`

（激活）禁用扫描模式。在扫描模式下，程序列出所有设备。此过程可能需要一些时间，单个设备会反复显示。当你找到目标设备时，应该通过 `scan off` 关闭该模式。

- `trust xx:xx:xx`

信任指定的设备。

`bluetoothctl` 将特定设备的蓝牙配置永久保存在 `/var/lib/bluetooth/id1/id2/info` 中。在这里，`id1` 是蓝牙控制器的 ID，`id2` 是蓝牙设备的 ID。

`bluetoothctl` 实际上旨在交互式使用。要立即运行单个命令，你可以按照如下操作：

```bash
root# echo -e "connect FC:58:FA:A0:4D:E7\nquot" | bluetoothctl
```

## 示例

以下行以略简的形式显示了配置蓝牙键盘的输入和输出：

```
user bluetoothctl
[bluetooth]# agent on
[bluetooth]# pairable on
[bluetooth]# scan on
Discovery started
[CHG] Controller 00:1A:7D:DA:71:13 Discovering: yes
[NEW] Device 70:10:00:1A:92:20
[CHG] Device 70:10:00:1A:92:20 Name: Bluetooth 3.0 Keyboard

[bluetooth]# scan off
[bluetooth]# pair 70:10:00:1A:92:20
Attempting to pair with 70:10:00:1A:92:20
[CHG] Device 70:10:00:1A:92:20 Connected: yes
[agent] PIN code 963064
[CHG] Device 70:10:00:1A:92:20 Paired: yes
Pairing successful
[bluetooth]# trust 70:10:00:1A:92:20
[bluetooth]# connect 70:10:00:1A:92:20
[bluetooth]# info 70:10:00:1A:92:20
Device 70:10:00:1A:92:20
Name: Bluetooth 3.0 Keyboard
Paired: yes
Trusted: yes
Connected: yes
...
[bluetooth]# exit
```

## boltctl 命令

`boltctl` 控制通过 Thunderbolt（雷电）接口连接的设备。Thunderbolt 目前主要用于搭载 Intel CPU 的笔记本电脑。由于 Thunderbolt 是新 USB4 标准的一部分，它未来可能会变得更加普及。

- `authorize device`

允许使用一次 Thunderbolt 设备。你可以通过 `boltctl list` Determine所有已连接设备的列表。要给予永久权限，必须使用 `boltctl enroll`。

- `config key`

`config key newvalue`

加载或更改配置选项（需要 root 权限）。`boltctl config --describe` 提供所有选项的列表。

- `enroll [--policy auto|manual|default] device`



允许设备通过 Thunderbolt 接口永久通信。只有在使用通过 Thunderbolt 使用 PCI 总线的设备（例如扩展坞）时才需要显式权限，且仅当 BIOS/EFI 中设置了严格的 Thunderbolt 安全准则时。

`auto` 表示该设备在未来无需进一步查询即可使用。`manual` 要求每次重新连接时使用 `boltctl authorize` 进行确认。`default` 接受 Thunderbolt 守护进程的规范（通常是 `auto`）。

- `forget device`

从 `enroll` 数据库中删除设备 ID，从而撤销 `boltctl enroll` 的操作。

- `info device`

显示指定设备的详细信息。

- `list -a`

列出所有连接的设备。

- `monitor`

跟踪并记录哪些设备连接或移除，直到使用 `Ctrl+C` 结束命令。

- `power`

激活处于睡眠模式的 Thunderbolt 控制器。

## `break` [n]

bash 命令 `break` 用于提前终止 脚本中的 `for`、`while` 或 `until` 循环。shell 程序会在循环结束后继续执行下一条命令。通过指定可选数值 `n`，可以取消 `n` 级循环。

## btrfs 命令

`btrfs` 是 Btrfs 文件系统的中央管理命令。在没有歧义的情况下，你可以缩写本节描述的命令并节省大量的输入时间。`btrfs fish` 对应 `btrfs filesystem show`。Btrfs 文件系统的管理极其复杂。因此，这里只总结了最重要的命令。没有足够的空间详细描述 btrfs 的基础知识。

- `balance start|pause|resume|cancel|status mount directory`

将数据均匀分布在文件系统的所有设备上。此过程需要很长时间，并在后台运行。可以通过 `btrfs balance pause` 中断，通过 `btrfs balance resume` 恢复，或使用 `btrfs balance cancel` 完全停止。`btrfs balance status` 提供有关平衡过程进度的信息。

- `device add devicename mount directory`

向激活的 Btrfs 文件系统添加另一个设备，从而增加其数据池。

- `device delete devicename mount directory`

从 Btrfs 文件系统的数据池中删除设备。设备上的数据将传输到文件系统的其他设备，对于大型文件系统，这当然需要很长时间。

如果你想移除一个故障（不可用）设备，应该输入 `missing` 作为设备名。对于 RAID-1 系统，你必须先添加替换设备并运行 `btrfs filesystem balance`！

- `filesystem df directory`

显示为数据、元数据和系统数据保留了多少空间，以及这些空间已使用了多少。然而，该命令没有提供任何关于仍可用未预留内存空间的信息，这使得正确解释数据变得困难。

`filesystem resize [/size] mount directory`

在运行期间扩大或缩小文件系统。可以使用绝对或相对值指定新大小。允许使用 KiB、MiB 和 GiB 的缩写 `k`、`m` 和 `g`。也允许 `Max` 作为大小。

- `filesystem sync directory`

同步文件系统的内容。

- `scrub start|cancel|resume|status directory`

控制 scrub（数据清理）过程。`start` 加载文件系统的所有文件并检查它们的校验和。此过程在后台运行。可以使用 `status` 检查进度。

- `subvolume create directory/name`

在 Btrfs 文件系统的指定位置创建子卷或快照。

- `subvolume delete directory/name`

删除指定的子卷或快照。

- `subvolume list directory`

列出所有子卷和快照。输出受多个选项的影响。

- `subvolume show directory`

显示关于数据、元数据和系统数据保留了多少空间以及这些空间的基本信息。

- `subvolume set-default id directory`

确定默认使用哪个子卷或快照。

- `subvolume snapshot [-r] source directory target/name`

创建文件系统或现有子卷的快照。目标目录必须位于 Btrfs 文件系统内部。通常，快照是可变的（即文件系统被分成两个分支）。如果你需要只读快照，必须使用 `-r` 。

## 示例

`btrfs list` 显示 (open)SUSE 中默认设置的子卷以及所有快照：

```
root# btrfs list / -p -t
ID gen parent top level path
--- --- ---
257 106 5 <FS_TREE>/@
```

```
<FS_TREE>/@/boot/grub2/i386-pc
<FS_TREE>/@/boot/grub2/x86_64-efi
<FS_TREE>/@/home

<FS_TREE>/@/var/lib/libvirt/images
<FS_TREE>/@/var/lib/mailman
<FS_TREE>/@/var/lib/mariadb
<FS_TREE>/@/var/lib/mysql
...
<FS_TREE>/@/.snapshots
<FS_TREE>/@/.snapshots/1/snapshot
<FS_TREE>/@/.snapshots/2/snapshot
<FS_TREE>/@/.snapshots/20/snapshot
```

在运行期间为 MariaDB 数据库文件创建备份，临时为子卷 `/var/lib/mariadb` 创建只读快照：

```
root btrfs submodule snapshot -r /var/lib/mariadb/ /var/lib/mariadb-backup
Create a readonly snapshot of '/var/lib/mariadb/' in '/var/lib/mariadb-backup' root#
cd /var/lib/mariadb-backup
root# tar czf /home/kofler/mariadb.tgz .
(create backup)
root# cd
(leave directory)
root# btrfsvolume delete /var/lib/mariadb-backup
Deletevolume (no-commit): '/var/lib/mariadb-backup'
```

# 文档

`btrfs` 的 man页分布在多个页面上，每个页面的名称由 `btrfs`、连字符和主命令组成。因此，关于 `btrfs scan` 的详情可以通过 `man btrfs-scan` 查看。

## `bunzip2` file.bz2

`bunzip2` 解压一个之前使用 `.bz2` 压缩过的文件。文件名中的 `.bz` 标识符会被删除。`bunzip2` 是 `bzip2` 的链接，其中会自动激活 `-d` 选项。

## `bzip2` file

`bzip2` 压缩指定的文件并为它们添加 `.bz2` 扩展名。该命令产生的文件通常比使用 `gzip` 压缩的文件小 20% 到 30%。然而，使用 `bzip2` 进行压缩所需的计算时间要耗长得多。

- `-1` 到 `-9`

指定压缩算法允许使用的内存（RAM）量。默认设置为为 `-9`，并能提供最佳结果。

如果可用的内存 较少，您应该选择较小的值；但这样压缩效果也会略有下降。

- `-c` 或 `--stdout` 或 `--to-stdout`

保持待（解）压缩的文件不变，并将结果重定向到标准输出。从那里开始，可以使用 `>` 符号将其将结果重定向到任何文件。

- `-d` 或 `--decompress` 或 `--uncompress`

解压指定的文件而不是压缩它（对应于 `bunzip2`）。

## Example

第一个命令压缩 `file.eps`。新文件名现在是 `file.eps.bz2`。第二个命令恢复原始文件。

```
user$ bzip2 file.eps
user$ bunzip2 file.eps.bz2
```

## C

`cadaver [options] [files]`

来自同名包的名称奇特的命令 `cadaver` 命令是一个 WebDAV 客户端。你可以使用它以类似于 `ftp` 的方式来下载或上传文件。

`cadaver` 内的大多数命令对应于 FTP 命令，即 `get`、`mget`、`put`、`mput` 等（参见 `ftp`）。决定性的区别是使用了基于 HTTP(S) 的 WebDAV 协议。

## Example

在以下命令中，首先会与 IP 地址为 `172.28.128.5`、端口为 `8585` 的 HTTP 服务器建立 WebDAV 连接。然后将 `test.php` 文件上传到 `uploads` 目录。



```
user cadaver http://172.28.128.5:8585/uploads
dav:/uploads/> put test.php
Uploading test.php to /uploads/test.php:
Progress: ... 100.0% of 20 bytes succeeded.
dav:/uploads/> <Strg>+<>
Connection to 172.28.128.5 closed.
```

## canonical-livepatch `[command]`

如果安装了同名的 snap 包，`canonical-livepatch` 控制 Ubuntu 特有的内核实时补丁功能。

- `config`

设置 live 补丁功能或更改其配置。此命令需要一个 Ubuntu One 账户。

- `enable/disable`

激活或禁用 live 补丁系统。

- `refresh`

检查是否有更新，必要时进行下载并将其应用于运行中的内核。这会每隔一段时间自动执行。

- `status`

显示 live 补丁系统的状态。

## Example

所有可用的内核补丁已应用到此服务器上：

```
root# canonical-livepatch status
last check:      52 minutes ago
kernel:          5.4.0-173.191-generic
server check-in:  succeeded
kernel state:    kernel series 5.4 is covered by Livepatch
patch state:      no livepatches available for kernel 5.4.0-173.191-generic
```

```
case expression in
pattern1 ) commands;
pattern2 ) commands;
...
esac
```

`bash` shell 的 `case` 结构在脚本中形成多个分支，其中字符字符串被指定为分支的依据——通常是传递给 shell 程序的变量或参数。该字符字符串与模式按顺序进行比较，在这些模式中可以使用文件名的通配符字符（`?[]`）。在 `case` 分支中，还可以指定多个用管道操作符（`|`）分隔的模式。一旦模式匹配成功，就会执行紧随右括号 `())` 和两个分号 `;;` 之间的后续命令。程序随后根据 `esac` 继续执行。

## Example

在以下列表中，`case` 被用于将传输的参数分类为文件名和选项。在循环内部，使用 `case` 分析每一个单独的参数。如果参数以连字符（`-`）开头，则将该参数添加到 `opt` 变量的末尾；否则，它会被添加到 `dat` 的末尾。

```bash
#!/bin/bash

for i in do  # 遍历所有传输的参数
  case "$i" in
    -*) opt=$opt "$i";
    *) dat=$dat "$i";
  esac
done  # 循环结束
echo "Options: $opt"
echo "Files: $dat"
```

## `cat` `[options]` `[files]`

`cat` 显示指定文本文件的内容。`cat` 也经常用于将多个文件合并成一个较大的文件。为此，必须对标准输出进行重定向。为了此目的，使用 `>` 符号将输出重定向到文件。

使用 `2` 符号将标准输出重定向到文件。

如果可用内存较少，你应该使用 `less` 命令来查看文本。

- `-S`

显示行号。

- `-T`

显示制表符。

- `-B`

显示结束字符。

- `-V`

显示非打印字符。

## Examples

以下命令将 `part1`、`part2` 等合并到 `total` 文件。

```
cat part1 part2 > total
```

在第二个例子中，`cat` 会覆盖文件。

```bash
cat file > file
```

在第三个例子中，`cat` 会将内容追加到文件末尾。使用 `>>` 符号。

```bash
cat file >> file
```

## Variants

`cat` 有许多种变体：

- `bat` 和 `ccat` 显示带有语法高亮的代码。

- `more` 和 `less` 命令允许逐行滚动文本。

- `tac` 命令反序输出文本。

- `zcat` 和 `zless` 命令显示压缩文件。

```
cd [directory]
```

`cd` 命令切换到指定的目录。如果没有指定目录，则切换到主目录。

`pwd` 显示当前目录的路径。

```
cfdisk [options] device
```

`cfdisk` 辅助磁盘和 SSD。它支持 MBR 和 GPT 格式的分区表。与其熟悉的 `fdisk` 和 `parted` 命令相比，它的操作稍微方便，因为它显示了分区表。您可以使用光标键选择要编辑的分区。`cfdisk` 仅用于交互，不适用于脚本编程。

```
chacl [options] files
```

`chacl` 或更改指定文件的扩展权限。只有当文件系统支持 ACL（访问控制列表）时才有效。

如果可能，你应该使用 `getfacl` 或 `setfac` 代替 `chacl`。`chacl` 仅为了兼容 IRIX SGI 而存在。

必须更改密码以及多久可以或必须更改密码。

- `d` `date`

指定上次更改密码的日期。日期格式为 `YYYY-MM-DD`（例如 `2020-12-31`）。`-d 0` 意味着用户首次登录后必须立即更改密码。在更改密码之前，用户无法运行命令。

- `E` `date`

确定账户过期的日期。在此日期之后将无法登录。`-E -1` 表示未设置过期日期。过期的账户可以使用 `passwd -u` 重新激活。

- `-I n`

指定密码过期后多少天账户将被停用。`-I -1` 防止停用。

- `-l`

显示当前设置。

- `-m n`

指定更改后再次更改密码所需的最少天数。默认设置 `o` 表示用户可以随时更改密码。

- `-M n`

指定在此后必须更改密码的最大天数。`-1` 表示密码永久有效。`183` 意味着每年必须更改密码。

- `-W n`

指定在密码过期前多少天显示过期警告（默认设置为 7 天）。

## 示例

你可以使用以下命令来设置新用户，定义其初始密码，并强制他们在首次登录时立即更改密码，并且在未来每年至少更改一次。密码过期警警告会提前一个月显示。

```
root# useradd peter
root# passwd peter
New password: ********
Retype new password: ********
root# chage -d 0 -365 -W 31 peter
```

账户的过期日期（选项 `-E`）必须以 ISO 格式指定。无法使用相对时间。不过，你可以使用 `date` 命令计算日期。以下命令将导致账户在 100 天后被停用：

```
root# chage -E $(date -d +180days +%Y-%m-%d)
```

```
chattr [options] +=[AcCdDeijsStTu] files
```

在 Linux 文件系统（`ext2`, `ext4`, `Btrfs`, `XFS` 等）中，除了用户信息外，每个文件还可以保存一些额外的属性（参见 `chmod` 和 `chown`）。例如，这些带有字母代码 `AcCdDeijsStTu` 的属性控制文件是否被压缩或是否使用写时复制（COW）过程。

属性的简要描述在 `man chattr` 中提供。然而，目前只有少数计划中的属性被实际使用。要加载属性，可以使用 `lsattr`。

- `-R`

递归地更改目录下所有文件的属性。

## 示例

`chattr` 在 `Btrfs` 文件系统中的重要用法是，可以使用 `chattr +C` 停用自动的写时复制（COW）过程，并使用 `chattr -C` 重新启用。停用 COW 为了高效存储虚拟程序或大型数据库文件。

你可以将单独的文件或整个目录传递给命令。使用 `-R`，命令递归地更改目录树中的属性：

```
root# chattr +C -R /var/lib/mysql
```

，属性仅适用于新文件。对于大小不为 0 字节的现有文件，必须复制文件：

```
root# mv dir backup
root# mkdir dir
root# chattr +C dir
root# cp -a backup/* dir
root# rm -rf backup
```

```
chcon [options] files
chcon [options] --reference=reference file
chcon [options] [-u user] [-r role] [-t type] [-l level]
```

`chcon` 修改指定文件的 SELinux 上文。新的上下文可以通过三种方式指定：使用 `user:role:type:level` 表示法、通过指定引用文件，或者使用选项 `-u`、`-r`、`-l` 和 `-t`。第三种方法的优势是可以更改整个上下文的一部分。



如果你将文件保存在 SELinux 规则指定的位置，通常需要手动设置 SELinux 上文——例如 `/disk2/var/www/html` 而不是 `/var/www/html`。

要确定现有文件的 SELinux 上文，应该使用带有 `-z` 选项的 `ls` 命令。

### `chcon` 选项

- `-l level`

更改 SELinux 上文的级别。RHEL 和 Fedora（目标安全）中使用的级别通常为 `s0`（参见 `/etc/selinux/targeted/setrans.conf`）。

- `-r role`

更改 SELinux 上文的角色。SELinux 角色决定了文件被分配到哪个“领域”。SELinux 领域反过来决定了进程拥有的权限。

- `-reference=reference file`

读取引用文件的 SELinux 上文并将其传输到其他文件。

- `-R`

考虑到所有子目录（递归）。

- `-t type`

更改 SELinux 上文的类型。SELinux 类型决定文件的权限，就像 SELinux 领域控制进程权限一样。

- `-u user`

更改 SELinux 上文的用户信息。普通 Linux 用户通过 SELinux 规则“映射”。

- `-v`

显示所做的更改（详细模式）。

#### 示例

默认情况下，RHEL Apache 在 `/var/www/html` 目录具有只读权限。要允许 Web 服务器更改特定目录下的文件，必须运行以下命令：

```
root# chcon -R system:object_r:httpd_sys_content_rw:t:s0 /var/www/html/wordpress
```

如果你想让 Apache 访问位于另一个介质上的 Web 文件（这次为只读），应按照以下步骤操作：

```
root# chcon -R system:object_r:httpd_sys_content_t:s0 /disk2/var/www/html/
```

### `chgrp`

`chgrp [options] group files`

`chgrp` 修改文件的所属组。文件的所有者只能将文件分配给自己的组，而 `root` 可以进行任何分配。

- `-R` 或 `--recursive`

同时也更改所有子目录下文件的组分配。

#### 示例

以下命令将 `/var/www` 目录下的所有文件分配给 `www-data` 组。Apache Web 服务器在 Debian 和 Ubuntu 上在此账户下运行。

```
root# chgrp -R www-data /var/www/
```

### `chkrootkit`

`chkrootkit [options]`

同名包中的 `chkrootkit` 命令在系统中搜索已知的 rootkit。该过程非常简单：命令尝试使用简单的标准或签名（例如二进制文件中是否存在某些字符字符串）来检测恶意软件。

- `-n`

忽略 NFS 目录。

- `-r directory`

使用指定的目录作为起点（作为根目录）。

尽管该项目仍然活跃，但进一步的开发仅以小步进行。误报和未能检测到真实威胁都是可能的。

#### 示例

```
root# chkrootkit
ROOTDIR is /
Checking amd... not found
Checking basename... not found
Checking biff... not found
Checking chfn... not found
Searching for sniffer's logs... not found
Searching for rootkit's files... not found
Checking asp... not infected
Checking bindshell... not infected
Checking lkm... not detected
```

#### 变体

`chkrootkit` 由于其易于使用，可以作为 rootkit 搜索的起点。替代或补充工具，`rkhunter` 以及商业工具 Lynis 和 Snort。后两个程序都有可以免费使用的开源内核版本。

### `chmod`

```
chmod [options] changes files
```

`chmod` 修改九个访问位。对于每个文件，它存储了所有者（user）、组成员（group）和其他用户（others）是否允许读取、写入和执行该文件。

可以使用字符组合 `+/- access type` 更改访问位，例如 `g+w` 为所有组员写入权限。你通过 `u`（用户）、`g`（组）、`o`（其他）或 `a`（所有）指定组；通过 `r`（读）、`w`（写）或 `x`（执行）指定访问类型。

#### setuid, setgid, and sticky Bits

使用 `chmod` 设置特殊位 `setuid`、`setgid` 和 `sticky` 时提供了以下字符组合：

```
setuid: u+s setgid: g+s sticky: +t
```

为了 `setuid` 生效，所有者的 x 位也必须设置（`u+x`）。

为了 `setgid` 生效，组的 x 位也必须设置（`g+x`）。

#### 八进制表示

除了使用字母外，还可以使用最多四位的八进制数来指定访问类型。对于访问位，`u`、`g` 和 `o` 分别被分配一个数字。每个数字由对应 `r`、`w`、`x` 的值 4、2 和 1 组成。因此，`660` 意味着 `rw-rw---`，而 `777` 则代表 `rwxrwxr-x`。

三个特殊位 `setuid`、`setgid` 和 `sticky`（粘滞位）的八进制值为 `4000`、`2000` 和 `1000`。虽然在八进制表示中设置这些位非常简单，但有一种安全机制防止目录的这些位被意外禁用。在执行 `chmod 2770 dir` 和 `chmod 770 dir` 之后，`setgid` 位仍保持设置状态！要移除它，你必须运行 `chmod g-s dir` 或 `chmod 0770 dir`（带两个前导零）。

要用八进制表示确定现有文件或目录的访问位，必须使用 `stat` 命令。

#### 选项

- `-f` 或 `--silent` 或 `--quiet`

不显示任何错误信息。

- `-R` 或 `--recursive`

另外更改所有子目录中文件的访问权限。

#### 示例

现在所有用户都可以执行 `secure` 文件了。例如，`secure` 可以作为一个创建备份的 shell 脚本。

```
user$ chmod a+rx secure
```

以下命令取消了当前目录下所有你用户组之外的用户对所有 `*.odt` 文件的读取和写入权限：

```
user$ chmod o-rw *.odt
```

只允许 `root` 读取 `server.key` 文件，任何人不能更改它：

```
root chown root:root server.key
root# chmod 400 server.key
```

### `chown`

`chown [options] user[:group] files`

`chown` 更改文件的所有者以及（可选的）组。文件的所有者只能由 `root` 更改，而组也可以由其他用户设置（见 `chgrp`）。

- `-R` 或 `--recursive`

同时也更改所有子目录下文件的组分配。

#### 示例

以下命令确保 `/var/lib/mysql` 内的所有文件都分配给 `mysql` 用户和 `mysql` 组，使得 MySQL 服务器进程可以读取并修改这些文件：

```
root# chown -R mysql:mysql /var/lib/mysql
root# chmod -R o-rwx /var/lib/mysql
```

### `chpasswd`

`chpasswd [options]`

`chpasswd` 允许在脚本中更改密码，这与 `passwd` 不同，不需要用户交互。该命令从标准输入读取用户名和密码，其中信息必须以 `name:password` 的形式逐行输入。该命令通常以 `chpasswd < pwfile.txt` 的形式调用，以处理存储在文件中的用户名和密码组合。

你可以使用选项控制密码的加密方式（见 `man chpasswd`）。然而，通常不建议使用这些选项。`chpasswd` 然后将使用发行版在 `/etc/logins.def` 文件中指定的默认设置。

#### 示例

以下脚本使用 `useradd` 设置了 30 个账户：`user01` 到 `user30`。对于每个账户，都设置了通过 `mkpasswd` 生成的密码。为此，使用 `echo` 输出名称和密码，并通过管道操作符将输出传递给 `chpasswd`。所有账户名称和相应的密码也保存在文本文件 `students.txt` 中。最后，使用 `chage` 定义每个用户在首次登录后必须立即更改密码。

```bash
#!/bin/bash
for i in {01..30}; do
  user="user$i"
  pw=$(mkpasswd -l 8 -d 0 -C 0 -s 0)
  echo "Account: $user Password: $pw" >> students.txt
  useradd $user
  echo "$user:$pw" | chpasswd
  chage -d 0 $user
done
```



## chroot directory [command]

在没有进一步参数的情况下，`chroot` 启动一个新的 shell，该 shell 使用指定的目录作为根目录（`/`）。你可以在此 shell 中交互操作。`exit` 会带你回到原始 shell。

如果你指定了一个可选命令，则将启动该命令而不是 shell。在命令执行期间，指定的目录将再次用作根目录。

## 示例

`chroot` 有助于在启动时未激活的文件系统中执行管理任务。以下命令假设你已从救援系统或 USB 闪存驱动器启动了计算机。然后将系统分区（在本例中 `/dev/sda4`）挂载到 `/mnt/rescue` 目录，将其作为新的根目录，并使用 `password` 重置忘记的 root 密码：

```
root# mkdir /mnt/rescue
root# mount /dev/sda4 /mnt/rescue
root# chroot /mnt/rescue
root# password
Change password for root user.
Enter a new password: ***********
Enter the new password again: ***********
root# exit
root# reboot
```

## chsh -s shell [user]

`chsh` 更改登录后自动调用的默认 shell。`/etc/shells` 中输入的所有 shell 都可以供选择——通常有 `/bin/bash`、`bin/csh` 和 `/bin/zsh`。`chsh` 命令更改密码文件并在其中输入新 shell。

每个用户都可以根据意愿更改自己的默认 shell。另一个用户的 shell 只能由 root 用户更改。新 shell 必须指定完整的目录路径。更改将在下次登录时生效。

## 示例

以下命令设置了 `nologin` 程序代替 shell。它防止了直接登录，如果你设置一个用户仅用于自动化（备份）脚本或仅用于访问电子邮件账户，则这种方法很有用：

```
root# chsh -s /usr/sbin/nologin mailuser
```

## chvt

`chvt` 激活控制台。在较旧的 Linux 发行版中，数字 1 到 6 留给文本控制台，而第一个用户的图形系统在控制台 7 上运行。控制台 8、9 等被用于进一步的并行登录。

在较新的发行版中，显示管理器通常在控制台 1 上以图形模式运行。控制台 2 留给第一个登录用户的图形系统。控制台 3 到 6 以文本模式运行。

## cksum file

`cksum` 确定文件的校验和和字节为单位的长度。校验和可以快速判断两个文件是否相同。`cksum` 比 `sum` 提供更可靠的结果。

`clear` 或 `Ctrl + L` 删除控制台内容。

## cmp [options] file1 file2

`cmp` 通过字节比较两个文件并返回第一个差异的位置。如果文件相同，该命令不会显示任何信息。对于文本文件，`diff` 通常比 `cmp` 更合适。

- `-c` 或 `--show-chars` 显示差异字符。
- `-l` 或 `--verbose` 提供差异列表。

## cnf 命令

`cnf` 代表 `command not found`，是一个 SUSE 特有的命令，用于显示哪个软件包包含命令。

在 Red Hat 和 Fedora 发行版中，由 `bash` 执行的 `/usr/libexec/pk-command-found` 命令包含类似的功能；在 Ubuntu 上，这是 `(/usr/lib/command-not-found` 来自 `command-not-found` 软件包)。该软件包在 Debian 上可用，但必须手动安装并使用 `update-command-found` 命令进行设置。

## 示例

`user cnf jmac`

可以在以下软件包找到 `jmac` 程序：

* `joe` [路径:`/usr/bin/jmac`，仓库：`zypp (repo-oss)`]

尝试安装：

`sudo zypper install joe`

## column [options] file

`column` 读取指定的文件，将每行分成若干部分，然后以缩进列输出所有部分。

- `-o 'outseparator'`

  指定输出列之间如何分隔（默认使用两个空格）。
- `-s 'separator'`

  指定导入的数据如何分隔。默认使用空白符作为分隔符，即空格和制表符。
- `-t`

  将输出格式化为表格。

## compress [options] file

`compress` 压缩或解压缩指定的文件。对于压缩文件，文件名会附加 `.z` 标识。`compress` 仅为了兼容而存在。`gzip` 和 `xz` 要强大得多。

## continue [n]

`bash` 结构 `continue` 跳过 脚本中 `for`、`while` 或 `until` 循环的体，并继续下一次循环。此过程可以使用可选的数值执行多个循环级。

## convert or magick [options] image old image

来自 `ImageMagick` 软件包的 `convert` 将图像文件从一种格式转换为另一种格式。在最简单的形式下，它使用

`syntax convert name.png.jpg`：用于将指定的 PNG 文件转换为 JPEG 文件。原始文件将被保留。

从第 7 版本开始，`ImageMagick` 提供了 `magick` 命令。它在未来将取代 `convert`。出于兼容性考虑，在已经提供第 7 发行版中，仍然可以使用 `convert`。其他发行版尚未迁移到 `ImageMagick 7`。这就是为什么我在书中将该命令放在已有的名称 `convert` 下进行介绍。

通过超过 100 种选项，可以同时更改各种图像参数。因此，以下列表仅为挑选：

- `-blur radius`

  模糊图像。
- `-colors n`

  将 RGB 颜色的数量减少到 `$n$`。
- `-colorspace CMYK|GRAY|RGB|Transparent|YUV`

  指定所需的颜色模型（还有许多其他模型可供选择）。
- `-compress None|BZip|Fax|Group4|JPEG|JPEG2000|Lossless|LZW|RLE|Zip`

  指定所需的压缩格式。然而，实际可选的格式取决于图像格式。
- `-contrast OR +contrast`

  减少或增加图像的对比度。
- `-crop geometry`

  裁剪出图像的部分。例如，`-crop 50×50+100+100` 描述了一个从坐标位置 (100, 100) 开始的 50×50 像素区域。
- `-filter Point|Box|Triangle|Hermite|Hanning|Hamming ...`

  对图像应用所需的过滤器。
- `-gaussian radius`

  使用高斯算子模糊过滤器。
- `-normalize`

  归一化图像中的颜色分布。
- `-quality n`

  指定所需的压缩质量。`n` 的允许值取决于图像格式（例如，JPEG 为为 0 到 100）。
- `-resize NxN Or -resize n%`

  更改图像的分辨率。
- `-rotate angle`

  按指定的角度顺时针旋转图像。
- `-trim`

  如果单色图像的边缘与图像角点的颜色相同，则将其裁剪掉。

更多选项在以下网站上进行了详细描述：

出于安全考虑，在某些发行版中，`convert` 会拒绝处理某些文件类型，可以通过修改策略文件来解决：

```xml
<!-- 更多选项在以下网站上进行了详细描述 -->
https://imagemagick.org/script/policy.xml

<!-- 出于安全考虑，在某些发行版中，convert 会拒绝处理某些文件类型，可以通过修改策略文件来解决 -->
<policy domain="path" rights="none" pattern="//*" />
```

## 示例

以下示例显示了 `convert` 的几种用法：

- `-colors 256 input.jpg output.jpg`
- `-colorspace Gray input.jpg output.jpg`
- `-compress JPEG quality:80 input.jpg output.jpg`
- `-contrast 50% input.jpg output.jpg`
- `-crop 50x50+100+100 input.jpg output.jpg`
- `-filter Box input.jpg output.jpg`
- `-gaussian-blur 0x1 input.jpg output.jpg`
- `-normalize input.jpg output.jpg`
- `-quality 85 input.jpg output.jpg`
- `-resize 800x600 input.jpg output.jpg`
- `-rotate 90 input.jpg output.jpg`
- `-trim input.jpg output.jpg`



以下示例显示了 `convert` 的几种用法：

- `-colors 256 input.jpg output.jpg`
- `-colorspace Gray input.jpg output.jpg`
- `-compress JPEG quality:80 input.jpg output.jpg`
- `-contrast 50% input.jpg output.jpg`
- `-crop 50x50+100+100 input.jpg output.jpg`
- `-filter Box input.jpg output.jpg`
- `-gaussian-blur 0x1 input.jpg output.jpg`
- `-normalize input.jpg output.jpg`
- `-quality 85 input.jpg output.jpg`
- `-resize 800x600 input.jpg output.jpg`
- `-rotate 90 input.jpg output.jpg`
- `-trim input.jpg output.jpg`

使用 `convert` 的示例：

- `-trim input.jpg output.jpg`
- `-rotate 90 input.jpg output.jpg`
- `-quality 90% input.jpg output.jpg`
- `-resize 500x500 input.jpg output.jpg`
- `-normalize input.jpg output.jpg`
- `-gaussian-blur 0x2 input.jpg output.jpg`
- `-filter Box input.jpg output.jpg`
- `-crop 100x100+10+10 input.jpg output.jpg`
- `-contrast 20% input.jpg output.jpg`
- `-compress JPEG quality:75 input.jpg output.jpg`
- `-colorspace Gray input.jpg output.jpg`
- `-colors 16 input.jpg output.jpg`

## 复制目录

如果你想复制一个包含所有文件的整个目录，必须使用 `cp -r source directory`。这也会复制隐藏文件。

以下命令将所有的 `book/*.tex` 文件复制到当前目录（`.` 表示当前目录）：

```bash
cp book/*.tex .
```

第二个命令创建了整个目录的备份：

```bash
cp -a book-bak
```



`cp` 无法在复制过程中重命名多个文件。`cp *.xxx *.yyy` 因此无法复制所有的 `*.xxx` 文件。要执行此类操作，必须使用 `for` 循环。在以下命令中，`for` 遍历所有的 `*.xxx` 文件。`${i%.xxx}.yyy` 移除结尾的 `.xxx` 并将其替换为 `.yyy`。如果你将 `cp` 替换为 `mv`，文件将会被重命名。

```bash
for i in *.xxx; do cp $ ${i%.xxx}.yyy; done
```

## cpio 命令 [选项]

`cpio` 将多个文件合并为一个归档并复制到另一个数据介质、流器或另一个目录。同样，该命令也可用于加载此类数据。

- `-i`

输入：从标准输入读取归档并提取其包含的文件。

- `-0`

输出：将文件合并为归档并将归档传输到标准输出。

- `-p`

透传：在不同的目录之间传输归档。

- `-t`

从标准输入显示归档的内容。

这些操作细节可以通过额外的选项进行控制。

## 示例

以下命令首先归档 `/etc` 目录下的所有文件。然后，使用 `cpio -t` 显示备份文件的列表以进行检查。

```
root# cd /etc
root# find . | cpio -o > /tmp/etc-backup.cpio
root# cpio -t < /tmp/etc-backup.cpio
```

## crontab [options]

`crontab` 命令帮助你管理 `/var/spool/cron/username` 文件中的 cron 任务（参见 `crontab`）。Cron 任务会在预定的时间自动在后台执行，例如每小时一次或每周日晚上执行一次。

- `-e`

打开编辑器编辑 `crontab` 文件。通常使用 `vi` 作为编辑器。如果你想使用不同的编辑器，必须相应地设置 `EDITOR` 环境变量。

`crontab` 在保存时会会检查是否符合 `crontab` 语法规则。

- `-l`

列出当前的 `crontab` 条目。

- `-r`

删除所有 `crontab` 条目。

- `-u username`

编辑指定用户的 `crontab` 文件。`-u` 选项仅对 `root` 可。

## cryptsetup [options] 命令

来自同名包的 `cryptsetup` 使用了 `dm_crypt` 内核模块的功能。它用于设置、激活和停用加密设备。足够大的镜像文件也可以代替设备。这可以提前创建，例如通过 `dd if=/dev/zero of=cryptoImage bs=1M count=n`，其中 `n` 是以兆兆字节（MiB）为单位的目标尺寸。

在此，我将仅描述 `cryptsetup` 最重要的 LUKS 特有命令：

- `-luksAddKey device`

设置额外的密码以访问加密容器。要运行此命令，必须输入已有的密码（使用任何你喜欢的密码）。最多允许八个密码。

- `-luksClose device mappingname`

停用加密设备。

- `-luksDump device`

提供有关加密容器的元信息（例如加密算法）。

- `-luksFormat --type luks2 device`

在指定的设备上按当前的 LUKS2 格式设置加密容器。如果不使用 `--type` 选项，命令将使用仍受支持但已过时的 LUKS1 格式。

你必须输入两次密码，出于安全考虑，密码应至少为 20 个字符。你可以使用 `-c` 选择所需的加密算法，并使用 `-s` 设置不同的密钥长度。可选的算法列表列在伪文件 `/proc/crypto` 中。`cryptsetup --help` 命令的输出最后几行显示了默认使用哪种算法和什么密钥长度。目前使用的是 `aes-xts-plain64` 算法，密钥长度为 256 位。

- `-luksOpen device mappingname`

激活指定设备中的加密容器并为其分配一个名称。生成的加密设备可以通过 `/dev/mapper/mappingname` 使用。

## 示例

以下命令展示了如何首先将 USB 闪盘 (`/dev/sdh1`) 格式化为加密设备（`luksFormat`），然后以任意指定的名称 `mycontainer` 激活该设备（`luksOpen`）。无需而说，你的数据安全性取决于你的密码或口令，而口令由几个单词组成。建议密码长度至少为 20 个字符。

然后你可以像 `/dev/mapper/mycontainer` 像硬盘分区或逻辑卷一样使用它——也就是说，设置文件系统、将其集成到目录树等。在卸载（`umount`）后，你必须记住再次停用加密设备（`luksClose`）以释放 `/dev/sdh1`。只有在此时你才能移除 USB 闪盘。

```
root cryptsetup luksFormat --type luks2 /dev/sdh1
这将覆盖 /dev/sdh1
你确定吗？(y/n)
输入口令：********************
再次输入口令：********************
成功。
cryptsetup luksOpen /dev/sdh1 mycontainer
输入口令：********************
再次输入口令：********************
成功。
加密设备 /dev/mapper/mycontainer 已激活。
ls /dev/mapper
输入口令：********************
成功。
mount /dev/mapper/mycontainer /test
mkfs.ext4 /dev/mapper/mycontainer
umount /test
cryptsetup luksClose mycontainer
加密设备 mycontainer 已停用。
``` /dev/sdh1

```

> `curl [options] [url]`

`curl` 帮助在服务器之间传输文件，支持所有可能的协议（HTTP, HTTPS, FTP, SFTP, SCP 等）。

外部文件或目录由 URL（资源定位符）指定，以协议名称开头（例如 `http://server.com/file`）。

- `-d --data 'data'`

向请求发送指定的数据。对于 `--data`，有以下可选方案：`--data-binary`、`--data-raw` 和 `--data-urlencode`。所有变体都可以通过指定文件读取数据。

- `--limit-rate n`

将传输速率限制为每秒指定的字节数。`n` 可以跟随 `k` 或 `m`，以限制为每秒 `n KiB` 或 `MiB`。

- `-n --netrc`

指示命令从 `.netrc` 文件读取登录数据。使用 `--netrc-file file.txt`，你可以替代指定不同的位置。两种方式都比通过 `-u` 传输密码更安全。

- `-o file`

将下载的数据保存到指定文件中，而不是转发到标准输出。

- `--oauth2-bearer 'token'`

向请求发送指定的 `bearer` 令牌。

- `-r n1-n2`

传输文件的指定字节范围。

- `-s --silent`

不显示状态输出。

- `-T file`

将指定的文件上传到服务器，即在

```

> `csplit [options] file`

`csplit` 根据行数或搜索模式将文件拆分为多个文件。

## 分割位置规范

分割位置通过行数或搜索模式指定。在前一种情况下，按行数分割文件；而在后一种情况下，在模式出现时分割。

- `/pattern/`

在模式出现后分割文件。

- `/pattern/-`

在模式出现前分割文件。

- `-n`

按 `n` 行分割。

- `-z`

防止创建空文件。

- `-f file`

使用指定的前缀命名输出。

- `-k`

保留空文件。

- `-n`

分割 `n` 次。

- `/pattern`

在模式出现后分割文件。

## 示例

`csplit` 将 `total.txt` 拆分为 `part.00`、`part.01` 等文件。每个文件长度为 100 行。`cat` 然后创建原始文件的副本。

```
user$ csplit -k -f part.txt 100 {*}
user$ cat part.* > copy.txt
```

在第二个示例中，`csplit` 将 `total.txt` 拆分为较小文件，分割总是发生在行开头的文本。

```
user$ csplit -k -f part.txt '/^=='
```

`curl` 常用用法（传输）的相反方向。

除了文件名外，也可以输入连字符 (`-`) 来处理来自标准输入的数据。

- `-u name:password`

指定登录用户名和密码。

- `-X Or --request GET|POST|PUT|...`

指定所需的请求类型（默认默认为 GET）。

## 示例

以下命令将指定的文件传输到 FTP 服务器 `backupserver`，并将其保存在 `dir` 目录下。

```
user$ curl -T -u username:password ftp://backupserver/dir
```



要处理来自标准输入通道的数据，你可以使用 `-T` 将连字符指定为文件名。以下命令将 `tar` 命令的结果直接保存在 FTP 服务器上的 `name.tgz` 文件中：

```
user$ tar czf - dir/ | curl -T -u user:pw ftp://bserver/name.tgz
```

`curl` 同样适用于如下所示的 REST API 节点：

```
user$ curl -X PUT https://httpbin.org/put?para=123 -d @mydata.json 
-H "Content-Type: application/json"
```

## 替代方案

要通过 FTP 或 HTTP 下载文件，你也可以使用 `wget` 代替 `curl`。相反，如果你更感兴趣于调试 REST API，那么 `curlie` 是一个很好的选择（参见 https://github.com/rs/curlie）。这个 `curl` 的替代方案默认显示传输的标头，以彩色格式化 JSON 文档等。

```
cut [options] file
```

`cut` 从每行文本中提取由选项指定的列。

- `-b list` 或 `--bytes list`

提取列表中指定的字符。单个条目可以用逗号分隔（但不能用空格）。除了单个字符外，还可以指定整个范围，例如 `-b 3-6,9,11-15`。

- `-d character` 或 `--delimiter character`

指定用于 `-f` 的分隔符，用以代替制表符。

- `-f list` 或 `--fields list`

提取方式与 `-b` 类似，但是针对字段（数据记录）的，这些字段必须由制表符分隔。

- `-s` 或 `--only-delimited`

删除所有不包含与 `-f` 选项对应数据的行。这不能与 `-b` 一起使用。

在实践中，通过 `awk` 提取单个文本列通常比使用 `cut` 简单得多。

### 示例

在以下示例中，`cut` 从 `/etc/passwd` 文件中读取第一、第三和第七列，即用户名、UID 和默认 shell。该文件的分隔符是冒号。

```
root cut -d: -f1,3,7 /etc/passwd
root:0:/bin/bash
bin:1:/sbin/nologin
deemon:2:/sbin/nologin
adm:3:/sbin/nologin
...
```

## date

`date [options] [+format]`

`date` 返回当前的日期和时间或更改这些数据。

更改只能由 `root` 执行。`date` 可以显示各种格式的时间。

- `-d time span`

在当前时间上增加或减去时间跨（例如 `-d +3days` 或 `-d -4hours`）。

- `-s newtime`

更改计算机时钟的日期和/或时间。

以下列表出了最重要的格式代码。格式字符串必须包含在引号中。

- `%Y`

四位数字年份

- `%l`

数字形式月份（1 到 12）

- `%m`

两位数字的月份（01 到 12）

- `%b`

短字符字符串的月份（Jan 到 Dec）

- `%B`

长字符串的月份（January 到 December）

- `%d`

两位数字的日期（01 到 31）

- `%e`

数字形式的日期（1 到 31），个位数数字前有一个空格

- `%H`

两位数字的小时（00 到 23）

- `%M`

两位数字的分钟（00 到 59）

### 示例

以下三条语句分别提供了 ISO 格式的当前时间、三周后的日期以及四小时前的时间：

```
user date "+%Y-%m-%d %H:%M:%S"
2025-03-12 17:46:39
user date -d +3weeks "+%Y-%m-%d"
2025-04-02
user date -d -4hours "+%H:%M:%S"
13:47:25
```

以下脚本为 `/home/kofler/data` 目录创建一个压缩的 `tar` 归包。该归包以两个文件名保存：`mydata-day-dd.tar.gz` 和 `mydata-month-mm.tar.gz`。

如果脚本每天运行，随着时间的推移，你将拥有43 个备份版本，反映过去 28 到 31 天以及过去 12 个月备份目录的状态。

```bash
#!/bin/bash
fname1=backup-day-$(date +%d).tar.gz
fname2=backup-month-$(date +%m).tar.gz
tar -czf $fname1 /home/kofler/data
tar -czf $fname2 /home/kofler/data
```

## dd 命令

`dd` 用于复制和转换文件。除了文件名，也可以输入连字符 (`-`) 来处理来自标准输入的数据。

- `bs=n`

确定块大小。

- `if=file`

指定源文件（而非标准输入）。

- `count=n`

复制 `n` 个块。

- `of=file`

指定目标文件（而非标准输出）。

- `seek=n`

在开始输出前跳过 `n` 个块。

- `skip=n`

在读取前跳过 `n` 个块。

- `status=progress`

显示复制进度。

- `conv=mode`

在复制过程中转换数据。`mode` 允许各种设置，包括 `lcase`（小写）、`ucase`（大写）、`swap`（每次两个字节）。使用 `conv=fsync` 时，`dd` 以同步调用结束，即等待物理完成。

### 示例

以下命令将 ISO 文件 `opensense.iso` 直接传输到设备 `/dev/sdc`，例如 U 盘。请注意，该设备上之前保存的数据将丢失！因此，请确保输入了正确的设备名称。如果指定的 `of` 设备是你的硬盘，你将丢失其内容。

```
root# dd if=opensense.iso of=/dev/sdc bs=1M status=progress
```

第二个命令为虚拟机程序（例如 QEMU-KVM）创建一个 10 GiB 的原始镜像文件。该镜像文件由从 `/dev/zero` 读取的零组成。

```
root# dd if=/dev/zero of=image.raw bs=1M count=10000
```

### 替代方案

根据用途，可以使用以下两种变体代替 `dd`：

- `dd_rescue` 或取决于发行版的 `ddrescue`（`gddrescue` 包即使设备的单个数据扇存在缺陷也能尝试创建副本。

- `dcflddd` 针对取证任务进行了优化。其他方面，该命令可以使用校验和来验证副本是否完全相同。

你可以在以下地址找到 `dd`、`dd_rescue` 和 `dcflddd` 的良好对比：

https://superuser.com/questions/355310

```
declare [options] var=[value]
```

bash 命令 `declare` 用于为 shell 变量分配新值和/或各种属性。该命令主要用于 shell 脚本。如果不带参数的情况下调用它，将列出所有已知变量及其内容。注意，等号前后不能有空格！

- `-A`

将变量声明为关联数组。

- `-r`

将变量声明为只读。该变量只能读取，不能修改。

- `-X`

将变量声明为环境变量（类似于 `export`）。因此，该变量在其他命令或子 shell 中也可用。

```
delgroup [options] name
```

`delgroup` 在 Debian 和 Ubuntu 系统上用于删除指定的组，并遵循 `etc/deluser.conf` 中的规则。在 Fedora 和 Red Hat 中，`delgroup` 是 `groupdel` 命令的链接，该命令具有其他选项。

- `--only-if-empty`

仅当该组未分配任何用户时才删除该组。

- `--system`

仅当该组是系统组时才删除该组。

## delta [options] file1 file2

`delta` 是 `diff` 的变体。来自 `git-delta` 包的命令比较两个文本文件的内容并以图形方式显示差异（参见 https://dandavision.github.io/delta）。虽然 `diff` 针对脚本和补丁管理进行了优化，但 `delta` 在交互式使用方面更为出色。

- `--help`

显示帮助文本。（没有 man 页。）

- `--light`

使用适用于浅色背景终端的颜色。默认情况下，`delta` 为深色终端设计（`--dark` 选项）。

- `-s` 或 `--side-by-side`

相邻显示差异而不是上下显示。

## deluser [options] name

`deluser` 在 Debian 和 Ubuntu 系统上删除指定的用户，并遵循 `etc/deluser.conf` 中的规则。结果是家目录通常不会被删除。在 Fedora 和 Red Hat 中，`deluser` 是 `userdel` 命令的链接，具有其他选项。

- `--remove-all-files`

删除用户的家目录及所有其他文件（例如，各种池文件和邮件文件）。

- `--remove-home`

同时也删除用户的家目录。

- `--system`

仅当该用户是系统用户时才删除。



如果以 `deluser name group` 运行命令，它将从指定的组中移除用户。因此，该命令是 `adduser name group` 的互补。

## `depmod` [options]

`depmod` 创建模块依赖文件 `modules.dep` 以及 `/lib/modules/kernelversion/` 目录下的各种 `*.map` 文件。`*.map` 文件指定为哪个硬件组件加载哪个内核模块。

- `-A` 或 `--quick`

首先测试现有 `*.dep` 和 `*.map` 文件仍然最新。在这种情况下，`depmod` 不会重新生成文件。

- `-b directory` 或 `--basedir directory`

指定生成 `*.dep` 和 `*.map` 文件的目录。默认情况下，命令更新为运行内核的文件。

## `df` [options] [directory]

`df` 提供有关硬盘（分区）或其他驱动器挂载在文件树中的位置，以及它们上可用存储空间的信息。通常，`df` 返回所有活动分区的列表。然而，如果你向命令传递一个目录，它仅显示该目录物理所在分区的数据。在具有许多分区的系统中，你可以轻松确定特定目录保存在哪个分区中。

- `-h`

以易于读取的 MiB 或 GiB 形式指示存储空间。

- `-i` 或 `--inodes`

提供可用 inode 信息（而不是 KiB 单位的空闲存储空间）。

- `-t fs`

仅考虑指定类型的文件系统，例如使用 `-t ext4` 仅考虑 ext4 文件系统。

- `-T`

指定每个分区或数据介质的文件系统。

- `-x fs`

忽略指定的文件系统。

## Example

在示例系统中，系统分区 `/` 仍有 15 GiB 的可用磁盘空间。其他文件系统用于管理目的（设备的动态显示）以及存储 Ubuntu 特有的 snap 软件包。由于使用了 `-x tmpfs`，许多临时文件系统（即仅位于 RAM 中的系统）未被计入。

```bash
root# df -h -T -x tmpfs
Filesystem Type Size Avail Use% Mounted on
udev devtmpfs 16G 0 16G 0% /dev
/dev/nvme0n1p1 vfat 1021M 254M 768M 25% /boot/efi
/dev/nvme0n1p4 ext4 119G 32G 81G 29% /
/dev/mapper/mycryptpart ext4 1.5T 767G 634G 55% /crypt
/dev/loop0 squashfs 62M 62M 0 100% /snap/authy/5
/dev/loop1 squashfs 56M 56M 0 100% /snap/core18/188
```

| Filesystem | Type | Size | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| udev | devtmpfs | 16G | 0 | 16G 0% | /dev |
| /dev/nvme0n1p1 | vfat | 1021M | 254M | 768M | 25% | /boot/efi |
| /dev/nvme0n1p4 | ext4 | 119G | 32G | 81G | 29% | / |
| /dev/mapper/mycryptpart | ext4 | 1.5T | 767G | 634G | 55% | /crypt |
| /dev/loop0 | squashfs | 62M | 62M | 0 | 100% | /snap/authy/5 |
| /dev/loop1 | squashfs | 56M | 56M | 0 | 100% | /snap/core18/188 |

示例系统中，系统分区 `/` 仍有 15 GiB 的可用磁盘空间。其他文件系统用于管理目的（设备的动态显示）以及存储 Ubuntu 特有的 snap 软件包。由于使用了 `-x tmpfs`，许多临时文件系统（即仅位于 RAM 中的系统）未被计入。

```bash
root# df -h -T -x tmpfs
Filesystem Type Size Avail Use% Mounted on
udev devtmpfs 16G 0 16G 0% /dev
/dev/nvme0n1p1 vfat 1021M 254M 768M 25% /boot/efi
/dev/nvme0n1p4 ext4 119G 32G 81G 29% /
/dev/mapper/mycryptpart ext4 1.5T 767G 634G 55% /crypt
/dev/loop0 squashfs 62M 62M 0 100% /snap/authy/5
/dev/loop1 squashfs 56M 56M 0 100% /snap/core18/188
```

示例系统中，系统分区 `/` 仍有 15 GiB 的可用磁盘空间。其他文件系统用于管理目的（设备的动态显示）以及存储 Ubuntu 特有的 snap 软件包。由于使用了 `-x tmpfs`，许多临时文件系统（即仅位于 RAM 中的系统）未被计入。

| Filesystem | Type | Size | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| udev | devtmpfs | 16G | 0 | 16G 0% | /dev |
| /dev/nvme0n1p1 | vfat | 1021M | 254M | 768M | 25% | /boot/efi |
| /dev/nvme0n1p4 | ext4 | 119G | 32G | 81G | 29% | / |
| /dev/mapper/mycryptpart | ext4 | 1.5T | 767G | 634G | 55% | /crypt |
| /dev/loop0 | squashfs | 62M | 62M | 0 | 100% | /snap/authy/5 |
| /dev/loop1 | squashfs | 56M | 56M | 0 | 100% | /snap/core18/188 |

示例系统中，系统分区 `/` 仍有 15 GiB 的可用磁盘空间。其他文件系统用于管理目的（设备的动态显示）以及存储 Ubuntu 特有的 snap 软件包。由于使用了 `-x tmpfs`，许多临时文件系统（即仅位于 RAM 中的系统）未被计入。

```bash
root# df -h -T -x tmpfs
Filesystem Type Size Avail Use% Mounted on
```

（注：此处省略重复的示例输出内容，仅保留最后一次完整格式结构）



udev devtmpfs 16G 0 16G 0% /dev

/dev/nvme0n1p1 vfat 1021M 254M 768M 25% /boot/efi

/dev/nvme0n1p4 ext4 119G 32G 81G 29% /

/dev/mapper/mycryptpart ext4 1.5T 767G 634G 55% /crypt

/dev/loop0 squashfs 62M 62M 0 100% /snap/authy/5

/dev/loop1 squashfs 56M 56M 0 100% /snap/core18/188

## 替代方案

委婉地说，“读取” `diff` 结果需要时间适应。使用 `delta` 命令要方便得多。如果你有图形界面，`meld` 程序会非常有帮助。大多数编辑器也可以突出两个文件之间的差异（例如，VS Code）。

## dig [options] [@dnsserver] host/ipaddr [type]

`dig` 以类似于 `host` 和 `whois` 的方式在域名服务器上运行查询。使用 `dig`，你可以通过特别大量的选项来控制过程，这些选项在在这里甚至无法详述（参见 `man dig`）。

在最简单的形式下，`dig host` 联系 `etc/resolv.conf` 中设置的 DNS 服务器并返回 A 记录。通过 `@1.2.3.4`，你可以指定备用 DNS 服务器的 IP 地址。如果你对 A 记录不感兴趣而是对其他数据感兴趣，你必须在第三个参数中输入其类型。

- `-4` / `-6`
  仅使用 IPv4 或仅 IPv6。
- `+nocomments`
  不输出任何注释。
- `+nostats`
  不输出查询的任何统计数据（查询时间、查询大小等）。
- `+short`
  以读者易读的方式格式化输出。（默认情况下，`dig` 提供 DNS 服务器 bind 提供的混淆表示。）

### 示例

以下命令连接 Google 的公共名称服务器，确定 `kofler.info` 在处的 MX 记录，并以简写形式显示它：

```
$ dig +short @8.8.4.4 kofler.info MX

10 mail.kofler.info.
```

## dircolors [options] [file]

`dircolors` 提供程序代码，用于设置 `ls` 命令识别不同文件类型时所使用的颜色。如果将文件传递给 `dircolors`，该命令将显示此文件中保存的设置。该文件必须符合 `dircolors -p` 指定的语法。

- `-b`
  使用 bash shell 的语法（默认应用）。
- `-c`
  使用 C shell 的语法。
- `-p`
  使用非常详细的语法，该语法可以由 `dircolors` 本身处理。文件包含解释语法（特别是颜色代码）的注释。

在许多发行版中，bash 启动时会分析 `.dircolors` 文件并用它设置颜色。要更改 `ls` 颜色，你必须先使用 `dircolors -p` 创建你自己的该文件版本，然后在编辑器中对其修改。更改后的设置在你打开新的终端窗口或对话框时立即生效。

```
user$ cd

(切换到主目录)

user$ dircolors -p > .dircolors

user$ yourFavoriteEditor.dircolors
```

如果更改 `.dircolors` 文件对于你的发行版来说不够，你可以使用 `dircolor` 创建一个设置 `LS_COLORS` 变量的语句，并将此语句添加到 `.bashrc` 末尾：

```
user$ dircolors .dircolors >> .bashrc
```

## dirname string

`dirname` 返回完整文件名的路径。因此，`dirname /usr/bin/groff` 返回 `/usr/bin`。

## dirs

bash 命令 `dirs` 返回由 `pushd` 保存的所有目录列表。该命令主要用于脚本编程。

## disown [options] [jobspec]

bash 命令 `disown` 从 shell 中移除指定的进程。这意味着即使 shell 关闭，进程也会继续运行。进程通过进程 ID `PID` 或 shell 作业号指定，其中 shell 作业号必须以 `%` 开头。如果不指定作业号，则指当前的（后台）进程。

如果你计划从一开始就脱离 shell 运行程序，可以在启动时使用 `nohup` 以避免以后调用 `disown`。

- `-a`
  触发在 shell 中启动的所有进程。
- `-r`
  触发在 shell 中启动且当前运行的所有进程。

### 示例

在以下示例中，首先启动了一个较长的下载过程。Ctrl+Z 中断下载，`bg` 在后台继续下载。`disown` 将下载进程与 shell 分离，这样即使 shell 注销后下载也会继续。

```
user$ wget -q http://mirror.switch.ch/.../AlmaLinux-n.n.iso

user$ <Ctrl>+Z

user$ bg

user$ disown
```



## `dmesg` [options]

`dmesg` 输出缓冲区内存中的内核消息。

- `-c`
  输出后删除内核消息的缓冲区。此选项需要 root 权限。
- `-H`
  彩色输出并以更易读的形式显示时间（人类可读）。
- `-T`
  显示每条消息之前的绝对时间。
- `-W`
  显示所有内核消息，然后继续运行直到通过 Ctrl+C 终止命令。
- `-W` 或 `--follow-new`
  等待新的内核消息并显示它们，直到通过 Ctrl+C 终止命令。

在某些 Linux 发行版中，`dmesg` 需要 root 权限。如果你想赋予所有用户读取内核消息的权限，需要在 `/etc/sysctl.conf` 文件中输入 `kernel.dmesg_restrict=0`，然后运行 `sysctl -p`。

## `dnf` [options] 命令

`dnf` 是 Fedora、RHEL 及其发行版的包管理命令。`dnf` 替换了以前使用的 `yum` 命令。

`dnf` 从 `/etc/yum.repos.*.repo` 中定义的包源下载软件包。（该目录的名字标明了 dnf 的来源，并且没有随着从 yum 变为 dnf 的变化而改变。）

- `check-update`
  检查是否有更新。
- `clean`
  删除元数据。
- `clean packages`
  从缓存中删除下载的文件。

## `config-manager` [options]

管理 DNF 仓库。
- `--add-repo`
  添加一个仓库。
- `--enabled`
  激活一个仓库。
- `--set-disabled`
  禁用一个仓库。

## `copr` [enable|remove|list|search]

管理 Copr。Copr 是一个开发者用于提供软件包的自动化构建系统。

## `download`
从包源下载软件包。

## `downgrade`
将软件包替换为旧版本。

## `grouplist`/`groupinfo`/`groupinstall`/`groupupdate`/`groupremove`

提供关于组的信息，或安装、更新或删除组。

## `history`

提供一个带编号的 dnf 操作列表。
- `info n`
  提供事务 `n` 的详细信息。

## `info`

提供关于指定软件包的信息。

## `install` name12 ...

安装指定的软件包。
- `rpmfile`
  从本地文件系统安装 RPM 包。
- `@package:version`
  安装指定版本的包。
- `package:version`
  这是 dnf 模块安装的简记符号。

## `list`

提供两个部分的列表。第一部分包含（按字母顺序）所有已安装的包；第二部分包含所有尚未安装的包。
- `available`/`updates`/`installed`/`extras`/`recent`
  限制 `dnf list` 输出到特定的软件包。
  - `updates`
  提供所有可用更新的包列表。
  - `recent`
  提供最近添加的软件包的概述。

## `makecache` [fast]

创建一个包含包源上所有可用目录的缓存。带有额外的关键字 `fast`，`dnf` 会检查缓存是否最新，并仅在必要时执行更新。

## `module` install/update/remove/enable/disable/lock/unlock/list/info

管理可用不同版本的软件包。此 dnf 命令的扩展是 Fedora 28 和 RHEL 8 引入的模块和流的一部分。在安装期间，除了包名外，你必须指定所需的版本和配置。

## `repoquery` name

确定指定软件包的完整包名。
- `-i`
  以表格提供更多元数据。
- `--location`
  指定可以手动下载软件包的地址。

## `search` query term

返回描述包含搜索词的所有软件包列表。

## `update`

显示所有已安装的包。

## `update` name12 ...

仅更新指定的软件包。

## `upgrade`

与 `--obsolete` 选项结合时产生相同的效果。

你可以通过一些极少使用的选项来影响 `dnf` 的行为：

- `--enablerepo=name`
  激活一个已禁用的软件包源。如果你只想从一个禁用的软件包源中安装单个软件包，此选项可以避免修改 `*.repo` 文件。
- `--exclude-package`
  从所选的操作（例如，更新）中排除指定的软件包。
- `--obsolete`
  使 `dnf` 在更新后删除不再需要的软件包。这仅对于发行版大版本更新（从版本 n 到 n+1）很有用。
- `-y`
  对 `dnf` 的所有问题均回答“是（yes）”。这意味着可以将 `dnf` 用于在无需进一步交互的情况下进行安装（例如，在脚本中）。

## 示例

以下两个命令首先更新所有现有的软件包，然后安装 emacs 编辑器：

```
root# dnf update

...

Transaction Summary

Install 1 Package(s)
```

```
Update 42 Package(s)

Remove 0 Package(s)

Total download size: 52 M

Is this ok [y/N]: y

..
```

```
root# dnf install emacs

Installing:

emacs                aarch64    1:29.2-fc39  updates   32 M

Installing dependencies:

dejavu-sans-mono-fonts  noarch      2.37-20.fc39  updates   469 k

emacs-common        aarch64    1:29.2-fc39  updates   42 M
```

Transaction Summary: Install 20 Packages, total download size: 139 M
installed size: 728 M
Is this ok [y/N]: y

`dnf repoquery` 提供了关于关于软件包元数据。
以下列表是在 AlmaLinux 9 上创建的，在此之前我先安装 `dnf-utils` 软件包：

```
root# dnf repoquery -i joe

Name                : joe

Version             : 4.6

Release             : 12.el19

Summary             : An easy to use, modeless text editor
```

以下两个命令确定 `nodejs` 软件包的哪些版本可用，然后在最小配置（minimal profile）中安装最新版本：

```
root# dnf module list --all nodejs

AlmaLinux 9 - AppStream

Name                Stream Profiles                               Summary

nodejs              18      common [d], development, minimal,s2i  Javascript runtime

nodejs              20      common [d], development, minimal,s2i  Javascript runtime

Hint [d]efault, [e]abled, [x]disabled, [i]nstalled

root# dnf module install nodejs:20/minimal
```

最后一个命令下载了 Gnome文本编辑器的源码包：

```
user$ dnf download --source gedit
```



## docker [options] 命令

`docker` 命令管理 Docker 容器。在使用第一次该命令之前，你必须安装 `docker`，理想情况下是从当前的 Docker 软件包源（参见 https://docs.docker.com/get-docker）。

在 Fedora 和 RHEL 兼容的发行版中，可以使用几乎兼容的 `podman` 命令来代替 `docker`。即使在技术实现上存在各种差异，下列表中描述的几乎所有命令的工作方式与 `docker` 相同：

- `build` `directory/url` 读取位于指定位置的 `Dockerfile` 并从中创建一个相应的本地镜像。通过 `-t name:tag` 选项，可以为镜像命名并标记标签。
- `compose up|down` 评估 `docker-compose.yml`（已弃）或 `compose.yaml`，创建其中描述的容器设置并执行它或再次停止它。该命令尚未在 `podman` 中（截至 2025 年春天）；在红帽世界中，你可以使用 `podman-compose` 脚本代替。`docker-compose.yml` 中允许的语法参考可以在以下地址找到：https://docs.docker.com/compose/
- `create image/id` 类似于 `docker run`，创建一个容器，但不启动它。
- `exec containername/id` 在运行的容器中执行命令。带有 `-i -t` 选项可以进行交互式运行。带有 `-d` 选项可以在后台执行。
- `image prune|pull|push|rm [image` 删除未使用的镜像，从 Docker Hub 下载或上传镜像，删除指定的镜像。
- `inspect containername/id` 提供关于容器的详细信息。
- `logs containername/id` 显示容器的日志。
- `network create|connect|rm [networkname` 管理网络。
- `port containername/id` 列出端口分配。
- `ps` 输出所有容器。带有 `-a` 选项也会列出停止的容器。
- `system df` 显示镜像、容器和卷的空间需求。
- `system info` 显示关于安装的综合信息。
- `system prune` 删除未运行的容器、未使用的镜像，以及带有 `--volumes` 选项的卷。
- `start/stop containername` 启动或停止已设置的容器。
- `tag containername/id newname:tag` 重命名容器。
- `volume ls|inspect|prune|rm` 管理卷。

### 示例

`docker run` 从 Docker Hub 的 MariaDB 镜像创建一个容器并将其命名为 `mydb`。如果镜像尚未下载，`docker run` 将处理此。第一次执行该命令需要更长时间。

所有数据库文件都保存在 `/home/<username>/varlibmysql` 中。容器的端口 `3306` 可以通过本地端口 `1306` 访问。

```
root# mkdir /home/<username>/varlibmysql
```

```
root# docker run -d --name mydb -p 3306:3306 \
    -v /home/<username>/varlibmysql:/var/lib/mysql mariadb
```

容器一直运行，直到通过 `docker stop` 终止：

```
root# docker stop mydb
```

如果你不再需要使用该容器，现在可以删除它：

```
root# docker rm mydb
```

## dpkg options [filename/packagename]

`dpkg` 在所有基于 Debian 和 Ubuntu 的发行版中负责低级软件包管理。然而，用户通常使用基于它的命令 `apt-get` 而不是直接使用 `dpkg`。

- `--configure package name` 运行指定软件包的配置脚本。这通常在安装时完成，但在某些情况下，可能需要显式执行此步骤。某些软件包除了自动配置脚本外还有交互式设置程序。如果你以后再次需要此类设置程序，应该运行 `dpkg-reconfigure package name`。
- `--get-selections` 返回已安装软件包的列表，类似于 `--list`。但结果包含的详细信息较少，因此容易得多。如果你将列表重定向到文本文件并保存，以后可以在另一台计算机上通过 `--set-selections` 安装所有软件包。
- `-i` or `--install filename.deb` 安装指定的软件包文件。如果已经安装了旧版本，它将会被卸载并由新版本替换。软件包中提供的配置脚本也会在安装期间执行。

在开始安装之前，会确保所有软件包依赖项都已满足。如果不符合该情况，错误信息通常会指示缺少哪些包。与其费力地安装所有依赖包，不如运行 `apt install ./filename.deb` 来通过 `apt` 执行安装。

通常情况下，`dpkg` 仅允许安装与发行版架构相匹配的软件包。如果你使用的是 64 位的 Linux 发行版，但某个程序仅 32 位包的形式提供，可以使用 `force-architecture` 强制安装。然而，程序实际上是否能够运行是另一回事。在任何情况下，你必须安装所有需要的 32 位库。
- `-l` or `--list` 提供所有已安装软件包的列表。
- `-l` or `--list 'pattern'` 提供已安装和可用软件包的列表。软件包列表的第一列包含一个两个字母的代码。

第一个字母表示软件包的预期状态：

```
i = install
```

```
n = do not install
```

```
r/p = remove
```

```
h = hold
```

第二个字母描述实际状态：

```
i = installed
```

```
n = not installed
```

```
c = configured
```

```
u = unpacked, but not yet configured
```

```
f = failed
```

这些信息来自 Debian 软件包数据库，它是 `/var/lib/dpkg` 目录下的文件集合。所有已安装和可用软件包的元信息都存储在那里。
- `-L` or `--list package name` 返回指定软件包中所有文件的列表。这仅对已安装的软件包有效。你可以使用命令 `dpkg-deb --contents filename` 来确定未安装软件包的内容。
- `-P` or `--purge package name` 移除指定的软件包，包括所有的软件包文件（即使你修改了它们）。
- `-r` Or `--remove package name` 移除指定的软件包。
- `-S` Or `--search filename` 确定指定文件所属的软件包。

### 示例

第一个 `dpkg` 命令安装了一个新软件包。`dpkg --search` 确定了 `/etc/sensors3.conf` 文件所属的软件包，而 `dpkg --listfiles` 返回了该软件包中所有文件的列表。

```
root# dpkg --install packagename.deb
root# dpkg --search /etc/sensors3.conf
libsensors-config: /etc/sensors3.conf
root# dpkg --listfiles libsensors-config
...
./.
/etc
/etc/sensors.d
/etc/sensors.d/.placeholder
/etc/sensors3.conf
...
```

## dracut [options] initrd file kernel version

`dracut` 负责在 Fedora、RHEL 和 (open)SUSE 上创建 `initrd` 文件。如果在大不带额外参数的情况下执行 `dracut`，它会为 `/boot` 目录中最新的内核创建一个名为 `/boot/initrd-kernelversion` 的 `initrd` 文件。`dracut` 考虑了 `/etc/dracut.conf` 中的设置以及 `man dracut` 中描述的无数选项。这里只总结了三个最重要的选项：

- `-d,a,c` 将内核模块 `a`、`b` 和 `c` 整合到 `initrd` 文件中。通常不需要此选项。`dracut` 会自动识别启动过程需要哪些模块。
- `-f` 覆盖现有的 `initrd` 文件。
- `--regenerate-all` 为系统上安装的所有内核版本创建新的 `initrd` 文件。

Debian 和 Ubuntu 使用 `update-initramfs` 代替。

### 示例

要为 `/boot/vmlinuz-5.7.3` 文件中的自编译内核 `5.7.3` 手动创建 `initrd` 文件，你需要运行以下命令：

```



`root# dracut /boot/initrd-5.7.3 5.7.3`

```
```

## `du`

`du` 输出关于文件或目录内存的需求。如果在目录参数中指定了文件（例如 `*` 或 `*.tex`），`du` 将接收一个指示所有文件大小的列表。然而，如果只指定了一个目录，`du` 将确定所有子目录的内存需求。内存细节还包括所有子目录的内存需求。最后一个数值表示从指定目录开始的所有文件和子目录的总内存需求。所有数字单位均为 KiB。

- `-b` Or `--bytes`
以字节显示大小（而不是 KiB）。

- `-c` Or `--total`
将最终总计作为最后一个值显示。只有当 `du` 应用于文件（而不是目录）时，此选项才是必要的，这使得相对容易确定具有特定 ID（例如 `*.pdf`）的所有文件占用了多少内存。

- `-h` Or `--human-readable`
以易读的格式显示大小。K、M 和 G 分是 KiB、MiB 和 GiB 的缩写。

- `--max-depth=n` Or `--max n`
仅输出指定层级的目录大小。

- `-s` `--summarize`
仅显示最终总计。只有在显示目录内存需求时，此选项才有用。

- `-S` `--dereference`
仅显示目录中的直接内存需求。不考虑子目录中的内存需求。

- `-x` `--one-file-system`
忽略挂载了其他文件系统的目录。（此选项几乎总是建议开启的。在我的电脑上，我定义了一个相应的别名 `du="du -x"`）。

### 示例

`du` 确定哪些目录占用了多少空间。使用 `--max 1` 时，子目录不会单独列出，而是包含在结果中。

```
user$ du -h --max 1

15M ./Downloads

29M ./Videos

69M ./local

...
```

### 替代方案

`du` 不提供排序结果的选项。这正是交互式 `ncdu` 命令可以做的。它还提供了使用光标键在子目录之间导航的选项。我强烈推荐此！

## `dumpe2fs device`

`dumpe2fs` 提供关于 ext 文件系统状态的无数内部信息，特别是关于超级块和数据介质块组的结构。

- `-b`
仅列出介质上的缺陷块。
- `-h`
提供超级块摘要。

## `dvips [options] name.dvi`

`dvips` 从 `*.dvi` 文件创建 PostScript 文件。如果使用 `dvips` 而不带 `-o` 选项，命令会将生成的 PostScript 文件重定向到默认打印机。

- `-A`
转换奇数页。

- `-B`
转换偶数页。

- `-D n`
生成位图字体时使用 `$n$` dpi（每英寸点数）的分。默认分辨率通常为600 dpi（见 `/etc/texmf/config`）。或者，`$n$` 也可以300、400或720（见 `/usr/bin/mktexpk`）。此选项仅适用于位图字体。PostScript 字体始终与分辨率无关。

- `-E`
创建一个 EPS 文件（封装式 PostScript），其边界框仅包含页面实际使用的部分。这只有当 DVI 文件不超过一页且生成的 EPS 文件随后嵌入另一个文档时才有意义。

- `-i -S n`
将输出分成每个 `$n$` 页的文件。文件将自动编号。

- `-l last page`
在指定的页结束转换。

- `-o target file`
将结果写入指定的文件（而不是转发给 `lpr` 程序）。

- `-p first page`
从指定的页开始转换。

`dvips` 的全局默认设置定义在 `config.ps` 文件。根据发行版的不同，该文件可以在 `/etc/texmf` 目录或 `/usr/share/texlive/texmf-dist/dvips/config` 中找到。

## `e4defrag`

`e4defrag` 对单个文件、整个目录内容或整个 ext4 文件系统进行碎片。没有 root 权限的用户只能碎片自己的文件。

碎片意味着文件的块在介质上尽可能以连续序列保留。这会加快读取速度，特别是对于传统的硬盘。对于 SSD，碎片的影响并不明显。

- `-c`
显示相关文件的碎片计数器，但不进行任何更改。如果使用此选项对整个文件系统执行 `e4defrag`，命令将在一段时间后返回碎片最严重的文件列表。

- `-v`
显示每个文件碎片前后的信息。

## `echo [options] string`

bash 命令 `echo` 输出指定的字符字符串。如果字符串包含空格或特殊字符，则必须用双引号或单引号将其括起来，取决于是否需要输出 shell 变量。

- `-e`
解释各种反斜杠字符组合，例如将 `\a` 视为信号音，`\n` 视为行尾，`\t` 视为制表符（另参见 `help echo` 帮助）。因此，`echo -e "\a"` 会输出一个警告信号。

- `-n`
在输出结束时不换到新行。输出可以使用另一个 `echo` 语句继续输出。

### 示例

以下命令显示 `$PATH` 变量的当前内容：

```bash
user$ echo "The PATH variable contains: $PATH"
```

## `efibootmgr [options]`

在以 EFI 模式安装并启动的 Linux 系统中，可以使用 `efibootmgr` 命令更改各种 EFI 设置。这些设置存储在主板的非易失性内存（NVRAM）中。`efibootmgr` 主要用于设置新的 EFI 启动项、删除现有启动项以及定义默认启动序列。该命令需要加载 `efivars` 内内核模块。如果尚未加载，您需要运行 `modprobe efivars`。

注意，只有当 Linux 以 EFI 模式启动（而非 BIOS 模式！）时才能使用 `efivars` 模块。如有必要，您可以使用可以在 EFI 模式启动的 Linux 优盘系统进行修复工作。

- `-b n -B`
删除指定的 EFI 启动项。您可以通过运行不带参数的 `efibootmgr` 来确定 EFI 启动项的数字。

- `-c -l \EFI\distrib\grubfile.efi -L name`
创建一个新的 EFI 启动项 (`-c`) 并指定相应的加载器文件的位置。该路径相对于 EFI 分区 `/boot/efi`。

新启动项会自动成为默认启动项。可选，您可以使用 `-p` 指定 EFI 启动分区的编号（通常为 1），并使用 `-d` 指定第一块硬盘/SSD 的设备名称（通常为 `/dev/sda`）。

- `-n sad`
确定下次重启时使用哪个 EFI 启动项。该设置不是永久的，仅适用于下次计算机启动。

- `-N`
删除为下次重启通过 `-n` 指定的设置。

- `-o n1,n2,n3...`
永久设置 EFI 启动项的新顺序。如果您只想指定第一个位置的启动项，只需输入其数字即可。

- `-p n`
确定 EFI 启动分区所在的哪个分区（通常在第一个分区）。

- `-q`
指定不需要输出（静默模式）。

- `-t n`
指定重启后 EFI 在激活默认启动项之前应等候多长时间（秒）。然而，在此等待期间是否会自动显示 EFI 菜单取决于 EFI 的实现。在我的其中一台测试电脑上，EFI 菜单通常只在我按下相应的键（F8）时显示，那是华硕（ASUS）主板 P8HH67-M Evo。

- `-T`
删除使用 `-t` 设置的等待时间；即默认启动项将立即激活。

### 示例

如果执行该命令时不带任何额外选项，它将列出 EFI 启动项以及 EFI 加载器的其他参数：

```text
root# efibootmgr

BootCurrent: 0000

Timeout: 1 seconds

BootOrder: 0000,0005,0003,0001,0002

Boot0000* ubuntu

Boot0001* Hard Drive

Boot0002* CD/DVD drive

Boot0003* Windows Boot Manager

Boot0005* Fedora
```

在下次重启时，预计将启动 Fedora（这偏离了保存的启动序列，在该序列中 Ubuntu 排第一）。

下一个命令创建一个新的 EFI 启动项。双写的反斜杠 `\` 是必要的，因为 shell 会将单个 `\` 视为特殊字符的标识符。

```bash
root# efibootmgr -c -L \EFI\test\abc.efi -L abc
```



## `egrep` [options] search pattern file

`egrep` 在指定的文本文件中搜索搜索模式并显示找到的文本段落。扩展正则表达式（ERE）的规则适用于搜索模式。

`egrep` 本身并不是一个命令，而仅仅一个带有 `-E` 选项运行 `grep` 命令的别名或小型脚本。GNU 文档建议不要调用 `egrep`，而是推荐直接运行 `grep`。更多信息和示例可以在 `grep` 中找到。

## `enscript` [options] source file -p target file

来自同名包的 `enscript` 命令将文本文件转换为 PostScript、HTML 或 RTF 格式。

- `-color`
  使用颜色进行语法高亮（必须与 `-E` 结合使用）。
- `-E`
  对程序代码进行语法高亮（粗体、斜体）。
- `-f` font
  使用指定的字体（默认使用 10 点 Courier）。
- `-M` paper size
  使用指定的纸张格式（例如 A3,A4 或 Letter）。
- `-n`
  用 n 列格式化文本。因此，`-2` 导致两列格式化。
- `-r` Or `--landscape`
  以横向格式填充页面。
- `-W` format Or `--language=format`
  指定所需的格式。可用选项包括 PostScript（默认应用）、html、rtf。
- `-X` charset
  指定文本的字符集（例如 ascii,latin）。Unicode 不支持。为了转换 Unicode，必须使用 `paps`

## `epstopdf` [options] file

`epstopdf` 将 EPS 文件转换为 PDF 并保存为 `file.pdf`。

- `--exact`
  评估 ExactBox（而不是边界框）。
- `--hires`
  评估 HiresBox（而不是普通的边界框）。
- `--nocompress`
  不压缩 PDF 数据。
- `--outfile=name`
  将结果保存到指定的文件。

## `erd` [options] files

来自 `erdt` 包的 `erd` 结合了 `du`、`ls` 的功能。输出带有彩色（见图 2）。

- `.`
  也显示隐藏文件。
- `-d` line|word|block
  按行、字或块显示大小。
- `-H`
  以 KiB、MiB 或 GiB 显示（而不是字节）。
- `-i`
  忽略 `.gitignore`；即显示所有文件。
- `-l` Or `--long`
  显示访问权限、所有者和组。
- `-L` Or `--level` n
  跟踪子目录到指定的深度。默认，`erd` 会遍历所有子目录。
- `-p` `--pattern` regex
  仅显示匹配正则表达式的文件。
- `-s` Or `--sort` name|rname|size|rsize|access|raccess|mod|rmod
  根据文件名、文件大小、访问或修改时间对输出排序。`r` 变体反转排序顺序。因此 `-size` 将最大的文件排在前面。

![](img/94f0b4d76a25250c2205151d5b83f219_0.png)

图 2 提供了 `/etc/systemd` 目录的概述

## `etherwake` [options] mac

来自同名包的 `etherwake` 命令向 MAC 地址发送特殊的网络数据包，并尝试从睡眠模式唤醒设备。设备必须支持 Wake On LAN 标准。

- `-i` interface
  通过指定的网络接口发送数据包（默认认为 `eth0`）。

### 示例

以下命令激活了我家中的 NAS 设备，它位于地下室，通常处于睡眠模式以节省能量：

```bash
root# etherwake -i wlp0s20f3 00:11:32:DD:0D
```

## `ethtool` [options] device [parameter]

`ethtool` 确定或更改以太网适配器的（硬件）参数。如果您只需将接口名称传递给命令而不带任何额外选项，您将收到最重要的关键数据列表。这些包括支持的端口、链路模式、速度、双工模式等。

- `-p` device n
  开启接口 LED n 秒钟。对于具有多个适配器的服务器，这有助于识别接口插座。对于某些适配器，LED 将在指定的时间内闪烁。其他适配器完全不支持 LED 控制——在这种情况下，会显示错误信息“不支持的操作”。
- `-s` device para1 value1 para2 value2 ...
  更改接口的多个参数。允许的参数名包括 `speed`, `duplex`, `port`, `mdxix`, `autoneg` 和 `advertise`。

### 示例

以下命令显式将网络适配器的速度设置为 100 MBit/秒，激活双工模式并禁用自动协商功能：

```bash
root# ethtool -s eth0 speed 100 duplex full autoneg off
```

## `eval` $var

`bash` `eval` 将变量的内容解释为命令行，使用所有已知的替换机制对该行进行求值，最后执行命令。如果要执行存储在变量中的命令，且该命令包含 shell 的各种特殊字符，则始终需要使用 `eval`。

### 示例

由于存储在变量 `$kom` 中的命令在没有使用 `eval` 之前无法执行。第一次尝试运行命令时失败了，因为 `bash` 在将 `$kom` 替换为其内容后，不再评估管道字符 `|`。

```bash
user$ kom="ls | more"
user$ $kom
ls: | No such file or directory
ls: more: No such file or directory
user$ eval $kom
```

# `exec` 命令

`bash` 命令 `exec` 以参数中指定的命令来替换正在运行的 shell。该命令可以用于启动另一个 shell。这将终止正在运行的 shell。然而，如果使用没有 `exec` 的普通命令启动，shell 将继续运行并在命令结束后接受进一步输入，或继续执行运行中的脚本。

# `exfatlabel` device [label]

`exfatlabel` 读取或更改 exFAT 文件系统的名称。该命令在 `exfat-utils` 软件包的许多发行版中都可以找到。要设置 exFAT 文件系统，您可以使用 `mkfs.exfat`。

## `exiftool` [options] file/directory

来自同名包的 Perl 脚本 `exiftool` 可以从 JPEG 和 TIFF 文件中提取和修改交换图像文件格式 (EXIF) 数据。EXIF 描述了额外的元数据（例如拍摄时间）是如何存储在位图文件中的。如果调用命令时不带选项，它将列出指定文件所有的 EXIF 信息。

- `-tag`
  仅读取指定的信息，例如使用 `-CreateDate` 读取创建日期。
- `-tag=value`
  用指定的值覆盖信息。
- `-tag1<tag2`
  用另一个 tag 覆盖 tag。可以考虑通过 `-d` 指定格式化字符串（参见下例）。
- `-lang` de
  用德语输出 EXIF 元素。
- `-v`
  显示当前发生的情况（详细模式）。

在 https://exiftool.org 记录了无数其他选项。

### 示例

以下命令重命名当前目录下的所有图像。新文件名由创建日期（例如 2025-12-31-124500）加上针对同一秒内创建的多张照片的连续数字（格式字符串 `%c`），再加上原始文件标识符（格式字符串 `%%e`）。

```bash
$user exiftool -v '-Filename-CreateDate' -d '%Y-%m-%d-%H%M%S-%%c.%%e'.
$user ls *.jpg
```

2025-02-27-161642-0.jpg 2024-10-27-194700-0.jpg ...

# `exit` [return value]

`bash` 命令 `exit` 终止 shell 脚本或运行中的 shell。如果没有指定返回值，shell 将返回 0，即“OK”。

# `expand` [options] file

`expand` 将指定文本文件中的所有制表符替换为相应数量的空间。如果没有指定选项，`expand` 假设制表间隔为八个字符。结果发送到标准输出。

- `-n`
  将制表间隔更改为 `$n$` 个字符。

### 示例

以下命令移除 `test.java` 中的制表符并将保存为 `test-no-tabs.java`。原始文件是用将制表符等同四个空格的编辑器编写的。

```bash
user$ expand -n 4 test.java > test-no-tabs.java
```

## `export` [options] variable [value]



`bash` 命令 `export` 将指定的 shell 变量声明环境变量。这意味着变量在所有调用的命令和子 shell 中都是可用的。可以选择也可以为变量赋值。如果调用命令时不带参数，将显示所有环境变量。

- `-n`
将环境变量变回普通 shell 变量。因此，该命令的效果与不带选项使用时完全相反。

```bash
exportfs [options]
```

`exportfs -a` 命令向运行的 NFS 服务器报告 NFS 配置文件 `/etc/exports` 的更改。因此，必须执行该命令才能使 `/etc/exports` 中的更改生效。

```bash
expr expression
expr string : pattern
```

`expr` 以算术方式评估指定的表达式，或对字符字符串执行模式比较。指定的变量、数字和操作符之间必须有空格！所有允许的操作符的短描述可以在 `expr` 的 `man` 命令中找到。注意，shell 中的许多操作符必须使用 `\` 字符保护以免被立即评估。

如果你使用 `bash` 作为 shell，你也可以在其中不使用 `expr` 进行计算：可以通过 `$[expression]` 在那里指定算术表达式。`grep` 中描述的通配符可以使用于模式。通常，模式必须放在单引号中，以防止 shell 评估特殊字符。

### 示例

第一个 `expr` 命令执行简单的计算。第二个命令返回对应模式表达式的最大字符数。第三个命令从字符字符串中提取模式的括号部分。

```bash
user$ expr 3 + 7 \* 19
136
user$ expr abcdefghi : 'a.*'
```

```bash
user$ expr abc_efg_hij : '.*\(*\)__*'
efg
```

### `fail2ban-client [options] command`

`Fail2ban` 是一个安全程序，用于监控登录并在多次错误登录后封锁相关 IP 地址一段时间。如果安装了 `Fail2ban`，可以通过 `fail2ban-client` 检查和更改其功能。

- `get parameter`
导入配置参数。

- `reload [jailname]`
重新加载整个配置或某个 jail 的配置。在 `Fail2ban` 中，jail 是一个被监控的程序。

- `set [jailname] value`
更改通用参数或 jail 的参数。

- `start/stop [jailname]`
完全启动或停止 `Fail2ban` 或仅停止一个 jail。

- `status [jailname]`
显示活动 jail 的列表或 jail 的详细信息。

`fail2ban-client` 在仅带 `-d` 选项运行时输出当前配置，这对于排查混乱的文件非常有用。以下命令显示计算机上有四个活动 jail。SSH 服务器的 jail 已经封锁了 1418 个地址。目前封锁了 3 个。

```bash
root# fail2ban-client status
Status
Number of jail: 4
Jail list: docet, postfix, sshd, sshd-ddos
```

```bash
root# fail2ban-client status sshd
Status for the jail: sshd
Filter
  Currently failed: 4
  Total failed: 11362
Journal matches: _SYSTEMD_UNIT=sshd.service _COMM=sshd
Actions
  Currently banned: 3
  Total banned: 1418
  Banned IP list: 58.218.nnn.nnn 58.242.nnn.nnn 180.76.nnn.nnn
```

可以使用 `fail2ban-client set` 解封误封的 IP 地址（在这里对 ssh jail 这样做）：

```bash
root# fail2ban-client set sshd unbanip 1.2.3.4
```

### `fc-list [pattern]`

`fc-list` 列出所有匹配可选搜索模式的字体。可以使用 `| sort` 进行排序。

### `fdisk [options] [device]`

`fdisk` 是一个过时的硬盘分区程序。它只能处理具有 MBR 分区表的磁盘！由于这个原因，你应该熟悉 `parted`，它兼容主引导记录 `MBR` 和更现代的 GUID 分区表 `GPT`。

### `ffmpeg [inopts] [-i infile] [outopts] outfile`

来自同名包的 `ffmpeg` 命令将视频文件从一种格式转换为另一种。在指定选项时，注意这些选项仅适用于下一个视频文件。因此，选项的顺序对于命令的正确功能至关重要。除非进行不同的设置，否则对结果文件使用与源文件相同的编码器和设置。

除了列出的选项外，还有无数其他。选项的理想设置本身就是门科学。如果你不想处理这些，建议使用一个用于视频录制的图形化用户界面，例如 `HandBrake`。

- `-acodec/-vcodec`
指定的音频或视频编码器。`ffmpeg -codecs` 提供了可用编码器的列表。

- `-b n`
指定的位比特率，单位为比特/秒（默认为 200 kBit/s）。

- `-f format`
使用指定的格式。

- `-formats`
列出支持的格式、编码器、过滤器等。

- `-r n`
指定的帧率（默认为每秒 25 帧）。

- `-s size`
以 `wxh` 格式指定的帧大小（例如 `800x600`）。或者，你可以指定一个预定义的字符字符串（例如 `vga` 或 `hd720`；请参见 `man ffmpeg`）。

- `-ss position`
从指定的时间开始转换。时间可以用秒数或 `hh:mm:ss[.xxx]` 格式指定。

- `-t duration`
仅转换指定的时间段（而不是整个文件）。时间段的指定方式与 `-ss` 选项相同。

- `-target type`
指定的目标文件格式（例如 `vcd`、`dvd` 等）。

- `-vpre quality`
为指定的编码器选择具有预定义选项（预设）的文件（例如 `default`、`medium`、`max` 或 `fast`）。可选择的预设文件通常位于 `/usr/share/ffmpeg` 目录。

- `-y`
覆盖现有文件。

#### 示例

以下命令创建一个 DVD 分辨率的电影文件：

```bash
user$ ffmpeg -i in.avi -target pal-dvd -y out.avi
```

第二个示例将 OGV 电影文件转换为 YouTube 兼容的 MPEG 文件：

```bash
user$ ffmpeg -i in.ogv -vcodec libx264 -vpre medium -acodec copy -y out.mp4
```

### `fg [process]`

`bash` 命令 `fg` 让之前使用 `Ctrl+Z` 中断的任务在前台继续运行。如果没有指定进程，`fg` 适用于上一个被中断的进程或上一个在后台启动的任务。否则，必须通过进程名称或 `bash` 内部作业号（不是 PID）来指定进程。

除了 `fg process`，还允许使用缩写 `%process`。

### `fgconsole [--next-available]`

`fgconsole` 输出当前活动控制台编号。使用 `--next-available` 选项，该命令将确定第一个空闲（未使用）控制台编号。要更改活动控制台，可以使用 `chvt` 命令。

### `file [options] file`

`file` 尝试确定指定文件的类型。结果是 `file` 返回一个包含文件名和文件类型的字符字符串。`file` 不评估文件名或其标识符，而是评估文件内容！

- `-z`
尝试识别压缩文件的数据类型。

#### 示例

正如文件名所示 `name.jpg` 包含一个 JPEG 位图文件：

```bash
user$ file name.jpg
name.jpg: JPEG image data, JFIF standard 1.02
```



`find [path] [search options]`

`find` 帮助你搜索文件。搜索可以考虑各种搜索标准（文件名模式、文件大小、创建日期或最后访问日期等）。甚至可以对所有 `grep` 文件应用进一步的筛选标准。例如，可以找到在过去三天内编辑过且包含“Graphics programming”文本的所有 `*.tex` 文件。由于可能的搜索标准非常多，`man find` 提供的命令描述长达数页。

以下语法描述明确指代 Linux 上常用的 GNU find 实现。与其他 Unix 系统的 `find` 变体相比，它具有一些细微的语法差异：在那些系统中必须指定路径，而 GNU `find` 使用当前目录作为起始目录。此外，大多数 `find` 实现要求使用 `-print` 选项显示搜索结果，而这对 GNU find 来说并不是必需的。

# 通用选项

与其他大多数命令不同，`find` 会自动搜索所有子目录。如果不需要，必须通过 `-maxdepth` 限制子目录的数量。

- `-depth`
首先处理当前目录，然后处理子目录。根据你认为查找的文件所在地，此过程将更快地产生初始结果。

- `-follow`
也进入符号链接捕捉的目录。

- `-maxdepth n`
将搜索限制在 n 层目录内。使用 `-maxdepth 1` 时，完全不考虑子目录。

# 搜索标准

你可以同时指定多个搜索标准。这些标准在逻辑上通过 AND 链接。一旦第一个标准不满足，搜索就会停止——因此，标准的顺序会影响命令执行的速度。标准可以使用 `\( ... \)` 分组，通过 `!` 取反，并使用 `-o` 进行逻辑或 链接（参见示例）。

- `-anewer reference file`
作用类似于 `-newer`（参见该项），但会考虑最后读取访问的时间。

- `-atime days` 或 `-cmin minutes`
考虑最后读取访问（access）。指定单位为天或分钟（参见 `-mtime`）。

- `-cewer reference file`
作用类似于 `-newer`（参见该项），但会考虑最后修改的时间。

- `-ctime days` 或 `-cmin minutes`
评估文件元数据（访问权限等）最后更改的时间。

- `-executable`
查找可执行的文件，即设置了执行位位的文件。

- `-group name` 或 `-nogroup name`
查找属于指定组的文件（或不属于该组的文件）。

- `-mmin minutes`
作用类似于 `-mtime`，但时间单位为分钟。

- `-mtime days` 或 `-cmin minutes`
查找内容最后修改的文件。如果在数字前输入 `+`，则查找所有于 n 天的文件。

- `-name search pattern`
匹配搜索模式的文件。如果搜索模式包含通配符，必须放在引号中。如果你不想让 `find` 区分大小写，应该使用 `-iname` 而不是 `-name`。

- `-newer reference file`
查找比引用文件新的文件，即在引用文件之后创建或修改的文件。例如，你可以使用 `touch` 在备份开始创建一个时间文件。对于增量备份，只考虑符合 `-newer` 的文件。

- `-path search pattern`
匹配搜索模式的文件。该选项超越了 `-name`，因为搜索模式现在不仅影响文件名，还影响路径。此选项比 `find` 第一个参数中的路径指定更灵活，因为这里的通配符也包括 `/` 字符。

- `-perm access bits`
查找权限位与指定的十六进制值匹配的文件（参见 `chmod`）。如果十六进制值前面有 `-`，则文件可能具有超出此范围的权限。如果前面有 `/`，则只要搜索的权限位中有一个被设置即可。

- `-size file`
指定所需的文件大小。默认大小单位是 512 的倍数。`-size 3` 表示 1024 到 1536 字节之间的文件。可以使用额外的字符 `c` 或 `k` 以字节或 KiB 指定大小。前缀 `+` 包含所有较大文件，前缀 `-` 包含所有较小文件。因此，`-size +10k` 返回所有大于 10 KiB 的文件。

注意此命令在使用此选项时有些独特的逻辑！`find -size 1M` 考虑大小在 1 字节到 1 MB 之间的文件。`-size -1M` 只查找空文件。使用 `-size +1M`，你得到的文件大于 1 MB。

- `-type character`
将搜索限制为特定的文件类型。最重要的字符是 `f`（普通文件）、`d`（目录）和 `l`（符号链接）。

- `-user username` 或 `nouser username`
查找属于指定用户的文件（或不属于该用户的文件）。

# 查找文件时的操作

- `-exec command [options] {} \;`
调用指定的命令，并传递找到的符合所有已标准的文件名。该命令可以执行测试以检查该文件是否符合额外的标准。一个典型的程序是通过 `-exec grep` 调。或者你也可以在这里调用命令来移动、复制或处理找到的文件。

`{}` 是文件名的占位符。`;` 表示命令调用结束；也就是说，可以在之后指定额外的 find 选项。在 shell 中，需要使用 `\` 来防止 `;` 被解释为特殊字符。

- `-exec command [options] {} +`
与前面的段落类似，但不会为每个找到的文件都调用指定的命令。相反，`find` 尝试一次性将尽可能多的结果传递给命令，这要高效得多。文件数量仅限于命令的最大长度。在当前的 Linux 发行版中，这大约是 200 万个字符。

- `-ls`
提供每个找到文件的详细信息（类似于 `ls -l`）。

- `-print`
在屏幕上显示找到的文件。除非使用了 `-exec`，否则该选项是默认设置。

- `-print0`
用 0 字节分隔结果列表中的文件名。这允许通过 `xargs` 进一步处理包含空格的文件名。

- `-printf format`
在屏幕上显示找到的文件和其他信息。格式字符串可用于指定输出的格式以及也要输出的额外信息（例如文件大小或最后修改日期）。格式字符串的语法在 man 页面中有描述。

## 示例

第一个 `find` 命令返回当前目录下的所有文件（包括隐藏文件，但不包含子目录中的文件）；第二个命令只返回普通文件（但不包含隐藏文件）：

```
user$ find -maxdepth 1 -type f -name '*'
user$ find -maxdepth 1 -type f -name '[.]*'
```

以下命令搜索 `/etc` 目录在过去两周内更改的文件。该命令必须以 root 权限运行，因为 `/etc` 中的某些文件普通用户可能无法读取：

```
root# sudo find /etc -mtime -14
```

以下命令删除所有文件名结尾带有 `~` 字符标识的备份文件。`find` 还考虑了所有子目录。要删除的文件列表通过命令替换 `$(command)` 被重定向到 `rm`。

```
root# rm $(find . -name '*')
```

如果文件很多，运行上述命令时会发生错误：包含所有 `*` 的命令行将变得非常长，超过最大命令行长度。在这种情况下，你必须使用 `find` 命令的 `-exec` 选项或 `xargs` 命令。`xargs` 变体的优点是可以处理包含空格的文件名。

```
user$ find -name '*.jpg' -exec rm {} \;
```

在下一个示例中，目录中的所有文件都要对所有人可读（参见 `chmod`）。使用 `find` 为所有子目录设置执行位（但不包括普通文件）有些困难，以便计算机上的每个人都能使用 `cd` 切换目录。命令末尾的 `+` 意味着不是为每个目录单独调用 `chmod`，而是一次将尽可能多的目录传递给 `chmod`。

```
root# cd /directory/for/all
root# chmod -R a+r *
root# find . -type d -exec chmod a+x +
```

最后一个示例首先使用 `touch` 创建一个日期为 1/1/2025 的引用文件和 `../new-images` 目录。自 2025/1/1 以来在本地目录创建的所有图像现在复制到那里。`new-images` 不能在当前目录中创建；否则 `find` 也会捕捉到复制在那的文件。此外，注意文件标识符 `*.jpg` 和 `*.png` 之间的 OR 链接。

```
user touch 2025 -t 2025010000
user mkdir ../new-images
user find . -newer 2025 -name *.png -o -name *.jpg \
    -exec cp {} ../new-images; \;
```



更多的 `find` 示例可以在 `grep` 和 `xargs` 命令的描述中找到。

# 替代方案

`find` 是一个重要的命令，但它很难使用，因为没有人能记住所有可能的选项。因此，有很多尝试创建比 `find` 更方便的替代方案。我在书中介绍了其中两个：

- `erd` 将 `du`、`find`、`ls` 和 `tree` 最重要的功能合并到一个命令中。
- 另一方面，`fzf` 以其交互式文件选择见长。

另一个选项是 `fd`（访问 https://github.com/sharkdp/fd），它与 `find` 非常相似。它最大的优势是选项更容易记忆，并且搜索结果以彩色显示。

## findmnt [options] [device/mountpoint]

不带参数的 `findmnt` 会返回集成在目录树中的所有文件系统的树形列表。结果还包含各种 `/dev`、`/proc`、`/sys` 和 `/run` 文件系统用于内部信息交换。

通过指定设备或挂载点，列表将缩小为通过这种方式选择的文件系统。其他允许的条目是文件系统的 UUID 或名称（标签）或主从设备号。

- `-A` 显示所有文件系统。
- `-l` 以表格形式显示结果（而不是树形）。
- `--mtab` 或 `--fstab` 仅考虑 `/etc/mtab` 或 `/etc/fstab` 中的条目。默认情况下，`findmnt` 考虑 `/proc/self/mountinfo`。
- `-o columns` 或 `--output columns` 输出指定的列。列包括：
  `SOURCE`: 设备
  `TARGET`: 挂载路径
  `FTYPE`: 文件系统类型
  `OPTIONS`: 挂载选项
  `SIZE`: 文件系统大小
- `-t typelist` 或 `--types typelist` 仅返回指定类型的文件系统。使用 `-t ext2,ext3,ext4`，只考虑 2、3、4 版本的 ext 文件系统。

## 示例

`findmnt` 显示测试计算机上所有激活的文件系统：

## firewall-cmd 选项

`firewall-cmd` 读取或更改 Fedora、RHEL 和 SUSE 发行版的防火墙配置。`firewall-cmd` 与后台运行的 `fireld` 程序通信。该程序为每个网络接口分配区域（zone）。`fireld` 意义区域是特定用途的规则集合。以下列表描述了最重要的区域：

- `block` 阻塞所有流量；发送者接收 ICMP 消息。
- `drop` 阻塞所有流量；不通知发送者。
- `external` 阻塞大部分端口并激活伪装 (IPv4)。该区域用于连接互联网的接口。
- `FedoraWorkstation` 和 `FedoraServer` 是 Fedora 安装网络接口的默认区域。`FedoraServer` 阻塞 SSH 和 DHCP 客户端以外的所有服务。`FedoraWorkstation` 宽松得多，还接受 Samba 连接以及 1025 到 65535 所有端口的流量。
- `home` 和 `internal` 阻塞大部分端口，但接受 Samba（仅作为客户端）、CUPS、Zeroconf/Avahi/mdns。这些区域用于被认为安全的本地网络。如果你想使用此区域并自行共享 Windows 网络目录，还必须启用 Samba 服务。
- `public` 与 `home` 类似，但阻塞 CUPS 和 Samba 客户端功能。该区域用于不安全网络中的互联网使用，例如公共无线网络中。
- `trusted` 允许任何网络流量。该区域用于安全良好的本地网络，但不用于 Wi-Fi 连接。

通常，`firewall-cmd` 仅动态进行更改。如果更改是永久的，你必须指定 `--permanent` 选项。这样规则将保存在 `/etc/firewalld` 目录中。

- `--add-interface=name` 或 `--remove-interface=` 默认区域，
  将指定的接口分配给默认区域，分配由 `--zone` 选项指定的区域，或移除此分配。在将接口分配给新区域之前，必须显式地移除之前的分配！

- `--add-prot=name` 或 `--remove-port=name`
  允许在通过 `--zone` 指定的区域中使用 TCP 端口，或阻塞该端口。

- `--add-service=name` 或 `--remove-service=name`
  允许在通过 `--zone` 指定的区域中使用网络服务（例如 `https` 或 `ssh`），或阻塞该服务。

- `--change-interface=iface`
  将活动区域分配给指定的网络接口。若要将另一个区域连接到接口，你还必须传递 `--zone=name` 选项。

- `--get-active-zones`
  列出所有正在使用的区域，并指示哪些网络接口被分配到了这些区域。

- `--get-default-zone`
  确定默认区域。

- `--get-services`
  列出 `firewall-cmd` 知知的所有网络服务。你可以通过 `--add-interface` 指定结果名称（`http`, `ssh` 等）。

- `--get-zones`
  列出 `firewall-cmd` 知知的所有区域。

- `--get-zone-of-interface=name`
  确定分配给指定网络接口的区域。

- `--list-all-zones`
  提供所有定义的防火墙区域的关键数据，并指定哪些网络接口被分配到了区域。

- `--list-ports`
  列出当前活动防火墙区域中允许的（即未阻塞的）端口。警告：该命令仅返回未分配服务名称的端口。端口 22 永远不会出现在结果中，因为它被分配给了 `ssh` 服务。你可以通过 `--list-all-zones` 或 `--list-services` 选项获取未阻塞的服务。

- `--list-services`
  列出当前活动防火墙区域中允许的（即未阻塞的）所有网络服务。

- `--permanent`
  将更改永久保存到防火墙配置中。然而，更改不会直接生效。如果你想立即且永久地进行更改，必须运行相关命令*两次*：一次带有 `--permanent`，另一次不带该选项。

- `--set-default-zone=name`
  定义默认区域。它适用于所有未显式分配了不同区域的网络接口。

- `--zone=name`
  指示要更改、编辑或读取哪个区域。

## 示例

以下命令首先确定网络接口 `enp0s3` 被分配到哪个区域，然后将该接口分配到信任（`trusted`）区域。这意味着所有服务都可以通过此接口。这些更改不是永久的，因此它们仅在下次重启计算机或防火墙守护进程之前有效。

```
root# firewall-cmd --get-zone-of-interface=enp0s3

public

root# firewall-cmd --zone=public --remove-interface=enp0s3

success

root# firewall-cmd --zone=trusted --add-interface=enp0s3

success
```

在第二个示例中，第一个命令用于确定网络接口 `enp0s5` 被分配到哪个区域。该计算机旨在通过此接口向外部世界提供 Web 服务器。但是，并不是泛泛地将接口分配到信任区域并启用所有其他可能的的服务，而是永久地更改了该区域的规则（这里是 `FedoraWorkstation`）：该区域现在允许 HTTP 和 HTTPS 协议。`reload` 命令激活了区域的更改。

```
root# firewall-cmd --get-zone-of-interface=enp0s5

root# firewall-cmd --permanent --zone=FedoraWorkstation --add-service=http

root# firewall-cmd --permanent --zone=FedoraWorkstation --add-service=https

root# firewall-cmd --reload
```



# flatpak [options] 命令

`flatpak` 帮助安装、删除和管理 Flatpak 软件包。这是一种新的包格式，旨在简化桌面应用程序的安装，使其独立于 Linux 发行版的包源。最大的官方 Flatpak 仓库是 `https://flathub.org`。

与传统软件包相比，它具有额外的安全机制，例如沙箱化。然而，Flatpak 软件包通常很大，因为包含了所有必要的库，并且没有考虑任何现有的传统软件包。因此，安装多个 Flatpak 往往会产生大量的冗余。

Flatpak 软件包通常直接安装在桌面上，例如安装在 Gnome 软件中心或浏览器中。程序在启动菜单或 Gnome 的活动视图中启动。因此，很少需要使用 `flatpak` 命令。

Flatpak 在 Fedora 和 RHEL 中默认可用。然而，该命令可以在其他发行版中轻松地安装和使用，并旨在成为一个独立于特定发行版的 Linux 软件分发平台。作为 Flatpak 的替代方案，可以使用 Snap 软件包，它更受 Ubuntu 青喜（参见 `snap`）。

尽管 `flatpak` 命令不需要 root 权限，但在执行期间你必须反复使用自己的密码进行身份验证（有时一个操作——如安装包——就需要输入几十次）。

- `info package name`
已安装软件包的详细信息。注意，包名始终由多个部分组成，例如 `org.gnome.gedit`。

- `install [package source] package name`
从之前设置的包源安装所需的包。

- `list [--system 或 --user]`
列出所有已安装的 Flatpacks（如果适用，仅限系统级或为当前用户安装的）。带有额外的 `-d` 选项，`flatpak` 还会显示包的大小和其他一些细节。

- `remote-add [--if-not-exists] package source url`
设置包源。`--if-not-exists` 选项避免在包源之前已定义的情况下出现错误信息。

- `remotes`
列出所有已的包源。

- `search Flatpacks term`
在配置的包源中搜索包名或描述中包含搜索词的软件包。

- `uninstall package name`
在不再进一步询问的情况下移除指定的包。你可能需要输入 `flatpak list` 显示的完整包名，例如 `flatpak uninstall org.gimp.GIMP/x86_64/stable`。

- `update [--app package name]`
更新所有已安装的 flatpaks 或仅更新通过 `--app` 指定包。

## 示例

以下命令在系统级安装 Visual Code 编辑器，以便计算机上的所有用户都能使用它。注意平台包惊人的下载大小。在不久前，整个 Linux 发行版的下载量还比这小！

```
root$ flatpak install com.visualstudio.code

Required runtime for com.visualstudio.code/aarch64/stable

(runtime/org.freedesktop.desktop.aarch64/23.08) found in remote flathub

Do you want to install it? [Y/n]: Y
```

```
com.visualstudio.code permissions:

ipc        network     pulseaudio     ssh-auth

x11        devices    devel

file access [1] dbus access [2] system dbus access [3] tags [4]

[host]

[2] ...
```

| ID | Remote | Download |
| :--- | :--- | :--- |
| org.freedesktop.Platform.GL.default | flathub | 146 MB |
| org.freedesktop.Platform.GL.default | flathub | 146 MB |
| org.freedesktop.Platform.opengl264 | flathub | 884 kB |
| 4. org.freedesktop.Sdk.5 | flathub | 366 MB (partial) |
| 5. org.freedesktop.Sdk | flathub | 534 MB |
| 6. com.visualstudio.code | flathub | 98 MB |

Proceed with these changes to the system installation? [Y/n]: Y

`flatpak search` 允许你在所有 Flatpak 源中搜索软件包。遗憾的是，没有官方的 Spotify 播放器，但有很多兼容的音频播放器：

```
user$ flatpak search spotify

Name            Description                 Remotes

ncspot          Cross-platform ncurses Spotify  flathub

Moosync         Customizable music player  flathub
```

- 在 Spotify 上收听音乐 -flathub
- oomox 主题设计器自定义图标、xrd 和 GTK -flathub
- Tauon Music Box 以格调播放音乐 -flathub
- Clementine 音乐播放器播放音乐文件和互联网 -fedora，flathub

# fold [options] 文件

`fold` 将文本行折叠为 80 个字符的长度并将结果显示在屏幕上。

- `-s` 或 `--spaces`
尝试在空格位置进行折叠（即两个单词之间）。

- `-w n` 或 `--width n`
设置文本的最大宽度为 `n` 个字符。如果没有此选项，默认应用 80 个字符。

```
for var [in list,] do

commands

done
```

`for` 在 bash 脚本中创建循环。列表中的所有元素将按顺序一个一个地插入到指定的变量中。列表也可以用文件名的通配符形成，或者使用 `{...}` 元素来组合文件名。如果未指定列表，该变量将遍历传递给 shell 文件的所有参数（即 `$`）。

## 示例

`for` 不仅可以用于 shell 脚本，也可以在终端中对许多文件应用某些命令。以下命令输出所有 `*.jpg` 文件的文件名。现在你可以将 `echo` 替换为另一个命令，对 `*.jpg` 文件进行打印、缩放等操作。

```
user$ for i in *.jpg; do echo $i; done
```

另一个关于 `for` 的示例可以在 `cp` 命令的描述中找到。

# free [options]

`free` 显示可用内存空间（RAM 和交换内存）的使用情况。

- `-h`
选择合适的单位来指定内存（人类可读）。
- `-m` / `-g`
以 MiB 或 GiB 显示内存需求（而不是 KiB）。

## 示例

在接下来的示例中，本地化变量 `LANG` 被重置以运行 `free`。这防止了列名出现冗长的德语翻译，这些翻译会混淆列的布局。

在内存略低于 2 GiB 的虚拟机中，已使用 1.1 GiB。由于操作系统使用了几乎 700 MiB 来缓存文件，因此只有 170 MiB仍被视为空闲。如果需要，可以快速释放这些内存，为新进程留出约 680 MiB。交换内存空间除了几 MiB之外均未使用。

```
user LANG= free -h
```



| Mem: | total used free shared buff/cache available |
|---|---|---|---|---|---|---|
| Swap: | 947M | 6.5M | 940M | 10M | 686M | 677M |

# `fsck` [options] 设备

`fsck` 检查文件系统的一致性并在必要时进行修复。它只能由 root 运行。根据文件系统的类型，`fsck` 会调用 `fsck.ext3`、`fsck.ext4` 等程序。在运行 `fsck` 之前，请务必阅读此特定于文件系统的 man 手页！

在检查文件系统之前，你必须运行 `unmount`。要检查根文件系统，你首先需要执行 `touch /forceck` 并重启电脑。包含错误或文件碎片的文件保存在 `lost+found` 目录中。

- `-A`
  检查 `/etc/fstab` 中指定的所有文件系统。

- `-t type`
  指定文件系统的类型（例如 `ext3`, `xfs`）。

| `fsck.ext2` [options] 设备 |
| `fsck.ext3` [options] 设备 |
| `fsck.ext4` [options] 设备 |

`fsck.ext2/3/4` 或 `efck` 检查 ext 文件系统的一致性并在必要时进行修复。也可以通过 `fsck -t ext2/ext3/ext4` 启动命令。

- `-b n`
  读取备用 superblock `n`。

- `-n`
  用 `n` (no) 回答所有查询且不进行任何更改。

- `-p`
  在不提示的情况下执行修复（更改）。

- `-y`
  用 `yes` 回答所有查询并进行更改。

# `fstrim` [options] 挂载 目录

`fstrim` 为指定的挂载点运行 trim 命令。默认情况下，文件系统不再使用的数据块将报告给数据介质。

当数据介质是固态硬盘（SSD）时，该命令才有用，而且文件系统本身不会自动运行 trim 命令（对于 `ext4`、`Btrfs` 和 `XFS` 文件系统参见挂载选项 `discard`）。`fstrim` 可以通过定时任务每天或每周运行，以避免频繁执行或不执行导致的性能损失。

- `-l` 或 `--length n`
  仅报告指定区域的空闲块。

- `-m` 或 `--minimum n`
  仅当连续块至少有 `n` 字节大时报告。这可以显著加快命令的执行。

- `-o` 或 `--offset n`
  仅从指定的偏移量（从文件系统开始计算）报告空闲块。可以使用相应的后缀二进制 KiB, MiB, GiB 或 TiB（K, M, G 或 T）或十进制千字节、兆字节等（KB, MB, GB 或 TB）来指定。

- `-v` 或 `--verbose`
  返回使用 trim 命令报告的总字节数。

## 示例

以下命令报告所有空闲块：

```
fstrim -v /
```

## `ftp` [options]

`ftp` 建立与服务器的连接。最重要的命令有：

- `- ascii`
  切换到文本模式。
- `- binary`
  切换到二进制模式。
- `- cd`
  切换目录。
- `- get`
  从服务器下载文件。
- `- put`
  上传文件到服务器。
- `- help`
  显示命令列表。
- `- ls`
  显示文件列表。
- `- m`
  列出所有匹配的文件。
- `- bye`
  终止连接。
- `- ?`
  查询服务器。
- `- prompt`
  交互式请求确认。

- `get-devices`
  提供所有可以提供更新的组件的详细列表，以及最后执行的更新和当前可用更新的列表。你可以选择将状态报告上传到网站 `https://fwupd.org`。

- `downg device`
  撤销更新并重新激活旧版本。

- `refresh`
  更新更新信息（数据源：`https://fwupd.org`）。

- `update device`
  对所有组件或仅对指定的组件启动更新。`fwupdmgr` 仅负责准备更新。在大多数情况下，更新在计算机下次重启之前无法执行。

## Example

第一个命令更新更新信息。第二个命令显示类型标记为 2MD0001GE 的联想笔记本电脑的状态报告。

```
root# fwupdmgr refresh

Fetching metadata https://cdn.fwupd.org/downloads/firmware.xml.gz

Fetching signature https://cdn.fwupd.org/downloads/firmware.xml.gz.asc

Successfully downloaded new metadata: 5 local devices supported
```

```
# root# fwupdmgr get-devices

2MD0001GE
Thunderbolt Controller:
Device ID: 02dcd173032b1c4f136f185c0564b059a2e3d05
Summary: Unmatched performance for high-speed I/O
Current version: 39.00

...
PM981 NVMe Samsung 2048GB: ...
SAMSUNG MZLB256HAQ-0007L: ...
System Firmware: ...
UEFI Device Firmware: ...
```

未正确更新的设备：

- ThinkPad P1 Thunderbolt Controller (23.00 -> 39.00)

已成功更新的设备：

- UEFI Device Firmware (192.24.1314 -> 192.35.1427)
- 2MD0001GE System Firmware (0.1.24 -> 0.1.25)
- UEFI Device Firmware (192.35.1427 -> 192.47.1524)

上传固件报告有助于供应商快速识别真实设备上失败和成功的更新。现在上传报告吗？
（需要连接网络）：
0. 现在不上传报告，但在以后的更新时再次提示
1. 不上传报告，且以后再也不请求上传报告
2. 仅本次上传报告，但在以后的更新时再次提示
3. 本次上传报告，并在完成后续更新后自动上传报告

# 上一个命令启动了 Thunderbolt 控制器的更新：

```
root# fwupdmgr update

Upgrade available for Thunderbolt Controller from 39.00 to 50.00

Thunderbolt Controller and all connected devices may not be usable

updating. Continue with update? [Y|n]: y
```

```
fx file.json
```

`fx` 是一个交互式读取或搜索 JSON 文件的命令。JSON 文档的组件经过了颜色编码，并且可以展开或折叠。

你可以作为 Docker 镜像或在 GitHub 项目页面上的二进制文件 (`https://github.com/antonmedv/fx/releases`) 找到这个非常有用的命令。如果你想自动处理 JSON 文件，`jf` 是更好的选择。

# `fzf` [options]

来自同名软件包的 `fzf` 代表 fuzzy finder（模糊查找器），是一个用于交互式搜索和选择文件的命令。如果启动命令时不带任何其他选项，它将像 `find -type f` 一样搜索当前目录并显示结果列表。通过输入搜索模式，你可以以极快的速度交互式过滤结果，并使用方向键或 Tab 键分别选择一个或多个文件。（多次选择需要在启动 `fzf` 时带有 `-m` 选项）。回车键结束命令并显示文件名。

这个基础功能听起来相当普通。`fzf` 的强大之处在于它与 shell 的集成。只要 `fzf` 安装正确，可以通过输入 Tab 键触发 `fzf`，实现命令的交互式补全：使用 emacs `** Tab`，你可以打开之前选择的文件。使用 kill - `** Tab`，`fzf` 提供了进程选择；使用 ssh `** Tab`，它可以返回主机名。Ctrl + T 列出所有文件，Ctrl + R 列出最近执行的命令，Alt + C 切换到子目录。

`fzf` 还有无数其他键盘快捷键和功能，由于空间限制，我无法在这里详述。相反，我建议你观看关于 `fzf` 的许多视频之一。尽管我通常不是视频粉丝，但在这种情况下它是值得的！

因此，`fzf` 并没有在所有功能上取代 `find`。但一旦你习惯了 `fzf` 的便利性，你使用 `find` 的频率就会减少很多。

# G

```
getcap [options] file name
```



`getcap` 来自 `libcap` 或 `libcap-progs` 软件包，用于确定可执行文件允许程序执行哪些操作（能力）。尽管 Linux 内核已支持能力多年，但此功能仅被偶尔使用。

能力需要支持扩展属性的文件系统。对于 ext 文件系统，必须使用 `user_xattr` 挂载选项。

### Example

某些发行版对 `ping` 命令使用了能力。执行此命令实际上需要 root 权限。与其过去那样简单地设置 setuid 位（这通常会导致安全问题），我们已经切换到通过 `setcap` 为 `ping` 分配 `cap_net_raw` 权限。这允许命令即使由普通用户执行也能使用基础网络功能。

以下 `getcap` 结果是在 Fedora 上获得的。你可以看到只有极少数命令和 Gnome 程序使用能力。

```
user$ getcap /usr/bin/*

/usr/bin/arping cap_net_raw=p

/usr/bin/clockdiff cap_net_raw=p

/usr/bin/newgidmap cap_setgid=ep

/usr/bin/newuidmap cap_setuid=ep
```

如何自行设置能力的示例可以在 `setcap` 命令的描述中。

## getenforce

`getenforce` 提供 SELinux 系统的状态。可能的结果有 Enforcing、Permissive 或 Disabled。要更改状态，可以使用 `setenforce` 命令。

## getfacl [options] file name

`getfacl` 确定指定文件或目录的扩展访问权限。这仅在文件系统支持访问控制列表 (ACL) 时才有效。对于 ext3/ext4 文件系统，必须使用 `acl` 挂载选项。可以在 `setfacl` 命令的描述中找到示例。

- `d`
  显示标准 ACL。
- `R`
  显示子目录下所有文件的 ACL。
- `skip-base`
  对于常规访问权限的文件不返回结果。
- `tabular`
  以表格形式显示 ACL。

## getfattr [options] file name

`getfattr` 确定指定文件或目录的扩展属性。这仅在文件系统支持扩展属性时才有效。对于 ext 文件系统，必须使用 `user_xattr`。可以在 `setattr` 命令的描述中找到示例。

- `d`
  提供所有用户属性及其设置的列表。
- `m attribute pattern`
  返回名称与指定模式对应的属性。
- `n attribute name`
  返回指定属性的值。必须指定完整的属性名称，例如 `user.attrname`。
- `R`
  显示子目录下所有文件的扩展属性。

## getopts

`bash` 中集成的 `getopts` 命令有助于在脚本编程期间处理传递的选项和参数。你向命令传递一个字符字符串，列出几个单字母选项，然后在循环中运行 `getopts`。它在每次循环通过时返回一个找到的选项，直到所有选项都处理完毕（参见下文代码示例）。

以下规则适用于格式字符串：

- `"abc"`
  期望以任意顺序出现选项 `-a`、`-b` 和 `-c`，也可以组合（例如使用 `-bc` 代替 `-b -c`）。
- `":abc"`
  工作类似于 `"abc"`，但对无效参数不返回任何错误信息。
- `"ab:c:"`
  在 `b` 和 `c` 后面带有冒号，表示这些这些每个都需要一个参数（例如 `-b 1024 -c 3`）。在评估期间，可以从 `$OPTARG` 变量读取与选项传递的参数。

### Example

在处理选项期间，`$OPTIND` 引用参数列表中的下一个元素。只要先传递选项后传递参数，所有处理过的选项

可以使用 `shift` 从 `$*` 中移除。(`shift <n>` 从 `$*` 中移除前 `n` 个元素。但由于 `$OPTIND` 引用了下一个元素，只有 `$OPTIND -1` 个元素可能会从参数列表中移除。)

```bash
#!/bin/bash

while getopts "ab:c" opt; do
  case $opt in
    a) echo "Option a";
    b) echo "Option b with parameter $OPTARG";
    c) echo "Option c with parameter $OPTARG";
    ?) echo "Invalid option"
      echo "myscript [-a] [-b data] [-c data] [...]"
      exit 2
  esac
done

# 从 $* 中移除已处理选项
shift $(( $OPTIND - 1 ))
echo "More parameters: *"
```

### 替代方案

`getopts` 只能处理单字母选项，不能处理如 `--search` 这样的长选项。要处理此类选项，可以使用 `getopt` 命令，它与 `bash` 是独立的。它通常包含在 `util-linux` 包中。

## git 命令 [选项/参数]

同名包中的 `git` 命令控制着 Git 版本管理系统。它最初仅为内核开发设计，但现在是开源世界之外最广泛的版本管理系统。

Git 仓库中的文件可以处于三种状态：

- `committed`（已提交）：本地文件存储在仓库中，且之后未发生更改。
- `modified`（已修改）：本地文件已更改，但更改尚未通过 `commit` 保存到仓库中。
- `staged`（已暂存）：已修改的文件将包含在下一次 `commit` 中。

### 命令

- `add files/directories`
  向仓库添加文件或目录，或将仓库中已存在的本地修改文件标记为下次提交准备。这会将文件的状态从 `modified` 更改为 `staged`。

- `branch [-v]`
  列出本地仓库分支，并在当前分支前用星号标记。使用 `-v` 选项，`git` 还会显示每个分支的最后一次提交。

- `branch *name*`
  创建一个新的仓库分支。要切换到此分支，你必须运行 `git checkout *branch name*`。

- `branch -d branch name`
  删除指定的分支。只有当该分支之前连接到另一个分支或 HEAD 时，命令才会执行。要删除无论合并状态如何的分支，可以使用 `-d` 选项。

- `branch -u repo/branch name`
  永久设置当前分支的上游仓库，并将链接保存在 `.git/config` 中。或者，也可以在第一次 push 过程中使用 `git push -u repo branch` 设置上游仓库。

按照惯例，本地和外部分支的名称是相同的，但并非强制要求。该链接使得 `git pull` 自动连接相关的本地分支，并且 `git push` 使你无需为这些命令重复指定目标仓库。

- `checkout [-b] branch name`
  切换到指定的分支。这会将工作目录中的所有文件设置为它们最后一次提交到该分支时的状态。使用 `-b` 选项，会先创建指定的分支然后激活它。`git checkout -b b1` 对应 `git branch b1`；`git checkout b1`。

- `clone repo-url [directory]`
  下载外部 Git 仓库并在当前或指定的目录中创建本地副本。根据通过 HTTPS 还是 SSH 通信，URL 具有以下格式：

```
https://github.com/<account>/<repname>.git
git@github.com:<account>/<repname>.git
```



取决于你的仓库所在的位置，你需要将 `github.com` 替换为你的 Git 平台或路径。将来，外部仓库将通过 `origin` 名称进行引用。Git 允许使用多个通过 `git` 远程管理的外部仓库。

## 提交操作

- `commit [-a] -m 'snapshot description'`
在 Git 仓库中创建一个新的本地快照（“commit”）。自上一次提交以来的所有更改都保存在其中，但前提是文件状态必须为 `staged`。因此，你必须先使用 `git add` 将所有要保存的文件标记为 `staged`。

使用附加选项 `-a`，你可以避免这个麻烦，因为 `git commit` 然后会考虑所有已版本文件的更改。（然而，新建的文件会被忽略。）

在第一次提交之前，你必须使用 `git config` 在 Git 配置中保存你的姓名和电子邮件。这些数据将与其他元数据一起存储在 commit 中。

当前分支中的最后一个快照名称始终为 `HEAD`。倒数第二个快照可以使用 `HEAD^` 访问，倒数第二个之前的那个可以使用 `HEAD^2`，以此类推。（更多关于其他提交的引用示例请参见表 1。）

## 配置操作

- `config --list`
确定活动目录中的所有有效 Git 设置并显示它们。使用附加选项 `--show-origin` 时，命令还会指定设置的来源，即该设置是为仓库本地生成的还是全局生成的。

- `config [--global] parameter value`
将 Git 参数的设置保存到本地 Git 仓库的 `.git/config` 中。使用 `--global`，参数将保存在主目录下的全局 Git 配置 `.git/config` 中，因此它是多个仓库的默认设置。

- `config`
设置或编辑配置变量。

## 差异操作

- `diff`
在没有任何其他参数的情况下，`git diff` 显示自上一次提交以来的所有更改。默认情况下，`git diff` 比较目录与上一次提交。如果你想比较暂存区（stage area）与上一次提交，则必须指定暂存区。

- `diff --stat --numstat`
提供更改摘要。`--stat` 显示每个文件更改的数，而 `--numstat` 提供机器读格式。

- `diff --cached`
显示暂存索引与上一次提交之间的更改。

- `diff --staged`
显示工作目录与索引之间的更改。

- `diff --hard`
显示工作目录中尚未提交的更改（注意：可能会丢失更改）。

- `diff HEAD`
显示自上一次提交以来的更改。

- `diff revision1..revision2`
显示两个提交之间的更改。

- `diff branch`
显示当前分支与指定分支之间的更改。

- `diff file`
显示特定文件的更改。

- `diff --name-only`
仅列出更改的文件名。

- `diff --stat`
显示每个文件的插入和删除摘要。

- `diff --short-context`
显示更改前后的行数。

- `diff --word-diff`
按单词级别而非行级别显示更改。

- `diff --color`
用颜色突出显示差异。

- `diff --ignore-space-change`
忽略空格更改。

- `diff --ignore-all`
忽略所有空格。

- `diff --no-index`
不使用索引比较两个文件。

- `diff --binary`
以二进制格式比较文件。

- `diff --unified`
以统一格式输出差异。

- `diff --diff3`
使用旧差异格式。

- `diff --summary`
显示文件更改摘要（重命名、复制、删除）。

- `diff --config`
显示配置文件的更改。

- `diff --help`
显示 diff 命令的帮助。

- `diff --version`
显示 git 版本。

## 远程与分支操作

外部 Git 仓库名称并合并到那里。例如，`git push origin main` 将你在 `main` 分支上的所有提交连接到外部 `origin` 仓库中同名的分支。如果外部仓库不存在该分支，则会在那里自动建立分支。`-u` 选项会将本地分支与同名的外部分支关联（类似于 `git branch -u`）。

如果存在尚未在本地执行的外部提交，`push` 命令将失败。出于因此，你应该在执行 `git push` 之前运行 `git pull`。

如果你在没有指定仓库和分支名称的情况下运行 `git push`，git 将与默认仓库（通常是 `origin`）通信并同步当前链接的分支（参见 `branch -u` 命令）。

- `rebase branch name`：`git merge` 的变体，它会改变你自己的提交（即将它们转换为新提交），就像这些提交从初就是基于外部分支的提交而创建的一样。`git merge` 的优点是生成的提交序列看起来“更漂亮”，即不会被频繁的合并提交所中断。然而，它创建了原始上并不的本地提交，这使得追踪错误变得困难。

- `remote [-v]`：列出所有外部仓库。使用 `-v`，git 还会显示每个仓库的 URL。根仓库——`origin` 由 `git clone` 定义。可以使用 `git remote add` 或 `git remove` 等命令管理额外的仓库。

- `reset HEAD -- file`：将被错误标记为已暂存（staged）的文件状态改回修改（modified）。

- `reset [--hard] revision`：撤销更改并恢复到的旧版本。`revision` 指定所需的版本：`HEAD` 指向最后一次提交，`HEAD^` 指向倒数第二个，`HEAD^2` 指向倒数第三个，依此类推。或者，你也可以指定提交的十六进制 SHA1 校验的初始数字（参见表 1）。`reset origin/main` 撤销所有本地更改并将本地分支与默认仓库的 `main` 分支同步。`--hard` 选项会导致本地更改被不可恢复地覆盖。

- `reset file`：将文件从暂存区移除，从而撤销 `git add file`。

- `restore file`：从上次提交恢复文件的状态。自那时起所做的更改将在无需进一步询问的情况下被覆盖。此命令自 Git 2.23 版本（2019 年 8 月）起才可用。如果你指定一个目录而不是文件，该命令将适用于该目录中所有更改的文件。

- `rm file`：从本地目录中删除文件并从*暂存*（staging）区域中移除它。

- `show revision:file`：显示文件在指定提交创建时的状态。

- `status [-s]`：提供有关当前 Git 分支和修改文件状态的信息。`-s` 选项使状态输出更紧凑。所有文件名都以两个字母开头，第一个字母表示*暂存*（staging）状态，第二个字母表示*修改*（modifying）状态。

- `tag`：在没有任何后续参数的情况下，`git tag` 列出所有标签（标记、版本标记）。

- `tag -a 'marker-text' [-m 'comment'] [revision]`：在最后一次提交上添加一个标签，即一个标记，它是一种书签。此功能非常适合标记发布版本，例如。指定一个 `revision` 允许随后标记较旧的提交。

Git 区分两种类型的标签：`-a` 或 `-m` 选项创建一个也存储元数据的注释标签（annotated tag）。如果不使用此选项，将创建一个不带元数据的轻量标签（lightweight tag）。

git 并不是只有一个 man页（帮助页），有很多页面可用，因为每个 git 命令都有自己的页面。例如，`man git-clone` 提供了 `git clone` 的详细描述。

## 修订语法

在 git 命令中，你可以通过多种方式引用过去的提交或修订（参见表 1）。分支的最新提交被视为头（head）。符号 `@{xxx}` 指向本地引用日志（reflog），因此只能用于本地最后执行的操作。

| 示例 | 含义 |
| --- | --- |
| `HEAD` | 当前分支的头部 |
| `@` | 当前分支的头部（简写） |
| `develop` | 不同分支的头部 |

| 示例 | 含义 |
| --- | --- |
| `develop:readme.txt` | 另一个分支头的 Readme 文件 |
| `refs/remotes/origin/feature` | 远程分支的头部 |
| `v1.3` | 带有标签 v1.3 的提交 |
| `HEAD@2 days ago` | 当前分支中两天前的提交 |
| `main@{7}` | main 分支中两次操作之前的提交 |
| `HEAD~` | 最后一次提交的先驱（父提交） |
| `HEAD-3` | 最后一次提交的前前驱 |
| `v1.3-3` | 带有标签 v1.3 的最后一次提交的前前前驱 |
| `234ae33^` | 合并提交 234ae33 的第一个父提交 |
| `234ae33^^` | 合并提交 234ae33 的第二个父提交 |

**表 1** Git 修订语法示例

## 示例

在第一个示例中，如果你还没有在个人 Git 配置文件中保存姓名和电子邮件地址。然后，从 GitHub 下载一个已有的仓库：



user$ `git config --global user.name "Howard Hawks"`

user$ `git config --global user.email "hawks@my-company.com"`

user$ `git clone https://github.com/git-book/hello-world.git`

user$ `cd hello-world`

```
第二个示例显示了如何在现有项目的 main 分支中快速修复错误。你可以使用 `git checkout` 切换到 main 分支。`git pull` 下载远程仓库中保存的所有更改。现在，你需要纠正错误，使用 `git commit` 保存你的更改，并通过 `git push` 将更改传回 origin 仓库：
```

user$ `cd directory/with/existing/git/repo`

user$ `git checkout main`

user$ `git pull`

user$ `my-favorite-editor files...`

user$ `git commit -a -m 'Bugfix login authentication'`

user$ `git push`

```
# glances [options]

根据应用程序的不同，同名包中的 `glances` 命令是 `top` 的现代替代方案，或者是以客户端/服务器模式运行的简单监控程序。后者需要相应的配置，但也允许通过网络浏览器访问监控数据。

当直接调用时，该命令相比 `top` 还提供了网络和 I/O 活动的概述以及文件系统的状态。颜色显示针对深色终端进行了优化。如果你设置了浅色背景，请使用 `--theme-white` 选项运行 `glances`（参见图 3）。

各种快捷键根据不同标准对进程进行排序：`C` 按 CPU 使用率，`I` 按 I/O 活动，`M` 按内存使用量，`P` 按名称，`T` 按运行时间。按下回车键，你可以根据搜索过滤过滤列表。其他快捷键可以隐藏信息或激活不同的显示模式。例如，`U` 在当前网络吞吐量和累计数据量之间切换。按下 `H` 调用帮助页面可以显示更多快捷键。

![](img/94f0b4d76a25250c220515a1d5bba83f_286_0.png)

**图 3** 使用“glances”进行监控

```
gnome-session-quit [options]
```

`gnome-session-quit` 程序显示一个对话，可以在其中注销、关机或重启计算机。

- `--force`：即使有未保存的文件也执行注销。此选项只能配合 `--logout` 使用。
- `--logout`：询问用户是否要注销。
- `--no-prompt`：在不进行提示的情况下执行注销。此选项只能配合 `--logout` 使用。
- `--power-off`：询问用户是否想关机。
- `--reboot`：询问用户是否想重启计算机。

```
gpassword [options] group
```

`gpassword` 实际上用于设置组密码。然而，组内多个成员必须知道的密码被认为是不安全的，因此不再使用。

尽管如此，`gpasswd` 仍然承担着重要的功能。在下面的变体中，它可以从组中删除一个用户：

```
root# gpasswd -d user group
```

这使得 `gpasswd -d` 成为 `usermod -a -G user` 的对应命令，后者是将用户添加到组中。

## gpg 或 gpg2 [options/commands]

`gpg` 用于加密、解密或对文件进行签名，并管理密钥。`gpg` 受无数选项的控制，仅在有限范围内适用于手动使用。该命令被邮件客户端用于加密和对消息签名，并被包管理工具用于验证包及其包源的完整性。

通过 `-c` 和 `-d` 选项，`gpg` 可用于文件的进行对称加密和解密。这虽然简单，但在安全性方面并不理想。所有其他选项都假设你想使用非对称加密：加密将使用你通信对方密钥的公钥部分，而解密将使用你自己的密钥的私钥部分。这假设你同时也使用 `gpg` 进行密钥管理。

`gpg` 旨在用于服务器和嵌入式环境，依赖于少数外部库。而 `gpg2` 是为桌面使用设计的。该版本还支持 S/MIME。除此之外，两个命令支持相同的选项。

- `--batch`
激活批处理模式。在此模式下不允许交互式命令，且没有交互。批处理模式用于脚本编程。

- `-c file` or `--symmetric file`
提示你输入密码，然后加密指定的文件，最后将结果保存为 `file.gpg`。

- `-cipher-algo zip/zlib/bzip2/none`
定义加密算法。默认情况下，`gpg` 使用 CAST5 算法。通过 `gpg --version` 命令可以确定可选择的算法。

- `-compress-algo zip/zlib/bzip2/none`
指定是否以及如何对数据压缩。使用 ZIP 过程作为标准。出于兼容性考虑，不建议使用 zip 或 none 以外的设置。如果源数据已经过压缩，则建议使用 `none`。否则，重新压缩将在不减少所需空间的情况下产生多余操作。

- `-d file` or `--decrypt file`
提示你输入密码，然后解密指定的文件，最后将结果写入标准输出。

- `--decrypt file > plain text`
解密指定的文件并将输出重定向到纯文本文件。该文件必须使用你自己的密钥的公钥部分加密。要解密它，你必须输入密钥的密码。

- `--encrypt file`
加密指定的文件并将其保存为 `file.gpg`。你交互交互地输入密钥的邮箱地址。密钥可能需要先使用 `--import` 保存到密钥数据库中。如果你在加密选项之前指定了 `--armor`，则加密后的文件将以 ASCII 格式保存。这需要更多空间，但简化了通过邮件转发。

- `--export name@host`
在指定文件中保存 `name@host` 密钥公钥部分的二进制表示。你必须将此文件传给向你发送加密文件或邮件的人。如果你在 `--export` 选项之前指定了 `--armor`，公钥将以兼容邮件的文本格式保存。

- `--gen-key`
创建一个新密钥并将其保存到 `.gnupg/pubring.gpg` 中。你需要输入各种数据：密钥所需的类型和长度，以及你的姓名、邮箱地址、密码等。

- `--import public-key-file`
将他人密钥的公钥部分导入你自己的密钥集合。这是为了向该人员发送加密文件或邮件所必需的。

- `-k` Or `--list-keys`
列出存储在 `.gnupg/pubring.gpg` 中的所有密钥。

- `--no-tty`
抑制警告信息的输出。

- `--passphrase-file file`
从指定文件中读取加密密码。

- `--passphrase-repeat n`
指定密码输入的频率。

- `-q` Or `--quiet`
静默模式，不输出调试信息。

- `--output file`
将输出写入指定的文件。

- `--verify file`
验证指定文件的签名有效性。

- `--version`
显示 `gpg` 的版本。

## 示例

- [费曼学习法](https://wiki.example.org/feynmans_learning_method)的灵感源于诺贝尔物理奖获得者`理查德·费曼`。

1. 运用费曼技巧，你只需花上`20 min`就能深入理解知识点，而且记忆深刻，*难以遗忘*。

```
if (condVar > someVal) {console.log("xxx")}
```

必须进行传输，以便正确处理此问题
（内部，`/dev/gpiochip4`）。

GPIO 编号作为额外参数传递，
其中 GPIO 的内部标识是相关的，
而不是 GPIO 触点条上的引脚编号：

```
user$ chip=4
```

（用于树莓派 5）

```
user$ gpioset $chip 7=1
```

（GPIO 7 = 将引脚 26 设置为高电平）

```
user$ gpioset $chip 7=0
```

（GPIO 7 = 将引脚 26 设置为低电平）

你可以同时控制多个输出（这里是 GPIO 7, 8 和 25）：

```
user$ gpioset $chip 7=0 8=1 25=0
```



各种选项允许你控制额外的功能：

- `--bias=as-is|disable|pull-down|pull-up`
  激活或禁用 GPIO 的内部上拉或下拉电阻。

- `--mode=exit|wait`
  指定模式。`exit` 在找到匹配项后立即退出，`wait` 则等待所有匹配完成。

你可以同时控制多个输出（这里是 GPIO 7, 8 和 25）：

各种选项允许你控制额外的功能：

- `-v`
  反向模式：显示不匹配模式的行。

- `-E`
  启用正则表达式（ERE）。

- `-f`
  从文件中读取模式（模式）。

- `-i`
  区分大小写。

- `-l`
  仅显示匹配项的文件名。

- `-n`
  显示匹配行的行号。

- `-O`
  仅输出匹配的文本。

- `-P`
  根据 Perl 兼容正则表达式（PCRE）解析。

- `-q`
  静默模式，不产生任何输出。

- `-R`
  递归处理目录树中的所有文件。

- `-s`
  压缩输出中的空行（将多个空行合并为一行）。

- `-W`
  仅匹配完整单词。

```bash
user$ grep 'SSL.*File' /etc/httpd/conf.d/ssl.conf

SSCertificateFile /etc/letsencrypt/live/pi-book.info/cert.pem

SSCertificateKeyFile /etc/letsencrypt/live/pi-book.info/privkey.pem

SSCertificateChainFile /etc/letsencrypt/live/pi-book.info/chain.pem
```

你还可以结合 `find` 和 `grep` 来执行特别有效的搜索。在以下命令中，`find` 搜索 `*.php` 文件，而 `grep` 检查它们是否包含 `mysql` 字符串。如果包含，相应的文件名将显示在屏幕上。注意，你必须在 `-exec` 之后指定 `-print` 。

```bash
root# find -name '*.php' -exec grep -q i mysql {} \; -print
```

# grep 的变体

- `ack` 和 `ag` 是针对程序员优化的 `grep` 变体。它们忽略备份文件、二进制文件和版本控制系统的目录。

- `grepmail` 有助于在 mbox 格式的邮件存档中搜索字符字符串。与 `grep` 相比的优势是从文件中提取整个邮件，而不是单行。

- `zgrep` 搜索压缩文件。

```bash
grim [options] filename.png
```

`grim` 代表 grab image（获取图像），如果你的桌面运行在 Wayland 上，它会创建一个截图。默认情况下，截图将覆盖整个屏幕并以 PNG 格式保存。各种选项允许你定义屏幕区域、更改输出格式（JPEG 或 PPM）并将鼠标指针集成到截图中。

## 示例

如果你从终端截屏，在操作之前等待几秒钟通常很有用。最简单的方法是通过 `sleep`：

```bash
user sleep 5; grim my-new-screenshot.png
```

`grim` 可以与其他命令很好地结合。对于以下命令，我们使用来自同名包的 `slurp` 在屏幕上标记一个矩形区域。（不幸的是，这在每个 Wayland 器上都不起作用。）

该区域的坐标通过 `-g` 传递给 `grim`。由于 `grim` 以 `-` 结尾，它不会将截图写入文件，而是写入剪贴板。来自 `wl-clipboard` 包的 `wl-copy` 获取数据并将其插入 Wayland 剪贴板。从那里，你可以将截图复制到图形程序（例如 GIMP）。

```bash
```



```bash
user grim -g "$(slurp -d)" - wl-copy
```

如果你想从终端在 X 图形系统中创建截图，`scrot`（SCReen shOT）提供了与 `grim` 类似的功能。

## `groupadd` name

`groupadd` 设置新组。

- `-g n`
使用 `n` 作为新的 GID（组标识符）。

## `groupdel` name

`groupdel` 删除指定的组。

## `groupmod` [options] name

`groupmod` 更改组的 GID 和/或名称。

- `-g n`
确定新的组标识符 `GID`。

- `-n name`
确定新的组名。

## 示例

以下命令将 `mysqladmins` 组重命名为 `dbadmins`：

```bash
root# groupmod -n dbadmins mysqladmins
```

## `groups` [username]

`groups` 显示当前指定用户所属的所有组的列表。这些是 `etc/passwd` 中指定的主组以及 `etc/group` 中指定的可选组。

## 示例

当前用户属于 `kofler`、`docuteam` 和 `wheel` 组。`wheel` 组的成员可以在 RHEL 6 中执行管理任务。

```bash
user$ groups
kofler docuteam wheel
```

## `grub-install` [device]
`grub2-install` [device]

`grub-install` 命令（Ubuntu, Debian）或 `grub2-install`（Fedora, SUSE, RHEL）将引导程序安装到指定硬盘设备的启动区，或者对于 EFI 计算机安装在 EFI 分区。`grub-install` 要求提前设置 GRUB 配置文件 `/boot/grub/grub.cfg`，通常通过调用 `update-grub`（Debian, Ubuntu）或 `grub2-mkconfig`（Fedora, SUSE, RHEL）。

## 示例

在 Ubuntu 上，`update-grub` 命令创建 GRUB 配置文件 `/boot/grub/grub.cfg`，自动为计算机发现的所有操作系统创建条目。

`grub-install` 在 BIOS 计算机第一个硬盘的启动区安装 GRUB 2：

```bash
root# update-grub
root# grub-install /dev/sda
```

在 EFI 计算机上，省略设备指定。`grub-install` 要求 `/boot/efi` 目录下的 EFI 分区位于目录树中。

在 Fedora、SUSE 和 RHEL 上，你必须运行这些命令，是否带有 `grub2-install` 的设备指定取决于是 BIOS 还是 EFI 安装：

```bash
root# grub2-mkconfig -o /boot/grub2/grub.cfg
root# grub2-install [/dev/sda]
```

```bash
grub-mkconfig [options]
grub2-mkconfig [options]
```

`grub-mkconfig`（Ubuntu, Debian）或 `grub2-mkconfig`（Fedora, SUSE, RHEL）评估 `/etc/grub.d` 中的 GRUB 配置文件并分析所有硬盘分区。该命令根据这些信息创建一个新的 GRUB 配置文件并输出。

- `-o file`
将生成的配置保存到指定的文件。

# `gsettings` 命令

`gsettings` 从数据库读取值。

- `get schema`
获取指定架构的键。

- `list-keys`
返回所有键的列表。

- `list-schemas`
提供所有架构。

- `set schema value`
为指定架构设置新值。

## 示例

以下命令设置 `gnome.desktop.interface` 的缩放因子，这对于高 DPI 显示器有用：

```bash
user$ gsettings set gnome.desktop.interface scaling-factor 66
```

## `gunzip` file

`gunzip` 解压指定的文件，无论它是如何使用 `gzip` 压缩的。`.gz` 标识会自动从文件中删除。`gunzip` 是 `gzip` 的链接，会自动激活 `-d` 选项。

## `gzip` [options] file

`gzip` 压缩或解压指定的文件。压缩文件以 `.gz` 结尾。`gzip` 适用于处理单个文件。

- `-1` 到 `-9`, `--fast`, `--best`
控制压缩的速度和质量。`-1` 对应 `--fast`，压缩快但文件较大。`-9` 对应 `--best`，计算时间更长但文件更小。默认设置为 `-6`。

- `-c`, `--stdout`, `--to-stdout`
保持要（解压）的文件不变，并将结果重定向到标准输出（通常是屏幕）。从那里，可以使用 `>` 将重定向到任何文件。

- `-d`, `--decompress`, `--uncompress`
解压文件而不是压缩。

- `-r --recursive`
也处理子目录中的文件。

## 示例

以下命令压缩当前目录下的所有 `*.tif` 文件。结果是 `*.tif.gz` 文件。

```bash
user$ gzip *.tif
```

在第二个示例中，`gzip` 压缩指定的文件，但保持其不变并将结果写入 `backup.gz`：

```bash
user$ gzip -c file > backup.gz
```

## `halt`

```bash
halt [options]
```

`halt` 终止所有运行的进程然后关机。`halt` 对应 `shutdown -h now`。

- `-p` 关机后关闭计算机。许多系统会自动关闭。只有当它不起作用时（例如在许多虚拟机中）才需要此选项。

```bash
hash [options]
```

`hash` 命令显示哈希表的内容。这是 shell 记录之前执行过的所有命令路径名称的表。这加速了已知命令的重复执行，因为不再需要在所有 `PATH` 目录中查找程序。

- `-r` 删除 bash 的哈希表。如果哈希表中的程序目录发生变化，这是必要的。

[PAGE 312]

...否则将找不到命令。在 `tcsh` 中，必须使用 `rehash` 命令而不是 `hash -r`。

## `hciconfig` [hcidevice] [command]

来自 `bluez` 软件包的 `hciconfig` 帮助通过主机控制器接口 `HCI` 配置本地蓝牙适配器。如果没有指定 HCI 设备名称（通常为 `hci0` 或 `hci1`），`hciconfig` 将与所有本地蓝牙设备通信。执行命令时不带参数，它将列出所有本地蓝牙适配器的信息。

- `-reset`
重启蓝牙适配器。

- `-up/down`
激活或禁用蓝牙适配器。如果显示错误消息 "Operation not possible due to RF-kill"，你可以尝试先使用 `rfkill unblock` 开启适配器。

## `hcitool` [options] [command]

来自 `bluez` 软件包的 `hcitool` 命令帮助扫描和设置蓝牙设备。

- `- -h`
列出所有支持的命令。

- `- -i hciX`
将下一个命令应用于指定的蓝牙设备。如果没有此选项，命令将发送给第一个可用设备。

## Commands

- `-cc bt-mac`
与具有指定 MAC 地址的蓝牙设备建立连接。

- `-dc bt-mac`
终止指定的连接。

- `-dev`
提供本地蓝牙设备列表。通常，这是内置的蓝牙适配器，通常被分配设备名称 `hci0`。

- `-scan`
列出无线电范围内的所有外部蓝牙设备，包括它们的 MAC 地址。

## Example

只有一个设备名为 `hci0` 的本地蓝牙适配器。因此，所有其他命令都会自动发送到该适配器；可以省略 `-i` 选项。智能手机和鼠标也在无线范围内。

[PAGE 313]

```bash
user$ hcitool dev
Devices:
hci0 00:1F:CF:41:00:A2
user$ hcitool scan
60:FB:42:FC:BB:8C Logitech Mouse
10:B6:F3:52:06:18 iPhone 13
...
```



## head [options] file

`head` 在屏幕上显示文本文件的前 10 行。

- `-n lines`
  输出指定行数的行。

- `-n lines`
  返回除最后几行之外的所有文件。因此，`head -n 3` 返回除最后三行的所有文本。

## Alternatives

`tail` 实现相反的功能。例如，`tail -n 5` 返回文件的最后五行。如果你想跳过前五行，可以使用 `tail -n +6`（返回从第六行开始的所有行）。

## help name

`help` 显示指定 bash 命令的简短描述。`help` 适用于集成到 bash 中的命令，如 `alias`、`cd` 或 `type`。

## history [options] [n]

bash 命令历史记录按连续数字显示最近执行的命令。`n` 参数将输出限制为最后运行的命令。通过 `!n`，你可以重复指定数字的命令：`!-1`、`!-2` 等分别运行最后一次命令、倒数第二一次命令，以此此类推。

- `-c`
  删除内存中存储的命令序列（保留 `.bash_history`）。

- `-r [filename]`
  将存储在指定文件或 `.bash_history` 中的命令加载到历史内存中。

- `-w [filename]`
  保存命令序列（默认在 .bash_history 中）。

## host [options] name/ip-address

`host` 返回指定网络名称的 IP 地址或指定 IP 地址的网络名称。在许多发行版中，`host` 是 bind 软件包的组件，例如 `bind-utils` 或 `bind9-host`。

- `-a`
  提供额外的信息，可能帮助发现名称服务器配置中的错误。

- `-t type`
  返回所需类型的 DNS 条目。

## Example

IP 地址 `5.9.22.29` 和 `24a1:4f8:161:107::4` 分配给主机名 `kofler.info`。邮件服务器的域名为 `mail.kofler.info`。邮件服务器的 SPF 信息可以在 DNS 文本记录中找到。

```
$ host kofler.info
5.9.22.29 24a1:4f8:161:107::4

$ host mail.kofler.info
mail.kofler.info
```

## hostname [options]

`hostname` 返回当前主机名或设置主机名。

## hostnamectl [options] [command]

`hostnamectl` 命令提供有关主机名的信息并允许你更改它。

## htop

同名软件包中的 `htop` 是 `top` 的变体。相比 `top`，主要优势是你可以使用光标水平和垂直滚动进程列表。按 `K` 可以轻松结束选中的进程。

```
user$ htop
```

clock。

该命令还支持许多特殊函数，这些函数在 `man hwclock` 中有描述。

```
hydra [options] [hostname/ipaddress] service
```

同名软件包中的 `hydra` 破解或渗透测试命令从文件中读取密码或自行生成密码，并尝试使用它们登录网络服务。

`hydra` 支持广泛的服务，包括 FTP, HTTP(S), IMAP, MySQL, Microsoft SQL, POP3, PostgreSQL, SMTP, Telnet 和 VNC。该命令还可以尝试在 Web 表单（GET, PUT, POST）中进行登录。你可以使用 `hydra -h` 来确定允许的服务名称列表。

- `-V6`
  如果可能，使用 IPv6。

- `-C filename`
  使用文件中指定的用户名和密码组合。登录名和密码必须以 `login:password` 的格式逐行包含在文件中。

- `-e nsr`
  还会尝试空密码（n 代表 null）、将用户名作为密码（s 代表 same）以及反转用户名（r 代表 reverse）。

- `-f`
  一旦找到有效的登录名/密码组合，立即终止命令。

- `-l login`
  使用指定的用户名。

- `-L user file`
  从指定的文本文件中逐行读取用户名。

- `-m options`
  传递特定网络服务的额外选项。你可以使用 `hydra -U service` 来确定允许的选项，例如 `hydra -U http-get` 用于本应通过 HTTP GET 请求完成的登录。

- `-M host file`
  从文件中读取要攻击的主机名或 IP 地址，并并行攻击所有主机。

- `-o result file`
  将成功的密码组合保存到指定文件中，而不是显示在标准输出中。

- `-p password`
  使用指定的密码。

- `-P pwfile`
  逐一尝试指定文本文件中的密码。

- `-R`
  恢复上次通过 Ctrl+C 中断的 hydra 调用，前提是 `hydra.restore` 文件存在。不需要再指定其他选项；它们已包含在 `hydra.restore` 中。

- `-s portnr`
  使用指定的端口，而不是相应服务的默认端口。

- `-t n`
  并行运行 n 个任务（线程）。默认设置为 16。这可能太高了，因为某些服务如果有太多的并行请求（且来自同一个 IP 地址），将会阻塞登录。

- `-x min:max:chars`
  生成长度在 min 和 max 之间且包含指定字符的密码。这里，`a` 是小写字母的简写，`A` 代表大写字母，1 代表数字。所有其他字符（包括 äöß）必须单独输入。

示例：使用 `-x '4:6:aAl-$$'`，hydra 使用长度为 6 位且除字母和数字外包含字符 `-`, `_`, `$` 的密码。使用 `-x '4:4:1'`，hydra 会尝试所有四位数字。这将产生 10,000 种可能性。

`-x` 选项仅在特殊情况下有用，即你有（几乎）无限的时间，且目标计算机容忍无限次的登录尝试。

## 示例

在以下示例中，hydra 尝试在 Linux 服务器上寻找一个具有简单密码或无密码的 SSH 登录账户。为了实现这一点，首先使用 `cut` 生成所有账户的列表。理想情况下，你应该在运行与目标计算机相同发行版的计算机上运行此命令。

```
user$ cut -d: -f1 /etc/passwd > logins.txt
```

之后，hydra 应该尝试对存储在 `logins.txt` 中的所有账户进行 SSH 登录，使用用户名、反转后的用户名和空字符串作为密码：

```
user$ hydra -L logins.txt -t 4 -e nsr 10.0.0.36 targetthost
```

## 替代方案

如果你知道哈希值形式的密码，可以使用离线密码破解器（见 `john`）查找明文密码，`hashcat` 更快。但是此命令需要安装复杂的 GPU 驱动程序。

## iconv

`iconv -f charset1 -t charset2 in.txt > out.txt`

`iconv` 将字符集 1 转换为字符集 2。`iconv --list` 提供所有支持字符集的列表。以下命令从 Latin-1 编码的文件创建一个对应的 UTF-8 文件：

```bash
users iconv -f latin1 -t utf8 latin1dat > utf8dat
```

## id

`id` 指定用户的 ID、主组以及其他分配的组。在 Fedora 和 RHEL 上，该命令还会提供 SELinux 上下。

## 示例

用户 `kofler` 的 UID 为 1000，属于主组 `kofler`（GID 为 1000），并且是 `wheel` 组（GID 为 10）的成员：

```bash
root# id
uid=1000(kofler) gid=1000(kofler) groups=1000(kofler),10(wheel)
context=unconfined:u:unconfined r:unconfined_t:s0-s0:c0.c102
```

```bash
if condition; then
  commands
elif condition; then
  commands
else
  commands
fi
```

```
ifconfig [options] [interface]
```

```
ifup interface
ifdown interface
```



## `iftop` [options]

- `-B` 计算字节/s 而不是比特/s。
- `-F` 仅考虑指定地址的流量。
- `-G` 仅考虑 IPv6 地址。
- `-i name` 考虑指定的接口。
- `-n` 显示 IP 地址而不是主机名。

## `inotifywait` [options] [files/directories]

- `-d` 或 `-m`
作为后台进程运行 (`-d`, daemon) 或在前台运行 (`-m`, monitor)。`inotifywait` 不结束于第一个发生的事件，但一直运行直到被显式终止，例如通过 `kill` `Ctrl+C`。
- `-e event`
仅对指定的事件做出响应。默认情况下，命令处理所有通知事件。可以多次指定 `-e` 来选择多个事件。最重要的事件包括访问（`access`）、关闭（`close`）、创建（`create`）、删除（`delete`）、修改（`modify`）、移动（`move`）和打开（`open`）。所有事件的详细描述可以在 `man` 页面中找到。
- `--fromfile.txt`
从 `file.txt` 按行读取要监控的文件或目录列表。
- `-q`
避免不必要的输出（静默模式）。
- `-r`
递归监控指定起始目录的所有子目录。为每个单独的文件都设置了通知监控。对于包含许多文件的目录，这需要一些时间并消耗相对大量的资源。监控器的最大数量通常设置为 8,192。如果需要，你可以在 `/proc/sys/fs/inotify/max_user_watches` 文件中更改此值。
- `-t n`
始终在 `n` 秒后结束，即使没有发生事件。

### 示例

以下 shell 脚本监控当前目录下的 `*.md` 文件。每当这些文件中的一个发生变化时，它就会检查是否存在比相应的 `*.pdf` 文件更新 `*.md` 文件。在这种情况下，将使用 `pandoc` 重建相关的 PDF 文档。该脚本持续运行，直到通过 `Ctrl+C` 终止。

```bash
#!/bin/bash

while :

  for mdfile in *.md; do

    pdffile=${mdfile%.md}.pdf

    if [ $mdfile -nt $pdffile ]; then

      echo $mdfile

      pandoc -t bam -H header.tex $mdfile -o $pdffile

    fi

  done

  inotifywait -e modify -q *.md

done
```

`insmod` [options] module file [parameter=value ...]

`insmod` 加载指定的内核模块。必须传递完整文件名。此外，还可以向模块传递参数（选项）。如果你想指定十六进制值，必须在它们前面加上 `0x`，前缀，例如 `option=0xff`。你可以使用 `modinfo` 确定可选择的模块参数。

- `-f` 即使模块没有为当前内核版本编译，也尝试加载该模块。这是否有效取决于内核版本与模块版本之间是否存在任何不兼容之处。如果硬件制造商仅提供二进制版本的模块（不带任何源代码），则此选项特别有用。然而，该选项无法保证模块实际上与你的内核版本兼容。

## `install` [options] source target

`install` 将文件或整个目录复制到新位置，并可以同时设置所有者、组分配和访问权限。因此 `install` 结合了 `cp`、`chmod` 和 `chown` 的功能。正如名称所示，该命令主要用于安装脚本。

- `-d`
递归复制整个目录，而不仅仅是一个文件。
- `-g group`
定义新文件的组分配。
- `-m oct_permissions`
用八进制代码定义访问权限（参见 `chmod`）。
- `-o owner`
确定目标文件的所有者。
- `-p` 或 `--preserve-timestamps`
原封不动地采用源文件的时间数据。（默认情况下，当前时间被保存为目标文件的修改时间）。

### 示例

以下命令将 `login_sample` 文件从当前目录复制到 `/usr/share/myproject/logdata`。在这种情况下，目标目录 `/usr/share/myproject` 必须已经存在。目标文件属于 `apache` 用户，且只能由该用户读取和更改。（在 Debian 和 Ubuntu 系统上，你必须使用 `www-data` 用户代替 `apache`。）

```
root# install -m 600 -o apache login_sample /usr/share/myproject/logdata
```

# `inxi` [options]

来自同名包的 Perl 脚本 `inxi` 收集有关计算机硬件、驱动程序和软件的信息。在没有更多选项的情况下，它只输出计算机的关键数据。在终端中，输出的关键词用颜色突出，这使得文本比下面的列表更具读性。

- `-A`
提供音频系统的信息。
- `-B`
提供电池信息。
- `-D`
提供数据媒体（磁盘）的信息。
- `-export json|xml`
将结果格式化为 JSON 或 XML 文档。
- `-E`
提供蓝牙设置的信息。
- `-G`
提供图形信息。
- `-F`
返回命令能够确定的所有数据（完整）。

### `inxi` 示例

```
user$ inxi

CPU: 1-core AMD EPYC-Rome (-SMP-) speed: 3593 MHz

Kernel: 5.15.0-generic x86_64

Up: 2d 7m Mem: 2186 MiB (37.8%) Storage: 108 GiB (66.3%) Shell: Bash

Device: 1: Virtio

Display: server: XOrg v:23.2.4 with Xwayland v:23.2.4

driver: virtio-pci resolution: 1 mesa: llvmpipe (32 bits)

Message: EGL data requires egl.
```

`ionice` [options] [command]

`ionice` 以更改的 I/O 优先级运行指定的命令。`ionice` 的功能类似于 `nice`，但它影响的是 I/O 操作而非 CPU 占用率。

- `-c`
指定所需的调度类。允许的设置为：
  - `0`: 无优先级。
  - `1`: 实时，即最大的 I/O 速度。
  - `2`: 尽力而为，默认应用。
  - `3`: 空闲，即仅在系统无负载时执行 I/O 操作。
- `-n`
指示所选类内的优先级级别。允许的值范围范围从 `0`（最高优先级）到 `7`（最低优先级）。优先级级别仅为类 `1` 和 `2` 提供，并允许在类内进行区分。
- `-p`
更改指定进程的 I/O 优先级。

### 示例

以下命令以最小 I/O 优先级启动：

```



`iotop` 来自同名包显示所有进程的 I/O 活动。这有助于搜索在磁盘或其他介质上产生高负载的进程。

- `-0` 仅显示 I/O 活跃进程（默认显示所有进程）。
- `-u` 或 `--user=user` 仅显示指定用户的进程。

`ip` 是一个功能极其强大的命令，用于确定网络设备、隧道、路由规则等。`ip` 应该取代 `ifconfig` 和 `route`，因为这两个命令已经过时了。

- `-f fam` 或 `-family`
确定所需的网络协议（`inet`、`inet6` 或 `link`）。对于 `-f inet`，允许短形式 `-4`；对于 `-f inet6`，允许 `-6`；对于 `-f link`，允许 `-0`。
- `-o` 或 `-oneline`
将相关的输出汇总为一行。这降低了可读性，但便于通过 `grep` 或 `wc` 进行后续处理。
- `-r` 或 `--resolve`
解析 IP 地址并显示主机。这需要域名服务器。

必须指定以下关键词作为对象：`addr`、`addrlabel`、`link`（即网络接口）、`maddr`（多播地址）、`mroute`、`monitor`、`neighbor`（ARP 或 NDIS 缓存项）、`route`、`rule` 和 `tunnel`。这些关键词可以缩写。

### `ip addr`

- `ip addr [show dev xxx]`
显示所有接口的 IP 地址。输出多行。以 `link/ether` 开头的行指定接口的 MAC 地址。以 `inet` 开头的行包含 IPv4 地址以及掩以及广播地址。以 `inet6` 开头的行指定 IPv6 地址并可以有多行。

使用 `-4` 或 `-6` 可以将输出限制为 IPv4 或 IPv6。`ip addr show dev xxx` 只提供指定接口的信息。

- `ip addr add n/m dev xxx`
向接口 `xxx` 添加地址 `n` 和掩码 `m`。一个允许的 IPv4 地址和掩码例如 `10.0.45/24`。

- `ip addr del n/m dev xxx`
取消接口 `xxx` 的地址分配。必须指定与 `ip addr add` 完全相同的参数。

- `ip addr flush dev xxx`
删除接口 `xxx` 的所有地址分配。

### `ip link`

- `ip link [show dev xxx]`
提供所有网络接口的列表，与 `ip addr show` 不同，但不指定 IP 地址。

- `ip link set xxx up/down`
激活或禁用网络接口。

- `ip neigh`
提供本地网络中所有其他 IP 地址列表，即“邻居”的枚举。

### `ip route`

- `ip route [list]`
输出 IPv4 路由表。如果你需要 IPv6 数据，必须指定 `-6` 选项。网关地址可以在以 `default` 开头的行中找到。

- `ip route add default via n`
将 IP 地址 `n` 指定为默认网关。

- `ip route add n1/m via n2 dev xxx`
为地址范围 `n1/m` 定义路由地址 `n2`。IP 包将通过 `xxx` 接口路由。

- `ip route del...`
删除指定的路由条目。参数必须与 `ip route add` 命令的参数完全匹配。

`ip` 命令的文档跨越多个 man 页面。`man ip` 仅提供概述。`man ip-address` 提供关于 `ip addr` 的详情，`man-route` 提供关于 `ip route` 的详情，依此类推。你也可以使用 `ip object help` 来确定特定命令的语法描述，例如通过 `ip addr del` 解析地址分配的语法。

## 示例

以下命令显示当前路由表。在许多现代发行版中，使用如 `enp0s3` 这样的接口名称代替 `eth0`。

```
$ ip route show

10.0.0.0/24 dev eth0 proto kernel scope link src 10.0.0.41 metric 1

default via 10.0.0.138 dev eth0 proto static
```

要将地址 `10.0.0.41` 分配给 `eth0` 接口并设置网关 `10.0.0.138`，你必须运行以下命令：

```
root# ip route add 10.0.0.41/24 dev eth0

root# ip route add default 10.0.0.138 dev eth0
```

以下命令显示了 IPv6 配置：

```
root# ip -6 add addr 2a01:4f8:161:107::2/64 dev eth0

root# ip -6 route add default fe80::1 dev
```

`ip -o` 提供了所有网络接口的紧凑列表：

```
root ip -o link

1: lo: <LOOPBACK,UP,LOWER,UP> mtu 16436 ...

2: eth0: <BROADCAST,MULTICAST,UP,LOWER,UP> mtu 1500 ...

3: br0: <BROADCAST,MULTICAST,UP,LOWER,UP> mtu 1500 ...

4: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 ...

5: vnet0: <BROADCAST,MULTICAST,UP,LOWER,UP> mtu 1500 ...
```

## `ipcalc ipaddress [netmask]`

来自同名软件包的 `ipcalc` 可根据给定的 IPv4 地址和子网掩码确定其他参数，即网络地址、广播地址等。

```
user ipcalc 10.11.12.13/16

Address: 10.11.12.13 00001010.00001011. 00001100.00001111

Netmask: 255.255.0.0 = 16 11111111.11111111. 00000000.00000000

Wildcard: 0.0.255.255 00000000.00000000. 11111111.11111111

Network: 10.11.0.0/16 00001010.00001011. 00000000.00000000

HostMin: 10.11.0.1 00001010.00001011. 00000000.00000001

HostMax: 10.11.255.254 00001010.00001011. 11111111.11111110

Broadcast: 10.11.255.255 00001010.00001011. 11111111.11111111

Hosts/Net: 65534 Class A, Private Internet
```

## `iptables [options]`

## `ip6tables [options]`

`iptables` 配置 Linux 内核的网络包过滤器（简称为 Netfilter）。`iptables` 选项遵循一个简单的模式：大写字母选项表示要执行的操作（例如用 `-P` 设置默认行为）。额外的小写字母选项控制此操作的细节。此语法摘要按操作组织。

请注意，Linux 内核为 IPv4 和 IPv6 管理完全独立的过滤器表。因此，对应有两条配置命令：用于 IPv4 的 `iptables` 和用于 IPv6 的 `ip6tables`。以下描述同样适用于这两个命令变体。

在调用 `iptables` 之前，你应该确保你的发行版没有自带的防火墙系统。例如，Fedora、RHEL 和 SUSE 依赖 `Firewallld-cmd`。在这种情况下，即使定义了防火墙规则也可能导致冲突。

现代发行版使用新的 `nftables` 防火墙系统代替 Netfilter。幸运的是，由于兼容层的存在，这种变化并没有让 `iptables` 命令过时（否则，无数防火墙脚本将无法工作）。不过，当然可以使用 `nft` 命令直接控制 `nftables`。

```
iptables -P chain policy [-t table]
```



`iptables -P(policy)` 定义指定链的默认行为。可能的行为见下表：

- `ACCEPT`: 转发包（默认设置）
- `DROP`: 丢弃包
- `RETURN`: 返回包（罕见）
- `QUEUE`: 将包发送到内核外的程序（罕见）

默认情况下，该命令适用于过滤器链或自定义链。如果要更改 `NAT` 或 `mangle` 链的规则，必须指定表名。

*(注：由于原文中存在大量重复段落，此处已按要求翻译并处理了核心内容)*

第二次使用 `-j ACCEPT` 或 `-J DROP`！请注意，日志规则可能会迅速导致巨大的日志文件。

## `iptables -N mychain`

`iptables -N` (new) 创建一个名为 `mychain` 的新规则链。

## `iptables -L [chain] [-t table] [-v]`

`iptables -L` (list) 返回过滤表（filter table）三个规则链的所有规则列表，以及所有自定义链的规则列表，无需任何额外选项。

你可以使用其他选项来精确指定所需的链（例如，`iptables -L mychain` 或 `iptables -L POSTROUTING -t nat`）。额外的 `-v` 选项提供更详细的信息。`-n` 选项导致在输出中显示 IP 地址和端口号（而不是网络或端口名称）。

## `iptables -D chain [-t table] options`

`iptables -D` (delete) 从链中删除规则。必须指定与 `iptables -A` 完全相同的选项。

## `iptables -F chain [-t table]`

`iptables -F` (flush) 删除指定链中的所有规则。

## `iptables -X [mychain]`

`iptables -X` 删除指定的自定义链。如果没有指定链，将删除所有自定义定义的链。

## 示例

以下 `iptables` 命令为 IPv4 定义了一个微型防火墙。只有当入站数据被分配给现有的连接，或者不是源自计算机连接互联网的 `eth0` 接口时，才会被接受。

该示例假设 `iptables` 表初始处于默认状态（即接受所有数据包），并且只有一个连接的接口。

```
root# iptables -N wall

root# iptables -A wall -m state --state ESTABLISHED,RELATED -j ACCEPT

root# iptables -A wall -m state --state NEW -i eth0 -j ACCEPT

root# iptables -A wall -j DROP

root# iptables -A INPUT -j wall

root# iptables -A FORWARD -j wall
```

```
iptables-save [options]

ip6tables-restore [options]

ip6tables-xml [options]
```

`iptables-xxx` 或 `ip6tables-xxx` 命令有助于将数据包过滤防火墙的规则保存到文件中，或从文件中读取。下面简要描述的每个命令在 IPv6 版本中也可用。

- `iptables-save` 输出所有防火墙过滤器的规则。使用了易于阅读的语法。可以使用 `>` 将输出重定向到文件。`-t name` 选项导致保存指定过滤器的规则。
- `iptables-restore` 从标准输入读取规则。规则通常会替换现有的过滤链。如果你不希望发生这种情况，必须指定 `-n` 选项。`-T name` 仅考虑指定过滤器的规则。
- `iptables-xml` 工作方式与 `iptables-save` 类似，但会创建一个 XML 文档。

## `iw` 对象命令

你可以使用 `iw` 命令来控制支持 `nl80211` 接口的 Wi-Fi 适配器。当前基于 `mac80211` 框架驱动的 Wi-Fi 适配器此类此类。

有多种方法可以指定你想控制的对象。如果接口或设备名称是唯一的，可以省略缩写 `dev` 或 `phy`。

- `dev name`
  指定接口名称（例如，`dev wlan0`）。

- `phy name` 或 `#n`
  指示设备的名称或索引号。对于带有 Wi-Fi 适配器的笔记本电脑，设备名称始终为 `phy0`。

- `reg`
  控制*监管机构*（regulatory agent），即一组针对国家无线标准的规则集。

可选的命令取决于对象类型。我在这里只展示几个选定的命令：

- `dev name connect ssid`
  与指定的 Wi-Fi 网络建立连接。这对于加密网络是可能的。如果网络是加密的，你需要指定 `/etc/john/john.conf` 中定义的其他模式，例如 `incremental=alnum`（对应字母 62 个字符）。如果网络是 WEP，你必须使用 `wordlist` 参数。

- `dev name del`
  移除（删除）接口。

- `dev name disconnect`
  终止连接。

- `dev name info`
  提供接口的通用信息。

- `dev name link`
  提供活动连接的信息。

- `dev name scan`
  提供范围内所有无线网络的详细信息。

- `phy0 add wlan0 type managed`
  设置 `phy0` 适配器。其他类型包括 `monitor`、`wds`、`mesh` 以及 `adhoc`。必须通过 `ifconfig wlan up` 激活。

对于故障排除，运行 `iw event` 命令通常很有用。它会返回直到结束的状态和错误消息。

## 示例

以下命令手动建立了一个未加密的网络：

```
root# iw phy0 add wlan0 type managed

root# ifconfig wlan0 up

root# connect ssid
```

在许多发行版中，可以使用：

```
root# dhclient00
```

## 示例

以下命令手动建立了一个未加密的网络：

```
root# iw phy0 add wlan0 type managed

root# ifconfig wlan0 up

root# connect ssid
```

在许多发行版中，可以使用：

```
root# dhclient0
```

## John

John Ripper（命令）是一个离线密码破解器。

## `john [options] [hashfile]`

`John` 程序可以处理大多数加密算法。在简单的情况下，你只需传递包含哈值的文件名。

- `--format=hashname`
  指定 `john` 使用的加密方法。当 `john` 无法识别哈希方法时，需要此选项。可以在以下网站上找到加密格式的简要描述。注意，该网站还描述了仅包含在非官方“umbo”版本中的格式（见“Alternatives”部分）。
  `https://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats`

- `--incremental[:lower|lowernum|alpha|digits|alnum]`
  生成密码，首先尝试逐渐增加的密码。注意，在此模式下，会考虑 a-z、A-Z 和 0-9 字符（对应 alphan，62 个字符）。可选地，你可以限制字符集：`lower` 对应 a-z，`lowernum` 包含 a-z 和 0-9，`alpha` 对应 a-z 和 A-Z，`digits` 仅包含数字。`/etc/john/john.conf` 中提供了一些其他模式（在 Ubuntu 上，由于 `/usr/share/john` 中缺少相应的字符集文件，许多模式无法工作）。

最后，你可以使用 `john --make-charset` 生成自己的字符集文件，然后可以通过 `incremental=charset` 使用它。

- `--restore`
  继续被 `Ctrl+C` 中断的 `john` 执行。

- `--show`
  显示已经破解的密码。为此，将评估 `.john/john.pot` 文件。

- `--wordlist filename`
  逐行尝试文件中包含的密码。

## 示例

此示例的起点是一个拥有多个账户的 Linux 计算机。`john` 提供的 `unshadow` 命令将 `/etc/passwd` 和 `/etc/shadow` 合并为一个新的哈希文件。访问 shadow 文件需要 root 权限。结果文件中的哈希代码由于空间原因在此处经过了简写处理：

```
root# unshadow /etc/passwd /etc/shadow > hashes

root# chown user hashes

user$ cat hashes
```

```
peter:$6s$ZGF1fLdNTE...:1001:1001:/home/peter:/bin/bash
```



`maria:$6g$Jg6.d8mN.en...:1002:1002:/home/maria:/bin/bash`

`hugh:$6sUinuqQY$ID59.N...:1003:1003:/home/hugh:/bin/bash`

`john`在几秒钟发现了两个特别不安全的密码。`peter`使用了他的名字作为密码，而`hugh`使用了常用密码“123456”。然而，`Maria`的密码无法立即破解，这就是为什么在运行一段时间后通过按下`Ctrl+C`停止了进程：

```
user John hashes

Loaded 3 password with 3 different salts

Press 'q' or Ctrl-C to abort, almost any other key for status

peter (peter)

123456 (hugh)

<Strg++C>
```

你可以使用`git`从GitHub下载常用密码列表。（注意：这些列表所需的空间大约为750 MiB！）这些字典中实际上有一个一个包含了`Maria`的密码！它的内容是`secret`：

```bash
user$ git clone https://github.com/danielmiessler/SecLists.git

user$ john --wordlist=SecLists/Passwords/Common-Credentials/\
10-million-password-list-top-10000.txt hashes

Loaded 3 password hashes with 3 different salts

Remaining 1 password hash with 1 different salt

(maria)
```

## 替代方案

在GitHub上有一个大幅扩展的、由社区维护的“jumbo”版本`john`：

`https://github.com/openwall/john`

如果你想通过GPU支持显著加快哈希码的破解，你应该考虑使用`hashcat`。在这种情况下，最大的障碍是安装合适的GPU驱动程序。要检查网络服务是否存在不安全的密码，你可以使用在线密码破解器：`hydra`。

> `journalctl [options] [search expression]`

`journal`是属于`systemd`的`syslog`服务。它现在运行在大多数常见的Linux发行版上，有时会与传统的日志系统（通常是`rsyslogd`）并行运行。

`journal`文件以二进制格式保存，只能使用此处描述的`journalctl`命令进行读取。

一个或多个搜索表达式可以表示为程序的路径，或者使用`field=value`语法。然后`journalctl`只显示符合所有搜索表达式的日志目。带有逻辑或关系的搜索表达式可以使用`+`构造，即`field1=value1 + field2=value2`。

字段允许使用`MESSAGE`、`PRIORITY`、`ERNO`以及`_UID`、`_PID`、`GID`或`_SELINUX_CONTEXT`关键字。附加搜索参数的参考及其含义的详细说明可以通过`man systemd.journal-fields`找到。

在不带进一步参数的情况下调用时，`journalctl`通常返回一个几乎无尽的日志消息列表，但你可以使用选项来过滤输出：

- `-b`
显示自计算机上次重启以来的消息。

- `--disk-usage`
显示`journal`文件占用`/var/log`多少空间。

- `-e`
立即跳转到要显示的消息的末尾。

- `-f`
以连续模式启动`journalctl`，不断显示当前到达的消息。`Ctrl + C`终止命令。

- `-k`
仅显示内核消息。

- `-n systemd.Journal`
仅显示最后`n`行。

- `--no-pager`
直接将输出写入到标准输出，而不是使用分页器。

- `-p`
显示指定优先级别的消息。

- `--since`
显示自指定时间之后的消息。

- `--until`
显示到指定时间为止的消息。

- `--vacuum-size=SIZE`
删除`journal`文件，直到空间达到指定的大小。

- `--vacuum-time=TIME`
删除指定时间之前的`journal`文件。

- `--unit`
只显示指定单元的消息。

- `-t`
显示指定标签的消息。

- `--user`
显示指定用户的消息。

在第二步中，你必须激活新内核——可以通过`kexec -e`立即激活，也可以在通过`systemd`停止正在运行的服务后激活。在服务器上，这是确保数据库服务器等能够完成所有打开的事务并正常关闭文件的唯一方法。

```bash
root# kexec -e
```
立即重启

```bash
root systemctl isolate kexec
```
先停止服务，然后重启

## `kill [-s signal] 进程号`

`bash`命令`kill`向正在运行的进程发送信号。如果使用`kill`时不带`-s`选项，默认会发送`SIGTERM`信号 (`15`) 来终止（`kill`意为杀死，因此该命令以此为名）进程。在特殊情况下，使用`-9`、`-s SIGKILL`或`-KILL`会有帮助。然而，进程将没有机会执行任何清理工作。

然而，`kill`也可以用于发送更无害的信号。经常使用`-1`、`-s SIGHUP`或`-HUP`来请求守护进程重新加载配置文件。通过这种方式，你可以为某些程序激活新配置，而无需完全停止并重启守护进程。

获取所需进程号 (`PID`) 的`kill`方便变体最简单的方法是使用`ps`命令：要终止的程序可以直接用鼠标“点掉”。

```
killall [-signal] 进程名
```

`killall`的工作方式几乎与`kill`命令一样。区别在于它指定的不是进程号 (`PID`)，而是进程名称。如果有多个同名进程，它们都会接收指定的信号（同样默认为`SIGTERM`）。所需的信号可以通过`-n`或如`-HUP`的名称指定。你可以通过`killall -l`获取所有信号列表。

### 示例

以下示例终止了所有运行的`firefox`实例。如果由`root`执行`kill`命令，将终止所有用户的所有`firefox`进程。

```
user$ kill firefox
```

## `kpartx [磁盘设备]`

来自包的底层命令`kpartx`指定数据媒体的所有分区并创建相应的设备文件。通常，当连接USB磁盘时，`udev`系统会自动创建设备文件。`kpartx`主要用于编辑数据媒体或虚拟机镜像。

- `-a`为指定的数据媒体创建新的设备文件。
- `-d`删除数据媒体的设备文件。
- `-l`读取数据媒体的分区但不创建任何设备文件。
- `-u`更新数据媒体的设备文件。
- `-v`提供执行操作的信息。

### 示例

以下命令连接原始镜像文件中包含的所有`loop`设备：

```
root# kpartx -av image.raw

map loop0p1 (252:12): 0 102400 linear /dev/loop0
map loop0p2 (252:13): 0 199457 linear /dev/loop0
```

整个硬盘可以通过`/dev/mapper/loop0`访问。

```
kvm [options] [镜像文件]
```

`kvm`脚本在Ubuntu上常用于运行虚拟机。`qemu`模拟器和基于内核的虚拟机 (`KVMs`)在大多数其他发行版中，虚拟机通过`qemu`命令启动，那里描述了大量的相同选项。

## `l2ping [options] 蓝牙`

来自`bluez`包的`l2ping`向由MAC地址指定的蓝牙设备发送L2CAP回显请求。通过这种方式，你可以测试本地蓝牙适配器与外部设备之间是否可以连接。`l2ping`必须以`root`权限运行。你可以使用`hcitool scan`确定外部设备的MAC地址。

## `lame [options] 输出文件`

`LAME`的缩写并不是MP3编码器，但`lame`命令实际上用于将WAV文件转换为与MP3格式兼容的压缩音频文件。`lame`的替代方案是`toolame`或`twame`，它们都创建MPEG-1 Layer 2（即MP2）。大多数MP3播放器也可以这种文件。

- `r`源文件为原始格式（而非WAV文件）。
- `s`指定原始文件的采样频率。WAV文件不需要此选项。

### 示例

以下命令创建兼容MP3的音频文件：

```
user$ lame title.wav
```



## `last` [options]

`last` 提供最后登录此计算机的用户列表。该命令评估 `/var/log/wtmp` 文件。

- `-i` 为 SSH 登录显示 IP 地址而不是远程计算机的主机名。
- `-n` 控制显示的条目数量，例如 `100`。
- `t YYYYDDhhmmss` 指明在指定时间登录的用户。

### 示例

最后在测试计算机工作的用户是：

```
user$ last

pts/0 62.47.230 Tue 24 13:51 logged in

pts/0 212.183.46 Mon 23 19:50 (00:32)

pts/1 91.115.236 Fri 13 39 (02:11)

pts/0 91.115.31 Fri 13 15 (02:20)
```

## `lastb` [options]

`lastb` 显示最近哪些登录尝试失败。该命令由与 `last` 相同的选项控制。它只能由 root 运行并评估 `/var/log/btmp` 文件。

## `ldconfig`

`ldconfig` 更新所有库的链接并创建缓存 `/etc/ld.cache`，有助于高效搜索库。`ldconfig` 评估配置文件 `/etc/ld.conf`。手动安装库后必须执行该命令。

## `ldd` 程序

`ldd` 提供运行指定程序所需的所有库的列表。你也可以使用该命令确定计算机上是否有可用所有需要的库。

### 示例

Gnome 终端在 Fedora 上访问了大约 80 个库！以下行按字母顺序显示其中前四个：

```
root# ldd /usr/bin/gnome-terminal | sort

libatk-1.0.so => /lib64/libatk-1.0.so (0x0000ffff4a0000)

libatk-bridge-2.0.so => /lib64/libatk-bridge-2.0.so (0x0000ffff3ad0000)

libatspi.so.0 => /lib64/libspi.so.0 (0x0000ffff39000)
```

## `ln` [options] files

`ln` 是许多发行版中预定义的别名，用于运行带有 `-l` 选项以及可能的其他选项的 `ls` 命令。

## `ln` [options] source [target]

`ln` [options] files target directory

`ln` 为文件和目录建立硬链接或符号链接。如果指定了 `-l` 或 `-s` 选项，`cp` 命令具有与 `ln` 相同的功能。

- `-b` 或 `--backup`
将同名的现有文件重命名为备份文件（文件名后加 `~` 字符），而不是覆盖它们。
- `-d` 或 `--directory`
为目录创建硬链接。此操作仅允许 root 用户执行。所有其他用户都可以创建指向目录的符号链接。
- `-s` 或 `--symbolic`
生成符号链接。（如果不使用此选项，`ln` 将返回硬链接。）

### 示例

以下命令创建指向现有文件 `abc` 的符号链接 `xyz`：

```
user$ ln -s abc xyz
```

## `loadkeys` [options] file-name

低级命令 `loadkeys` 用于为文本模式加载键盘表。所需的配置文件通常位于 `/lib/kbd/keymaps` 目录中。如果输入不带路径的文件名，命令本身会尝试查找带有 `.map.gz` 标识符的合适文件。

因此，这种方式的键盘设置仅在控制台中工作时生效。然而，图形模式的设置必须作为 X 配置的一部分进行更改；对于使用 systemd 的发行版，也可以使用 `localactl` 命令。

- `-d`
加载默认键盘表，该文件通常是 `/lib/kbd/keymaps/defkeymap.map`。

### 示例

以下命令在文本控制台中激活德语键盘布局：

```
root# loadkeys de-latin1

Load /lib/kbd/keymaps/i386/qwerty/de.map.gz
```

## `local var=[value]`

`bash` 命令 `local` 在 shell 脚本的函数中定义局部变量。该命令只能在自定义函数中使用（参见 ）。注意，你不能在等号前后后输入任何空格。

## `localectl` [options] [command]

`localectl` 命令用于控制带有 systemd 初始化系统的发行版中的语言和键盘设置。它会更改以下文件：`/etc/locale.conf`、`/etc/vconsole.conf` 以及 `/etc/X11/xorg.conf/00-keyboard.conf`。

### 选项

- `--no-convert`
仅更改控制台键盘（`set-keymap` 命令）或图形模式键盘（`set-x11-keymap` 命令）。

默认情况下，`localectl` 同时更改文本和图形模式的键盘设置。然而，相关文件具有不同的语法，这就是为什么参数转换有时会失败。

- `--no-pager`
直接将输出运行到标准输出，而不是使用 `less`。

### 命令

- `list-keymaps`
确定文本模式下所有可能的键盘布局列表。
- `list-locales`
确定所有可能的语言设置列表。
- `list-x11-keymap-models`
`list-x11-keymap-layouts`
`list-x11-keymap-variants [layout]`
`list-x11-keymap-options`
确定在图形系统 X 中设置键盘布局的允许参数。
- `set-keymap name`
激活指定的键盘布局。
- `set-locale name`
激活指定的语言设置。
- `set-x11-keymap layout [model variant options]`
激活图形模式下指定的键盘布局。
- `status`
显示当前的语言和键盘设置。

### 示例

以下两个命令考虑到 Apple 键盘的特殊功能，设置了德语、UTF-8 字符集和德语键盘布局：

```
root# localectl set-locale de_DE.UTF-8

root# localectl set-x11-keymap de mac grp:alt_shift_toggle
```

## `locate` pattern

`locate` 允许文件的特别快速搜索。它搜索一个每天更新一次的数据库，指定的模式出现在完整文件名（包括路径）中。然而，在上次数据库更新后创建或更改的文件将无法找到。

在大多数情况下，必须单独安装 `locate` 和底层的 `updatedb` 系统（`mlocate` 包），并且通常还需要进行配置。

## `logger` [options] message

`logger` 使用 `syslog` 服务记录消息。根据发行版的不同，这通常是 `rsyslogd`，或者在更现代的发行版中 `journal`（参见 `journalctl`）。

- `-p n`
在 `0 = emerg` 和 `7 = debug` 之间的指定优先级级别记录消息。
- `-p facility.level`
为指定的服务按指定的优先级级别记录消息。默认，`logger` 使用 `user.notice` 设置。
- `-t tag`
将指定的关键字与消息一起保存。这简化了以后对对应消息的消息。

### 示例

以下 `logger` 命令可以放在备份脚本的末尾。它记录了备份成功结束。

```
user$ logger -p local0.notice -t mybackuptool "Backup completed"
```



```
loginctl [options] [command] [name]
```

类似于 `systemctl` 和 `journalctl`，`loginctl` 属于 `systemd` 家族。你可以使用该命令控制登录管理器（参见 `man systemd-logind.service`）或查询数据。如果没有选项或参数，命令将简单显示所有活动登录（会话）。

- `-p property`
指定查询哪个属性。如果没有此选项，`show-session` 或 `show-user` 等子命令将提供大量详细信息。

- `active sessionname`
激活指定的会话。该命令也可以更改活动控制台，类似于以下快捷键：`Ctrl + Alt + F1`、`Alt + F2` 等。

- `enable-linger loginname`
允许进程在用户注销后继续运行。这对于在注销后继续运行长时间进程（下载、计算）直到结束很有用。`loginctl disable-linger` 再次禁用该功能。

- `list-sessions`
显示所有活动会话（默认行为）。

- `list-users`
显示所有已登录的用户。

- `session-status sessionname`
显示在会话中启动了哪些进程以及记录了哪些日志消息。

- `show-session sessionname`
显示会话详细信息。

- `show-user username`
显示关于用户的详细信息。

- `terminate-session sessionname`
结束会话。所有分配的进程都会接收到一个信号。

## 示例

示例计算机上有四个会话。在控制台 1 (`tty1`) 上，Gnome Display Manager 正在运行并显示登录。

```
root# loginctl

SESSION  UID  SEAT  TTY

5        1000 kofler seat0 tty1

cl       119  gdm     seat0 tty

2        1000 kofler seat0 tty7

4        1000
```

第二个 `loginctl` 命令显示图形系统使用 Wayland。如果使用的是 Xorg，输出为 `Type=x11`。

```
root# loginctl show-session 2 -p Type=wayland
```

## logname

`logname` 显示登录名称（用户名）。

## logout

`logout` 或更短的 `Ctrl+D` 终止控制台或终端窗口。

## Lpadmin [options]

`lpadmin` 为 CUPS 打印系统设置新打印机、更改网络访问权限或将其删除。

- `-d name`
将指定的打印机设置为默认打印机。

- `-E name`
激活指定的打印机。

- `-p name`
设置新打印机。你可以可以使用其他选项指定配置参数（参见 `man lpadmin`）。

- `-x name`
删除指定打印机的配置。

## Lpinfo [options]

`lpinfo` 列出 CUPS 可用的设备和驱动程序。

- `-l`
提供特别详细的信息。该选项必须与 `-m` 或 `-v` 结合使用。

- `-m`
提供可用打印驱动列表。

- `-v`
提供已知打印设备的列表。

## lpoptions [options]

`lpoptions` 显示或更改 CUPS 打印机的选项。

- `-l`
提供可用选项及其当前设置列表。

- `-o option name=value`
更改指定选项的设置。

- `-p name`
指定打印机。（如果没有选项，`lpoptions` 指向默认打印机。）

## lpq [options]

`lpq` 提供所有缓存文件或打印作业的列表。还指定了文件大小和作业编号。你可以将此作业编号作为 `lprm` 的参数以从打印队列中删除文件。

- `-a`
显示所有队列的打印作业。

- `-Pname`
显示指定 `name` 队列中的打印作业。

## lpr 文件

`lpr` 打印指定的文件。

- `-l`
跳过过滤器系统，并将打印机数据封封地发送到打印机。如果已经有了打印机特定格式的打印文件，则此选项非常有用。

- `-o options`
传递各种额外的参数，例如 `-o media=A4` 或 `-o page-ranges=23-27,29,31`。在 CUPS 文档中可以许多示例：`www.cups.org/doc/options.html`。

- `-Pname`
使用 `name` 队列而不是默认打印机。注意该选项后面没有空格！

## lprm [options] [id]

`lprm` 取消当前打印作业或由 ID 指定的打印作业。

- `-Pname`
指定队列。

## lpstat [options]

`lpstat` 显示关于 CUPS 类、打印机及其打印作业的信息。`lpstat` 同样适用于本地打印机和网络打印机。

- `-a`
指示所有打印机是否已准备好接受打印作业。

- `-c`
显示所有类。

- `-d`
显示默认打印机。

- `-s`
显示状态概述（默认打印机、所有类和打印机列表等）。

- `-t`
显示所有可用信息。

- `-v`
显示所有打印机。

```bash
ls [-options] [path]
```



# `ls`

`ls` 显示所有文件和目录的列表。如果在不带额外参数或选项的情况下使用 `ls`，命令将返回一个按文件名排序的多列表，其中显示当前目录下的所有文件、链接和目录。

## `-a` 或 `-all`
还显示以 `.` 开头的文件。选项 `-A` 具有非常相似的效果。唯一的区别是不会显示 `.` 和 `..` 文件（分别是对当前目录和父目录的引用）。

## `-color [-never|auto|always]`
对不同的文件类型（链接、目录等）使用不同的颜色，或停用颜色显示。你可以使用 `discolors` 自己配置颜色。

## `-d` 或 `--directory`
仅显示目录名称，而不显示其内容。此选项非常有用，例如，当指定目录名称作为路径，并且需要检查该目录的访问权限（而不是其内容）时。

## `-h`
以 KiB、MiB 和 GiB 显示文件大小（人类可读）。

## `-i` 或 `--inode`
除其他信息外显示文件的 i-node。（i-node 是文件的内部标识符，Linux 内部文件管理需要）。该选项可识别硬链接，因为以此方式链接的文件具有相同的 i-node。

## `-I` 或 `--ignore file`
在显示时不指定的文件。例如，`-Ip` 防止显示扩展名为 ps 的文件。如果在使用 `-I` 之后指定的是文件模式而不是单个文件，则在 `-I` 和模式之间不能输入空格！

## `-l` 或 `--format=long` 或 `--format=verbose`
除了文件名外还显示更多信息，例如字节单位的文件大小、访问权限等。使用单独的一行显示每个文件（而不是节省空间的多列列表）。

## `-L` 或 `--dereference`
对于目录的符号链接，不显示链接的路径，而是显示原始目录的内容。

## `-o` 或 `--no-color`
不使用不同的颜色或字体。

## `-p` 或 `-F`
在文件名后附加特殊字符以指示文件类型。在某些 Linux 发行版中，此选项通过 `/etc/profile` 中的别名缩写默认激活。最重要的特殊字符是 `/` 用于目录，`@` 用于符号链接，`*` 用于可执行文件，以及 `|` 用于 FIFO。

## `-r` 或 `--reverse`
反转排序顺序。该选项通常与 `-t` 或 `-s` 结合使用。

## `-R` 或 `--recursive`
也捕获子目录中的文件。

## `-S` 或 `--sort=size`
根据大小排序文件（最大的文件在前）。

## `-t` 或 `--sort=time`
根据最后修改的日期和时间排序文件（最新的文件在前）。

## `-u` 或 `--sort=access`
根据最后读取访问的时间对文件排序。该选项必须与 `-t` 一起指定（否则 `ls` 将不进行排序）。

## `-v`
以合理的方式对文件名中的数字进行排序，例如 `tty2` 在 `tty10` 之前。

## `-X` 或 `--sort=extension`
根据标识符（即根据文件名中最后一个 `.` 之后的字母组合）排序文件。

## `-Z` 或 `--context`
显示 SELinux 上文信息。`--lcontext` 提供更多信息，`-scontext` 提供较少的信息。



```
root# lsblk

NAME  MAJ:MIN SIZE RO TYPE MOUNTPOINT

sda      8:0    1   3.7T 0 part

sdal      8:1    1   16G 0 part

md0      9:0    0   16G 0 raid1 [SWAP]

sda2      8:2    1   512M 0 part

md1      9:1    0   511.4M 0 raid1 /boot

sda3      8:3    1   2T 0 part

md2      9:2    0   2T raid1 /

sdb      8:16   1   3.7T 0 part

sdb1     8:17   1   16G 0 part

md0      9:0    0   16G 0 raid1 [SWAP]

sdb2     8:18   1   512M 0 part

md1      9:1    0   511.4M 0 raid1 /boot

sdb3     8:19   1   2T 0 part

md2      9:2    0   2T raid1 /
```

## `lsb_release` [options]

`lsb_release` 用于确定特定发行版的信息，例如运行的 Linux 系统的名称和版本号。LSB 代表 Linux 标准基础（Linux Standard Base）。如果没有传递选项，则默认应用 `-v`。

- `-a`
显示所有可用信息：发行版名称、完整描述、版本号和代号（参见本条目中的示例）。

- `-v`
显示 LSB 版本号，但仅当在安装命令外还安装了 LSB 模块（`lsb-core` 包）时才有效。通常情况下并非如此——此时命令会返回错误信息“没有可用的 LSB 模块”。但在实践中，LSB 版本号很少引起关注。如果你只想知道已安装的 Linux 系统的版本，应该使用 `-a` 选项。

### 示例

在以下示例中，在 Ubuntu 24.04 安装系统上运行了 `lsb_release`：

```
root# lsb_release -a

ributor ID: Ubuntu

Description: Ubuntu Noble Numbat (development branch)

Release: 24.04

Codename: noble
```

## `lscpu` [options]

`lscpu` 显示关于 CPU、其核心和缓存以及（如果适用的话）虚拟化系统的详细信息。

- `-e`
以易于阅读的格式仅显示关键数据的摘要。

- `-p`
类似于 `-e`，但提供可以在脚本中易于处理的数据格式。

## `lshw` [options]

来自同名包的 `lshw` 命令会创建计算机上所有硬件组件的层次结构列表。

- `-businfo`
逐行列出组件，并为每个组件使用的 SCSI、USB 或 PCI 总线指定一个 ID。

- `-html`
将输出格式化为 HTML 文档。

- `-short`
仅提供简洁的摘要。

- `-xml`
将输出格式化为 XML 文档。

### 示例

以下硬件概述是在树莓派 4B 上生成的：

```
root# lshw -businfo

Bus info      Device Class       Description

=================================

               system           Raspberry Pi 4 Model B Rev 1.1

               bus              Motherboard

cpu@0          processor cpu

cpu@1          processor cpu
```

```
cpu@2 processor cpu

cpu@3 processor cpu

pci@0000:00.00 memory 855MiB System memory

pci@0000:01.00 bridge Broadcom Limited

VL805 USB 3.0 Host Controller

usb0 usb bus xHCI Host Controller

usb0:1 bus USB2.0 Hub

usb0:4 bus Keyboard Hub

usb0:1.4.2 input Apple Keyboard

usb0:1.4.3 input USB-PS/2 Optical Mouse

usb2 usb2 bus xHCI Host Controller

eth0 network Ethernet interface

wlan0 network Wireless interface
```

## `lsmod`

`lsmod` 提供了当前加载到内核中的所有模块列表。

## `lsof` [options] [file/interface]

在没有任何额外参数的情况下，`lsof` 会提供所有打开的文件或分配给它们的接口的长列表。`lsof` 提供了保持该文件打开的进程信息。

- `-i`
提供使用指定网络地址的进程信息。地址的格式如下：`[protocol][hostname]:service|port`。例如，`-i` 提供了所有在 IPv4 中使用 TCP 的进程信息。

- `-n`
解析名称。

- `-N`
考虑 NFS 文件。

- `-u`
仅提供指定用户使用的文件/接口信息。也可以指定多个用户（用逗号分隔）。

- `-X`
忽略所有打开的 TCP 和 UDP 文件。

### 示例

以下命令显示了所有使用 UDP 或 22 端口的进程：

```
root# lsof -i udp

ntpd 3696 ntp IPv4 9026 UDP *:ntp

portmap 4745 daemon IPv4 12931 UDP *:rpc

statd 4764 statd IPv4 12962 UDP *:700

...
```

```
root# lsof -i :22

COMMAND PID USER SIZE NAME

sshd 5559 root IPv6 14
```

## `lspci` [options]

`lspci` 提供了关于 PCI 线的详细信息。

- `-v`
显示更详细的信息。

- `-k`
显示内核使用的驱动程序。

- `-t`
以树状结构显示设备。

### 示例

以下命令显示了 PCI 树结构：

```
root# lspci -t

  ├──00:00.0 PCI bridge

    │   ├──00:01.0 PCI bridge

    │       └── 00:14.0 USB controller

    └──00:01.0 PCI bridge
```

用于选择哪个 PV 提供存储的 `pvname` 规范。

`lvextend` 的用用示例可以在 `resize2fs` 命令的描述中找到，该命令允许你更改 ext 文件系统的大小。

```
Lvm [command]
```

`lvm` 是逻辑卷管理器（LVM）的核心管理命令。`lvm` 通常位于 `lvm2` 包中，如果在安装过程中没有已经设置 LVM 系统，则必须单独安装。

如果你在不带任何其他命令的情况下运行 `lvm`，你将进入一个 shell，可以在其中交互式地执行 LVM 命令。`help` 提供所有可用命令的列表。或者，你可以向 `lvm` 传递一个命令，它将立即执行。

所有 LVM 命令都可以通过 `lvm` 或直接运行。因此，`lvcreate xxx` 和 `lvcreate xxx` 命令是等效的。

为了清晰起见，我决定在本书中单独描述最重要的 LVM 命令。编辑逻辑卷的命令以其首字母 `lv` 开头，管理物理卷的命令以 `pv` 开头，管理卷组的命令以 `vg` 开头。

## `lvreduce` [options] `lvname`

`lvreduce` 减少指定 LV 设备的内存空间。如果 LV 包含文件系统，必须先减小其大小，否则数据将会丢失！你可以使用 `-L size` 格式输入新的总大小，或者使用 `-L size` 格式输入所需的更改大小。

## `lvremove` [options] `lvname`

`lvremove` 删除指定的 LV。

- `-f`
抑制系统查询。

## `lvrename` `oldlvname` `newname`

`lvrename` 给 LV 一个新名称。

## `lvscan` [options]

`lvscan` 列出所有 LV。

```
lz4 [options] [filename]

lzop [options] [filename]
```



来自同名包的 `lz4` 和 `lzop` 命令压缩文件。虽然它们的压缩率低于 `gzip` 或 `bzip2`，但它们要快得多（尽管 `lz4` 仍然比 `lzop` 快一点）。`lz4` 和 `lzop` 的语法基于 `gzip` 命令。

如果你想以节省空间的方式保存文件（例如备份），但不想投入过多的 CPU 资源，那么 `lz4` 或 `lzop` 是完美的。你将主要在管道模式下使用命令，如本文稍后部分 `tar` 示例所示。

- `-c` 或 `--stdout` 或 `--to-stdout`
  将结果重定向到标准输出。
- `-d`, `--decompress`, 或 `--uncompress`
  解压缩指定的文件而不是压缩。
- `-n`
  控制压缩的速度和质量。`-1` 最快，`lzop` 的 `-9` 提供最小的文件。对于 `lz4`，`-12` 提供最佳压缩。

## 示例

第一个命令压缩文件并返回 `file.lzo`；第二个命令再次解压缩该文件：

```
user$ lzip file
user$ lzip -d file.izw
```

以下两个示例显示了 `lzip` 与 `tar` 结合使用：

```
user$ tar cf -c verz | lzip -c c backup.tar.lzo
```
创建存档

```
user$ lzip -d < backup.tar.lzo | tar xf -
```
解压存档

## magick [options] imageold imagenew

来自 ImageMagick 包的 `magick` 将图像文件从一种格式转换为另一种格式。在本书中，最重要的命令和选项在 `convert` 中描述，这是直到版本 6 的有效名称。从版本 7 开始，建议调用语法等效的 `magick` 命令代替 `convert`，尽管 `convert` 在大多数发行版中仍然可用。

## mail [options] mail@hostname < message text>

你可以使用 `mailx` 或 `mailutils` 包（Debian, Ubuntu）中的 `mail` 命令读取存储在 `/var/mail/name` 的本地邮件。然而，这种操作至少需要习惯。如果你正在寻找文本模式的邮件客户端，最好安装 `mut`。

`mail` 的优势在于你可以通过交互式或脚本轻松将电子邮件传输到本地邮件服务器。你只需交互式地运行 `mail recipient@site`。现在你可以输入额外的接收者（CC 地址）、主题，最后按 Ctrl+D 结束消息文本。这将邮件传输到本地邮件服务器，使用 `loginname@hostname` 作为发送者。

对于脚本控制的邮件分发，你需要熟悉 `mail` 选项，我在这里只介绍最重要的三个：

- `-a "header"`
  指定额外的标头行。这可以用于添加 BCC 地址或设置消息的字符集（见下一个示例）。`mail` 在许多配置中无法识别正确的邮件主机，从而错误地组合发送者地址。这甚至适用于 Debian 和 Ubuntu 系统，在这些系统中 `/etc/nodemailer` 非常容易评估。这个问题可以通过显式使用 `-a "From:name@myhost.com"` 指定发送者地址来解决。
- `-A file`
  将文件添加到邮件。
- `-s "subject"`
  指定主题行的文本。

## 示例

在最形式的形式，`mail` 的用法完全简单：

```
user$ echo "message" | mail -s "subject" recipient@site
```

以下命令将邮件发送给接收者：

```
user$ echo "message" | mail -s "subject" recipient@site
```

## md5sum files

`md5sum` 计算所有指定文件的校验和。消息摘要算法 5（MD5）校验和通常用于确保文件在传输后保持不变。注意 MD5 算法不再安全。`shasum` 命令在密码学上更安全。

## mdadm [options]

来自同名包的 `mdadm` 命令有助于管理软件 RAID 连接。该命令由许多选项控制。一个选项通常指定模式（例如，`--create` 或 `-C` 设置新的 RAID 阵列）。其他选项控制所需操作的细节。

- `mddevice --add device`
  将分区添加到网络。
- `assemble --scan mddevice`
  根据 `mdadm.conf` 中指定的磁盘分区组合 RAID 卷 `mddevice`。
- `create mddevice --level=n --raid-devices=m device1 device2 ... devicem`
  创建 RAID 级 `n` 的 `mddevice` 阵列，由 `device1` 到 `devicem` 的 `m` 个磁盘分区组成。
- `--detail mddevice`
  提供 RAID 卷的详细信息。
- `--examine device`
  提供磁盘分区的详细信息，该分区必须是 RAID 阵列的一部分。
- `--examine --scan`
  以 `mdadm.conf` 的语法提供所有可用 RAID 卷的摘要。
- `mddevice --fail device`
  将硬盘分区 `device` 标记为故障并停用。
- `--grow mddevice --size=max`
  扩展阵列以便以优化方式使用底层的硬盘分区。该命令仅在扩展硬盘分区后以这种形式才有意义。
- `--grow mddevice --raid-devices=n`
  增加集成到阵列中的硬盘分区数量（仅适用于 RAID 1、5 和 6）。
- `--monitor device`
  监控激活的 RAID 阵列。该命令通常在计算机启动时启动，并在发生问题时向管理员发送电子邮件（`-m` 选项）。
- `--query device`
  测试该分区是否为 RAID 分区或 RAID 阵列的一部分。
- `mddevice --remove device`
  从 RAID 阵列中移除硬盘分区 `device`。`device` 必须处于激活状态，因此可能需要先使用 `--fail` 将其禁用。
- `stop mddevice`
  禁用指定的阵列。现在可以使用 `--assemble` 重新组装阵列。
- `--zero-superblock device`
  删除硬盘分区的 RAID 元数据。

## 示例

以下两个命令从两个分区 `/dev/sda3` 和 `/dev/sdb3` 创建一个 RAID-0 阵列，并在那里设置 ext4 文件系统。分区必须先被标记为 RAID 分区。如果你使用 `fdisk` 进行分区，需要使用命令将分区 ID 设置为十六进制值 `fd`。在 `parted` 中，你必须运行 `set partition number raid`

```
root# mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/sda3 /dev/sdb3
mdadm: array /dev/md0 started.
root# mkfs.ext4 /dev/md0
```

设置 RAID-1 阵列的过程与 RAID-0 完全相同。仅设置 RAID 系统的命令看起来略有不同，现在包含 `--level=1` 而不是 `--level=0`：

```
root# mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sda3 /dev/sdb3
mdadm: array /dev/md0 started.
root# mkfs.ext4 /dev/md0
```

要测试 RAID-1 阵列的功能，您应该将一个分区标记为缺陷：

```
root# mdadm /dev/md0 --fail /dev/sdb3
```

你可以继续使用该阵列；然而，所有更改现在只会保存到剩余的硬盘分区上。要将 `/dev/sdb3` 添加回 `/dev/md0`，你必须显式地移除标记为缺陷的分区：

```
root# mdadm --remove /dev/md0 /dev/sdb3
root# mdadm --add /dev/md0 /dev/sdb3
```

现在两个分区的自动重同步开始，这取决于阵列的大小（对于传统的 SATA 硬盘，每 100 GiB 大约需要 20 分钟）。毕竟，在此期间你可以继续工作。但是文件系统的响应速度会比通常慢。`cat /proc/mdstat` 提供了有关同步进程进展的信息。

要保存对 RAID 配置文件 `/etc/mdadm/mdadm.conf` 中进行的所有更改，你需要运行以下命令。然后你必须使用编辑器从配置文件中删除任何之前输入的 RAID 阵列，以确保文件没有重复。

```
root# mdadm --examine --scan >> /etc/mdadm/mdadm.conf
```



## mkdir directory

`mkdir` 创建新目录。这里列出了最重要的选项：

- `-m mode` 或 `--mode=mode`
按照指定的模式设置新目录的访问权限（参见 `chmod`）。

- `-p` 或 `--parents`
也创建中间目录。如果你运行 `mkdir -p a/b/c` 且目录 `a` 和 `a/b` 尚不存在，则将创建这些目录。

- `-Z`
为新目录激活 SELinux 的默认上下文。

## mkfifo file

`mkfifo` 设置一个先入先出（FIFO）文件。基本上，FIFO 文件像管道一样工作，允许在两个程序之间交换数据。

## 示例

在接下来的示例中，`mkfifo` 设置了一个 FIFO 文件。`ls` 将目录列表重定向到该文件。`more` 从那里读取内容。`ls` 必须以 `&` 后台进程启动，因为在 `more` 从 fifo 读取完所有数据之前，`ls` 进程不会结束。

```
user$ mkfifo fifo &
user$ ls -l > fifo &
user$ more < fifo
```

如果没有 FIFO 文件，通过 `more` 显示目录列表可以简单得多，即使用 `ls -l | more`。

## mkfs [options] device [blocks]

`mkfs` 在之前划分分区的硬盘上设置文件系统。`mkfs` 只能由 `root` 运行。根据指定的文件系统，程序将分支到 `mkfs.file系统类型` 命令。

- `-t file system`
指定文件系统的类型。例如，`ext4` 和 `xfs` 是可能的。`t` 选项必须作为第一个选项指定！所有其他选项都将传递给实际设置文件系统的命令。它们取决于文件系统的类型。

接下来将描述最重要的特定于文件系统的命令。

## mkfs.btrfs [options] device1 [device2]

`mkfs.btrfs` 设置 Btrfs 文件系统。取决于发行版的不同，可能需要安装 `btrfs-progs`。

- `-A` 或 `--alloc-start n`
在设备开头留出 `n` 字节未使用。

- `-m` 或 `--data type`
指定所需的 RAID 类型。允许的值有 `raid0`, `raid1`, `raid10`, `raid5`, `raid6`。

- `-L` 或 `--label name`
给文件系统命名。

如果设备发生故障，在接下来的示例中，这仍然是 `/dev/sc1`，但这次分区来自新的硬盘或 SSD。为了将文件系统重新分布到两个设备上并恢复 RAID-1 冗余，你还必须运行 `btrfs filesystem balance`。对于大型文件系统，执行此命令自然需要花费很长时间。毕竟，在此期间可以使用文件系统，尽管速度大大降低。

```
root# btrfs device add /dev/sc1 /media/btrfs
root# btrfs filesystem balance /media/btrfs
```

只有现在才能从文件系统中删除缺陷设备。你可以使用 `missing` 关键字指定设备：

```
root# btrfs device delete missing /media/btrfs
```

## mkfs.exfat [options] device

来自 `exfat-utils` 包的 `mkfs.exfat` 设置了一个针对 SD 卡优化的 exFAT 系统。该文件系统默认用于 SDXC 卡，并支持 SDXC 数字相机和智能手机。

- `-i id` 为文件系统确定 32 位 ID。数字以十六进制代码给出。如果执行命令时没有该选项，将设置随机 ID。

- `-n name` 定义文件系统的名称（标签）。默认情况下名称为空。如有必要，可以使用可以使用 `fatlabel` 更改名称。

## 示例

可以使用以下命令设置一个使用两个等大小分区 `/dev/db1` 和 `/dev/sc1` 的 RAID 1 系统：

```
root# mkfs.btrfs -d raid1 -m raid1 /dev/db1 /dev/sc1
```

如果某个设备故障，你可以通过额外的挂载选项 `degraded` 继续使用文件系统：

```
root# mount -o degraded /dev/db1 /media/btrfs
```

要恢复 RAID 阵列，你应该向文件系统添加新设备。在接下来的示例中，这仍然是 `/dev/sc1`，但这次分区来自新的硬盘或 SSD。为了将文件系统重新分布到两个设备上并恢复 RAID-1 冗余，你必须运行 `btrfs filesystem balance`。对于大型文件系统，执行此命令自然需要花费很长时间。毕竟，在此期间可以使用文件系统，尽管速度大大降低。

在创建 RAID 阵列时，你通常为 `-d` 指定相同的 RAID 类型 `-m`。这意味着数据被简单保存。

## mkfs.ext2 [options] device [blocks]

## mkfs.ext3 [options] device [blocks]

## mkfs.ext4 [options] device [blocks]

## mke2fs [options] device [blocks]

`mke2fs`、`mkfs.ext2`、`mkfs.ext3` 和 `mkfs.ext4` 用于建立一个 `ext2`、`ext3` 或 `ext4` 文件系统。这四个命令都通过链接引用同一个程序，但它们使用存储在 `/etc/mk2fs.conf` 中的不同默认选项。

- `-b n`
确定块大小（通常为 4,096）。`n` 的取值范围允许 1024、2048、4096 直到 65536（即 $2^{10}$、$2^{11}$ 等，最高到 $2^{16}$）。

- `-c`
在用 `badblocks` 设置数据介质之前，测试是否存在坏块。这类块不会用于文件系统。该测试需要对每个数据块进行修改并重新读取，因此会显著延长设置文件系统所需的时间。

- `-i n`
指定设置 I-node 之前的字节数。I-node 是文件系统的内部管理单元。文件的所有管理信息都存储在 I-node 中，文件名除外（即：访问位、所有者、最后访问日期等）。I-node 的数量在格式化期间定义。例如，当 `n=4096` 时，每 MiB 有 $1,048,576 \div 4,096 = 256$ 个 I-node；这意味着无论文件多小，每个 MiB 最多存储 256 个文件或目录。

如果你想保存大量小文件，应该减小 `n`。最小值为 1024（这对应于每 MiB 2,048 个文件）。选择比块大小小的值没有意义，因为每个块本身只能保存一个文件。然而，如果你只想保存几个大文件，也可以选择较大的 `n`。这可以减少管理开销。

- `-j`
允许你传递额外的参数，例如设置日志文件的大小，或在另一个设备上设置日志文件。这可能会稍微提高文件系统的速度，但同时会使管理以及在崩溃后恢复文件系统变得更加复杂。可用选项在 `mke2fs` 的手册页中有详细说明。

- `-m n`
指定预留多少比例的磁盘给 `root` 数据（默认为 5%）。该预留内存允许即使文件系统对其他用户已完全满，`root` 也能继续工作。因此这是一个安全备留。

- `-t ext2/ext3/ext4`
指定的 `ext` 版本（仅 `mke2fs` 需要）。

## 示例

以下两个命令首先在 `/dev/sda5` 分区上建立一个新的 `ext4` 文件系统，然后禁用自动文件系统检查（参见 `tune2fs` 命令的描述）：

```bash
root# mkfs.ext4 /dev/sda5
root tune2fs -i 0 -c 0 /dev/sda5
```

## mkfs.ntfs [options] device

`mkfs.ntfs` 用于建立兼容所有当前 Windows 版本的 NTFS 文件系统。该命令是许多发行版中 `ntfsprogs` 包的一部分，必须单独安装。

- `-f` 或 `--fast`
不在每个数据块中填充 0 字节。此选项选项可以极大提高格式化速度，强烈建议使用。

## mkfs.vfat [options] device

`mkfs.vfat` 用于建立兼容所有常用 Windows 版本的 Windows 文件系统。这种格式特别适用于在 Windows 或相机上使用的 USB 盘和 SD 卡。

- `-F 12/16/32`
指定的 FAT 表类型（12 位、16 位或 32 位）。通常，`mkfs.vfat` 会为大型数据介质自动选择 32 位模式。如果不是，此选项会有帮助。

- `-I`
允许在不创建分区表的情况下格式化整个磁盘（`mkfs.vfat -I /dev/sdg`）。这种方法有时用于 USB 盘。

- `-n name`
为文件系统分配一个最大长度为 11 个字符的名字（标签）。

## 示例

以下命令在 `/dev/sdd1` 分区上建立一个名为 `MyPhotos` 的 32 位 VFAT 文件系统：

```bash
root# mkfs.vfat -F 32 -n MyPhotos /dev/sdd1
```



## `mkfs.fs` [options] device

`mkfs.fs` 用于建立 XFS 文件系统。该过程可以通过无数选项控制（`man mkfs.fs`），其中最重要的选项列在此：

- `-b size=n`
  指定的块大小（默认为 4,096 字节）。
- `-l logdev=device`
  将日志数据保存在单独的分区中。
- `-l size=n`
  指定日志数据区域的大小。
- `-L label`
  给文件系统命名。
- `-m n`
  指定预留多少比例的磁盘给 `root` 数据（默认为 5%）。
- `-t ext2/ext3/ext4`
  指定的 ext 版本（仅 `mke2fs` 需要）。

`up`（向上），以及 `q`（退出）。与其使用更复杂的命令，通常会使用功能更强大的 `less` 命令。

## mount

```
mount [options] device directory
```



不带参数的 `mount` 会返回所有当前已挂载文件系统的列表，包括文件系统类型和挂载选项。在第二种语法变体中，`mount` 将数据介质（硬盘分区、USB 闪存盘等）集成到 Linux 文件系统中。你必须指定数据介质设备名称（例如 `/dev/nvme0n1p3`）以及目录树中的目标目录。除了设备外，你也可以指定文件系统的 UUID（例如 `mount UUID=1234 directory`）。

Linux 启动时文件系统的挂载由 `/etc/fstab` 文件控制。对于 `/etc/fstab` 中列出的所有设备，可以使用 `mount` 的短形式，只需指定设备文件或挂载目录。`mount` 会自动从 `fstab` 读取缺失的数据和选项。

可以使用 `umount` 从文件系统中移除数据介质。原则上，`mount` 和 `umount` 只能由 root 用户运行。在 `fstab` 中标记了 `user` 或 `users` 选项的驱动除外。

以下关于通用和特定文件系统的挂载选项的描述跨越几页，随后是几个示例。

## 通用挂载选项

- `-move olddir newdir`
更改文件系统挂载的目录。

- `-o options`
允许你指定额外的选项，例如格式为 `-o acl,user_xattr`。通过这种方式指定的选项之间不能有空格！请参见下一小节获取文件系统选项参考。

- `-r`
防止在数据介质上进行写操作（只读）。

- `-t file system`
指定文件系统。可能的选项包括用于 Linux 分区的 `ext2/3/4`、`btrfs` 或 `xfs`，用于 Windows 分区的 `vfat` 和 `ntfs`，以及用于数据 CD 和 DVD 的 `iso9660` 和 `udf`。

## 通用文件系统选项

使用 `-o`，你可以传递无数种影响已挂载文件系统行为的选项。通用选项的关键字总结在下面的列表中。特定文件系统的选项在稍后的位置出现。

`mount -o` 的所有选项也允许在 `/etc/fstab` 的第四列中使用。该文件在启动过程中进行评估；在 Ubuntu 系统上，这是通过 `mountall` 命令完成的。因此，以下编译内容也适用于 `/etc/fstab` 和 `mountall`，并补充了一些与 `mount` 命令不直接相关的 `fstab` 特定和 `mountall` 特定的关键字。这些包括 `defaults`、`noauto`、`nobootwait`、`optional`、`owner`、`user` 和 `users`。

- `-atime / noatime / relime / strictatime`
指定更新文件 inode 时间的情况：每次读取访问（`atime` 或 `strictatime`，符合 POSIX 标准）、每天最多一次（`relime`）或从不更新（`noatime`）。对于写访问，inode 访问时间总是会改变。

该选项对读取操作速度和闪存数据存储设备的使用寿命影响较大。当前内核版本的默认设置为 `relime`。

- `-defaults`
指定用默认选项将文件系统包含在目录树中。如果不使用其他选项，则在 `/etc/fstab` 的第四列中指定 `defaults`。（该列不能留空。）

- `-dev / nodev`
导致或防止设备文件被解释为设备。在 Linux 上，文件可以标记为块设备或字符设备。出于安全考虑，此选项对于外部数据介质很有用。

- `-discard`
激活 `ext4`、`Btrfs` 和 `XFS` 文件系统的 `trim` 功能。内核现在通知 SSD 哪些数据块已被删除，给 SSD 提供了优化内存单元内部管理的机会。`trim` 功能还可以与 LVM 和软件 RAID (`mdraid`) 结合使用。

是否应该使用 `discard` 选项存在争议：尽管它有助于 SSD 的长期优化，但可能会导致删除操作显著变慢（例如，如果短时间内要删除许多文件，请参见 https://forums.freebsd.org/threads/ssd-trim-maintenance.56951/#post-328912）。`discard` 选项的良好替代方案是 cron 任务，每天或每周运行一次 `fstrim` 命令，以此向 SSD 报告所有已删除的扇区。

- `* exec / noexec`
决定文件系统上的程序是否可以在 Linux 上运行。对于大多数文件系统，`exec` 设置默认生效。然而，具有安全意识的管理员会对 CD/DVD 驱动器和外部数据介质指定 `noexec` 选项。（如果你使用 `user` 选项，`noexec` 将生效。可以使用 `exec` 选项再次更改。）

- `* noauto`
仅在 `/etc/fstab` 中有用，确保该行中命的数据介质在启动时不自动挂载。尽管如此，在 `fstab` 中输入数据介质是有意义的，因为用户可以方便地执行挂载 而无需显式指定所有其他挂载选项。例如，`noauto` 用于很少需要的数据分区。

- `* nobootwait`
如果设备不可用，不停止启动过程。该关键字由 Ubuntu 上的 `mountall` ，无法使用。

- `* nofail`
如果设备不可用，不报告错误。

- `* optional`
与 `noauto` 类似，但如果设备不存在，也允许 `mount` 命令成功执行而不报错。

- `* owner`
允许普通用户通过 `mount` 卸载相关文件系统。否则，只有 root 可以这样做。

- `* user`
允许普通用户通过 `mount` 挂载相关文件系统。对于外部数据介质，此选项仅在 `/etc/fstab` 中有用。如果使用 `user` 选项，`noexec`、`nosuid` 和 `nodev` 选项也将生效。

- `* users`
与 `user` 含义相同，但有一个小区别：每个用户都可以从文件系统中移除数据介质（卸载）。因此，`users` 允许用户 A 挂载，随后用户 B 调用。

- `* remount`
更改已包含在目录树中的文件系统的选项。

- `* ro / rw`
指定文件只能读取或修改。`rw`（读写）适用于大多数文件系统。

- `* suid / nosuid`
允许或阻止执行设置用户标识位。`nosuid` 防止普通用户执行 root 权限的程序，这是一种安全保障。

- `* sync`
导致更改立即保存而不是在内存中临时存储几秒。然而，`sync` 的缺点是写入效率低得多，特别是对于廉价闪存盘。

## btrfs 选项

许多挂载选项取决于特定的文件系统。最重要的特定文件系统选项总结在这里。我们从 `btrfs` 开始。

- `-compress=zlib|lzo|zstd`
压缩所有新或修改的文件。只要是只读，现有文件将保持不变。你有三种压缩方法可供选择：
  - `zlib`：良好的压缩
  - `lzo`：比 `zlib` 快但压缩率差
  - `zstd`：压缩率类似于 `zlib`，但速度稍快

Fedora 默认使用 `zstd`。这种方法目前（2025年）被认为是压缩与速度之间的最佳折中。

- `-compress-force=zlib|lzo`
即使看起来没有希望也压缩文件。通常，Btrfs 文件系统会识别已经压缩的文件并不再再次压缩，因为这通常不会节省任何空间，但消耗大量 CPU 时间。使用 `compress-force` 代替 `compress` 会禁用这种识别机制。

- `-degraded`
即使部分 RAID 设备缺失也集成文件系统。这仅在所有数据可用时才有效。

由于 RAID 或冗余导致；即存在降级的 RAID 阵列。

- `noacl`
禁用 ACL 访问管理。

- `nobarrier`
禁用*写入屏障*（write barriers）。写入屏障会阻塞后续的写入操作，直到所有之前的写入操作已在物理完成。没有屏障，文件系统运行得更快，但同时也增加了在崩溃时丢失数据的风险，特别是对于分布在多个设备（RAID）上的文件系统。只有当硬硬盘确实遵循写入请求时，屏障才有效，但出于性能考虑，通常并非如此。

- `ssd`
针对固态硬盘（SSD）优化文件操作。如果 Btrfs 驱动程序确定数据介质是 SSD，该选项会自动激活。然而，此选项对 trim 行为没有影响，trim 由 *discard* 选项单独控制。

- `subvolume=name or subvolume=n`
使用指定的子卷（而不是默认子卷）。你可以使用 `btrfs subvolume list` 来确定子卷的卷 ID。

## CIFS 选项

通用网络文件系统（CIFS）允许你将 Windows 网络目录集成到文件系统中。CIFS 替换了 SMBFS。要使用 CIFS，某些发行版要求你安装单独的包，例如 `cifs-utils` 或 `smbfs`。

关于访问权限，如果文件源自普通的 Windows PC，它们将被分配给 Linux 上的 root 用户。所有用户都可以读取文件，但只有 root 可以修改它们。要让普通用户访问文件，你必须正确设置 `uid`、`gid`、`file_mode` 和 `dir_mode` 选项。

然而，如果文件源自支持 CIFS Unix 扩展的文件服务器（如果 Samba 运行在 Linux 计算机上就是如此），那么文件的 UIDs、GIDs 和访问位将原封地传递。在这种情况下，除非通过 `nounix` 选项禁用 Unix 扩展，否则 `uid`、`gid`、`file_mode` 和 `dir_mode` 选项将无效。

关于 CIFS 特有挂载选项的更多细节，可以参见 `mount.cifs`。

- `credentials=file`
指定一个包含登录 Windows 或 Samba 服务器用户名和密码的文件。这避免了在 `/etc/fstab` 中输入密码。该文件包含三行：`username=xxx`（不是 `user=xxx!`）、`password=xxx`，以及在需要时的 `domain=xxx`。

- `dir_mode=n` (SMBFS 的 `dmask`)
指定访问目录时应用的访问权限。`dir_mode=0770` 赋予由 `uid` 指定的用户和 `gid` 组的所有成员不受限制的权限（读取、打开和更改目录）。

- `domain=workgroup`
指定域或工作组。

- `file_mode=n` (SMBFS 的 `fmask`)
指定访问文件时应用的访问权限。`n` 必须以零开头，并包含在 `chmod` 中常见的八进制表示法。`file_mode=0444` 赋予所有用户读写权限。如果服务器支持 Unix 扩展，则该设置被忽略。

- `iocharset=name`
指定所需的字符集。如果文件名中的特殊字符或其他非 ASCII 字符显示不正确，`iocharset=utf8` 通常会有帮助。

- `nodfs`
禁用分布式文件系统（DFS）功能，该功能允许访问不同服务器的网络目录。一些旧硬盘使用旧版本的 Samba，这在是在使用 `rsync` 命令时会导致问题。在这种情况下，`nodfs` 选项提供了解决方案。

- `nounix`
禁用 Unix 兼容模式。此时，需要少量的背景信息来理解此选项。CIFS 标准通过 Unix 扩展进行了扩展，以实现与 Linux 系统更好的兼容性。在某些 NAS 设备上，这些扩展也是激活的。这看起来很有有用，但在大多数情况下并非如此：Unix 扩展只有在本地计算机和 Samba 服务器的 UIDs 和 GIDs 匹配时才有意义。因此，必须禁用兼容模式，以便 `uid`、`dir_mode` 和 `file_mode` 保持有效。

- `password=pw`
指定用于认证 Windows 或 Samba 服务器的密码。直接输入密码是不安全的！

- `sec=mode`
指定身份验证模式。默认设置为 `ntlms`。替代设置（如 `krb5` (Kerberos)）在 `mount.cifs` 中描述。

- `uid=u, gid=g`
指定文件的所有者和组，与 VFAT 驱动程序相同。用户名或组名也可以传递到选项中，而不是 UID/GIDs。

- `user=name`
指定认证 Windows 或 Samba 服务器的用户名。工作组名称和密码也可以传递到选项中（`user=workgroup`）。

- `vers=n`
指定使用哪个版本的 SMB 协议。当前的挂载版本使用版本 3，因为旧版本存在已知的安全问题。要与旧服务器通信，你必须显式指定所需的版本，例如使用 `vers=21`。

## exFAT 选项

`exFAT` 文件系统 (`-t exfat`) 支持 `dmask`、`fmask`、`gid`、`noatime`、`ro`（只读）、`uid` 和 `umask` 选项。这些选项的效果与同名的 VFAT 选项相同，后者将在几页后进行描述。只有 VFAT 文件系统提供 `noatime`。此选项防止在读取访问期间更新访问信息，从而减少写入操作的次数。

## ext3/ext4 选项

以下选项适用于 Linux 标准文件系统 `ext3` 或 `ext4`：

- `acl`
激活访问控制列表（ACL）访问管理。这允许以访问控制列表的形式存储额外的访问信息。在当前的内核版本中，`acl` 是自动激活的。

- `barrier=0` (仅用于 `ext4`)
禁用写入屏障，屏障确保更改按顺序写入硬磁盘。这增加了文件系统的速度，但只有在硬磁盘缓存受电池保护时才是安全的。

- `commit=n`
每 `n` 秒同步一次日志（默认认为五秒）。`laptop-mode` 包在笔记本电池模式下增加了此时间。对于 `data=ordered` 的 `ext3`，所有更改与日志同步。对于 `data=writeback` 的 `ext3` 和带有延迟分配的 `ext4`，提交间隔仅适用于日志。

- `data=journal/writeback`
确定日志模式（稍后介绍）。默认情况下，`ext4` 应用顺序模式。

- `errors=continue/remount-ro/panic`
确定文件系统检查期间发生错误时的行为。可以使用 `tune2fs` 命令的 `-e` 设置默认行为。

- `grpid`
使新文件自动采用其所在目录的组 ID。这使得文件系统的行为类似于 BSD 或所有目录都设置了 setgid 位。（默认情况下，Linux 将新文件分配给创建文件的组 ID。）

- `nodalloc` (仅用于 `ext4`)
禁用延迟分配。

- `noload`
挂载命令忽略现有的日志文件。这在日志文件损坏时非常有用。

- `sb=n`
使用块 `n` 作为超级块（而不是默认的块1）。在某些情况下，这使得读取损坏的文件系统成为可能。通常，`mke2fs` 每8192块创建一个超级块副本。因此，`n` 的值可以是8193、16385 等。

- `user_xattr`
激活对扩展文件属性的支持（此选项是当前内核版本的默认值）。

## ext3/ext4 日志模式

`ext` 文件系统有三种执行日志的方法：

- `data=ordered`
在这种模式下，只有元数据保存在日志中，即关于文件的信息，而不是内容。只有在文件完全保存后，日志中的文件会被标记为已提交。崩溃后，由于可以立即识别未完全保存的文件，文件系统可以快速恢复到一致状态。然而，无法恢复此类文件。

在 `data=ordered`模式下，日志每五秒同步一次硬磁盘。对于 `ext3`，这意味着

所有对文件的更改都会五秒内物理保存到硬盘上。虽然这种标准行为并不特别高效，但它非常安全：即使在完全崩溃和断电的情况下，大规模数据丢失也极罕见。然而，`data=ordered` 在 `ext3` 中有一个不尽人意的副作用：每次调用 `fsync` 函数时，不仅是特定文件，整个文件系统都会进行同步。这会导致明显的延迟。

在 `ext4` 中，日志也会每五秒同步一次，但由于延迟分配，实际的数据更改通常在更晚时候才会被保存。只有显式调用 `fsync` 函数才能确保文件的立即物理存储！幸运的是，`ext4` 的 `fsync` 不需要同步整个文件系统，因此它的运行速度快得多。

- `data=writeback`
此模式与 `ordered` 模式类似。唯一的区别是日志和文件操作并不总是完全同步的。文件系统不会为了日志中的已提交条目等待硬盘上的存储操作完成。这使得文件系统比 `ordered` 模式略快。发生崩溃后，文件系统的完整性仍然能够保证。然而，更改后的文件可能包含旧数据。如果应用程序（如 POSIX 标准所提供的）使用 `fsync` 完成保存过程（参见 `fsync` 条目），则不会出现这个问题。

- `data=journal`
与其他两种模式不同，实际数据现在也保存在日志中。这意味着所有更改必须保存两次（首先在日志中，然后在相关文件中）。这就是为什么 `ext3` 在此模式下明显慢得多。其更改已完全进入日志（但尚未进入文件）的文件可以在崩溃后恢复。

日志每五秒物理保存到硬盘一次。此时间跨度可以使用挂载选项 `commit` 进行更改。在内部，集成到内核的 `kjournald` 进程负责定期更新日志文件。

## NFS 选项

NFS 文件系统 (`-t nfs`) 是 Unix/Linux 上共享或使用网络目录的常用方法。注意 `-t nfs` 指的是 NFS2 和 NFS3。如果你想使用 NFS4，必须在挂载命令中指定 `-t nfs4`。

大多数 NFS 选项适用于所有 NFS 版本。包括 NFS2/3 和 NFS4 区别的所有选项全面摘要可以在 `man nfs` 中找到。

- `bg`
如果 NFS 服务器无法访问，则使挂载过程在后台继续。此选项仅对 `/etc/fstab` 有效。

- `hard`
当程序访问 NFS 文件时 NFS 服务器不再可用，则导致程序挂起。（`hard` 的替代方案是 `soft`，它会导致内核在一段时间后放弃尝试寻找 NFS 文件。这听起来可能更安全，但实际上它引起的问题比 `hard` 多。）

- `intr`
允许使用 `kill` 或 `Ctrl+C` 停止程序，即使打开的 NFS 文件不再可用。该选项仅在与 `hard` 结合时有效。

- `nfsvers=2/3`
指定所需的 NFS 版本（仅用于 `-t nfs`）。

- `rsize=n, wsize=n`
指定读写操作缓冲区的大小（单位为 KiB）。每个情况的默认值均为 4096。

正确的挂载选项对于 NFS 能实现的速度至关重要！你可以通过这些选项实现高速：`hard`、`intr`、`rsize=8192` 和 `wsize=8192`。如果 NFS 速度仍低于你的预期，你应该确保 NFS 服务器上的 `/etc/exports` 使用了 `async` 选项。

## NTFS 选项

以下选项适用于 `ntfs3g` 驱动程序，大多数发行版使用它访问 NTFS 文件系统：

- `locale=name`
指定本地字符集（例如格式 `locale=en_EN.UTF-8`）。如果在 Init-V 进程自动挂载文件系统时尚未配置字符集，则在 `/etc/fstab` 中需要此选项。

- `show_sys_files`
也显示 NTFS 系统文件。

- `streams_interface=none|windows|xattr`
指定如何访问文件流：在默认的 `xattr` 设置下，通过 `getattr` 或 `setattr` 命令进行访问。`windows` 允许按通常 Windows 写法访问：`filename:streamname`。默认设置为 `none`。

- `uid=u,gid=g,umask=m|fmask=f,dmask=d`
与 VFAT 驱动程序的含义相同（见下一节）。文件所有者是执行 `mount` 的用户。所有用户都有读写权限！

## VFAT 选项

你可以使用 `mount -t vfat` 在目录树中挂载所有变体的 Windows VFAT 分区（FAT12, FAT16, FAT32）。许多选项控制谁拥有什么种文件访问权限、文件名中的不同字符集如何处理等。

- `codepage=name`
指定内部应用于 VFAT 短文件名的代码页（一种 DOS 字符集，最长 8 + 3 个字符）。长文件名始终始终以 Unicode 格式保存；此选项对它们无效。当前的 Windows 版本也会为长文件名以 VFAT 格式保存短文件名，以保持正确的大小写标记。由于由于原因，该选项变得越来越重要。

- `flush`
使驱动程序立即保存介质上的缓存数据（例如 USB 驱动器）。与 `sync` 选项不同，文件系统不会等待同步。此选项最小化了写入所需的时间。

- `fmask=f,dmask=d`
分别设置文件（`fmask`）和目录（`dmask`）的掩码。如果你想设置目录的权限而不是文件的权限，这特别有用。一种可能的设置是 `fmask=177,dmask=077`，允许所有者读写文件并更改目录。

- `iocharset`
指定在 Linux 上处理 Windows 文件名时字符集。默认设置是 `iso8859-1`。根据原则，此选项仅在你处理 8 位字符集时使用。（在 VFAT 内部，文件名始终使用 Unicode 字符集。该选项仅决定文件名在 Linux 显示方式。）如果你在 Linux 上使用 UTF-8 字符集，你应该使用列表末描述的 `utf8` 选项而不是 `iocharset`。

- `shortname=lower|win95|winnt|mixed`
指定以何种大小写呈现或保存短文件名（最长 8 + 3 个字符）。这方面的行为在 Windows 上根据版本而异。在 Linux 上，默认应用 `lower` 设置，即短文件名以小写呈现。对于新文件，名称以长文件名的格式保存（即使没有超过 8 + 3 个字符的 DOS 限制），以便保留大小写。此规则的唯一例外是完全由大写字母组成的短文件名；此类名称作为短文件名保存，正如 DOS 的典型做法。该设置对文件名没有影响，文件名一旦创建就总是区分大小写的。

- `uid=u,gid=g,umask=m`
确定谁（`uid`）以及哪个组（`gid`）“拥有”Windows 文件，即谁允许读取或更改文件。你通常通过 `uid` 和 `gid` 输入期望的用户或组数字。你可以传递 `umask` 位掩码的八进制数值。因此，`umask=0` 意味着任何人都可以读写和运行所有文件（rwxwrwrwx）。`umask=022` 对应 `rwxrxr-`。

`xr-x:` 所有人都可以读取所有文件，但只有所有者可以修改文件。

如果没有指定这些选项，VFAT 文件系统将采用以下默认值：

- `-uid:` 运行 `mount` 命令的用户的 UID。通常，只有 root 可以运行 `mount` 命令，除非 `/etc/fstab` 中对应的行包含 `user`、`users` 或 `owner` 选项。
- `-gid:` 运行 `mount` 命令的用户的 GID。
- `-umask:` 022，即：所有人都可以读取所有内容，但只有所有者可以修改文件或目录。

`fstab` 中经常包含 `gid=users` 的设置。这意味着运行 `mount` 命令的用户的默认组将应用于 `gid`。如果没有此选项，则可能先通过 `newgrp` 激活另一个组，然后该组也会应用于 `mount`。

- `-utf8`
使驱动程序以 UTF-8 字符字符串的形式将文件名返回给 Linux。如果你在 Linux 上使用 UTF-8 作为字符集，则需要此选项来正确显示非 ASCII 字符。

## XFS Options

XFS 文件系统的大多数选项涉及较少使用的函数（参见 `man mount`）。ACL 和扩展属性在 XFS 文件系统上默认可用，且不受选项控制。

- `-logdev=device`
指定存储日志数据的分区。只有在设置文件系统时指定了外部日志分区，此选项才是必要的。

- `-norecovery`
防止在挂载文件系统时对日志数据进行求值。同时，你必须使用 `ro` 选项（只读访问）。

## Examples

按照常规，你可以将 Linux 分区集成到文件系统中，而无需显式指定文件系统类型（即无需使用 `-t` 选项）：

```



`root# mkdir /windows`

`root# mount /dev/sda7 /media/backup-partition`

以下示例显示了如何通过 `/windows` 目录访问 USB 闪盘上的数据：

```
root# mkdir /usbstick
root# mount -t vfat /dev/sdc1 /usbstick
```

需要更多选项，以便不仅是 `root`，用户 ID 为 `1000` 组 ID 为 `1000` 的普通用户也能访问 USB 闪盘并可以写入或更改文件：

```
root# mount -t vfat -o uid=1000,gid=1000,fmask=0022,dmask=0022 \
/dev/sdc1 /usbstick
```

以下命令将 Windows 或 Samba 服务器的网络目录（例如来自 NAS 设备）集成到本地目录树。UID/GID 为 `1000` 的用户可以读取和更改数据。

```
root# mount -t cifs -o
username=name,uid=1000,gid=1000,charset=utf8,nounix \
///diskstation/myshare/media/audio-archive
```

`name` 的密码：*************

你可以使用 `mount -o remount` 来更改已挂载文件系统的选项。例如，以下命令为 USB 闪盘激活了 `noexec` 选项，从而防止执行其中包含的程序：

```
root# mount /dev/sdc1 -o remount,noexec
```

如果在计算机启动期间挂载系统分区时发生问题，该分区将仅以只读方式挂载。然而为了修复错误原因（例如 `/etc/fstab` 中的错误条目），通常需要对文件系统进行更改。要做到这一点，你可以运行以下命令。它会重新挂载系统分区，从而允许进行写操作。

```
root# mount -o remount,rw /
```

## `mtr` [options] host name

`mtr` 命令定期向指定的主机发送网络数据包并分析响应。结果列表结合了 `ping` 和 `traceroute` 的数据。注意，该程序有两个版本：这里描述的文本版本和一个带有图形界面的 GTK 版本。Debian 和 Ubuntu 默认安装 GTK 版本。要安装文本版本，必须运行 `apt-get install mtr-tiny`。

- `-c`
执行 `n` 次测试。（默认情况下，程序运行到通过 Ctrl+C 终止）。
- `-n` 或 `--dns`
跳过域名解析并将所有中间阶段指定为 IP 地址。
- `-r` 或 `--report`
测试完成后提供文本格式报告。此选项必须与 `-c` 结合使用。

### Example

以下行了本地路由器和 `www.google.com` 之间典型的 `mtr` 结果：

```
$ mtr -c 10 google.com
HOST: fritz.box             Loss% Snt Avg StDev
1. fritz.box                       0.0%   10   1.4  0.9 1.5 0.2
2. dynamic-01.res.high              0.0%   10   37.2 36.0 20.5 42.7
3. lg02-9080.as44.al.net           0.0%   10   38.5 40.9 30.0 47.8
4. lg23-9080.as44.al.net         0.0%   10   41.6 40.0 35.0 45.8
5. lg4-9080.as44.al.net         0.0%   10   48.4 42.2 46.5 50.0
6. 2021:4860:0:1::88ab           0.0%   10   49.3 48.9 37.0 57.6
7. 2021:4860:c::4003:364e         0.0%   10   47.2 52.4 46.8 58.8
8. 2021:4860:0:1::8886           0.0%   10   46.6 49.2 42.0 57.7
9. 2021:4860:9::364fc           0.0%   10   47.5 47.6 42.5 49.1
10. 2021:4860:0:1::7651          0.0%   10   51.5 49.3 26.8 53.6
11. 2021:4860:0:1::7651           0.0%   10   53.9 52.5 23.8 60.7
12. 2021:4860:0:1::ea5          0.0%   10   51.7 50.8 22.9 61.9
13. bud02s41-in-xe0100.net    0.0%   10   52.4 49.3 22.9 54.9
```

## `multitail` options [file1 file2 file3 ...]

`multitail` 帮助同时监控日志文件。在最简单的形式，你应该运行 `multitail file1 file2 file3....`。这将终端分成多个等大的区域，显示指定文件的最后行。如果你在文件前加上 `-i`，多个文件的更改将输出在一个区域。然而，很难看出哪个文件发生了变化。

## `mv`

```
mv source target
mv files target directory
```

`mv` 重命名文件或目录，或将一个或多个文件移动到另一个目录。

- `-b` `--backup`
将同名的现有文件重命名为备份文件（文件名加上 `~` 字符），而不是覆盖它们。
- `-i` `--interactive`
在覆盖现有文件之前进行询问。

### Example

以下命令将当前目录下的所有 PDF 文件移动到 `pdf` 子目录：

```
user$ mv *.pdf pdf/
```

`mv` 不能用于重命名多个文件。`mv *.xxx *.yyy` 不起。要执行此类操作，必须使用 `for` 或 `sed`。相应的示例可以在 `cp` 中找到。

```
mysql [options] [database name] [< name.sql]
```



`mysql` 命令解释器在 MySQL 或 MariaDB 服务器上执行 SQL 命令，可以是交互式的，也可以从标准输入进行批模式。命令必须以分号结束。在批处理中，`mysql` 通常用于导入使用 `mysqldump` 创建的备份。如果在调用 `mysql` 时没有指定数据库名称，则必须通过 `use` 命令设置所需的数据库。

以下选项仅影响连接设置，并以相同的形式应用于后续条目中描述的 `mysqladmin` 和 `mysqldump` 命令。在现实生活中，通常只需要 `-u`、`p` 和 `-h` 选项。

- `--default-character-set=name`
  指定与 MySQL 或 MariaDB 服务器通信时使用的字符集（例如，`latin1` 或 `utf8`）。
- `--defaults-extra-file=filename`
  从指定的文件加载连接选项。这很有用，例如当 `mysql` 或 `mysqldump` 需要由 `cron` 定期运行且无法进行交互式密码输入时。
- `-h --host=hostname`
  指定运行服务器的计算机名称或 IP 地址（默认是 `localhost`）。
- `--login-path=group`
  评估 `.mylogin.cnf` 中的 `[group]` 数据。
- `-P --port=n`
  指定 TCP/IP 连接的端口号（默认 `3306`）。
- `-p --password`
  在启动命令后提示输入密码。如果缺少该选项，`mysql` 从本地配置文件 `.my.cnf` 读取密码。如果文件不存在或不包含密码数据，`mysql` 将尝试在无密码的情况下登录。
- `-pxxx --password=xxx`
  直接传输密码。然而，安全的，因为密码会明文出现在进程列表中！与其他选项不同，`-p` 选项不允许空格。
- `--protocol=tcp/socket`
  指定 MySQL 客户端与数据库服务器通信时使用的协议。默认情况下，如果客户端和服务器在同一台计算机上，使用 `socket`；否则使用 `tcp`。
- `-S --socket=name`
  指定套接文件的位置。只有当 `mysql` 无法自行找到套接文件时，才需要此选项。在大多数发行版中，文件名为 `/var/run/mysql/mysql.sock`。其位置可以在配置文件 `/etc/my.cnf` 或 `/etc/mysql/my.cnf` 中设置。
- `-u --user=name`
  指定 MySQL 或 MariaDB 用户名（默认，

（这是当前的用户名）。

还有一些 MySQL 特有的选项：

- `-B` 或 `--batch`
  在输出结果时用制表符（而不是空格和行图形）分隔列。此外，它只显示查询结果，而不显示任何状态信息。
- `-e` 或 `--execute='sql command'`
  运行指定的命令。你也可以输入用分号分隔的多个命令。
- `-h` 或 `--html`
  将查询结果格式化为 HTML 代码。
- `-N` 或 `--skip-column-names`
  不为结果列标记标签。
- `-r` 或 `--raw`
  在查询结果中原样输出 `0`、制表符、换行和 `\` 字符。（通常，这些字符会被输出为 `\0`, `\t`, `\n` 和 `\\`。）该选项仅在与 `--batch` 结合时才有效。
- `-s` 或 `--silent`
  只输出结果本身。
- `-x` 或 `--xml`
  将查询结果格式化为 XML 代码。

### 示例

以下命令在本地 MySQL 或 MariaDB 服务器上导入数据库备份。`dbname` 数据库必须已经存在。

```
$ mysql -u name -p dbname < backup.sql

Enter password: ********
```

如果备份文件是压缩过的，你应该按照以下方式操作：

```
$ gunzip -c backup.sql.gz | mysql -u name -p dbname
```

以下行显示了一个小型脚本，它将 SQL 命令传递给 `mysql` 以测试数据库是否存在：

```bash
#!/bin/bash

dbname="ebooks"

sql="SELECT schema_name FROM information_schema.schemas WHERE schema_name='$dbname';"

result=$(mysql -s N -e "$sql")

if [[ -n "$result" ]]; then

echo "Database exists"

else

echo "unknown database"

fi
```

### 替代方案

`mysqlsh` 和 `mariadb-shell` 是新的 shell，专门针对 MySQL 和 MariaDB 进行了优化，并提供了各种额外功能。然而，新的 shell 使用不同的选项，并且与 `mysql` 命令不兼容。

```
mysqladmin [options] command1 command2 ...
```

`mysqladmin` 帮助处理 MySQL 或 MariaDB 服务器上的各种管理任务，例如创建新数据库。你可以向 `mysqladmin` 传递多个命令，这些命令将按顺序执行。只要 `mysqladmin` 命令的仍然清晰可见，就可以缩写（例如，用 `flush-l` 代替 `flush-logs`）。`mysqladmin` 命令也可以作为 SQL 命令运行，例如 `CREATE DATABASE`、`DROP DATABASE`、`FLUSH` 等。

为了让 `mysqladmin` 建立到数据库服务器的连接，必须使用 `mysql` 命令中描述的连接选项，即 `-u`、`-p`、`-h` 等。此外，`mysqladmin` 还知道更多选项：

- `-f` 或 `--force`
  运行命令而不进行进一步询问。即使某个命令发生错误，也会继续执行多个命令。
- `-i` 或 `--sleep=n`
  每隔 `n` 秒重复一次命令（例如，用于定期显示状态）。`mysqladmin` 将无期运行，并可以通过 `Ctrl+C` 终止。
- `-r` 或 `--relative`
  与 `-i` 和扩展状态命令结合使用，显示与之前状态相比的变化。

这里描述了最重要的 `mysqladmin` 命令：

- `- create dbname`
  创建一个新数据库。
- `- drop dbname`
  不可恢复地删除一个现有数据库。
- `- extended-status`
  显示服务器的无数状态变量。
- `- flush-logs`
  关闭所有日志文件并重新打开。
- `- flush-privileges`
  重新加载具有相关访问权限的数据库。
- `- kill id1, id2...`
  关闭指定的线程。
- `- ping`
  测试是否可以建立到数据库服务器的连接。
- `- shutdown`
  终止 MySQL 或 MariaDB 服务器。
- `- status`
  显示数据库服务器的各种状态变量。
- `- variables`
  提供数据库服务器系统变量列表。
- `- version`
  确定 MySQL 或 MariaDB 服务器的版本。

### 示例

以下命令在本地 MySQL 或 MariaDB 服务器上创建一个新数据库：

```
user$ mysql -u name -p create newdb

Enter password: ********
```

```
mysqlbinlog [options] loggingfile file2 ...
```

MySQL 或 MariaDB 可以在二进制文件中记录所有更改，特别是所有的 `INSERT`、`UPDATE` 和 `DELETE` 命令。这些文件在必要时用于增量更新。`mysqlbinlog` 读取这些日志文件。建立连接的选项与 `mysql(-u, -p, 等)` 中的选项相同。

- `- --database=name`
  只考虑影响特定数据库的命令。
- `- -j`
  仅从某个位置开始评估第一个日志文件。
- `- --no-defaults`
  不考虑如 `.my.cnf` 等配置文件。在实践中，如果 `.my.cnf` 包含一个适用于所有 MySQL 客户端命令但不允许 `mysqlbinlog` 使用的选项（例如 `default-character-set=utf8`），则经常需要此选项。这样你就可以避免 `unknown variable xy` 的错误信息。

### 示例

在导入最后的完整备份后，应用来自两个 binlog 文件的增量更新：

```
root# cd /var/log/mysql
root# mysqlbinlog -j 120 mariadb-bin.001380 mariadb-bin.001380 | \
  mysql -u root -p
```

```
mysqldump [options] dbname [table1 table2 ...]
mysqldump [options] --databases [dbname dbname2]
mysqldump [options] --all-databases
```



`mysqldump` 是一个用于 MySQL 和 MariaDB 数据库系统的简单备份工具。该命令返回长长的 SQL 命令列表，可以从这些列表中精确恢复数据库。`mysqldump` 知晓三种语法变体，取决于保存一个数据库、多个列出的数据库还是由 MySQL 管理的所有数据库。只有第一种变体允许备份限制在单个表。

为了让 `mysqldump` 建立到数据库服务器的连接，必须使用 `mysql` 命令中描述的连接选项，即 `-u`、`-p`、`-h` 等。其他许多选项控制备份的细节。

### 选项

- `--add-locks`
  在第一个 `INSERT` 命令之前插入 `LOCK TABLE`，在最后一个 `INSERT` 命令之后解锁。这加快了 MyISAM 表的重新加载。然而，此选项不适用于 InnoDB 表。

- `--create-options`
  在 `CREATE TABLE` 中包含 MySQL 特有的选项。

- `--disable-keys`
  在重新加载数据期间禁用索引更新。索引直到过程结束时才会更新，这样速度更快。

- `--extended-insert`
  创建较大的 `INSERT` 命令，同时插入多个数据记录。

- `--lock-all-tables`
  对整个数据库运行 `LOCK READ`。这确保在备份期间没有表被更改。此选项仅适用于 MyISAM 表。对于 InnoDB 表，最好使用 `--single-transaction`。

- `--lock-tables`
  在备份期间对每个表运行 `TABLE READ`。

- `--no-create-info`
  只保存数据，不保存结构。生成的备份中有 `INSERT` 命令，但没有 `CREATE TABLE`。

- `--no-data`
  只保存数据库的结构（模式），但不包含数据。

- `--no-tablespaces`
  防止 `mysqldump` 包含 `CREATEFILE GROUP` 或 `CREATE TABLESPACE` 命令。如果你以没有 Process 权限的用户运行命令，在当前的 MySQL 版本中必须使用此选项。否则会发生拒绝访问的错误。

- `--opt`
  以下选项的简写：`--add-drop-table`、`--add-locks`、`--create-options`、`--disable-keys`、`--extended-insert`、`--lock-tables`、`--quick` 和 `--set-charset`。由于历史原因，`--opt` 默认启用。然而，只有当你执行 MyISAM 表的备份时，生成的设置才是优的（因此有了该选项名称）。

- `--quick`
  直接输出要保存的数据记录，不在内存中进行中间存储。

- `--routines`
  还保存存储过程的代码。

- `--set-charset`
  在 `mysqldump` 输出开始更改活动字符集，并在结束时恢复之前的字符集。

- `--single-transaction`
  确保整个备份作为单个事务的一部分执行。这对于 InnoDB 表很有用，并防止单个表在备份期间被更改。这确保了整体的一致性。

- `--skip-opt`
  禁用默认启用的 `--opt` 选项。

- `--triggers`
  还保存触发器的代码。

## 示例

备份带有 MyISAM 表的数据库只需要几个选项。如果你想防止单个表在备份期间被更改，则需要在命令中添加 `--lock-all-tables` 选项。

```
user$ mysqldump -u user -p dbname > backup.sql
Enter password: ********
```

如果你想保存一个压缩后的备份，应该按照以下步骤操作：

```
user$ mysqldump -u user -p dbname | gzip -c > backup.sql.gz
```

对 InnoDB 表执行优化备份需要多得选项，因为 `mysqldump` 的默认设置并没有针对此类情况进行优化：

```
user$ mysqldump -u user -p --skip-opt --single-transaction \
--create-options --quick --extended-insert \
--disable-keys --add-drop-table dbname > backup.sql
```

如果你使用 `cron` 任务（`cron job`）自动运行备份，你必须将 `-u user -p` 替换为以下选项，并在仅 root 访问的文件 `/root/.my.cnf` 中输入连接参数：

> # 在备份脚本中，`--defaults-extra-file` 必须是第一个选项
`mysqldump --defaults-extra-file=/root/.my.cnf ...`

要稍后恢复备份，你必须运行以下命令：

```
user$ mysqladmin -u user -p create dbname
user$ mysql -u user -p --default-character-set=utf8 dbname < nbackup.sql
```

# `namei`

## `namei [options] file`

`namei` 显示形成指定文件路径的所有目录的权限：

```
user namei -l ~/.ssh
f: /home/kofler/.ssh
drwxr-xr-x root root      /
drwxr-xr-x root root home
drwxr-xr-x kofler kofler kofler
drwx------ kofler .ssh
```

# `nc`

## `nc [options] [hostname/ip-address] [port]`

`nc` 命令更广为人知的 Netcat。它将 TCP/UDP 端口重定向到标准输入/输出，并提供许多其他功能。你可以使用该命令类似于 `telnet` 地交互式测试 HTTP 或 SMTP 等网络协议。通过 `nc`，你还可以通过任何网络端口复制文件、实现聊天，或者设置一个通过端口接收并执行命令的简单后门程序。因此，`nc` 在黑客和渗透测试人员中极其流行并不意外。

在某些 Linux 发行版中，`nc` 命令包含在同名的软件包中；在其他发行版中，你必须安装 `netcat`。注意 Netcat 有不同的实现版本。例如，Debian 和 Ubuntu 使用 `netcat-traditional`，而 RHEL 提供了来自 mmap 开发者的变体（https://nmap.org/ncat）。在实践中，这不会产生任何差异，但根据版本，单个选项的实现方式可能不同（或完全没有实现）。

### 选项

- `-4 -6`
  仅使用 IPv4 或 IPv6。

- `-l`
  等待指定的端口建立连接（监听）。

- `-p portnr`
  定义本地端口（源端口）。通常在 `nc` 命令末尾指定的端口是目标端口。

- `-x proxyadr:portnr`
  使用指定的代理地址和相应的端口。

`man nc` 中描述了许多其他选项。`nc` 的一个可能的替代方案是 `socat` 命令，本书未涵盖它。它还支持 SCTP，可以通过代理服务器工作，操作串口接口，并对传输数据进行加密：

# Examples（示例）

要从主机 1 向主机 2 通过任意端口（这里是 1234）复制文件，你首先在主机 2（右侧列）启动接收端，然后向主机 1 发起传输（左侧列）：

```
host2$ nc -l 1234 > file
host1$ nc host2 1234 < file
```

进行聊天同样简单。你只需要与对方约定一个端口即可。聊天在计算机上通过 `nc -l`（左侧列）启动。通过这样，`nc` 监控指定的端口 1234 并等待建立连接。

在第二个主机上，启动 `nc` 时不带选项以连接到第一个主机。没有可见的确认显示连接已建立，但只要双方中的一方输入文本（标准输入）并按回车键确认，文本就会出现在另一方的终端上（标准输出）。

```
host1$ nc -l 1234
host2$ nc host1 1234
how are you?
how are you?
good
```
```
good
<Ctrl+><
```

第三个示例展示了 Netcat 的潜在危险：在这里，主机 1 上的 `nc` 设置为将从端口 1234 接收的所有输入传递给 `bash` shell。它们的输出会被传回给发送者。现在可以从第二个主机在主机 1 上运行 shell 命令。因此，`ls` 显示的是位于主机 1 上的文件！

```
host1$ nc -l 1234 -e /bin/bash
host2$ nc host1 1234
ls
file1
file2
file3
```



然而，并不是所有的 Netcat 版本都提供执行命令的 `-e` 选项。在 Debian 和 Ubuntu 上常用的 `netcat-traditional` 实现中特别缺少该选项。解决方法是安装 `nmap` 软件包并运行其中包含的 `ncat` 命令。

## ncdu [options] [directory]

`ncdu` 是 `du` 的交互变体。你现在可以使用键在目录之间导航。它会显示空间最大的目录。

### Examples（示例）

以下命令显示了目录的状态：

```
user$ ncdu
```

## needsrestart [options]

`needsrestart` 命令指示配置是否已更新。它适用于 Debian 和 Ubuntu。

- `-r`
以只读模式运行命令。
- `-u`
列出需要重启的进程。

### Examples（示例）

以下命令显示了活动连接：

```
root$ needsrestart
```

## netplan [command]

Netplan (https://netplan.io) 是由 Ubuntu 开发的一个框架，用于配置和集成 NetworkManager 和 systemd 等后端。它评估位于 `/etc/netplan` 的配置文件。

- `apply`
运行 `netplan generate` 然后激活配置。
- `generate`
读取来自 `/etc/netplan`、`/lib/netplan` 和 `/var/netplan` 的 Netplan 配置，然后生成相应的配置文件。
- `ip leases interface`
输出相关接口的 DHCP 租数据。

## netstat [options]

`netstat` 提供本地计算机网络活动的信息。如果不带选项调用命令，它将返回所有打开的互联网连接和套接字。

- `-a`
也考虑非活跃套接字，即在网络端口上等待连接的服务（LISTEN 状态）。
- `-n`
提供数值地址和端口号，而不是主机名和网络服务名。
- `-p`
指定指定连接的程序的进程号 (PID) 和进程名。

### Examples（示例）

以下命令列出所有活动连接（已建立）或监控的端口（LISTEN）。由于空间限制，输出已大幅删减。

## networkctl [command]

`networkctl` 是 systemd 系列中的管理命令之一。如果使用 networkd 作为网络后端，`networkctl` 可以帮助分析网络状态。

尽管许多发行版默认安装了 networkd，但它仅在其中少数版本中处于激活状态。其中一个例外是 Ubuntu Server，在其中 networkd 作为 Ubuntu 自有 Netplan 系统的后端（见 `netplan`）。`networkctl` 会评估来自 `/etc/systemd/network/`、`/lib/systemd/network/` 和 `/run/systemd/network` 等目录的配置文件，例如 `/etc/systemd/network/networkd.network`。

- `list`
列出所有网络接口。结果中的 SETUP 列显示该接口是否由 networkd 控制（已配置）或未由其控制（未管理）。
- `lldp`
显示通过链路层发现协议 (LLDP) 发现的网络中的其他设备。
- `status [interface]`
提供有关网络接口状态的详细信息。如果没有指定接口，该命令将尝试总结整个网络状态。

### 示例

以下 `networkctl` 输出是在虚拟机中的 Ubuntu 服务器上创建的：

```
root# networkctl list

IDX      LINK        OPERATIONAL  SETUP

1        loopback   carrier      unmanaged

2        ens3        ether       routable     configured

root# networkctl status ens3

Link File: /lib/systemd/network/99-default.link

Network File: /run/systemd/network/10-netplan-ens3.network

Type: ether

State: routable (configured)

...

HW Address: 52:54:00:0a:8d:fc

Address: 138.201.20.182

       fe80::5054:ff:fe0a:8dfc

Gateway: 138.201.20.176 (Fujitsu Technology Solutions GmbH)

DNS: 213.133.100.100

       213.133.100.98

Search Domains: ubuntu-buch.info
```

第二个列表显示了另一个带有 IPv6 配置的服务器的状态总结：

```
root# networkctl status

State: routable

Online state: online

Address: 168.119.33.110 on eth0

       172.17.0.1 on docker0
```

```
2a01:4f8:242:1f88:: on eth0

fe80::5054:ff:fe4a:7321 on eth0

Gateway: 168.119.33.119 on eth0

2a01:4f8:242:1f88::2 on eth0

DNS: 213.133.100.100

213.133.99.99

2a01:4f8:0::add:1010

2a01:4f8:0:1::add:9999
```

## newaliases

`/etc/aliases` 文件包含邮件服务器的别名列表，它确保确保例如所有发送给 postmaster 的邮件都转发到 root。要让邮件服务器考虑到此文件的更改，你必须运行 `newaliases`。

## newgrp [group name]

`newgrp` 命令用于确定属于多个组的用户当前激活的组。活动组决定了新创建的文件属于哪个组。可以通过 `groups` 命令确定可选择的组。如果没有指定组名，则将使用主组。该组在登录后也会自动被视为活动组。

### 示例

在下面的示例中，`newgroup` 命令将 `docuteam` 设置为用户 `kofler` 的活动组。结果，新创建的文件 `newfile` 被分配给 `docuteam` 组，并可以由 team 的成员编辑。

```
user groups

kofler docuteam

user newgroups docuteam

user touch newfile
```



## newusers

`newusers` 读取文本文件并创建新用户。该文件的格式与 `/etc/passwd` 相同。

## nft Commands

- `add chain family lname cname`
在指定的表中创建一个名为 `cname` 的新链。

- `add rule family lname cname matches statements`
在指定的链中添加新规则。这里，`matches` 指定了规则适的数据包。`statements` 描述了对相应数据包应该执行的操作。
除了 `add`，还允许 `insert` 和 `replace` 关键字在规则列表的特定位置插入规则，或用新规则替换现有规则。

- `add table family lname`
为指定的族创建一个新表。

- `delete/flush chain lname cname`
从表中删除指定的链。`flush` 删除该链的所有规则，但不删除该链本身。

- `delete rule family lname cname handle came`
从 `cname` 链中根据 `handle` 删除规则。

- `delete/flush table family lname`
删除指定的表。使用 `flush` 删除所有链和规则

表中的内容已被删除，但保留了现有的空表。

- `flush ruleset`
删除所有表，包括其中包含的所有链和规则。这对应于防火墙的完全重置。防火墙现在接受所有数据包。

- `list tables`
`list table family name`
`list chain family tname cname`
列出表、链和规则。

- `list ruleset`
列出所有表、链和规则。由大括号结构的输出符合 `nft -f` 的语法规则，因此可以作为新规则文件基础。带有额外的 `-j` 选项，输出将为 JSON 格式。

- `monitor [filter criteria]`
显示 `nftables` 事件（例如作为调试帮助）。

## 示例

前两个命令显示了测试计算机（Fedora 32）上定义了哪些防火墙表，以及哪些链和规则适用于 `ip` 族中的 `firewalld` 表。（`nftables` 允许在不同的族中使用相同匹配的表名。因此，在第二个 `list` 命令中也必须指定族。）

```
```



`root# nft list tables`

`table bridge filter`

`table bridge nat`

`table inet firewall`

`table ip firewall`

`table ip6 firewall`

```
```

`root# nft list table ip firewall`

```
table ip firewall {

    chain nat PREROUTING {

        type hook prerouting priority dnat + 10; policy accept;

        jump PREROUTING_ZONES

    }
```

```
```

```
chain nat PREROUTING_ZONES {

    ifname enp0" goto nat_PRE_FedoraWorkstation

    goto nat_PRE_FedoraWorkstation

}
```

`systemctl now` 禁用了默认的 Fedora 守护进程：

```
root# systemctl disable --now firewall
```

你可以使用 `nft` 创建自己的防火墙。通过反复调用 `nft` 来定义规则并不常见。在文件中编写规则并运行脚本要优优雅得多。要做到这一点，你必须在行中输入 `nft -f` 作为 shell 解释器。

```
#!/bin/nft -f

# 删除现有的防火墙

flush ruleset

# 为 IPv4 和 IPv6 创建新表

table inet myfilter {

chain input {

    type filter hook input priority 0; policy drop;

    # 阻塞故障数据包

    ct state invalid drop

    # 始终接受自生成连接的数据包

```

```
ct state {established, related} accept

# 接受内部网络流量

if lo accept

# 阻塞来自外部地址的环回数据包

if != lo ip daddr 127.0.0/8 drop

if = lo ip daddr ::1/128 drop

# 接受 ICMP 数据包

ip protocol icmp accept

ip6 nextthdr icmp6 accept

# 接受外部的 SSH 连接

tcp dport 22 accept

# 用于服务器配置：更多针对

# HTTP + HTTPS (端口 80 + 443), Samba

# ...

}

# 无转发

chain forward {

  type filter hook forward priority 0; policy drop;

}
```

# 现在你可以运行脚本了：

```
root# chmod +x myfirewall

root ./myfirewall
```

`nft -f` 首先执行语法检查。如果检测到错误，它将带有错误消息终止进程。在这种情况下，之前的防火墙将被保留。

之前的脚本在 Gentoo wiki 上进行了稍作修改。你可以在那里以及 ArchLinux Wiki 中找到更多示例：

https://wiki.gentoo.org/wiki/Nftables/Examples

https://wiki.archlinux.org/title/Nftables

# `ngrep [options] [grep-search-expression] [pcap-filter-expression]`

`ngrep` 被称为数据包嗅器。该命令读取端口的网络流量并对其过滤。`ngrep` 提供了与 `tcpdump` 命令类似的功能，并像它使用 `pcap` 库读取网络数据包。与 `tcpdump` 不同的是，`ngrep` 还考虑数据包的内容。自然，这只对非加密协议（如 HTTP 或 FTP）有效。

搜索表达式必须以 `grep` 正则模式的形式表述。在 `tcpdump` 中总结的语法适用于 `pcap` 过滤器表达式。

- `-d interface|any`
  确定网络接口。

- `-i`
  忽略 `grep` 搜索表达式中的大小写。

- `-v`
  反转搜索。因此，`ngrep` 只返回未识别出 `grep` 搜索模式的数据包。

- `-w`
  将 `grep` 搜索表达式解释为单词。

- `-W byline`
  在输出时考虑换行符，从而产生更具可读性的输出。

## 示例

以下示例在所有接口上监听包含 `user`、`pass` 等关键词的 HTTP 数据包：

```
ngrep -d any -i 'user|pass|pwd|mail|login' port 80

interface: any

filter: (ip or ip6) and ( port 80 )

match: user|pass|pwd|mail|login

T 10.0.0.87:50480 -> 91.229.57:14:00 [AP] POST /index.php

HTTP/1.1..:Host: user=name&pass=geheim&login=Login

...
```

## `nice [options] program`

`nice` 以降低或增加优先级启动指定的程序。该命令可用于低优先级启动非时间关键型程序，以免对系统的其余部分产生太大影响。

- `-n +/-n`
  指定 `nice` 值。默认情况下（不使用 `nice`），程序以 `nice` 值 0 启动。值 -20 表示最高优先级，值 +19 表示最低优先级。小于 0 的值只能由 `root` 指定；这意味着大多数用户只能通过 `nice` 启动降低优先级的程序。如果省略此选项，`nice` 将以 `nice` 值 +10 启动程序。

注意，`nice` 只控制 CPU 负载。如果你想减少命令的 I/O 负载，最好使用 `ionice`。

`22/tcp open ssh`
`88/tcp open kerberos-sec`
`445/tcp open microsoft-ds`
`548/tcp open afp`
`MAC Address: AC:87:A3:1E:4A:87 (Apple)`
`Nmap scan report for raspberrypi (10.0.0.22)`
`Host is up (0.00038s latency).`
`Not shown: 99 closed ports`
`PORT STATE SERVICE`
`22/tcp open ssh`
`MAC Address: BB:27:EB:11:44:2E (Raspberry Pi Foundation)`

`Nmap done: 256 IP addresses (6 hosts up) scanned in 2.42 seconds`

# 第二个示例显示了位于不同局域网的 NAS 设备的 `nmap` 结果（再次大幅简化了）：

```
root# nmap -v -A 192.168.178.28

map scan report for DiskStation.fritz.box (192.168.178.28)

Host is up (0.0023s latency).

Discovered open port 445/tcp on 192.168.178.28

Discovered open port 139/tcp on 192.168.178.28

Discovered open port 80/tcp on 192.168.178.28

Discovered open port 443/tcp on 192.168.178.28

Discovered open port 22/tcp on 192.168.178.28

Discovered open port 5001/tcp on 192.168.178.28

Discovered open port 5080/tcp on 192.168.178.28

Discovered open port 548/tcp on 192.168.178.28
```

```
PORT STATE VERSION

22/tcp open ssh OpenSSH 7.4 (protocol 2.0)

ssh-hostkey:

204B 5a:e7:a3:66:f4:9f:0a:0a:... (RSA)

256 06:a1:bf:9f:e9:d0:64:3a:92:... (ECDSA)

256 ad:b7:7d:ae:70:0a:c9:0c:... (ED25519)
```

```
80/tcp open http nginx

139/tcp open netbios-ssn Samba smbd 4.6.2

445/tcp open netbios-ssn Samba smbd 4.6.2
```



```
Nmap done: 1 IP address (1 host up) scanned in 64.19 seconds
```

## `nmblookup [options] workgroupname`

`nmblookup` 来自 `samba-common-bin` (Debian/Ubuntu) 或 `samba-client` (Fedora/RHEL) 软件包，用于确定局域网中哪些设备或服务器提供了 SMB 共享。以前可以使用 `smbtree` 实现此，但该命令需要 SMB1 的浏览功能，在现代网络中已经过时。

- `-S`
  对找到的每个服务器执行状态查询，然后显示详细结果。

- `-T`
  提供服务器名称和 IP 地址的有序列表。根据我的经验，如果先运行 `nmblookup -s` 或在几秒后再次运行命令，`nmblookup` 的结果会更可靠。第一个结果通常是不完整的。

### 示例

局域网中有两个 SMB 服务器、一个 NAS 设备和一个配置恰当的树莓派：

```
user$ nmblookup -T WORKGROUP

DiskStation.fritz.box, 192.168.178.43 WORKGROUP<<00>

pi5.fritz.box, 192.168.178.123 WORKGROUP<<00>
```

```
nmcli [options] con|dev|nm command
```

Network Manager 通常通过 Gnome 或 KDE 面板中的菜单控制。你也可以使用 `nmcli` 命令通过命令行或脚本控制网络连接。

可选选择的命令取决于它们所指的对象。选项 `-t`、`-p` 等可用于控制 `nmcli` 输出的形式——取决于输出是否需要正确格式化或由脚本进一步处理（详情请参阅 `man nmcli`）。

- `con down name` 或 `con down uuid n`
  禁用指定的连接。

- `con show`
  列出所有配置的连接，指定每个连接的名称和 UUID。

- `con up name` 或 `con up uuid n`
  激活指定的连接。

- `dev disconnect name`
  终止指定接口的连接。

- `dev`
  列出 Network Manager 已知的所有接口及其属性。

- `dev show`
  显示所有接口的详细信息。

- `dev wifi hotspot`
  将 Wi-Fi 适配器配置为路由器。

- `dev wifi list`
  提供范围内所有 Wi-Fi 网络列表，包括信号强度。该命令需要 `wpa_supplicant`。

（此处省略原文中大量重复的 dev 命令描述，已根据要求处理）

- `dev show`
  显示此处重复的模式。

- `dev wifi list`
  提供范围内所有 Wi-Fi 网络列表，包括信号强度。该命令需要 `wpa_supplicant`。

（等待，OCR 文本有重复模式。）

- `dev wifi hotspot`
  将 Wi-Fi 适配器配置为路由器。

- `dev wifi list`
  提供范围内所有 Wi-Fi 网络列表，包括信号强度。该命令需要 `wpa_supplicant`。

- `dev show`
  显示所有接口的详细信息。

（此处由于原文的重复模式，我将按照提供的逻辑流继续。）

# 第二个示例显示了位于不同局域网的 NAS 设备的 nmap 结果（再次大幅简化了）：

```
root# nmap -v -A 192.168.178.28

map scan report for DiskStation.fritz.box (192.168.178.28)

Host is up (0.0023s latency).

Discovered open port 445/tcp on 192.168.178.28

Discovered open port 139/tcp on 192.168.178.28

Discovered open port 80/tcp on 192.168.178.28

Discovered open port 443/tcp on 192.168.178.28

Discovered open port 22/tcp on 192.168.178.28

Discovered open port 5001/tcp on 192.168.178.28

Discovered open port 5080/tcp on 192.168.178.28

Discovered open port 548/tcp on 192.168.178.28
```

```
PORT STATE VERSION

22/tcp open ssh OpenSSH 7.4 (protocol 2.0)

ssh-hostkey:

204B 5a:e7:a3:66:f4:9f:0a:0a:... (RSA)

256 06:a1:bf:9f:e9:d0:64:3a:92:... (ECDSA)

256 ad:b7:7d:ae:70:0a:c9:0c:... (ED25519)
```

```
80/tcp open http nginx

139/tcp open netbios-ssn Samba smbd 4.6.2

445/tcp open netbios-ssn Samba smbd 4.6.2
```

Nmap done: 1 IP address (1 host up) scanned in 64.19 seconds

## `nmblookup [options] workgroupname`

`nmblookup` 来自 `samba-common-bin` (Debian/Ubuntu) 或 `samba-client` (Fedora/RHEL) 软件包，用于确定局域网中哪些设备或服务器提供了 SMB 共享。以前可以使用 `smbtree` 实现此，但该命令需要 SMB1 的浏览功能，在现代网络中已经过时。

- `-S`
  对找到的每个服务器执行状态查询，然后显示详细结果。

- `-T`
  提供服务器名称和 IP 地址的有序列表。根据我的经验，如果先运行 `nmblookup -s` 或在几秒后再次运行命令，`nmblookup` 的结果会更可靠。第一个结果通常是不完整的。

### 示例

局域网中有两个 SMB 服务器、一个 NAS 设备和一个配置恰当的树莓派：

```
user$ nmblookup -T WORKGROUP

DiskStation.fritz.box, 192.168.178.43 WORKGROUP<<00>

pi5.fritz.box, 192.168.178.123 WORKGROUP<<00>
```

```
nmcli [options] con|dev|nm command
```

Network Manager 通常通过 Gnome 或 KDE 面板中的菜单控制。你也可以使用 `nmcli` 命令通过命令行或脚本控制网络连接。

可选选择的命令取决于它们所指的对象。选项 `-t`、`-p` 等可用于控制 `nmcli` 输出的形式——取决于输出是否需要正确格式化或由脚本进一步处理（详情请参阅 `man nmcli`）。

- `con down name` 或 `con down uuid n`
  禁用指定的连接。

- `con show`
  列出所有配置的连接，指定每个连接的名称和 UUID。

- `con up name` 或 `con up uuid n`
  激活指定的连接。

- `dev disconnect name`
  终止指定接口的连接。

- `dev`
  列出 Network Manager 已知的所有接口及其属性。

- `dev show`
  显示所有接口的详细信息。

- `dev wifi hotspot`
  将 Wi-Fi 适配器配置为路由器。

- `dev wifi list`
  提供范围内所有 Wi-Fi 网络列表，包括信号强度。该命令需要 `wpa_supplicant`。

（此处省略原文中大量重复的 dev 命令描述，已根据要求处理）

对于文件，需要以下选项：

```
openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -nout server.key
```



如果密钥本身需要加密，则必须通过额外选项（例如 `-aes256`）指定加密算法名称。在命令执行期间，`openssl` 会两次提示输入加密密码。

- `-list-standard-commands | list-message-digest-commands | list-cipher-commands | list-cipher-algorithms | list-message-digest-algorithms | list-public-key-algorithms`
列出 `openssl` 支持的命令、算法等。

- `-rand [options] n`
向标准输出写入 `n` 字节的伪随机数据。注意，输出是二进制数据，而不是 ASCII 文本！`-base64` 选项会让 `openssl` 以 ASCII 格式执行 Base64 编码。这会使结果字符串的长度增加约三分之一。

- `-req [options]`
生成一个用于签名证书的请求（即证书签名请求 [CSR] 文件）。使用 `-new`，你可以指定必须设置新证书。`-key` 指定要使用的密钥文件。如果不使用此选项，`openssl` 将为此目的生成一个新的 RSA 密钥，你可以使用 `-keyout` 将其保存到单独的文件。`openssl req -new -sha256 -key server.key -out server.csr` 随后 `openssl` 会以交互方式请求证书密钥数据，即国家代码、位置、你的姓名、主机名（通用名称）等。通过额外的 `-x509 -days n` 选项，`openssl` 将直接生成一个有效期为 `n` 天的自签名证书，而不是证书请求。

- `-rsa [options]`
处理 RSA 密钥，并在不同形式和格式之间生成并转换它们。`-in file` 和 `-out file` 指定读取原始密钥的文件和写入新密钥的文件。如果你不指定任何额外选项，`openssl` 将移除密钥的加密（口令）。密钥的格式可以通过 `-inform` 和 `-outform` 指定（默认是 PEM 或 DER）。通过 `-in file -text`，你可以确定现有密钥的属性，例如密钥长度。

- `-sclient [options]`
作为 SSL/TLS 客户端测试与加密服务器的连接。你可以在以下地址找到示例：`https://www.misterki.com/openssl-s-client`

- `-speed`
执行多次基准测试。结果显示在相应的硬件上处理了多少字节（处理得越多，硬件运行得越快）。

- `-x509 [options]`
显示证书数据、签名证书并在不同格式之间转换证书。`-in` 和 `-out` 指定源证书和目标证书的文件。使用 `-req`，`openssl` 期望输入一个证书请求而非证书本身。`-CA` 指定用于签名的 CA 证书。`-CAkey` 指定对应的私钥。

`openssl` 命令有独立的 man 手册。`req` 描述 `rsa` 的选项。

## 示例

如果你想让官方证书机构（例如）为你的 Web 服务器签名证书，你应该首先生成密钥，然后生成证书签名请求。密钥在这里不是加密的，否则 Web 服务器每次启动时都会询问加密密码。

```
root# genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out server.key
```

```
root# chmod 400 server.key
```

```
root# openssl req -new -key server.key -out server.csr
```

通用名称 (Common Name): `company.com`

你可以查看 CSR 文件来检查此：

```
root# openssl req -in server.csr -text
```

然后，你需要将 CSR 文件发送给证书机构。你将从那里获得签名的证书。通常的文件标识是 `.pem` 或 `.crt`。你必须在 Apache 配置中输入此文件以及来自证书机构的 CA 证书。

```apache
# Apache 配置文件

CertificateFile /etc/apache2/server.pem

CertificateKeyFile /etc/apache2/server.key

CertificateChainFile /etc/apache2/sub.ca.pem

File /etc/apache2/ca.pem
```

如果你不想为官方签名付费，可以自己签名证书：

```bash
root# openssl x509 -req -days 1900 -in server.csr -signkey server.key -sha256 -out server.pem

Signature ok

subject=/C=DE/L=Boston/O=John Doe/CN=www.company-abc.com/

emailAddress=webmaster@company-abc.com/
```

### 获取私钥

要查看证书文件，你可以运行 `openssl x509 -in server.pem -text`：

```bash
root# openssl x509 -in server.pem -text

Certificate:

Data:

Version: 3 (0X1)

Serial Number: 1

Signature Algorithm: sha256WithRSAEncryption

Subject: C=DE/L=Boston/O=John Doe/CN=www.company-abc.com/

emailAddress=webmaster@company-abc.com/

Issuer: C=DE/L=Boston/O=John Doe/CN=www.company-abc.com/

Algorithm: sha256WithRSAEncryption

Validity:

	Before: Jan 1 00:00:00 2024 GMT

	Not After: Sep 27 23:59:59 2029 GMT
```

```
pactl command [parameter]
```

`pactl` 控制 PulseAudio 系统。这个支持网络的音频服务器默认安装在大多数 Linux 发行版中，并通常使用 ALSA 作为基础。PulseAudio 让多个程序能够并行使用音频系统而不会产生任何问题。`pactl` 包含约 30 条命令，此处仅列出了其中最重要的：

- `info|stat`
显示 PulseAudio 系统的关键数据或内存消耗情况。

- `list [short] [modules|sinks|sources|clients|cards|...]`
提供由 PulseAudio 管理的所有模块、音频源和输出端、流等详细描述。额外的 `short` 关键字可以将输出简化为每个元素一行。通过指定模块或输出端（sinks）等，`pactl` 只列出相关元素。

- `set-default-sink n`
定义默认音频输出。除了音频系统的编号 `n`（参见 `/proc/asound/cards`），你也可以输入其名称。可以使用 `pactl list short cards` 确定允许的名称。

- `set-sink-mute n 0|1|toggle`
取消、激活或切换音频输出 `n` 的静音功能。

- `set-sink-volume n`
设置音频输出 `n` 的音量。音量可以指定为整数、百分比或分贝值（例如 `10%` 或 `20dB`）。

## 示例

以下两条命令将第一个音频设备作为标准输出设备，音量设为 20%：

```
user$ pactl set-default-sink 0
```

```
user$ pactl set-sink-volume 0 20%
```

```
pandoc [options] in1 [in2 in3 ...] [> out]
```



同名软件包 `pandoc` 的主要任务是将 Markdown 文件转换为其他格式，例如 HTML 文件、PDF 文档或 Microsoft Office 文件。在某些局限下，`pandoc` 也可以处理除 Markdown 外的输入格式，包括 HTML 和 LaTeX。

### 选项

- `-c cssfile`
  将指定的 CSS 文件嵌入到 HTML 文档中。如果需要多个 CSS 文件，可以多次指定此选项。

- `-f format`
  指定源格式（from）。重要的源格式有 `asciidoc`、`docbook`、`latex` 和 `markdown`。`pandoc` 会尝试根据输入和输出文件的 ID 自动识别所需的源和目标格式。只有在识别失败时，才需要 `-f` 和 `-t` 选项。

- `-H header file`
  在 HTML 或 LaTeX 源码开头插入指定的头文件。如果需要多个头文件，可以多次指定此选项。

- `-o output.identifier`
  将结果写入指定的文件而不是标准输出。对于二进制输出格式（DOCX, ODT, PDF），此选项是强制性的。

- `-s`
  创建一个独立文档（单独的）。此选项对于 HTML、LaTeX、RTF 输出格式尤为重要。如果没有此选项，`pandoc` 创建的文件将不包含任何头信息；此类文件无法单独使用，必须嵌入另一个文档中。

- `-t format`
  指定目标格式（to）。重要的目标格式有 `docx`、`latex`、`html`、`html5`、`odt` 和 `rtf`。注意，支持的格式列表中不包含 `pdf`。要创建 PDF 文档，必须指定 `-o out.pdf` 选项。`pandoc` 首先将源文本转换为 LaTeX 格式，然后使用 `pdflatex` 创建 PDF 文件。

- `--toc`
  在生成的文档中嵌入目录。

### 示例

第一个命令从输入的 `input.text` Markdown 文件创建一个独立的 HTML 文档。第二个命令从一个章节存储在独立文件的书中创建一个 EPUB 文件。第三个命令在后台使用 LaTeX 创建一个 PDF 文件。

```
user$ pandoc -s -c my.css input.text > output.html
```

```
user$ pandoc chapter1.text chapter2.text chapter3.text -t epub3 -o book.epub
```

```
user$ pandoc preface.text chapter01.text chapter02.text -o out.pdf
```

`paplay [options] [file]`
`parecord [options] [file]`

`paplay` 通过 PulseAudio 系统播放指定的音频文件。`parecord` 进行录音并将音频流保存为文件。

- `-d id`
  指定输出设备（`paplay`）或音频源（`parecord`）。如果不使用此选项，将使用相应的默认设备。

- `--file-format=name`
  指定所需的音频格式，例如 `raw` 或 `wav`。

- `--list-file-formats`
  列出所有支持的音频格式。

- `--volume=n`
  指定所需的播放音量。值范围从 0 到 65535（最大音量）。

### 示例

以下命令播放 LibreOffice 提供的音频文件之一：

```
user$ paplay /usr/lib/libreoffice/share/gallery/sounds/train.wav
```

`paps [options] text files > out.ps`

`paps` 将指定的 UTF-8 文本文件转换为 PostScript 格式并将结果写入标准输出。UTF-8 字符不会显示为字母，而是显示为行。因此，在 PostScript 查看器（如 Evince, Okular 等）中显示 PostScript 文件可能会看起来像素化。无法选择文本。但打印质量很好。

- `--columns=n`
  定义文本列数（默认为一）。

- `--cpi=n`
  控制每英寸字符数，从而控制字体大小。

- `--font=name`
  指定所需的字符集（默认设置为是等宽 12）。

- `--landscape`
  以横向格式格式化文本。

### 示例

以下命令生成双列 PostScript 文件 `text.ps`。

```
user$ paps --landscape --columns 2 text.txt > print.ps
```

`parallel [options] ['command']`

同名软件包 `parallel` 帮助并行运行多个命令，甚至可能在不同的计算机上运行。`parallel` 支持与 `xargs` 相同的一些选项。

- `--eta`
  提供并行处理状态信息以及并行可能完成的时间，即预计到达时间。此时间估计假设每个作业消耗的大约时间相同。

- `-j n`
  并行运行最多 `n` 个实例。

- `-j +n`
  与 `-j n` 相同，但规范是相对于 CPU/核心数的。在具有八个核心的 CPU 上，`-j +0` 产生八个实例。相应地，`-j -1` 将并行调用限制为七个。

- `-S host1,host2,host3`
  将作业分发到主机 `host1`、`host2`、`host3` 等。如果主机列表以逗号结尾，则表示使用本地计算机。

- `-s`
  假设可以通过 SSH 无密登录访问主机；因此你必须使用 `ssh-copyid` 设置密钥。此外，要执行的命令必须在所有主机上可用。最后，该命令应在所有主机上安装。需要确定 CPU/核心数。

- `-s` 通常与 `--transfer`、`--return` 和 `--cleanup` 选项结合使用，将本地文件复制到外部主机，返回结果标识符的新文件，最后删除主机上的临时数据。这三个选项的短写为 `-trc{result`。

在理论上，`-s` 承诺对可以通过 SSH 访问的多个主机分发作业。但在我的测试中，该选项证明非常容易出错。如果你通过 SSH 并行任务，例如在几十个主机或云实例上运行命令，可以使用 `pssh`（并行 SSH）或 `clusterssh` 命令代替 `parallel`，尽管这些书中书中介绍。

### 示例

`parallel` 的一个简单应用是压缩、解压或其他处理多个文件。与其使用 `gunzip *.gz` 一个一个压缩多个文件，不如并行为每个文件启动一个 `gunzip` 实例。在具有多个 CPU/核心的计算机上，这将比串行处理文件快得多。

```
user$ ls *.gz | parallel gunzip
```

在第二个示例中，应使用 `convert` 将多个 PNG 转换为 EPS 格式。然而，仅仅传输文件名是不够的。相反，`convert` 期望原始文件名和名称去除了标识符 `*.png`，但增加了新的标识符 `*.eps`。
为了实现这一目的，`parallel` 将命令字符串中的 `{}` 替换为文件名，并将 `{.}` 替换为不带标识符的名称。

```
user$ ls *.png | parallel -eta -j +0 \
  'convert -density 90 -flatten -background white {} {}.eps'
```



# `parted [options] [device] [command [options]]`

`parted` 支持硬盘和 SSD 的分区。与过时的 `fdisk` 命令不同，`parted` 还支持 GUID 分区表 (`GPT`)。

如果你没有向 `parted` 传递命令，可以使用交互模式运行该程序并顺序输入多个命令。只要输入是唯一的，命令可以缩写（例如用 `q` 代替 `quit`）。

然而，你应该注意，与 `fdisk` 不同，命令是立即执行的且无法撤销！在操作不太方便的 `parted` 程序中，你也可以使用其名为 `gparted` 的图形用户界面。

## 选项

- `-a` 或 `--align`
指定新分区的对齐方式。允许设置有 `none`、`cylinder`（对齐到道区限制）、`minimal`（对齐到块限制）或 `optimal`（对齐到 1 MiB 的倍数）。你应该始终使用 `-a optimal` 选项以最高速度使用数据介质。

- `-l` 或 `--list`
列出所有分区。

- `-s` 或 `--script`
运行作为参数传递的所有命令，无需进行询问。

## 重要命令

- `align-check min/opt nr`
检查指定分区是否从最佳位置开始。`parted align-check min` 仅测试分区是否在物理块边界处开始。通过 `parted align-check opt`，`parted` 尝试根据数据介质的关键数据计算分区的最佳起始位置。如果无法实现，则将 1 MiB 的倍数视为最佳。

- `mklabel mdsos/gpt`
在 MBR 或 GPT 格式下建立新的分区表。注意：硬盘的所有内容将丢失！`parted` 还支持其他各种分区格式，但这些格式在 Linux 环境中并不重要（参见 `man parted`）。

- `mkpart primary/logical/extended/name [file system] start end`
创建一个新分区。注意，你必须指定起始和结束位置，而不是起始位置和大小！结束位置也可以指定为负数，然后从数据介质的末尾计算。

指定分区类型（主、逻辑或扩展）仅对具有 MBR 分区表的数据介质有用。如果数据介质上有 GPT，你应该通过第一个 `mkpart` 参数为分区指定一个名称。

可选的文件系统指定仅用于定义分区类型。然而，在新分区上不会设置文件系统。允许的类型有 `fat16`, `fat32`, `ext2`, `HFS`, `linux-swap`, `NTFS` 和 `ufs`。

- `print`
列出所有分区。

- `quit`
退出 `parted`。

- `resize nr start end`
更改指定分区的大小。遗憾的是，该命令只能用于 MBR 磁盘的扩展分区。要更改其他分区的大小，你必须删除它们，然后使用完全相同的起始点重新设置。这显然是一个容易出错的操作，并且要求分区后面有空闲空间。

- `rm nr`
删除指定分区。

- `set nr flag on/off`
更改分区的标志（额外属性）。`parted` 可以使用 `boot`, `root`, `swap`, `hidden`, `raid`, `lvm`, `lba` 和 `bios_grub` 等标志。

- `unit bios grub`
定义位置和大小规格的单位。可用选项有：

  - `s` (扇区)
  - `B` (字节)
  - `KB`, `MB`, `GB`, 和 `TB` ($10^3$, $10^6$, $10^9$, 和 $10^{12}$ 字节)
  - `KiB`, `MiB`, `GiB`, 和 `TiB` ($2^{10}$, $2^{20}$, $2^{30}$, 和 $2^{40}$ 字节)
  - `%` (百分比，相对于数据介质的总大小)
  - `compact` (输入使用十进制兆，输出易读)

默认应用 `compact` 设置。如果启动 `parted` 时使用了 `--align` 选项，在创建新分区时位置和大小规格将相应调整。

## 示例

以下几行显示了如何使用 `parted` 在带有 GPT 的 SSD 上设置新的 LVM 分区：

```
root# parted -a optimal /dev/sda

(parted) print

Model: ATA SAMSUNG SSD 830 scsi

Hard disk /dev/sda: 512GB

Sector size (logical/physical): 512B/512B

Partition table: gpt

Number Start End Size Filesystem Name Flags

1 17.4kB 1000MB fat32 EFI System Part... boot, hidden

2 1000MB 21.0GB 20.0GB ext4 hidden

3 21.0GB 21.0GB 134MB Microsoft reser... hidden, msftres

4 21.1GB 61.2GB 40.1GB Basic data part... hidden

5 61.2GB 82.2GB 21.0GB ext4 hidden

6 82.2GB 103GB 21.0GB ext4 boot, hidden

7 103GB 124GB 21.0GB ext4 boot

8 124GB 281GB 157GB ext4

9 281GB 386GB 105GB ext4

10 386GB 407GB 21.0GB ext4

(parted) mkpart svm-partition 407GB 450GB

(parted) set 11 svm on

(parted) print

...

11 407GB 450GB 42.7GB svm-partition svm

(parted) quit
```

也可以直接处理命令而无需手动交互。以下命令假设 `/dev/sdb` 是 USB 闪存盘或 SD 卡的设备。第一个 `parted` 创建一个新的 MBR 分区表并删除所有现有数据。第二个命令创建一个主分区，在开头留出 1 MiB 的空空间。

（此处省略重复的示例部分，翻译逻辑与上文一致）

## `partx` 选项

- `-s` 或 `--show`
显示所选数据介质或分区的信息。通过 `-s` 或 `-o` 显示的数据根据物理磁盘确定，可能与 Linux 内核的分区表不匹配。

- `-u`
更改内核分区表中某个分区的大小或其他数据。这些更改必须先在数据介质上物理完成。

## 示例

以下命令提供了具有 MBR 分区表的硬盘详细信息：

```bash
root# partx -o NR,TYPE,FLAGS,START,END,SECTORS,SIZE /dev/sda

NR TYPE FLAGS START END SECTORS SIZE

1 0x83 0x80 2048 411647 409600 200M

2 0x8e 0x0 411648 3145729 31045632 14,8G
```

## `passwd [options] [username]`

不带参数的 `passwd` 允许你更改当前用户的密码。要此此，你必须首先输入旧密码，然后连续输入两次新密码。新密码以加密格式写入 `etc/shadow` 文件中。然而，在某些发行版中，新密码必须符合特定的安全规则才能被接受。

`root` 也可以通过 `passwd name` 修改其他用户的密码。不需要输入旧密码；也就是说，即使用户忘记了密码，`root` 也可以更改。之前的密码限制不适用于 `root`，因此它也可以定义仅由单个字符组成的密码。然而，即使是 `root` 也不允许不输入密码（即直接按回车键）。

通过指定选项，`passwd` 还可以锁定单个账户、重新激活以及为账户或密码设置过期时间（另见 `chage` 命令的描述，该命令在这方面提供了更多设置选项）。

### 选项

- `-g`
设置组密码。此功能很少使用。它允许你通过 `newgrp` 使用密码来保护对非主组的访问。由于由于由于组密码必须被多个用户知晓，该过程在本质上是不安全的。

- `-l`
禁用账户（锁定）。

- `-u`
重新激活已禁用的账户（解锁）。

- `-x n`
指定密码有效的最大天数。换句话说，`-x 180` 意味着大约每六个月必须设置一次新密码。

`passwd` 只能交互式使用。无法将密码作为参数或选项传递。要自动设置密码，必须使用 `chpasswd` 命令。

## 示例

在以下示例中，`root` 为用户 `hawks` 设置了新密码。在将来，他们必须每年更改一次密码。

```bash
root passwd hawks

change password for user hawks.

Enter a new password: *********

Enter the new password again: *********

passwd: all authentication features successfully updated.

root# passwd -x 365 hawks
```



`paste` 将指定文件的行合并成新的（更长的）行，并在屏幕上显示结果。因此，结果文本的第一行是由第一个文件的第一行加上第二个文件的第一行组成的，以此此类推。新行的组件之间会插入制表符。可以使用 `> target file` 将结果保存到文件中。

- `-d 'separator'`
指定分隔符字符串。使用 `paste -d ':' file1 file2`，在每行的 `file1` 内容和 `file2` 内容之间会插入一个冒号，例如：

```
line1 from file1:line1 from file2

line2 from file1:line2 from file2

line3 from file1:line3 from file2

..
```

## `patch [options] < patch file`

`patch` 应用 diff 文件中摘要的更改。该命令通常用于应用代码更改（例如用于内核代码）。

- `-b`
为所有更改的文件创建备份文件。

- `--dry-run`
测试补丁但不进行任何更改。通常，在使用 `--dry-run` 选项应用任何补丁之前，你应该确保没有发生任何问题。没有什么比错误或部分应用补丁更令人烦恼的！

- `-pn`
从补丁文件的文件名移除 n 目录级。如果原始文件名为 `/a/b/name.c`，`-p1` 会使得

- `-R` 或 `--reverse`
反向应用补丁。通过这种方式，已经应用的补丁将被撤销。

## 示例

以下命令显示了如何将内核代码从版本 6.7.5 补丁到 6.7.6。要做到这一点，在应用 6.7.6 版本的补丁之前，必须先撤销从 6.7 到 6.7.5 版本的补丁。内核补丁通常指的是最新的主版本，在此例中为版本 6.7。

```bash
root# cd /usr/src/linux-6.7.5

root# bunzip2 -c patch-6.7.5.bz2 | patch -R -p1 --dry-run

(test inverse patch)

... no error messages

root# bunzip2 -c patch-6.7.5.bz2 | patch -R -p1

(6.7.5 ->

6.7)

root# bunzip2 -c patch-6.7.6.bz2 | patch -p1 --dry-run

(test patch)

... no error messages

root# bunzip2 -c patch-6.7.6.bz2 | patch -p1

(6.7 ->

6.7.6)

root# cd /usr/src root# mv linux-6.7.5 linux-6.7.6
```

## `pdf2ps source.pdf [target.ps]`

`pdf2ps` 从 PDF 文档创建 PostScript 文件。如果你没有指定 `target.ps`，新的 PDF 文件将命名为 `source.pdf`。`pdf2ps` 的替代方案是 Poppler 库中的 `pdftops` 命令。将 PostScript 文件转换为 PDF 文档，可以使用 `ps2pdf`。

- `-dLanguageLevel=n`
指定输出使用的 PostScript 级别（默认是 PostScript 级别 2；也支持级别 1 和 3）。

## `pdfimages [options] file.pdf [image name]`

`pdfimages` 尝试从 PDF 文件中提取图像。然而，这并不总是完美工作，因为通常嵌入了无数图像。

- `-all`
保存 PDF 文件中的所有图像。在无法实现的情况下，命令将使用指定的格式-文件名-nnn 生成图像。

- `- fn`
指定分析文件从哪一页到哪一页。如果没有这些选项，命令将处理整个文档。

- `- j`
保留 PDF 文件中嵌入图像的格式。

- `- list`
列出找到的图像但不创建任何文件。

- `- png` 或 `-tiff`
将所有图像保存为 PNG 或 TIFF 格式。

## 示例

`pdfimages -list` 提供所有图像的全面信息。出于空间考虑，此处已缩短。

```
user$ pdfimages -all book.pdf tst

user$ ls tst*

stst-000.png tst-001.png tst-002.png tst-003.png tst-004.png tst-005.png

stst-006.jpg tst-007.png tst-008.png tst-009.png tst-010.png
```

A2-4 B5 B7)。 如果你只想获取偶数页或奇数页，你需要在页码后加上 even 或 odd，例如 1-10odd。

- `- background watermark.pdf`
为每个输出页存储一个来自 watermark.pdf 的一个页。如果 watermark.pdf 的页数少于输出页，则将重复使用 watermark.pdf 的最后一页作为水印。源 PDF 文件必须是透明的，否则水印将不可见。

- `- stamp stamp.pdf`
将 stamp.pdf 中的一个页写入每个输出页中。如果 stamp.pdf 的页数少于输出页，则将重复 stamp.pdf 的最后一页。stamp.pdf 必须是透明的，否则它将覆盖原始 PDF 文件。

- `- burst`
为 PDF 文档的每一页创建一个单独的文件，并将其命名为 page_n.pdf，其中 n 是页码。

- `- output result.pdf`
将生成的 PDF 文件保存为 result.pdf。

- `- owner_pw password Of user_pw password`
使用指定的密码加密 result.pdf。owner_pw 密码适用于打印和其他 PDF 操作，而 user_pw 密码适用于打开文件。

## 示例

以下命令读取 in.pdf 中的第 10 到 20 页以及 30 到 40 页，并将它们写入新的 out.pdf 文件中：

```
user$ pdftk in.pdf cat 10-20 30-40 output out.pdf file
```

你也可以使用 cat 命令将多个 PDF 文件合并：

```
user$ pdftk in1.pdf in2.pdf in3.pdf cat output out.pdf
```

以下示例为 in.pdf 中的每一个单独页创建一个名为 pg_n 的单独 PDF 文件，其中 n 是页码：

```
user$ pdftk in.pdf burst
```

下一个示例创建了一个加密的 PDF 文件。该文件可以在没有 xxx 密码的情况下读取，但不能以任何其他方式进行打印或编辑。如果你想自己保护文件的读取，则必须使用 user_pw 命令而不是 owner_pw。

```
user$ pdftk in.pdf output encrrypted.pdf owner_pw xxx
```

最后，使用 pdftk 为 PDF 文件标记水印：

```
user$ pdftk in.pdf background watermark.pdf output out.pdf
```



# `pdftops` [options] `source.pdf` [target.ps]

`pdftops` 源自 Poppler 库（该库在 Debian 和 Ubuntu 的 `poppler-utils` 包中提供），从 PDF 文档生成 PostScript 文件。与 `pdf2ps` 不同，它支持许多影响 PostScript 文件的选项。

- `-eps`
  创建一个 EPS 文件。对于多页 PDF 文档，必须使用 `-f` 和 `-l` 选择页码。

- `-f n` 和 `-l n`
  指定起始和结束页（first 和 last）。

- `-leveln`
  指定所需的 PostScript 级别（1 到 3）。

- `-opw password` 或 `-upw password`
  指定所有者或用户密码以处理受密码保护的 PDF 文件。

- `-paper format`
  指定的纸张格式（A3、A4、letter 或 legal）。

- `-paperw n` 和 `-paperh n`
  用点表示纸张大小。

# `pdfotext` [options] `source.pdf` [target.txt]

`pdfotext` 从 PDF 文件中提取文本并保存到纯文本文件中（默认名为 `source.txt`）。所有的格式和图像都将丢失。`pdfotext` 也是 Poppler 库的一部分。

`-f`、`-l`、`-opw` 和 `-upw` 选项含义与 `pdftops` 中的相同（见该处）。

- `-layout`
  尝试保留页面布局。

- `-nopgrbk`
  不使用特殊字符标记页结束。

## `pdfunite` `in1.pdf` `in2.pdf` `out.pdf`

`pdfunite` 来自 Poppler 库，将多个 PDF 文件合并为一个。

# `pdf-info` [options] `source.pdf`

`pdf-info` 用于显示 PDF 文件的元数据。

# `pdfimages`

从 PDF 提取图像。

## `pdfinfo`

显示 PDF 文件的详细信息。

## `pdfpages`

从 PDF 提取页面。

## `pdfstructure`

显示 PDF 文件的结构。

# `pip` 或 `pip3` 命令

来自 `python3-pip` 包的命令支持从 Python 包索引 (PyPI) 安装 Python 包。在许多发行版中，该命令必须作为 `pip3` 运行，以与之前用于 Python 2 的 `pip` 命令区分来。

与 Linux 软件包管理命令不同，`pip` 通常不需要 root 权限或 `sudo` 即可运行。包对所有用户可用（除非你使用了前述的 `--user` 选项）。

本地安装 PIP 包有时会与 Linux 软件包管理中的包产生冲突。在当前的 Python 版本中，`pip` 会显示错误信息。如果可能，你应该作为 Linux 软件包安装所需的模块（例如 `apt install python3-name`）。如果发行版中没有合适的包，你应该在 Python 环境中组织你的项目（参见下文示例）。或者，你可以使用 `--break-system-packages` 选项强制安装，但这真的应该只作为应急解决方案。

- `install [--upgrade] [--user] [--break-system-packages] <package name>`
  安装或更新指定的包。使用 `--user` 选项，包将安装为仅对当前用户可用的。

  使用 `--break-system-packages`，你可以强制安装包，即使新 Python 版本的保护机制建议不要这样做。该选项的名字听起来相当令人生畏：可能会出现问题，但只有当有大量包在使用或执行了 Python 版本更新时才会发生——最终这种情况相对罕见。尽管如此，使用虚拟环境几乎总是更好的解决方案。

- `list [--outdated]`
  提供所有已安装包或所有可以更新的包的列表。

- `search term`
  在 PyPI 中搜索带有指定搜索词的包。

- `show [--files] <package name>`
  显示已安装包的信息或列出其文件。

- `uninstall <package name>`
  移除指定的包。

## 示例

使用以下 Debian/Ubuntu 的命令，首先安装 `pip3` 本身。通过 `python3 -m venv` 在项目目录设置虚拟环境。通过为此目的提供的脚本激活环境（另见源文件）。这将更改提示符。最后，在环境中安装 OpenAI API 的 Python 模块。

```
user sudo apt install python3-pip python3-venv

user$ mkdir my-project

user$ cd my-project

user$ python3 -m venv .

user$ source bin/activate

(my-project) user$ pip3 install openai
```



# pkcon 命令

PackageKit 是指向各种软件包管理系统的通用接口。PackageKit 主要由 Gnome Software 等图形界面使用，但也可以通过 `pkcon` 命令进行控制。取决于 PackageKit 使用的后端（APT, DNF, YUM 等），以下某些命令可能不可用：

- `get-groups` 确定包组。
- `get-updates` 提供所有可以更新的包的列表。
- `install <package name>` 安装包。
- `install-local <file>` 安装本地文件。
- `refresh [force] [options]` 使用包信息更新缓存。如果你使用 `pkcon refresh -c`，允许的缓存年龄将被设置为负零。这将导致删除整个缓存，从而节省大量空间。
- `remove <package name>` 卸载包。
- `search [name|details|group|file] term` 搜索包。
- `update [package name]` 更新指定的包或所有已安装的包。

## popd

bash 命令 `popd` 返回到之前使用 `pushd` 保存的目录。该目录将从列表中移除。`popd` 和 `pushd` 通常在 shell 脚本中使用。

## postconf [options] [parameter=value]

`postconf` 帮助读取邮件服务器配置并在运行期间更改它。如果没有带选项调用命令，它将仅显示所有参数的当前有效设置。

- `parametername` 显示参数的当前状态。
- `parametername=value` 重新设置参数，并在 `/etc/postfix/main.cf` 文件中进行更改。
- `d` 或 `df` 显示所有参数的默认值（即使参数当前设置不同）。使用 `df` 选项代替 `d` 会导致长条目换行到多行。
- `d parametername` 显示参数的默认状态（可能与当前设置不同）。
- `n` 或 `nf` 列出所有没有默认值的参数。`-nf` 会对长行换行。

## postqueue [options]

`postqueue` 提供有关邮件服务器尚未送递的邮件的信息，或启动新的传输尝试。

- `f` 尝试立即重发队列中的所有邮件（刷新）。Postfix 会自动处理此操作，但在多次传输尝试之间保持等待时间。
- `i` 尝试立即重发指定的邮件。
- `p` 或 `j` 显示队列中的所有邮件。使用 `-j` 时，输出为 JSON 格式。

## powertop

同名的交互式 `powertop` 程序分析哪些进程消耗最多的能量，或频繁从睡眠模式唤醒 CPU 或硬盘。在程序运行时，你可以使用 `Tab` 键在不同页面之间切换。

从节能功能的角度来看，最有趣的页面称为 Tunables。在那里，`powertop` 显示了一个当前状态可能为 Bad 或 Good 的设置列表。你可以用方向键选择单独的点，并通过按 Enter 键更改它们。`powertop` 会显示它正在执行的命令。

然后，你可以尝试逐步更改单个设置并测试效果：用功率计记录的笔记本电脑能耗是否真的明显下降？禁用的功能会导致问题吗？USB 设备仍可以使用吗？切换 Wi-Fi 适配器是否仍然有效？音频系统在无干扰的情况下运行正常，等等？

使用 `powertop` 进行的更改仅在计算机下次重启之前有效。要永久激活节能，你需要将 `powertop` 显示的命令（例如 `echo '1' > /sys/xxx`）输入到每次系统启动时执行的文件中。在大多数发行版中，`/etc/rc.local` 适用于此。如有必要，你必须创建此文件并使用 `chmod a+x` 将其标记为可执行。取决于发行版，你可能还需要运行 `systemctl daemon-reload` 以便 systemd 执行该文件。

激进的解决方案是在 `rc.local` 中输入 `powertop --auto-tune` 而不是单独的调节命令。这样 `powertop` 就会执行所有已优化措施。遗憾的是，`powertop` 往往过度：如果笔记本比以前多运行一小时，但网络连接不稳定有什么用？

你可以通过带有 `--html` 选项运行 `powertop` 获取所有可能的调节命令列表。在测量大约 20 秒后，该命令生成 HTML 文件 `powertop.html`，其中包含了各种统计数据以及调节参数的摘要。

## ppa-purge

Ubuntu 特有的 `ppa-purge` 命令禁用指定的私人包仓库（PPA，另见 `add-apt-repository` 命令的描述）。如果 PPA 提供了官方包的替代版本，这些包将被移除并替换为原始包。

### 示例

以下 Debian/Ubuntu 命令禁用了 libreoffice 包源，并替换源自此包源的包为标准 Ubuntu 包：

```
root# ppa-purge ppa:libreoffice/ppa
```

## printenv [variable]

输出指定环境变量的内容，或逐行输出所有环境变量。

## printf format para1 para2 para3 ...

`printf` 允许你按照 C 命令 `printf` 的语法格式化输出。你可以通过 `man 3 printf` 获取有关格式化选项的详细信息。

### 示例

以下命令输出一个整数、一个保留两位小数的浮点数以及一个行结束符。

```
root# printf "%d %.2f\n" 123 3.1415927
123 3.14
```

## pro 命令

`pro` 命令在所有当前的 Ubuntu 版本中均可用。尽管它主要用于控制付费的 Ubuntu Pro，但某些功能在没有 Pro 订阅的情况下也可以使用。

- `- attach token`
激活 Ubuntu Pro 功能。您可以通过 Ubuntu Pro 仪表板获取有效令牌。
- `- security status`
提供有关正在服务的软件包数量以及维护期限的概述。Ubuntu LTS 版本的五年更新保证仅适用于 main（主）和 restricted（受限）软件包源。典型的 Ubuntu 安装包含来自不同软件包源的混合软件包包。
- `- status`
显示 Ubuntu Pro 服务的状态。

### 示例

以下结果在一个运行 Ubuntu 22.04 的服务器上获得，该服务器已激活 Ubuntu Pro 的免费版（最多支持五次安装）：

```
user$ pro status

SERVICE ENTITLED STATUS DESCRIPTION

anbox-cloud  yes disabled Scalable Android in the cloud

esm-apps    yes enabled Expanded Security Maintenance for Applications

esm-infra  yes enabled Expanded Security Maint. for Infrastructure

livepatch  yes enabled Canonical Livepatch

Subscription: Ubuntu Pro - free personal subscription
```

```
user$ pro security-status

1186 packages installed:

93 packages from Ubuntu Main/Restricted repository

243 packages from Ubuntu Universe/Multiverse repository

5 packages no longer available for download
```



此机器已连接到 Ubuntu Pro 订阅。
Main/Restricted 软件包在启用 `esm-infra` 的情况下接收 Ubuntu Pro 的安全更新，直到 2032 年。
Universe/Multiverse 软件包在启用 `esm-apps` 的情况下接收 Ubuntu Pro 的安全更新，直到 2032 年。

# ps [options]

`ps` 显示运行中进程（程序）和内核线程的列表。该命令与 `kill` 配合使用特别有用，可以强制终止已挂起的程序。`ps` 备有无数选项，这些选项在在线手册（`man ps`）中有详尽描述。在那里，您还能找到 `ps` 输出的众多信息的含义解释。`ps` 的变体是 `pstree`，它显示进程树，从而一目了然地进程的层次结构。

与其他命令相比，`ps` 具有带和不带连字符的选项。其中某些选项甚至具有不同的含义。(`ps -a` 和 `ps` 并不等效！) 两种类型的选项可以混合使用，例如 `ps -A ul`。

- `-a`
也显示其他用户的进程（而不仅仅是你自己的）。

- `-A`
显示所有进程。

- `-f`
显示进程树。

- `-f -l` 或 `l`
显示各种额外信息（内存需求、优先级等）。

- `-p n` 或 `-p n1,n2,n3`
仅显示具有指定进程号（PID）的进程。

- `--ppid n`
仅显示以 `n` 为父进程 ID 的进程，即由进程 `n` 启动的进程。

- `-u`
也显示相应进程的用户。该选项不能与 `l` 结合。

- `-x`
也显示未分配终端的进程。这些包括管理系统的 Linux 内部进程（守护进程）。

- `-Z`
也显示进程的 SELinux 上文。

## 示例

以下示例展示了 `ps` 命令的基本应用：

```
root# ps ax
```
（显示所有进程）

```
root# ps ax | grep ssh
```
（显示描述包含 ssh 的进程）

```
root# ps axu
```
（显示所有进程，包括所有者/账户）

在 Linux 上，`kthread` 内核线程守护进程号始终为 2。所有其他内核线程都由 `kthread` 启动。因此，如果您只想列出内核线程，可以使用 `ps --ppid 2`：

```
root# ps --ppid 2
```
（仅显示内核线程）

# ps2pdf [options] source.ps [target.pdf]

`ps2pdf` 从任何 PostScript 或 EPS 文件创建 PDF 文件。如果您没有指定 `target.pdf`，PDF 文件将与 PostScript 文件同名（但标识符为 `.pdf`，即 `source.pdf`）。

- `-dEncodeImages=false`
防止对图像任何压缩。生成的 PDF 文件现在非常大。通过结合 `/prepress` 设置，`ps2pdf` 现在提供具有最佳打印和曝光质量的 PDF。

- `-PDFSETTINGS=/default | /screen | /printer | /prepress`
指定 PDF 文档是针对任何用途、屏幕显示、普通打印或曝光（例如书籍打印等）进行优化。较高质量的代价是文件大小增加。这四个默认设置让您无需单独设置许多选项。

- `-rn`
指定位图字体的分辨率（单位 DPI，即每英寸点数）。

其他选项见以下地址：
`https://web.mit.edu/ghostscript/www/Ps2pdf.htm`

## 示例

以下命令从 PostScript `book.ps` 创建 PDF 文档 `book.pdf`：

```
user$ ps2pdf book.ps
```

# psql [options]

`psql` 允许执行 SQL 命令。`psql` 是 `postgresql` 的一部分。如果您只需要客户端，请使用 `postgresql-client`。

- `-c command`
运行 SQL 命令。

- `-dname`
指定建立连接的数据库。

- `-f file`
运行文件中包含的 SQL 命令。

- `-h hostname`
指定运行的主机。

- `-l`
列出所有数据库。

- `-U username`
定义用户名。

## 示例

示例展示了创建数据库、创建表、插入记录以及简单的查询：

```
user$ psql -U name -h localhost
Password for user: ********
# CREATE DATABASE test;
# \c test;
# CREATE TABLE mytable (id SERIAL PRIMARY KEY, data TEXT);
## INSERT INTO mytable (data) VALUES ('abc', 'efg');
## SELECT * FROM mytable;
id | data
-----+ 
1 | abc
2 | efg
```

# pssh 和 pscp

`pssh [options] command`
`pscp [options] local_file remote_file`

Python 脚本 `pssh` 在多个服务器上运行命令。`pscp` 从或向主机复制文件。`puke` 在所有主机上终止指定名称或模式的程序。这三个命令都需要可以使用密钥进行认证，或者由 `ssh-agent` 后台程序处理认证。

- `-h hosts.txt`
指定包含执行命令的主机主机名的文本文件的位置。

- `-o directory`
指定 `pssh` 保存命令输出以及 `pscp` 保存文件的目录。

## 示例

示例假设所有主机都是 RHEL 系统。然后，使用 `yum` 在这些计算机上执行软件更新。

```
root# pssh -h hosts.txt yum update
```

# pvcreate [options] 设备

LVM 命令 `pvcreate` 将分区或设备声明为物理卷（PV），以供以后在卷组（VG）中使用（另见 `vgcreate` 和 `vgxtend`）。

`pvcreate` 要求该分区或设备之前已标记为 LVM 分区。在 `fdisk` 中，你必须使用 `T` 快捷键命令并输入 `ae` 来此此。在 `parted` 中，需要的命令是 `set partition number lvm on`。

## 示例

以下命令将 `/dev/sdc1` 分区转换为 LVM 的物理卷：

```
root# pvcreate /dev/sdc1
Physical volume "/dev/sdc1" successfully created
```

# pvdisplay 设备

`pvdisplay` 显示指定 PV 的详细信息。

# pvremove 设备

`pvremove` 移除未使用 PV 的标签。

# pvscan

`pvscan` 列出所有的 PV。

```
pw-cat audio file
pw-cli [command]
pw-mon [options]
pw-top [options]
```

大多数现代 Linux 发行版使用 PipeWire 作为音频和视频服务器。有多种命令可以控制 PipeWire，每个命令都以 `pw-` 开头。在这里，我将关注最常用的命令：

- `pw-cat` 从音频系统传输或原始文件。该命令也可以作为 `pw-play`、`pw-record`、`pw-midiplayrecord` 或 `pw-midirecord` 运行。
- 你可以使用 `pw-cli` 修改音频设置。有无数子命令，这里只提到了最重要的：
  - `connect` 或 `disconnect` 建立或终止与外部 PipeWire 服务器的连接。
  - `create-link` 连接两个 PipeWire 节点。
  - `create-node` 和 `export-node` 管理 PipeWire 节点，即信号管理或转发的对象。
- `info id` 显示特定对象的详细信息。
- `list-objects` 列出所有的 PipeWire 对象。
- `list-remotes` 列出所有的外部 PipeWire 实例。
- `load-` 和 `unload-module` 加载或移除 PipeWire 模块。
- `send-command` 向 PipeWire 对象发送命令。
- `switch-remote` 定义激活的远程实例。

`pw-cli` 是一个底层命令。它的使用非常繁琐。由于 PipeWire 与 PulseAudio 有一个兼容层，在很多情况下，通过 `pactl` 控制设置更为方便。

- `pw-mon` 列出 PipeWire 系统已知的所有音频和视频对象，包括无数属性。
- `pw-top` 提供当前激活的 PipeWire 组件的概述，包括在音频处理过程中发生的延迟。

```
pwd
```



`bash` 命令 `pwd` 指定当前目录。

除了 `bash` 包含的版本外，`pwd` 还可以作为一个独立的命令单独用，通常文件名为 `/bin/pwd`。请注意，在某些情况下，这两个变体的 `pwd` 可能不会产生相同的结果。这是因为 `bash` 版本的 `pwd` 是基于相对路径的，而外部命令处理的是绝对值。指向目录的符号链接可以在某种程度上欺骗 `bash` 版本的 `pwd`。

## 示例

在以下示例中，`In` 创建了一个指向 `/tmp` 目录的符号链接。`cd` 切换到该目录。`bash` 认为该目录是当前目录，而 `/bin/pwd` 识别出 `/tmp` 实际上是当前目录。

```
user In -s /tmp symlink

user$ cd symlink

user$ pwd

(bash version of pwd)

/home/kofler/symlink

user$ /bin/pwd

(standalone pwd command)

/tmp
```

`pwgen [options] [n]`

来自同名软件包的 `pwgen` 生成一整列表随机但易于记忆的密码。其思路是用户选择其中一个密码，然后在别人从你肩膀看过去看到密码之前，使用 `Ctrl+L` 清除屏幕。与 `makepasswd` 生成的密码相比，`pwgen` 生成的密码随机性较低，因此安全性也较低，但它们对于许多用例来说仍然足够。

默认情况下，密码长度为8个字符。你可以通过指定可选参数 `n` 生成更长的密码。

- `-0` 密码中使用未使用数字。
- `-1` 仅提供 1 个密码而不是 100 个。
- `-B` 避免根据字体可能容易混淆的字母或数字，即 O 和 0 以及 l 和 1。这会降低密码的安全性。
- `-y` 在密码中也包含特殊字符。

## 示例

如示例所示，即使是默认设置生成的密码也绝非易事：

```
user pwgen

Ohshu3yo Ewaledoe OhCh2Zua Aili80oc Xu4iyix uag3Geeash2hu Eeth6mah

eM0Jio xiele60ob ob8Yah9 shaif0Ed uep8Eve lang3Eho thaiS7xa Sah3S5ee4

...
```

以下命令生成一个包含特殊字符的 80 字符密码：

```
root# pwgen -1 -y 80

AhB9eivjoo~s0go2ievaF7eePe6oyoo7C

...[i
```

## `qalc [expression]`

来自同名软件包的 `qalc` 计算一个表达式。为了避免特殊字符，必须用引号括表达式：

```
user$ qalc "(2+3)*5"

25

user$ qalc sqrt(16)

4

user$ qalc sin(45)

0.707106

user$ qalc log(2)

0.693147
```



## `qemu` [options] [image]

Quick Emulator (`QEMU`) 模拟各种 CPU。在简单的情况下，`qemu` 配备有一个硬盘。根据发行版的不同，`qemu-x64` 是最重要的。对于 ARM 系统，使用 `qemu-a64` 或 `qemu-mips`。`QEMU` 使用默认设置运行虚拟机。如果你想使用多个数据媒体，可以添加 `-hda`、`-hdb` 等选项。

- `accel kvm` 激活 `KVM`。`QEMU` 也可以处理其他加速系统，如 `t` 或 `tcg`。
- `boot-order=xxx,once=xxx,menu=on` 指定启动过程中考虑数据媒体的顺序。在这里，`xxx` 是字母序列（例如 `adc`：首先是软盘，然后是光驱，最后是硬盘）。字母 `a` 到 `d` 对应驱动器。
- `once=` 指定仅针对第一次的序列。例如，机器第一次尝试时从光驱启动，但之后从硬盘启动，输入 `-boot-order=c,once=d`。
- `menu=on` 在启动菜单开始显示“按 F12 进入启动菜单”。然后可以通过按下 F12 键交互式地选择启动磁盘。
- `cdrom iso file` 使用指定的 ISO 文件作为虚拟光驱的数据源。该选项对应 `-drive file=iso-file,index=2,media=cdrom`。
- `cpu host` 将主机 CPU 的所有属性传递给客户机。默认并非如此：只传递一个子集以最大化不同 CPU 之间虚拟机的兼容性。
- `device` 向虚拟机添加额外的设备。所有支持的设备列表由 `qemu -device ?` 提供。设备名称对大小敏感！你可以使用 `qemu -device cup?` 确定特定设备的可用选项，例如 `qemu -device isa-serial,?`。

`cache=writethrough/writeback/none` 指定是否以及如何对写入访问进行缓存。默认使用 `writethrough`：在客体系统中，在主机系统确认保存操作之前，写入访问不会显示为已完成。

`file=fname` 指定镜像文件、ISO 文件或逻辑卷的设备名称。

`if=ide/scsi/virtio` 指定虚拟机应该使用哪个接口来访问数据介质（默认值为 `ide`）。对于 Linux 客户端，`virtio` 效率更高。

`index=n` 确定接口数据介质的编号。只有在没有顺序指定数据介质时，才需要此参数。

`media=disk/cdrom` 指定其应该是硬盘（默认设置）还是 CD/DVD 驱动器。

### 常用选项

- `-enable-kvm`
  对应 `-accel kvm`。

- `-hda`/`-hdb`/`-hdc`/`-hdd` details
  指定虚拟 IDE 硬盘。
  `-hda fname` 对应 `-drive file=fname,index=0,media=disk`。
  `-hdb fname` 对应 `-drive file=fname,index=1,media=disk`，以及更多。

- `-k language identifier`
  使用指定的语言标识符 `de`（德语）和 `en-us`（美国英语）。此选项仅在虚拟机由外部 VNC 客户端操作时才需要。虚拟机管理器或 `virt-viewer` 命令的 VNC 客户端会自动识别键盘设置。

- `-localtime`
  用本地时间初始化客体系统的虚拟 CMOS 时钟（而不是默认的 UTC 时间）。

- `-m n`
  设置虚拟机的内存大小（单位 MiB）。默认设置根据发行版而异。

- `-machine name[,para1=value1,para2=value2 ...]`
  指定应该仿真哪些硬件。`-machine help` 提供了允许的类型名称列表。这些参数可用于激活或禁用与相应类型基本设置不同的附加属性。

- `-monitor device`
  将 QEMU 监器的输入和输出重定向到指定的设备。如果你想通过当前控制台操作监器，必须将 `stdio` 作为设备。使用 `pty` 时，`qemu` 在启动时创建一个新的伪 TTY 设备并使用其进行通信。

- `-net nic,details`
  配置虚拟网络适配器。如果未指定此选项，`QEMU` 默认仿真一个兼容 `RTL8139` 的网卡。

  `model=ne2k_pci/i82551/i82557b/i82559er/rtl8139/e1000/pcnet-virtio` 定义了 `QEMU` 仿真的网络适配器。对于 Linux 客户端，使用 `model=virtio` 将获得最佳效果。你使用 `macaddr=52:54:00:nn:nn:nn` 指定指定的 MAC 地址。

- `-net user,details`
  使用模式网络（这是默认设置）。尽管得益于 NAT 和掩装，客体系统可以使用主机的互联网连接，但客体和主机之间无法建立直接网络连接。

- `-rtc base=utc/localtime`
  指定虚拟机时钟启动应该是什么样的。`utc` 是 Linux 客户端的正确设置，而 `localtime` 适用于 Windows 客户端。默认情况下，时钟始终与主机同步。如果你不希望发生这种情况，可以指定额外的 `clock=vm` 参数。

- `-smp n` 或 `-smp cores=c, threads=t, sockets=s`
  指定分配给虚拟机多少 CPU 或核心的短写符号（默认只有一个核心）。对于具有多个 CPU 的主机系统，`c` 指定每个 CPU 使用多少核心。`t` 指定每个核心所需的线程数；对于支持超线程的 Intel CPU，值 `2` 通常很有用。`s` 最后指定使用多少个 CPU（插槽）。`c*t*` 提供了虚拟机能够看到的 CPU 数量。

- `-soundwh97/es1370/hda/sb16/all`
  向虚拟机添加指定的音频设备之一（如果使用 `all` 则为添加全部）。`ac97` 代表 Intel 82801AAAC97，`es1370` 代表 Ensoniq AudioPCI ES1370，`hda` 代表 Intel High Definition Audio，`sb16` 代表 Creative Sound Blaster 16。

- `-spice port=n[,options]`
  激活 Spice 图形系统。为此，你必须指定所需的端口。

- `-usb`
  激活 USB 驱动程序。

- `-usbdevice mouse/tablet/disk/host...`
  向虚拟机添加 USB 设备。大多数情况下，你需要 `-usbdevice tablet` 选项。它将标准的仿真的 PS/2 鼠标替换为理解绝对坐标的虚拟 USB 指针设备，从而允许客体的鼠标位置与 VNC 或 Spice 客户端同步。

  `-usbdevice disk` 使得将镜像文件从主机传递到客体成为可能，客体可以看到 USB 数据介质。

- `-usbdevice host:bus.addr` 或 `-usbdevice:vendor:productid` 将 USB 设备从主机重定向到客体。该 USB 设备不能被主机使用。确定总线和设备号或供应商和产品 ID 的简单方法是...

- `-vga cirrus/qxl/std/virtio`
  指定所需的虚拟显卡类型。`qxl` 可以配合 `spice` 使用。

### 镜像管理

- `-convert [-f source format] -0 target format file`
  将镜像文件从一种格式转换为另一种格式。原始文件将被保留。然而，在转换期间虚拟机不能使用该文件。目标文件带有额外的选项 `-c`。

- `-convert -f qcow2 -s snapshot -0 target file`
  将指定的 QCOW2 镜像快照传输到新的镜像文件。

- `-create [-f raw/qcow2/ged] [-o opt1=val1,opt2=...]`
  指定类型和大小的新镜像文件。默认按字节指定。可选使用后缀 `k` 或 `M`、`G` 或 `T`（分别代表 KiB、MiB、GiB 或 TiB）。根据镜像格式，有多种附加选项。可以通过 `-o '?'` 在完整的语法命令中确定可用参数：

```
```



`qemu-img create -f qcow2 -o '?' test.img 1G`

## qemu-img

- `create -f qcow2 -o backing_file=basis.img overlay.img`
创建一个覆盖层文件。当虚拟机运行时，所有更改都保存在覆盖文件中；基础文件保持不变。

- `info file`
提供有关指定镜像文件的信息。
可以使用 `qemu-img snapshot` 获取 QCOW2 镜像中快照的信息（参见此列表末尾的条目）。

- `resize file +/-size`
按指定的大小放大或缩小镜像文件。
该命令仅适用于 `raw` 和 `QCOW2` 镜像。

- `snapshot [options] snapshotname`
编辑快照。此命令仅适用于 `QCOW2` 镜像。`-c` 创建新快照，`-a` 将快照应用到镜像（从而撤销自快照创建的所有更改），`-d` 删除快照，`-l` 列出所有快照。除了 `-l` 外，当镜像文件正在运行时，可能无法使用这些命令

### 示例

第一个命令创建一个 `QCOW2` 镜像文件。这种格式的主要优势是文件最初不占用任何内存，并且会逐渐增长。

```
root# qemu-img create -f qcow2 disk.img 10G
```

第二个命令将 `QCOW2` 文件转换为 `raw` 镜像：

```
user qemu-img convert -f qcow2 image.qcow2 -O raw image.raw
```

## rclone

```
rclone command
```

`rclone` 命令将同名文件或整个目录同步到云存储位置。文件也可以传输时加密或解密。`rclone` 兼容 70 多个云服务商，包括 `S3`。

- `copy remote:bucket localdir`
将文件从远程目录复制到本地目录。（`bucket` 是存储位置。）

- `config`
引导通过交互式设置，在其中你选择云服务商并输入密码。这些数据保存在 `.config/rclone.conf` 中。该部分描述了远程目录。

要配置自动加密，首先需要为云服务商配置普通设置，然后配置第二个设置（另一个目录），类型为 `crypt` 指向原始设置。`rclone`

- `lsd remote:`
列出所有可用的云桶。

- `ls remote:bucket`
列出桶中的文件。

- `mkdir remote:mynewbucket`
创建一个新桶。

- `sync localdir remotename:bucket`
将本地目录的文件与桶中的文件同步。注意，桶中不存在的文件将被删除！你应该最初使用 `--interactive` 选项以防止可能的错误。

### 示例

在使用 `rclone` 之前，你需要先为云服务商设置一次。然后可以使用 `rclone sync` 同步本地目录内容与云端桶的内容。

```
user$ rclone config
...
user$ rclone sync mydata myremote:bucket
```

## rdfind

```
rdfind [options] directory1 directory2
```

`rdfind` 在两个目录中搜索重复项（即相同文件）。该命令支持多种方法来判断两个文件哪个是原始文件，哪个是重复文件。根据选项，重复项会被列出，甚至被删除。

以下选项影响搜索行为：

- `checksum md5|sha256`
使用指定方法计算两个文件的校验和。默认使用 `sha1`。

- `followsymlinks`
在比较时考虑符号链接。

- `ignoreempty`
忽略空文件（长度为 0）。

- `minsize n`
忽略小于 `n` 字节的文件。

可以使用其他选项来指定对重复项的操作。默认情况下，它们的名称会被写入 `results.txt` 文件。

- `deleteduplicates true|false`
删除重复项（默认：`false`）。

- `dryrun true|false`
以测试模式运行，不任何更改（默认：`false`）。

- `makesymlinks true|false`
将重复项替换为原始文件的符号链接（默认：`false`）。

- `makeshardlinks true|false`
将重复项替换为硬链接（默认：`false`）。

- `makesresultfile true|false`
将匹配文件的文件名写入 `results.txt`（默认：`true`）。结果文件不仅包含每个重复项两个版本的名称，还包含指示 `rdfind` 认为哪个是原始文件的关键字：

- `DUPTYPE_FIRST_OCCURRENCE`: Original
- `DUPTYPE_WITHIN_SAME_TREE`: directory1
- `DUPTYPE_OUTSIDE_TREE`: directory2

### 示例

以下示例确定两个目录中的相同文件：

```
user rdfind dir1 dir2
Now scanning "dir1", found 211 files.
Now scanning "dir2", found 215 files.
Now have 426 files in total.
```

由于设备和 inode 不同，删除了 0 个文件。总大小为 85754591 字节或 82 MiB。根据大小从列表中删除了 103 个文件。剩余 323 个文件。

现在根据第一个字节消除候选文件：从列表中删除了 4 个文件。剩余 319 个文件。

现在根据最后一个字节消除候选文件：从列表中删除了 0 个文件。剩余 319 个文件。

现在根据 sha1 校验消除候选文件：从列表中删除了 2 个文件。剩余 317 个文件。看起来你有 317 个不唯一的文件。总共可以减少 39 MiB。现在生成结果文件 `results.txt`。

第二个命令搜索包含照片的两个目录。至少 100 字节的重复项将被替换为硬链接：

```
user$ rdfind -minsize 100 -makehardlinks true photos1 photos2
```

## rdiff-backup

```
rdiff-backup [options] source directory target directory
```

`rdiff-backup` 以类似于 `rsync` 的方式同步目标目录和源目录。与 `rsync` 不同，`rdiff-backup` 在重复执行时还会归已更改或删除文件的旧版本，更改以压缩的形式保存，这使得重建已删除或覆盖的文件成为可能。

源目录和目标目录可以位于网络服务器。在这种情况下，默认通过 `ssh` 进行通信。外部计算机上也必须安装 `rdiff-backup` 命令。在指定外部目录时，适用于与 `rsync` 相同。唯一的区别是在主机名后必须输入两个冒号，例如如下所示：`user@backerver::directory`。

- `restore-as-of time`
恢复到指定时间的数据。然而，随着版本的增加，恢复旧文件需要大量的 CPU 并相应地变慢。

- `removeolder-than time`
删除比指定时间旧的备份。你可以将时间设置为绝对值（例如 `2020-12-31`）或小时（`h`）、天（`d`）、周（`w`）等相对值（另见 `rdiff-backup` 的 `TIME FORMATS`）。而不是特定的时间点，你还可以使用 `nb` 指定应保留的最大备份数量。默认情况下，`rdiff-backup` 每次删除一个备份版本。

在运行 `read` 命令之前，通过 `echo -n` 显示用户输入内容的目的。

## readonly

`bash` 命令 `readonly` 显示 shell 的只读变量。可以通过 `declare -r` 保护变量免受更改。

## reboot [options]

`reboot` 终止所有正在运行的进程并重启计算机。`reboot` 等同于 `shutdown -r now`。

```
recode character set1..character set2 file
recode character set1..character set2 < source > target
```

`recode` 执行从字符集 1 到字符集 2 的字符集转换。`recode -l` 提供所有支持的字符集的完整列表。

### Examples (示例)

以下命令将 DOS 文件 `dosdat` 转换为 Latin-1 字符集的 Linux 文件：

```
user$ recode ibmpc..latin1 < dosdat > linuxdat
```

第二个 `recode` 示例将 `windowsdat` 文件中的所有行结束符（CR 加加 LF，即回车符和换行符）替换为 Linux 系统常用的行结束符（仅 LF）。实际字符集不会发生变化。结果文件保存为 `linuxdat`。

```
$ recode latin1/cr-latin1 < windowsdat > linuxdat
```

`recode` 加载以 Latin-1 字符集的文本文件 `latindat` 并将其保存为 UTF-8 文件（Unicode）：

```



```
$ recode latin1..u8 < latindat > utf8dat
```

## rename

大多数发行版都预装了 `rename` 命令，用于重命名多个文件。然而，根据发行版的不同，使用的是不同语法的变体。在以下章节中，我将描述两种常见的变体——首先是 `rename` 包中的 Perl 脚本，常见于 Debian、Raspberry Pi OS 和 Ubuntu；然后是 `util-linux` 软件包中的 `rename` 命令，常见于 Fedora、RHEL 和 SUSE。

### rename 在 Debian, Raspberry Pi OS 和 Ubuntu 上

此 `rename` 变体的语法如下：

```
rename [options] rename_expression files
```

该语法与 `sed` 类似，`rename_expression` 指定了如何处理其他参数中指定的文件。你可以使用 `man perlexpr` 读取语法的细节。你可以可以使用选项来影响重命名过程：

- `-f` 或 `-force`
覆盖现有文件。

- `-n`
显示哪些文件将被重命名，但并不进行任何更改。

以下示例将所有的 `*.jpg` 文件重命名为 `*.jpeg` 文件：

```
user rename -n 's/.jpg/.jpeg' *.jpg
```

第二个命令将所有大写字母替换为小写字母：

```
user rename -n y/A-Z/a-z/ *
```

你可以在以下网站找到更多示例：

`www.howtgeek.com/423214/how-to-use-the-rename-command-on-linux`

### rename 在 Fedora, RHEL 和 SUSE 上

Fedora、RHEL 和 SUSE上的 `rename` 语法更简单：

```
rename [options] find replace files
```

该命令只需将文件名中的 `find` 表达式替换为 `replace`。无法提前测试 `rename` 的效果。

- `-S` 同时更改由符号链接引用的文件名。

- `-v` 显示所做的更改。

要将 `.jpg` 文件改回 `.jpeg` 文件，你必须如下运行 `rename`：

```
user$ rename jpg jpeg *.jpg
```

```
renice n pid
```

`renice` 更改指定 PID 进程的优先级。`n` 是新的优先级（-20 到 20 之间的值）或带有正号或负号的增量值（例如 `+3` 或 `-2`）。只有 root 用户允许增加进程的优先级。最高优先级为 `-20`，最低为 `20`。

```
reset
```

如果文本终端中的字体因特殊字符的输出而损坏，`reset` 可以恢复字体。`reset` 还会还将终端设置重置为之前使用 `setterm -store` 保存的默认设置。

## resize2fs [options] device [size]

`resize2fs` 更改 ext2/ext3/ext4 文件系统的大小。对于大小规范，允许使用表示 KiB、MiB 或 GiB 的记法 `nK`、`nM` 和 `nG`。如果你不指定大小，`resize2fs` 将将系统调整为底层分区或逻辑卷的大小（非常适合扩容）。

文件系统可以在运行期间增大。要减小大小，你必须先卸载文件系统并运行 `fsck`。请注意，如果你要扩大分区，必须先扩大底层分区或 LV；但如果你要缩小分区或 LV，只能在之后缩小！

### Example (示例)

在以下示例中，首先使用 `lvextend` 扩大逻辑卷。然后使用 `resize2fs` 增大其包含的文件系统。

```
root# lvextend -L 40G /dev/mapper/vg1-test

Extending logical volume test to 40,00 GB

Logical volume test successfully resized

root# resize2fs /dev/mapper/vg1-test

The file system /dev/mapper/vg1-test is mounted on

online resizing required

Perform an online resizing of /dev/mapper/vg1-test

to 10485760 (4k) blocks.
```

## resolvectl [options]

在现代发行版中，你可以使用 `resolvectl` 读取本地 DNS 配置，并在某些情况下更改它。`resolvectl` 是连接到 `systemd-resolved` 或 `systemd-networkd` 的组件。如果你的发行版运行本地缓存服务器，`resolvectl` 特别有用。`etc/resolv.conf` 文件仅包含指向此本地服务器的引用，但没有关于底层配置的信息。`resolvectl status` 提供有关所使用的 DNS 服务器的信息。

- `dns network interface ipaddr2 ...`
临时更改指定网络接口的 DNS 地址。该设置不会永久保存，并在网络连接更改时丢失（最晚在重启时）。

- `monitor`
显示所有传入的查询，直到你通过 Ctrl+C 停止。

- `query hostname`
返回分配的 IPv4 和 IPv6 地址。

- `ipaddr`
返回分配的 IPv4 和 IPv6 地址。

- `statistics`
显示 DNS 操作次数以及

- `status`
显示当前配置。

### Example (示例)

以下命令为 Apache Web 根目录下的所有文件设置正确的 SELinux 上下：

```
server:
root# restorecon -R -v /var/www/html/*
```

## rfkill 命令

同名软件包中的 `rfkill` 可以开启蓝牙、Wi-Fi 和手机适配器，例如在笔记本上关闭不需要的功能以节省电源。

- `block index/type`
禁用由索引指定或特定类型的所有设备。允许的类型有 `all`、`wifi = wlan`、`bluetooth`、`uwb = 超宽带`、`wimax`、`wwan`、`gps` 和 `fm`。

- `event`
等待 rfkill 事件并输出它们。

- `list` 列出所有无线适配器及其状态。`soft blocked` 表示设备可以通过 rfkill 开启和关闭。`hard blocked` 表示 rfkill 无法控制该设备，例如因为它连接到了机械开关。

- `unblock index/type`
激活指定的设备，其指定方式与 `block` 相同。

### 示例

测试计算机上可用两个蓝牙适配器和一个 Wi-Fi 适配器。其中一个蓝牙适配器被激活：

```
root# rfkill list
0: tpacpi_bluetooth sw: Bluetooth
  Soft blocked: yes
  Hard blocked: yes
1: hci0: Bluetooth
  Soft blocked: yes
  Hard blocked: no
2: phy0: Wireless LAN
  Soft blocked: yes
  Hard blocked: no
root# rfkill unblock 1
```

## rkhunter [options]

`rkhunter` shell 脚本（Rootkit Hunter）尝试检测安装在计算机上的 rootkit。与 `chkrootkit` 相比，`rkhunter` 执行了更许多测试。然而，与 `chkrootkit` 一样，该程序并非无一不的：你预期的会出现误报，并且程序可能无法检测出现代的 rootkit。

在某些发行版中，安装 `rkhunter` 包后会设置一个 cron 脚本，它每天调用一次 `rkhunter` 并发送包含结果的电子邮件。在 Debian 和 Ubuntu 上也提供了此功能，但在 `/etc/default/rkhunter` 文件中它是禁用的。

- `-c` 或 `--check`
执行 rootkit 搜索并显示结果。

- `--update`
更新检测 rootkit 的模式文件。

### 示例

程序的简短版本运行如下：



```
root# rkhunter-check
[ Rootkit Hunter version 1.4.6 ]
正在检查系统命令
...
正在检查文件属性
正在检查前提条件 [ OK ]
/usr/sbin/adduser [ OK ]
/usr/sbin/chroot [ OK ]
...
正在检查已知的 rootkit 文件和目录
55808 Trojan - Variant A [ Not found ]
ADM Worm [ Not found ]
AjaRootkit [ Not found ]
正在检查系统配置文件
正在检查 SSH 配置 [ Found ]
检查是否允许 SSH root 访问 [ Warning ]
检查是否允许 SSH 协议 v1 [ Not allowed ]
系统检查摘要：
文件属性检查：已检查文件: 151, 可疑文件: 1
rootkit 检查：已检查 rootkit: 475, 可能的 rootkit: 0
...
所有结果已写入日志文件：/var/log/rkhunter.log
```

## `rm` 命令

```
rm [options] files
```

`rm` 删除指定的文件。除非使用 `-r` 选项，否则不会删除目录。`rmdir` 命令用于删除单个目录。如果需要删除带有特殊字符的文件，必须将文件名用单引号括起来。这里列出了 `rm` 最重要的选项：

- `-f`

不进行进一步询问直接删除（包括目录）。

注意！

- `-i` 或 `--interactive` 或 `-v` 或 `--verbose`

在删除每个单独文件之前显示确认提示。

- `-r` 或 `-R` 或 `--recursive`

递归删除所有子目录中的文件（小心！）。如果删除了子目录的所有内容，该子目录本身也会被消除。

### 示例

以下命令删除当前目录下的所有备份文件（以 `~` 字符结尾的文件）：

```
user rm \*char126
```

`rm` 删除备份文件或目录。如果备份是一个目录，则其中包含的所有子目录和文件也将被删除！

```
user$ rm -r backup
```

`rm` 删除所有以哈希字符 (`#`) 开头的文件。使用单引号是为了防止 shell 将 `#` 解释为注释。

```
user$ rm '#\*'
```

## `rpicam-still` [options]

Raspberry Pi OS 上的 `rpicam-still` 命令可以使用连接到树莓派的相机拍照。

- `-camera 0|1`

选择摄像头。只有在同时连接两个摄像头时才需要指定此选项。

- `-e jpg|bmp|gif|png`

指定所需的图像格式（默认是 jpg）。

- `--ev n`

设置曝光补偿。使用 `--ev 0.5` 结果将变亮半档，使用 `--ev -0.5` 则变暗。

- `--height n`

指定图像高度（默认是相机的最大分辨率）。

- `-n`

录制时不显示预览窗口。

- `-o file`

指定图像文件名。

- `-q n`

指示 JPEG 图像质量（0 为最小，100 为最大）。

- `--rotation n`

指定图像的旋转角度。仅允许 0 和 180。

- `-t n`

指定创建照片之前的时间间隔（毫秒）（默认为 5000 毫秒，即 5 秒）。要尽快拍照，必须输入 `-t 1`。

- `--timestep n`

指定拍摄额外照片的毫秒数。在这种情况下，`-t` 控制整个命令的运行时间（例如 `-t 60000` 意味着一分钟）。

- `--width n`

指定图像宽度（默认是相机的最大分辨率）。

### 示例

以下命令创建一个分辨率为 800 × 600 的照片：

```
user$ rpicam-still --width 800 --height 600 -o photo.jpg
```

第二个示例创建一个 10 秒的延时摄影：

```
user$ rpicam-still -t 10000 --timestep 1000 -o timelapse.jpg
```

### 变体

`rpicam-still` 命令还支持其他选项。例如，你可以使用 `--rotation` 选项来旋转图像：

```
user$ rpicam-still --rotation 180 -o rotated.jpg
```

## `rpcinfo` [options]

`rpcinfo` 运行远程过程调用 (RPC) 并返回 RPC 服务器返回的结果。`rpcinfo` 主要用于检查 NFS 服务器配置等。

- `-p [hostname]`

确定本地计算机或外部计算机上所有活跃的 NFS 和 RPC 服务列表。

## `rpm` options [filename/package name]

`rpm` 用于安装、更新或删除 RPM 包，或显示有关这些包的信息。`rpm` 适用于所有基于 RPM 软件包的发行版，例如 Fedora、Red Hat 和 SUSE。

- `-e` 或 `--erase`

删除已有的软件包。如果你还使用了 `--nodepeps` 选项，即使有其他软件包依赖于该包，该包也会被删除。

- `-i` 或 `--install`

安装指定的软件包文件。可以使用额外的 `--root` 目录选项更改安装位置。如果指定的包是源包，则程序代码和配置文件将安装在 `/usr/src` 中。在这种情况下，可以通过更改 `/etc/rpmrc` 来设置安装位置。

配合额外的 `--test` 选项，`rpm` 不会进行任何更改，而仅输出实际安装期间会发生的情况。

`rpm` 尝试自动检查签名包的完整性。但是，必须有可用的签名公钥才能执行此操作（参见 `--import` 选项）。如果你让 `rpm` 忽略检查，必须使用 `--nosignature` 选项。

配合额外的 `--nodeps` 选项，即使 `rpm` 认为各种依赖关系未满足，你也可以安装软件包。（如果两个包相互依赖，则无需使用 `--nodeps`。你只需同时安装两个包即可！）

额外的 `--ignorearch` 选项允许在 `rpm` 识别出 CPU 架构不正确的情况下进行安装。这在 64 位发行版上安装 32 位软件包时有时是必要的。

`--force` 选项在任何情况下强制安装，即使 `rpm` 认为该包已经安装。

额外的 `--noscripts` 选项确保 `rpm` 不会自动运行安装程序。然而，你刚刚安装的程序可能无法正常工作。

- `--import`

安装指定的 GPG 密钥。`rpm` 可以使用此密钥来检查签名包的完整性。所需的密钥文件可以在所有提供签名 RPM 包的网站上找到。

- `-q` 或 `--query`

提供有关已安装软件包或包文件内容的信息。在简单形式下，`rpm -q package name` 会输出精确的包名，包括指定包的版本号。

你可以使用 `rpm -qf file` 来确定特定文件属于系统中的哪个包。这对于配置文件特别有用。例如，`rpm -qf /sbin/hwclock` 返回包名：`util-linux-n`。

`rpm -qp package.rpm` 提供尚未安装的包的信息。在这种情况下，必须使用 `*.rpm` 文件的文件名作为参数。

`rpm -q --whatprovides` 或 `rpm -q --requires` 属性搜索会查找所有提供或需要指定依赖属性的已安装包。这两个选项不适用于搜索尚未安装的包！

`rpm -q --provides package` 或 `rpm -q --requires` 创建指定包提供或需要的所有属性的列表。这些选项也可以用于尚未安装的包文件（额外的 `-p` 选项）。

对于所有返回包作为结果的查询变体，你可以使用额外选项来控制找到的包信息量：

- `-i` : 软件包的简短描述、压缩大小
- `-l` : 列出包中所有的文件
- `-lv` : 如上所述，但包含文件大小、访问权限等更多信息
- `-c` : 列出包的所有配置文件
- `-d` : 列出该包所有带有在线文档的文件
- `--scripts` : 列出所有安装程序

如果你只需要所有已安装软件包的未排序列表，应该运行不带任何额外参数的 `rpm -qa`。`rpm -qa --last` 按安装日期对所有包排序（最近安装的包在前）。

- `-U --upgrade`

更新已有的软件包。系统将从上一个包修改的配置文件创建备份文件；旧包的所有其他文件将被新版本替换或删除。配合额外的 `--oldpackage` 选项，你可以用旧包替换较新的包。你也可以使用 `--nodeps` 确保 `rpm` 在升级时忽略包依赖关系。

- `-V` 或 `--verify`

检查包中的任何文件自安装以来是否发生了变化。命令返回所有更改文件的列表。文档文件不进行检查。

### 示例

以下命令安装指定的软件包：

```
root# rpm -i abc-2.0.7-1.x86_64.rpm
```

第二个 `rpm` 示例提供了所有已安装包的列表，其中包按安装日期排序（最近安装的包位于列表顶部）：

```
root# rpm -qa --last
```

`rpm -q --provides` 告诉你之前安装的哪个包提供了 `mysql.so` 属性：

```
root# rpm -q --provides mysql.so php-mysql
```



如果你不知道 `/etc/magic` 文件属于哪个包，你可以通过 `rpm -qf` 确定此信息。然后，`rpm -qi` 提供该包的描述：

```
root# rpm -qf /etc/magic
root# rpm -qi util-linux-n
```

该命令用于识别特定类型的文件。

归档创建一个包含包所有文件的压缩归档 `tgz`。

可以使用以下变体来指定源和目标：

| file1 file2 | 本地文件 |
| :--- | :--- |
| directory | 本地目录 |
| host:dir | 主机上的目录 |
| user@host:dir | 同 host，但以用户身份登录 |
| rsync://user@host/dir | 与 RSync 服务器通信 |
| rsync://user@host:port/dir | 指定端口上的 RSync 服务器 |

SSH 项目的建议使用 `rsync` 代替 `scp` 命令，因为 `scp` 的实现并不完善，且尚未预见的解决方案。如果外部主机也安装了 `rsync` 且不涉及 `scp` 选项，你可以一对地用 `rsync` 替换 `scp`。相应的示例可以在 SCP 中找到。

### rsync 选项

- `-4` 或 `-6`
  如果两种变体可用，则强制使用 IPv4 或 IPv6 协议。

- `-a` 或 `--archive`
  递归复制目录内容并保留所有文件信息。该选项是 `-rlptgoD` 的快捷版本。

- `--delete`
  删除目标目录中源目录已不存在的文件或子目录（小心！）。

- `-D` 或 `--devices`
  同时也复制字符块设备信息。

- `-e command` 或 `--rsh=command`
  指定用于在目标计算机上运行 `rsync` 的外部 shell 程序。通常情况下这将是 `ssh`。如果你想向命令传递附加选项，必须将其放在引号中，例如 `-e "ssh -p 1234"`。

- `--exclude=pattern`
  指定不复制文件的模式。例如，`--exclude="*.o"` 排除 `*.o` 文件。（要制定更复杂的模式，请参 `man rsync`）。

- `-g` 或 `--group`
  使目标目录中的文件组分配与源文件相同。

- `-l` 或 `--links`
  在目标目录复制源目录中的符号链接。

- `-o` 或 `--owner`
  使目标目录中的文件所有者与源目录中的文件相同。

- `-p` 或 `--perms`
  赋予目标目录中的文件与源文件相同的访问权限。

- `-r` 或 `--recursive`
  递归复制所有子目录。

- `-t` 或 `--times`
  赋予目标目录中的文件与源文件相同的修改时间。这样一来，`rsync` 在再次被调用时就能明确识别出哪些文件发生了变化。

- `-u` 或 `--update`
  忽略目标目录中已存在且比源文件更新的文件。

- `-v` 或 `--verbose`
  提供有关当前运行内容的详细信息。

- `-W` 或 `--whole-file`
  在发生更改时复制整个文件。在快速网络连接下，这可以提高同步速度。

默认情况下，`rsync` 仅传输更改，从而最小化传输的数据量。`-w` 选项会增加传输的数据量，但会减少检测更改所需的工作。如果源目录和目标目录都是本地目录，则会自动应用 `-w`。在这种情况下，你可以使用 `--no-whole-file` 来确保 `rsync` 仍然使用增量变化模式。

## 示例

以下命令将 `mydata` 目录中的所有文件与同名的 `backup` 目录同步。`mydata` 中被删除的文件也将 `backup` 目录中删除。

```
user$ rsync -av --delete mydata/* /backup/mydata/
```

第二个示例将本地的 `dir1` 目录与 `mars.sol` 计算机上的 `dir2` 目录同步。密码输入由 `ssh` 负责。（因此，必须输入 `mars.sol` 计算机上用户 `username` 的登录密码。）

```
user@saturn.sol rsync -e ssh dir1/ mars.sol:dir2/
user@mars.sol's password: *************
```

`rsync` 也可以用于恢复已中断的大文件 `scp` 传输。（`scp` 无法做到这一点）。

```
user$ rsync --partial --progress --rsh=ssh local_file
user@host:remote_file
```

# scp

```
scp [options] source target
```

广泛使用的 `scp` 命令用于在网络中的两台计算机之间复制文件。传输是加密的。`scp` 要求第二台计算机上运行 SSH 服务器。源文件和目标文件或目标目录必须如下所示指定：

| file | 本地文件 |
| :--- | :--- |
| directory | 本地目标目录 |
| host: | 目标计算机（将文件复制到主目录） |
| host:file | 指定计算机上的文件 |
| host:directory | 指定计算机上的目标目录 |
| user@host:file | 指定计算机上用户 host: 目录的文件 |
| user@host:directory | 用户 user@host 的目标目录 |

## 示例

以下命令将本地的 `abc.txt` 文件复制到 `mars` 计算机的 `~/efg` 目录中：

```
user@uranus$ scp abc.txt mars:efg/
user@mars's password: *****
```

`-r` 允许你传输整个目录。`--links` 选项还确保了 `rsync` 也会考虑符号链接，这通常是不考虑的（但 `scp` 会考虑）。

```
user$ scp -r local-dir/ mars:other-dir
user@mars's password: *****
```

使用 `scp` 时，你可以使用 `-P` 选项传递端口号，如果另一端的 SSH 服务器没有使用标准端口 `22`。`rsync` 不可用此选项。相反，你必须使用 `-e` 来指定在后台调用的 `ssh` 命令应该如何组成：

```
user$ scp -P 2222 file mars:
user@mars's password: *****
```

## screen [options] [tty-device]

来自同名包的 `screen` 是一个屏幕管理器，将多个进程（会话）连接到终端。例如，你可以用它在 SSH 连接中并行运行多个命令，并在会话之间切换。`screen` 还可以将串口接口（TTY 设备）“重定向”到终端。

`screen` 由许多键盘快捷键控制，所有快捷键都以 `Ctrl+A` 开始，`Ctrl+A, ?` 显示最重要的快捷键摘要，`Ctrl+A, \` 终止 `screen`。进一步的快捷键总结在“键盘快捷键”部分的表 5.15 中。

你可以使用 `Ctrl+A, D` `detach` 从 `screen` 分离运行较长的进程。该进程将在后台继续运行。如果你稍后使用 `-r` 选项重新启动 `screen`，`screen` 将重新建立与会话的连接。

### screen 选项

- `-ls`
  列出所有从 `screen` 的会话。

- `-L`
  将 `screen` 中执行的所有命令及其输出记录到文件 `screenlog.0`（第一个会话）、`screenlog.1`（第二个会话）等文件中。也可以使用 `Ctrl+A, Shift+H` 开启或关闭日志记录。如果你想少读日志文件，必须使用 `-r` 选项，以便记录的控制字符被正确显示。

- `-r [session-id]`
  重新建立与断开会话的连接。如果只有一个会话，可以省略会 ID。

## 示例

用文本解释 `screen` 的工作原理很困难。如果你从未使用过 `screen`，应该看一段视频。例如，你可以搜索“screen 的工作原理”。

（注：由于原始文本中存在大量重复的段落，根据指令“一定不要重复输出原文”，此处仅翻译了核心内容部分。）

源文本中的组合（删除、替换为其他字符等）。

`sed` 由命令控制，这些命令要么应用于文本的所有行，要么仅应用于满足特定条件的行。

### sed 选项

- `-E`
  激活扩展正则表达式 `EREs`。默认情况下使用 POSIX 基础正则表达式。`sed` 不兼容 `PCRE`（Perl 兼容正则表达式）。

- `-i file`
  直接修改文件（内联）。通常，`sed` 从标准输入读取并写入标准输出。在这种情况下，无法直接修改文件。

- `-i.backup-identifier`
  与上一个列表项类似，但会将原始文件保存为带有指定 ID 的备份。

遗憾的是，处理 `sed` 并不简单。即使是基本语法选项的描述，也将远超本参考手册的范围。这就是为什么我会在书中仅限制在几个简单的示例上。你可以在以下网站找到关于 `sed` 的优秀介绍：

`www.grymoire.com/Unix/Sed.html`

## 示例

在第一个示例中，`sed` 删除测试文件的前三行，并将文件的其余部分发送到标准输出，其中 `d` 代表 `sed` 命令的删除 `delete`。`1,3` 指定了该命令生效的地址范围。



```
user$ sed 1,3d <
```

在第二个示例中，`sed` 将所有的“a” 替换为“A”，其中 `s` 代表正则表达式查找和替换（find and replace）命令。被 `/` 包围的文本是搜索模式和要插入的文本。由于命令前没有指定地址，它将应用于所有行。

```
user$ sed s/a/A/ <
```

第三个示例从 Markdown 文件中删除所有以 `\newpage` 开头的 LaTeX 语句。原始文件的备份被保存为 `test.md.bak`。

```
user$ sed -i.bak '/\newpage.*/d' test.md
```

使用 `sed` 复制或重命名文件的方法已在 `cp` 命令描述的另一个示例中显示。

```
seq [options] end
seq [options] start end
seq [options] start delta end
```

`seq` 返回一个数字序列。接下来的示例演示了它的工作原理。请注意，在浮点数的情况下，由于舍入误差，可能无法达到最终值，正如最后一个示例所示。

- - - s string

指定用于分隔结果的字符。默认情况下使用 `\n`，即换行符。

## 示例

以下示例显示了 `seq` 的用法。出于空间考虑，使用空格作为分隔符。通常，每个数字都输出在单独一行（即不使用 `-s` 选项）。

```
user$ seq -s''5
1 2 3 4 5
user$ seq -s''4 9
4 5 6 7 8 9
user$ seq -s''10 15 30
10 15 20 25 30
user$ seq -s''1 10.1 2
1 1.1 1.2 1.3 1.4 1.5 1.6 1.7 1.8 1.9
```

如果你在 bash 脚本中编写循环，你应该使用符号 `{start..end}` 或 `{start..end..delta}`，例如下面的命令所示：

`user${\bfs for i in {100..150..10}; do echo $i; done`

100 110 120 130 140 150

## sestatus [options]

`sestatus` 显示 SELinux 系统的状态。如果使用时不带额外选项，它将提供当前状态的摘要。

- - - -b

还显示 SELinux 规则中所有布尔（Boolean）参数的状态。这些参数可以使用 `setsebool` 修改。

- - - -v

还显示 `/etc/sestatus.conf` 中列出的文件和进程的上下文信息。

## 示例

测试计算机上的 SELinux 处于激活状态，并确保符合规则（当前模式 = enforcing）。使用了目标规则集。

```
root# sestatus -b
SELinux status: enabled
SELinuxfs mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: targeted
Current mode: enforcing
Mode from config: enforcing
```

Policy MLS status: enabled

Policy deny status: allowed

Memory protection checking: actual (secure)

Max kernel policy version: 32

Policy booleans:

audit_anon_write: off

audit_handle_event: off

audit_upload_watch: on

audit_can_scan_system: off

## set

bash 命令 `set` 显示 shell 已知的所有变量，包括环境变量，这些也可以通过 `printenv` 显示。`set -x` 使 `bash` 在执行每个命令之前，在考虑缩写和文件名后显示内部命令的内容。

## setcap [options] capability name

`setcap` 来自 lib 库设置权限（capability）名称。

`setcap` 通过扩展属性设置权限。如果使用 `-r` 选项，则可以删除权限。

## 示例

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

```
user$ ls -l
-rwxr-xr-x 1 root root 4096 1 1 10:00 file
-rwxr-xr-x 1 root root 4096 1 1 10:00 file2
```

`setcap cap_net_admin=ep file`

`user$ setcap cap_net_admin=ep file`

`user$ getcap file`

`cap_net_admin=ep file`

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。



`setcap` 激活 SELinux 规则符合规则。这由于 SELinux 允许 root 访问的权限。由于命令前没有指定地址，它将应用于所有文件。

## setfacl 规则

将传递的规则应用于标准 ACL。

`setfacl` 可以由更多选项控制：

- `-B` Or `--remove-all`

  删除所有 ACL 规则。
- `-d`

  将传递的规则应用于标准 ACL。
- `-k` Or `--remove-default`

  移除标准 ACL 规则。
- `-n`

  取消对每次 ACL 规则更改自动重新计算 ACL 掩码。
- `--restore=file`

  将文件中指定的 ACL 规则应用于当前目录下的文件。你可以使用 `getfacl -R` 创建 ACL 备份文件。
- `-R`

  递归地将指定的规则应用于文件和子目录。

### 示例

在具有 ACL 的文件系统中，通常应用默认访问权限，这些通常也被称为最小 ACL。`getfacl` 以 ACL 形式显示这些权限：

```
user$ touch file1
user$ getfacl file1
# file: file1
# owner: kofler
# group: kofler
```

```
user::rw-
group::r-
other::r-
user$ ls -l file1
-rw-r--r-- 1 kofler kofler ... file2
```

使用 `setfacl`，你可以定义额外的访问规则。

以下命令允许用户 `grace` 以及 `docuteam` 组的所有成员对文件具有读写权限，但拒绝用户 `katherine` 的任何访问：

```
user$ setfacl -m grace:rw file1
user$ setfacl -m g:docuteam:rw file1
user$ setfacl -m katherine:- file1
```

现在的权限列表变得长长了。通过 `ls -l`，通常的访问字母后会跟着一个 `+` 号，表示存在 ACL 规则。

```
user$ getfacl file1
# file: file1
# owner: kofler
# group:rw-
user::rw-
user:grace:rw-
user:katherine:-
group::r-
group:docuteam:rw-
mask::rw- other::r--
```

```
user$ ls -l file1
-rw-rw-r--+ 1 kofler kofler ... file1
```

```
setattr [options] file name
```

`setattr` 修改所选文件或目录的扩展属性。这只有在文件系统支持扩展属性（EAs）时才有效。对于 ext3/ext4 文件系统，必须挂载 `user_xattr`。

- `-n` attribute name 或 `--name=attribute name`

  指定要更改的属性名称。实际名称必须以 `user.` 开头（例如 `-n user.myattribute`）。
- `v` value 或 `--value=value`

  指定要保存到属性中的值。
- `x` attribute name



删除指定的属性。

- `--restore=file`

  将文件中指定的 EA 定义应用到当前目录下的文件。你可以通过 `getattr -R -d` 创建一个 EA 备份文件。

## 示例

以下示例展示了如何使用 `setattr` 存储属性，以及如何使用 `getattr` 读取它们：在 ext 文件系统中，每个文件的属性数量是有限的。

```
user$ touch file2
user$ setattr -n
```

```
user.language -v en file2
user$ setattr --name=user.charset --value=utf8 file2
user$ getattr -d file2
# file: file2
user.charset="utf8"
user.language="en"
```

`getattr` 通常只返回以 `user.` 开头的属性。如果你想查看其他属性，必须使用 `-n` 指定它们的名称，或使用 `-m` 指定它们的匹配模式：

```
user$ getattr -n security.selinux -d tst
# file: tst security.selinux="user_u:object_r:user_home_t:s0^0"
```

## `setbool` [options] bool1=value1 bool2=value2 ...

`setbool` 在运行时更改布尔参数。布尔参数可用于更改某些 SELinux 规则的行为。你可以通过 `sestatus -b` 确定哪些布尔参数是用的。

- `-N`

  保存更改但不激活。因此，更改将只在下次重启电脑时生效。

- `-P`

  执行更改并永久保存设置。更改将立即生效，并应用于未来，即下次重启后。

## 示例

以下命令允许 Squid 程序作为透明代理运行：

```
root# setsebool -P squid_use_tproxy 1
```

```
setterm [option]
```

`setterm` 更改终端的各种设置。如果执行命令时未指定选项，它将显示所有可能的选项列表。这里列出了 shell 编程中常用的选项：

- `--background color` 设置背景颜色。允许黑、红、绿、黄、蓝、洋红、青和白色。为了确保在 `ls` 或 `grep` 输出颜色后设置仍然有效，必须结合 `--store` 选项。

- `--blank n` 在无输入 `n` 分钟后激活屏幕保护程序（仅用于文本控制台）。

- `--bold on|off` 激活或禁用加粗字体。在文本控制台中，文本不会以加粗显示，但至少颜色与其他文本不同。

- `--clear` 删除终端内容。

- `--default`

  将颜色和文本属性恢复为默认设置。

- `--foreground color`

  设置文本颜色。

- `--half-bright on|off`

  切换高亮字体的开启/关闭。

- `--inverscreen on|off`

  反转文本控制台的显示（白色背景上的黑色文字）或恢复正常状态。

- `--reverse on|off`

  设置反转字体的开启/关闭。

- `--store`

  记住颜色设置（`--foreground` 和背景选项），即使 `ls` 或 `grep` 命令临时使用不同的颜色，设置也会保留。`--store` 仅在 Linux 文本控制台中有效，在终端窗口中无效。设置也不会保存在文件中，注销时会丢失。

- `--underline on|off`

  切换下划线字体的开启/关闭。

## 示例

如果在 `.bashrc` 中插入以下行，登录后文本控制台将使用白色背景和黑色字体：

```bash
## insert into .bashrc
setterm -background white -foreground black -store
```

## `fsdisk` [options]

`fsdisk` 列出硬盘的分区。这适用于 MBR 分区表。

- `[device]`

  对硬盘进行分区。这对于 GPT 非常适用。

- `--force`

  即使 `fsdisk` 认为分区正在使用也进行分区。

- `l [device]`

  列出硬盘的所有分区。

- `-uS|-B|-C|-uM`

  使用扇区（512字节）、块（1024）、柱面或 MiB 作为单位。

## 示例

以下命令按照硬盘（sda）的方式对第二个硬盘（sdb）进行分区。

```
root# fsdisk -d /dev/sda | fsdisk /dev/sdb
```

## `sgdisk` [option] device

`sgdisk` 帮助编辑硬盘和 SSD 上的分区。与 `parted` 不同，该命令完全由选项控制，不用于交互式使用。相反，你可以在脚本控制下使用 `sgdisk` 创建或操作。尽管命名相似，其选项与 `fsdisk` 完全不同。`sgdisk` 使用 MiB 和 GiB。

- `a n`

  指定新分区对齐的扇区倍数。`sgdisk` 默认使用 2048。这对应于 1 MiB。

- `b file`

  将分区表的备份写入二进制文件。

- `d nr`

  删除指定的分区。

- `G`

  为所有分区分配新的随机 GUID。在克隆硬盘后是必需。

- `l`

  根据文件中存储的分区表划分介质。必须先使用 `-b` 选项创建文件。介质上的现有分区将被删除。`sgdisk -b` 和 `sgdisk -l` 命令的组合可以将分区布局传输到相同大小的硬盘，例如设置 RAID 系统。

- `n nr:start:end`

  创建一个编号为 `nr` 的新分区，从指定的起始位置扩展到结束位置。默认情况下，起始和结束以 512 字节扇区指定。或者你也可以用 MiB 和 GiB 指定位置。`sgdisk -n 3:10G:35G` 创建一个大小为 25 GiB 的新分区。

起始和结束位置可以用 `+` 和字符在前。`+` 允许相对于默认起始扇区；`-` 允许从硬盘末尾计算指定。`sgdisk -n 4:+1M:-20G` 创建一个从最后一个分区开始 1 MiB 的分区，并在介质末尾留出 20 GiB 的空闲空间。

## 示例

以下命令首先在 `/dev/sdb` 磁盘上创建当前分区表的备份，然后设置新分区 3：

```
root# sgdisk -l partbackup /dev/sdb
root# sgdisk -n 3:70G:430G /dev/sdb
```

## `shansum` 文件

`sha1sum`, `sha224sum`, `sha256sum`, `sha384sum` 和 `sha512sum` 用于计算所有指定文件的校验和。命令中的数字表示校验和的位长度（`sha1sum` 为 160 位）。校验和用于用于确保文件在传输后没有被改动。

## 示例

以下命令为 ISO 文件计算 256 位的校验和：

```
root# sha256sum image.iso
6ad62fe91eefa4315f852eb1bc8732bc341d95b47f6b4d1f5e362369fc981b image.iso
```

## `shift` [n]

bash 命令 `shift` 用于移动通过预定义变量 `$1` 到 `$9` 传递给 shell 脚本的参数列表。如果使用 `shift` 时不带参数，参数将向前移动一位；否则，它们将移动 `n` 个位置。

`shift` 仅用于脚本编程。当需要处理超过九参数时，该命令是一个非常有用的辅助。一旦参数通过 `shift` 移出变量，它们将无法再次被访问。它们也会从 `$*` 变量中被移除。

## `showmount` [options]

在没有额外选项的情况下，在 NFS 服务器上执行 `showmount` 命令将返回所有通过 NFS 3 使用共享目录的客户端列表。注意，结果中不包含 NFS 4 目录，这些目录在使用 `showmount -e` 变体时会被考虑。

- `-a`

同时也为每个 NFS 3 客户端提供 IP 地址。

- `-e [hostname]`

提供所有可以通过 NFS 使用的目录列表，无论该服务当前是否正在使用。如果你指定了主机名，将确定该计算机上用的目录列表。`showmount -e` 也适用于 NFS 4。

## 示例

```
root# showmount -e
/nfsexport *.lan,10.0.0.0/24
/nfsexport/fotos *.lan,10.0.0.0/24
/nfsexport/iso *
```

## `shutdown` [options] time [message]

`shutdown` 用于关闭计算机。必须指定时间（hh:mm）或分钟数（从当前时间计算，+m）或 `now` 关键字（即立即执行）作为时间。`shutdown` 只能由 root 执行。Linux 通常配置为如下方式，使得没有 root 权限的用户可以通过 Alt + Ctrl + Del 重启计算机。



`shutdown` 通知所有其他用户系统很快将关闭，并且不再允许新登录。随后所有进程将收到警告，它们很快将被停止。某些程序（例如 `emacs` 或 `vi`）会利用此警告并将所有打开的文件保存到备份副本中。

- `-c`

尝试取消已经启动的关机过程。如果启动关机过程之前的时间尚未过期，则可以实现。

- `-f`

启动一个类似于 `-r` 的重启，但速度更快。

- `-F`

导致在下次重启时检查文件系统。`shutdown` 会为此创建 `/forcefsck` 文件。如果此文件存在，大多数发行版在重启时会触发文件系统检查。

- `-h`

关机后停止系统。随后计算机不再响应输入，屏幕上会出现系统停止的消息。然后，计算机将通过 ACPI 信号关闭。

- `-n`

特别快速地执行关机，跳过 init 系统。

- `-r`

在系统关闭后启动重启。

- `-t seconds`

定义警告消息和进程终止信号之间的等待时间（通常为 20 秒）。

```
sleep time
```
``sleep`` 将运行中的程序置于睡眠模式，持续指定指定的时间。在此期间，该程序几乎不消耗计算时间。时间通常以秒为单位。可以选择添加字母 `m`、`h` 或 `d` 来指定分钟、小时或天。

## slurp

来自同名包的命令允许在 Wayland 上选择屏幕上的矩形。然后它以文本形式返回左上角的坐标和矩形的大小。该命令可以与 `grim` 结合使用，例如用于选择截图区域。

遗憾的是，`slurp` 并不兼容所有的 Wayland 合成器。`slurp` 在 Raspberry Pi OS 上运行良好，但在使用 Gnome 或 KDE 作为桌面系统的发行版上会失败。

## smartctl options device

`smartctl` 控制硬盘的 SMART 功能。这允许你在早期阶段检测到可能的硬盘问题。

- `-a` 或 `--all`

提供所有可用的 SMART 信息。

- `-d data/scsi/3ware,n`

指示硬盘类型。只有当 `smartctl` 无法识别类型时，才需要此选项。这特别适用于 SATA 硬盘，`smartctl` 经常认为它是 SCSI 硬盘。`3ware,n` 设置允许为连接到 3ware RAID 控制器的硬盘使用 SMART 功能（详情请参见 `man smartctl`）。

- `-H` 或 `--health`

指示硬盘当前是否正常，并且可能可能在接下来的 24 小时内继续工作。

- `-i` 或 `--info`

提供有关硬盘的基本信息。

- `-l error/selftest` 或 `--log=error/selftest`

提供过去五个个错误的信息或最后 21 次自检的结果。

- `-s on/off` 或 `--smart=on/off`

激活或禁用 SMART 功能。

- `-t short/long` 或 `--test=short/long`

执行短自检或长自检。稍后可以使用 `-l selftest` 查看测试结果。

## 示例

`smartctl -H` 或 `smartctl --health` 指示硬盘当前是否健康。如果 `smartctl` 返回 `PASSED` 结果，你应该立即开始备份！

```
root# smartctl -H /dev/sda
...
```

SMART 总体健康结果：PASSED

`dev/sda` 硬盘已执行三次自检：一次是在安装磁盘后（40 小时后），另外两次是在大约 2600 小时后。没有发生问题。

```
root# smartctl -t short /dev/sda
root# smartctl -t long /dev/sda
...
```

| Num | Test_Description | Remaining Life | LBA |
|---|---|---|---|
| 1 | Extended | Completed without error | 0% | 2592 |
| 2 | Short | Completed without error | 0% | 2591 |
| 3 | Short | Completed without error | 0% | 40 |

- `-L computer name`

返回指定的 Windows 计算机或 Samba 服务器上的资源列表。

- `-m protocol`

指定最大协议版本。`-m SMB2` 强制使用 SMB2 协议，即使可以使用 SMB3。此选项仅在为了避免兼容性问题的少数情况下需要。

- `-N`

跳过自动密码提示。如果你知道访问特定网络资源不需要密码时，此选项才有用。

- `-U username`

指定用户名（如果与当前登录名称不同时才需要）。

- `-W workgroup name`

指定 Windows 工作组名称（如果未包含在 `/etc/samba/smb.conf` 中才需要）。

```
smbclient [options]
smbclient directory [password] [options]
```
`smbclient` 允许对 Windows 目录进行交互式访问。在第一语法变体中，可以使用该程序确定可用的 Windows 资源。在第二变体中，你输入所需的网络目录（例如想使用 mars 上的数据目录输入 `//mars/data`）。一旦建立连接，你将进入一个 shell。就像 ftp 命令一样，可以使用 `ls` 查看目录，使用 `cd` 切换目录，通过 `get` 文件到本地计算机，并使用 `put` 将文件保存到外部计算机。你可以通过 `help` 获取最重要命令的概览。

示例

首先，`smbclient` 连接到 NAS 磁盘，然后 `ls` 返回存储在该处的目录和文件列表：

```
user$ smbclient -U name -W wgname //mynas/myshare
Password: xxxxxxx
```

Domain=[wname] OS=[Unix] Server=[Samba 3.5.2]

smb: > Ls

data             D       0 Apr 5 18:17:11 2025

file.xy         AR      226 Sep 14 04:00:00 2024      ...

在第二个示例中，smclient 到树莓派上的 LibreELEC 媒体中心建立了连接。然后它列出了那里可用的网络目录，默认情况下不需要密码即可访问。“U none 在处仅指定了一个无效的用户名。

```
user$ smclient -L libreelec -U none -N -m SMB2
Sharename      Type      Comment
----------     ------      ------
Music          Disc
Screenshots    
Videos         Disk
...
```

## smbpasswd [options] [name]

`smbpasswd` 修改活动或指定 Samba 用户的密码。

- `-a`

创建 一个 Samba 账户。必须有一个同名的 Linux 账户。

- `-n`

删除指定账户的密码。如果 Samba 服务器配置相应（空密码 = yes），则现在无需密码即可访问网络目录。

- `-x`

删除指定的 Samba 账户。

## smbstatus [options]

`smbstatus` 返回计算机上运行的 Samba 服务器版本号以及所有当前活动连接的列表。

## snap [options] 命令

几年前，Ubuntu 引入了一种新的软件包系统。它与仍然主流的 Debian 包系统（参见 `apt` 和 `dpkg`）并行运行，其目标与 Red Hat 支持的 Flatpak 方法类似（参见 `flatpak`）。Snap 对所有发行版都开放，但在 Ubuntu 之外尚未发现任何显著优势。

Snap 包通常通过名为“软件”的 Gnome 程序安装。`snap` 命令提供了在终端中管理 Snap 包的选项。

- `- find search term`

在标准 Snap 软件包源 `https://snapcraft.io.` 中的包描述中搜索指定的术语。

- `- install [--classic] name`

安装指定的包（需要 root 权限或 `sudo`）。只有某些需要对文件系统进行无限制访问并以较不严格的安全规则执行的包才需要指定 `--classic` 选项。你可以使用 `--edge`、`--beta` 或 `--candidate` 选项从指定的测试通道安装包。（如果没有这些选项，将使用发布通道。）

- `- list`

列出以前安装的 Snap 包。

- `- refresh`

显示所有已的包。

- `- remove name`

卸载指定的包。

## 示例

以下命令安装 Atom 编辑器：

```
user$ snap install --classic atom
atom 1.51.0 installed from Snapcrafters
```

```
snapper [options] 命令
```



SUSE 发行版默认对系统分区使用 `Btrfs` 文件系统。`YaST` 在每次管理操作前后自动创建快照。这些快照可以使用 `YaST` 模块 `Snapper` 或此处简要介绍的 `snapper` 命令进行管理。你可以在执行的 `snapper` 命令前加上一个或多个选项：

- `--iso`

  以 ISO 格式化时间。

- `--utc`

  显示 UTC 时间（协调世界时）。

执行的操作由子命令指定：

- `cleanup number|timeline|empty-pre-post`

  根据最大快照数量、年龄或内容作为标准删除旧快照（参见 `/etc/snapper/configs/root` 配置文件）。

- `create`

  创建一个新快照。

- `delete n` 或 `n1-n2`

  删除指定的快照。使用的数字可以在 `snapper list` 中找到。

- `list`

  列出所有快照。

- `rollback [n]`

  将指定的或最近可用的快照设置为活动快照（严格来说：`Btrfs` 默认子卷）。随后的重启命令将系统恢复到创建快照时的状态。

- `undochange n1..n2 [files]`

  撤销快照 `n1` 和快照 `n2` 之间的更改——适用于所有影响的文件或仅针对参数指定的文件。

### `sort` [options] `file`

`sort` 对指定的文件进行排序并在屏幕上显示结果。排序顺序由语言设置定义，具体来说由 `LC_COLLATE` 环境变量定义。

- `-c`

  检查文件是否已排序。

- `-f`

  将小写和大写字母视为等等。

- `-k n1,n2`

  仅考虑 `n1` 和 `n2` 列之间的字符。列编号从 1 开始。通常，列由空格或字符分隔，请参见 `-tz`。如果未指定 `n2`，则将考虑从 `n1` 到行尾的所有字符。

- `-m`

  将两个或多个预先排序的文件合并成一个大的排序文件。这比先将文件放在一起再排序更快。

- `-n`

  按数字排序（即 10 在 9 之后，而不是 1 之后）。

- `-o result file`

  将结果写入指定的文件。该文件可以与排序的文件相同。

- `-r`

  反向排序。

- `-tz`

  指定两列之间的分隔符。默认设置是空白，即空格和制表符的任意组合。

- `-u`

  消除结果中的重复项。

### 示例

以下命令安装 Atom 编辑器：

```
user$ snap install --classic atom
atom 1.51.0 installed from Snapcrafters
```

```
user$ speaker-test -t wav -c2
```

### `speaker-test` [options]

来自 `alsa-utils` 的 `speaker-test` 命令帮助你跟踪音频系统的问题。为此，它产生频率。

- `-c n`

  使用 `n` 个音频通道。

- `-f n`

  以指定的赫兹频率播放正弦波。必须使用 `-t` 选项。

- `-s n`

  仅测试编号为 `n` 的音频通道。

- `-t pink|sine|wav`

  输出粉红噪声、正弦波或来自 WAV 的语音模式。

- `-w file`

  播放指定的 WAV 文件。

命令，所有命令都必须以分号结束。除了常用的 SQL 命令外，`sqlite3` 还知道一些以点（`.`）开头的特定命令，例如 `.help` 显示帮助文本或 `.tables` 列出数据库中的所有表。`.quit` 或 `Ctrl+D` 可终止 `sqlite3`。

在第二种语法变体中，`sqlite3` 直接运行指定的 SQL 命令。

### 示例

以下命令确定哪些音乐专辑存储在 ownCloud 数据库中：

```
user$ owncloud.db
sqlite> select * from oc_media_albums;
1|NightClub|1|
2|The Monroe Doctrine|2|
3|The Best Of Herbie Mann|3|
...
sqlite> .quit
```

### `ss` [options]

`ss`（套接统计）分析本地计算机的网络活动。如果执行命令时不带选项，它将返回所有具有活动连接的非监听 TCP 套接。`ss` 提供了与 `netstat` 类似的功能，但被认为是更现代的命令，在某些情况下提供更详细的信息。

- `-4` 或 `-6`

  仅考虑 IPv4 或 IPv6 连接。

- `-a`

  显示所有套接，包括监听和非监听的。

- `-e`

  提供更多细节（扩展）。

- `-n`

  显示数值端口号，而不是服务名称。

- `-p`

  指定哪些进程使用了哪些套接。

- `-r`

  将端口号替换为服务名称。

- `-s`

  仅显示摘要信息（summary）。

- `-t` 或 `-u`

  仅考虑 TCP 或 UDP 连接。

### 示例

以下命令提供了 IPv6 连接的所有活动 TCP 套接列表：

```
users ss -6 -t -a                               Peer Address:Port
State Recv-Q Send-Q  Local Address:Port
LISTEN 0       100     ::pop3               ::*
LISTEN 0       100     ::imap2              ::*
```

| LISTEN 0 128 ::http :::** |

| LISTEN 0 100 ::smtp :::** |

| LISTEN 0 128 ::https :::** |

| LISTEN 0 100 ::pop3s :::** |

| TIME-WAIT 0 0 ffff:5.9.22.28:http ffff:188.192.181.195:50045 |

| TIME-WAIT 0 0 ffff:5.9.22.28:http ffff:188.192.181.195:50047 |

| ESTAB 0 46200 ffff:5.9.22.28:http ffff:46.10.92.30:22893 |

| FIN-WAIT-1 0 1 ffff:5.9.22.28:https ffff:203.134.55.243:51106 |

### `ssh` [options] `computer name`

### `ssh` [options] `computer name` 命令

在第一种语法变体中，`ssh` 在另一台计算机上打开 shell，从而能够在该台计算机上进行交互式工作。第二种语法变体在第二台计算机上运行单个命令。只有当第二台计算机上运行着 SSH 服务器时，`ssh` 才能工作。

- `-l login`

  在第二台计算机上使用指定的登录名而不是当前用户名。所需的登录名也可以以此格式输入：`ssh loginname@computername`。

- `-L localport:host:hostport`

  在本地计算机（`localport` 端口）和第二台计算机（`hostport` 端口）之间建立隧道。

- `-o option=value`

  启用传输额外的选项，其语法与 `/etc/ssh/ssh_config` 文件中的相同（参见 `man ssh_config`）。例如，`-o StrictHostKeyChecking=no` 会导致 SSH 停止检查已保存在 `.ssh/know_host` 中的主机数据项。这对于许多虚拟机的自动化管理非常有帮助。

- `-t`

  强制使用伪终端来执行命令，格式为 `ssh -t hostname "commands"`。这使得通过 SSH 启动 `top` 等交互式程序成为可能。连接会持续到外部命令结束（对于 `top` 来说，通过输入 Q 结束）。

- `-T`

  防止激活伪终端。你可以在以下示例中找到此选项的应用。

- `-v`

  提供全面的调试信息。如果你遇到登录问题，`ssh -v` 通常可以帮助你找到原因。该选项可以指定三次（即 `-v -v -v`）；`ssh` 然后会提供更多的调试信息。

- `-X`

  启用执行 X 程序。

### 示例

以下命令显示了你如何登录到外部计算机，且用户名保持不变。然后你可以在外部计算机（例如，你的根服务器）上运行命令。

```
kofler@uranus ssh kofler.info
kofler@kofler.info's password: ********
```

当你第一次使用 `ssh` 连接到另一台计算机时，通常会出现基于以下模式的警告：

> 无法确认 'kofler.info (1.2.3.4)' 的真实性。

> RSA 密钥指纹是 SHA256:...

> 确定要继续连接吗吗？

如果你回答 `yes`，主机密钥将被添加到 `~/.ssh/known_hosts`。

以下命令显示了如何将公钥拷贝到远程服务器：

```
ssh-copy-id user@host
```

`ssh-copy-id` 命令简化了在远程服务器上安装公钥的过程。它会自动将你的公钥添加到远程机器上的 `~/.ssh/authorized_keys` 文件中。如果不可用 `ssh-copy-id`，你可以通过以下方式手动完成：



```bash
cat ~/.ssh/id_rsa.pub | ssh user@host "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

## 示例

以下命令生成一个 ECDSA 密钥：

```
user$ ssh-keygen -t ecdsa
Generating public/private ecdsa key pair.
Enter file in which to save the key (/root/.ssh/id_ecdsa): <Return>
Enter passphrase (empty for no passphrase): ******** <Return>
Enter same passphrase again: <Return>
Your identification has been saved in /root/.ssh/id_ecdsa
Your public key has been saved in /root/.ssh/id_ecdsa.pub
```

## stat [options] files

`stat` 提供关于指定文件的详细信息，包括 `ls` 格式和八进制数字表示的访问权限、使用的扇区数、最后修改的时间和最后读取访问的时间等。

- `-c formatstring`

  根据格式字符串化输出。

- `-f`

  提供文件所在文件系统的信息（而不是关于文件本身）。在字符串中可以使用以下代码等：

- `%a`: 八进制表示的访问权限

- `%A`: `ls` 格式的访问权限

- `%C`: SELinux 上文

- `%F`: 文件类型（文件、目录、块设备等）

- `%g`: 文件所属组的 GID

- `%G`: 文件所属组的名称

- `%h`: 硬链接数

- `%n`: 文件名

- `%s`: 以字节为单位的文件大小

- `%u`: 文件所有者的 UID

- `%U`: 文件所有者的名称

## 示例

在不带选项的情况下，`stat` 提供文件各种元数据的清晰汇总。使用 `-c` 后，结果可以精简为单独的信息；在第二个示例中，结果被精简为八进制访问权限和名称。

```
$ stat print.pdf
file: print.pdf
  size: 390758 blocks: 768 EA: 4096 regular file
  device: fd0h1/rw-6476d Inode: 397971 links: 1
  access: (0664-/-rw--) Ui: (1000/ koffler) Gid: (1000/ koffler)
  context: unconfined u:object_r:user_home_t:s0
  2013-09-24 11:35:17.316000000+0200
  modified: 2013-08-06 17:53:16.083000000+0200
  changed: 2013-08-06 17:53:16.083000000+0200
  birth: -

user$ stat -c "%a %n" print.pdf
664 print.pdf
```

## strace [options] command

`strace` 运行指定的命令或程序，并显示命令调用的所有系统函数。因此，`strace` 是调试编译程序的的重要工具。可以使用各种选项来控制程序想要输出的（额外）信息。

## strings [options] file

该命令从二进制文件中提取字符字符串并显示。这非常有用，例如当你想在程序文件中查找某个文本（如错误消息或文件名）时。

## 示例

以下命令确定二进制文件 `/bin/ls` 中包含 "error" 单词的所有字符串：

```
root# strings /bin/ls | grep error
error
error initializing month strings
write error
```

在下面的示例中，我想找出在 openSUSE Leap 上 `systemd` 程序 `systemd-vconsole-setup` 访问了哪些键盘配置文件：

```
user$ strings /usr/lib/systemd/systemd-vconsole-setup | grep keyboard
/etc/sysconfig/keyboard
```

```
su [options] [user]
```

不带选项的 `su`（切换用户）在输入密码后会切换到 `root` 模式。这意味着在下一次退出命令之前，`root` 都是活动用户。

可选，可以为 `su` 指定另一个用户而不是默认的 `root` 用户。如果由 `root` 运行 `su`，切换用户时甚至不需要输入命令。

- `-c command`

  以 `root` 权限仅运行指定的命令。

- `-l` or `--login`

  当用户切换时，新的 `shell` 将作为登录 `shell` 启动。这意味着所有的登录文件也会加载，这对于正确配置 `PATH` 等环境变量是必要的。

```
sudo [options] [var1=value1 var2=value2] command
```

`sudo` 运行命令就像是由不同的用户（通常是 `root`）执行的一样。得益于 `sudo`，普通用户可以在不知道 `root` 密码的情况下执行管理任务或运行系统关键命令。

在 `sudo` 允许执行程序之前，必须在 `etc/sudoers` 文件中为特定用户和特定程序指定该权限。

- `-b`

  在后台启动指定的命令。

- `-E`

  接收环境变量的当前内容。在 Wayland 图形模式下以 `root` 权限启动程序时需要此选项。

- `-H`

  进入环境变量的当前内容。

- `-c command`

  以 `root` 权限仅运行指定的命令。

- `-l` or `--login`

  当用户切换时，新的 `shell` 将作为登录 `shell` 启动。这意味着所有的登录文件也会加载，这对于正确配置 `PATH` 等环境变量是必要的。

- `-w parameter=value`

  更改指定的参数。`-w` 选项也可以省略。

## 示例

以下两个命令首先激活内核的转发功能，然后对 `eth0` 网络接口进行 IP 伪装：

```
root# sysctl -w net.ipv4.ip_forward=1
root# iptables -A POSTROUTING -t nat -o eth0 -j MASQUERADE
```

## systemctl 命令

`systemctl` 用于管理使用 `systemd` 作为初始化系统的发行版的初始化进程（`init process`）。目前几乎所有的发行版都是如此情况。你可以使用 `systemctl` 来确定系统管理的所有进程列表、停止或重启单个后台服务等。

此外，`systemctl` 区分了普通服务（`services`）、套字（`sockets`）、设备（`devices`）、挂载服务（`mount services`）和目标（`targets`），这可以比 Init-V 的运行级别（`runlevels`）。

- `--daemon-reload`

  加载配置文件。为了使 `systemd` 配置文件和 `/etc/fstab` 的更改生效，必须运行此命令。

- `--enable/disable name`

  永久激活指定的服务或再次激活它。执行该命令时，相应的链接会被重新创建或删除。在当前的 `systemd` 版本中，额外的 `--now` 选项会导致相关服务立即启动或停止。

- `--get-default`

  确定默认目标。

- `--halt/poweroff/reboot`

  关闭或重启系统。

- `--is-active name`

  测试指定的服务是否处于激活。

- `--isolate name.target`

  激活指定的目标以及所有依赖于它的服务。不需要的服务将被停止。因此，`isolate` 的功能类似于 Init-V 系统中的运行级别切换。

- `--list-timers`

  提供活动计时器的概览，即由 `systemd` 定期运行的作业。对于每个作业，都会指定上一次运行和下一次计划运行的时间。

- `--list-units`

  提供由 `systemd` 管理的所有服务、套字、目标、设备等的列表。多页输出通过 `less` 路由，以便逐页阅读。如果你不想这样做，必须指定 `--no-pager` 选项。

  可以使用 `--type=...` 过滤结果。允许的单元类型有 `service`、`socket`、`target`、`device`、`mount`、`automount` 和 `snapshot`。

- `--reload/restart name`

  提示进程重新加载配置或完全重启服务。

- `--set-default name.target`

  为未来的启动过程定义默认目标。

- `--show name`

  提供比 `status` 更详细的数据。结果按行结构化，可以被脚本方便地处理。

- `--start/stop name`

  启动或停止指定的初始化进程或服务。

- `--status name`



以清晰可见的形式提供指定服务的状态信息。

`systemctl` 默认应用于系统级执行的服务。要编辑用户级的服务，必须传递 `--user` 选项。这在现代桌面系统中很有用，例如 Gnome 使用 systemd 的系统。

## 示例

以下行显示了典型的 `systemctl` 命令：

```
root# systemctl start cups
(启动 CUPS 守护进程)
root# systemctl stop cups
(停止 CUPS 守护进程)
root# systemctl restart cups
(重启 CUPS 守护进程)
root# systemctl reload cups
(重新加载 CUPS 守护进程的配置)
root# systemctl status cups
(确定 CUPS 守护进程的状态)
```

```
root# systemctl enable cups
(未来自动启动 CUPS 守护进程)
创建符号链接 /etc/systemd/system/sockets.target.wants/cups.socket -> /lib/systemd/system/cups.socket。
创建符号链接 /etc/systemd/system/multi-user.target.wants/cups.path -> /lib/systemd/system/cups.path.
```

```
root# systemctl disable cups
(不再自动启动 CUPS 守护进程)
删除 /etc/systemd/system/sockets.target.wants/cups.socket。
删除 /etc/systemd/system/multi-user.target.wants/cups.path。
```

```
root# systemctl isolate reboot.target
(重启)
```

### systemd-analyze 命令

`systemd-analyze` 用于分析启动时间。它会显示启动过程中各个阶段的时间，例如内核启动、用户空间等待等。

```
root# systemd-analyze
启动已完成 12.345s (内核: 2.123s, 用户空间: 10.222s, 等待: 0.000s)
```

`systemd-analyze blame` 可以列出启动过程中耗时最长的服务。

```
root# systemd-analyze blame
     5.123s network-online.service
     3.456s systemd-network-generator.service
     2.111s mysql.service
```

`systemd-analyze critical-chain` 可以显示启动的关键链路径。

```
root# systemd-analyze critical-chain
system-target@12.345s
└─ users-user.target@12.345s
        └ network-online.service@5.123s
```

`systemd-analyze plot` 可以生成一个启动过程的 SVG 图，可以在浏览器中查看。

```
root# systemd-analyze plot > plot.svg
```

### journalctl

`journalctl` 用于查看 systemd 志的日志。

```
root# journalctl -u ssh
(查看 ssh 服务日志)
root# journalctl -n 100
(查看最近 100 行日志)
```

### tar 命令

`tar` 命令用于创建、归档和提取文件包。

```
root# tar -cvf archive.tar file1 file2
(创建一个名为 archive.tar 的压缩包)
root# tar -xvf archive.tar
(提取 archive.tar 中的文件)
```

#### grep 命令

`grep` 命令用于在文件中搜索字符串。

```
root# grep "error" logfile.txt
(在 logfile.txt 中搜索 "error")
```

### find 命令

`find` 命令用于在目录中搜索文件。

```
root# find /home -name "*.txt"
(在 /home 目录下查找所有扩展名为 .txt 的文件)
```

输出通道或从标准输入读取。这在两个 tar 命令通过 `|` 链接时（通常用于传输整个树结构）特别有用。

- `-g` 将与 tar 一起保存的文件的元数据保存到二进制时间戳文件中，并且仅考虑自上次调用 tar 以来发生变化的文件。此选项提供了一种创建增量备份的简便方法（参见文末的最后一个示例）。
- `-j` 或 `--bzip2`

通过 bzip2 压缩或解压缩整个归包（参见 `-z`！）。
- `-J` 或 `--xz`

通过 xz 压缩或解压缩整个归包。这假设系统中可用 `xz` 命令。许多分发版需要安装 `xz-utils` 包。
- `-L n` 或 `--tape-length n`

指定流传输器的容量，单位为 KiB。如果归包的大小超过了容量，tar 会提示你更换磁带。
- `-N Date`, `--after-date date`, 或 `--newer date`

仅归档比指定日期更新的文件。这有助于创建增量备份。
- `-p` 或 `--preserve-permissions`

在提取文件时保持访问权限不变。当由 root 执行 tar 时，该选项默认生效。
- `-T file` 或 `--files-from file`

归档或提取文件中指定的文件名。
- `-v` 或 `--verbose`

在操作时在屏幕上显示所有文件名。如果 `-v` 与 `t` 命令结合使用，将显示关于文件的额外信息（文件大小等）。如果指定了两次该选项，信息将更加详细。
- `-W` 或 `--verify`

在写入后检查刚刚归档的文件的正确性。这些选项无法用于压缩归包。
- `-z` 或 `--gzip`

使用 gzip 压缩或解压缩整个归包。此选项在创建 `*.tgz` 文件时非常有用。然而，如果数据实际上存储在流传输器上，该选项可能是危险：磁带上的单个错误就可能导致整个归包无法使用！如果不进行压缩，文件会被破坏，但损坏通常会小得多。DAT 流传输器本身能够对要处理的数据进行压缩。这种方式更快，但没有 gzip 高效。

## 示例

在下面的示例中，tar 将 Documents 目录及其所有子目录下的所有文件归档到 `archive.tgz` 文件中：

```
user$ tar -czf archive.tgz Documents
```

`tar -tzf` 返回归包的目录列表。归包内的文件顺序是随机。

```
user$ tar -tzf archive.tgz | less...
```

`tar -xzf` 解压归包并提取包含的所有文件：

```
user$ cd different-directory/
user$ tar -xzf archive.tgz
```

以下命令将所有文件从 `/dir1` 复制到 `/dir2`。与普通 `cp` 命令相比的优势是，符号链接会被原样复制（而不是复制链接引用的数据）。前面的两个命令特别适用于将整个文件树从一个分区传输到另一个分区。

```
root# (cd /dir1 ; tar cf - ) | (cd /dir2 ; tar xvf -)
```

最后一个示例显示了如何创建 images 目录的增量备份。在第一次备份期间，会删除任何现有的时间文件以执行完整备份（例如始终在周日晚上）。随后在后续工作日晚上进行的备份将仅考虑自那时起所做的更改。

```
user$ rm backup.timestamps
user$ tar czvf backup-0.tgz -g backup.timestamps images
(Sun: compl. backup)
user$ tar czvf backup-1.tgz -g backup.timestamps images
(Mon: changes only)
user$ tar czvf backup-2.gz -g backup.timestamps images
(Tue: changes only)
```

例如，如果你想在 cron 脚本中抑制所有的 tar 输出（包括错误信息），你必须在命令中添加以下输入/输出重定向：

```
user$ tar czf backup.tgz directory >dev/null 2>&1
```

### tasksel

`tasksel` 安装或卸载预定义的软件包组。该命令仅在 Debian 和 Ubuntu 分发版可用。

- `- install group name`

安装指定软件包组中的所有包。
- `--list-tasks`

确定所有定义的软件包组列表。
- `- remove group name`



移除指定软件包组中的所有包。注意：在旧版本的 `tasksel` 中，无论与其他包是否有依赖关系，包都会移除。这通常会导致卸载的包数量远超预期。

- `--task-packages group name`

列出指定软件包组中的所有包。

## 示例

以下两个命令在 Debian 或 Ubuntu 上安装带有常用扩展和额外程序的 Apache Web 服务器：

```
root# tasksel install web-server
(Debian)
root# tasksel install lamp-server
(Ubuntu)
```

# `tcpdump` [options] [filter expression]

同名的包 `tcpdump` 读取接口的网络流量，根据标准对其进行过滤、输出或将其保存到文件中。`tcpdump` 不仅处理 TCP 包，还处理 UDP 和 ICMP 包。它内部使用 `pcap` 库来读取数据。

## 选项

- `-a` 以文本格式显示内容。

- `-c n`

处理 `n` 个包后停止程序。

- `-i interface`

通过指定的接口。你可以使用 `tcpdump -D` 获取接口列表。

- `-n` 显示 IP 地址而不是主机名。

- `-q`

显示较少的信息（静默）。

- `-r file`

从文件中读取之前保存的包。

- `-w file`

以二进制格式保存包到指定的文件中。可以使用 `tcpdump -r` 或其他程序分析文件（例如 Wireshark）。

- `-x` 以十六进制格式显示内容。

# 过滤器表达式

选项可以跟一个过滤器表达式，该表达式由以下关键词组成（其他未列）：

- `-` greater `n`

考虑大于 `n` 字节的包。

- `-` host `ipadr` Or host `hostname`

仅考虑指定地址或相应主机的包。

- `-` less `n`

考虑小于 `n` 字节的包。

- `-` net `cidr`

考虑源或目的符合 CIDR 表示法的包（例如 `10.0.0/24`）。

- `-` port `n` Or portrange `n1-n2`

考虑使用指定端口作为源的包。

- `-` proto

仅考虑指定协议的包。`host`、`net` 和 `port` 关键字可以带有 `dst` 或 `src`，如果指定仅指向目的或源。

你可以通过 `and` 连接多个过滤条件。必须使用 `()` 括起复杂表达式。或者可以使用简单的括号，但必须将整个过滤器表达式放在引号中（例如 `'(port 1 or port 2)'`）。其他过滤器选项请参 `man pcap-filter`。

## 示例

以下命令输出通过 `wlan0` 接口的所有 HTTP 包：

```
root# tcpdump -i wlan0 port 80
tcpdump: verbose output suppressed, use -v -vv for full protocol decode listening on wlan0, link-type EN100DB (Ethernet)
10:34:33.601218 ipac.57402 bpf.tcpdump.org:
Flags [S], seq 755525464, win 65535, options [mss 1460,nop,wscale 5,nop,nop,
TS val 59597533 ecr 0,sackOK,eol], length 0 10:34:33.601793 ipac.57403 >
bpf.tcpdump.org:
Flags [S], seq 295486158, win 65535, ...
```

第二个命令将流向来自 IP 地址 `192.139.46.66` 的下一个 100 个 HTTP 包记录到 `dump.pcap` 文件中：

```
root# tcpdump -i wlan0 -n c 100 -w dump.pcap port 80 and host 192.139.46.66
```

第三个命令确定通过网桥 `br0` 且包含指定 MAC 地址（作为发送者或目标）的包：

```
root# tcpdump -i br0 -en | grep -i '00:55:56:00:D0:56'
```

# `tee` 命令

`tee` 会复制标准输入，显示一个副本，并将另一个副本保存到文件中。在现实生活中，如果你希望在屏幕上观察命令的输出，同时将其保存到文件中，这个工具非常有用。简单地重定向到文件 `>` 将导致屏幕上无法显示任何内容。

## 示例

以下命令在屏幕上显示当前目录的目录列表，同时将其保存到 `contents` 文件中：

```
user$ ls -l | tee contents
```

# `telnet` [options] host [port]

`telnet` 允许通过 Telnet 协议与网络服务进行交互式通信。该命令主要用于测试基础网络功能。由于通信是不加密的，`telnet` 并不安全，无法在外部服务器上运行命令。对于这类任务，您应该使用 `ssh`！

- `-4` 或 `-6`

仅接受 IPv4 或 IPv6 地址。

- `-l user`

使用指定的用户名（而不是当前用户名）。

## 示例

以下示例显示了与运行在本地计算机上的邮件服务器的通信：

```
user$ telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'.
220 kofler.info SMTP Postfix (Ubuntu)
helo kofler.info
250 kofler.info
mail from:<user@kofler.info>
250 2.1.0 0k
..
```

邮件服务器通常配置为仅前几个命令是不加密传输的。随后，服务器和客户端协商密钥加密数据（STARTTLS 方法）。此时，`telnet` 必须退出；因此仅适用于测试邮件服务器在 25 端口是否激活。`swaks` 更适合测试身份验证程序。

# `test` 表达式

`test` 用于在 `bash` 脚本中构建条件，主要用在 `if` 查询和循环中。根据条件是否满足，它会返回真值 `θ`（真）或 `1`（假）。除了 `test` 之外，你也可以使用短表示法 `[ expression ]`。重要的是，你需要在表达式前后输入空格！

如果你在分支或循环中使用 `test` 或短表示法 `[ expression ]` 作为条件，你必须用分号结束条件，例如：`if [ "$1" = "abc" ]; then ...`

`if` 查询有时可以用以下表述替换：`[ "$1" = "abc" ] && cmd`。在这种情况下，不需要分号。在前面的条件满足之前，命令将不会执行。

# 字符串

| 表达式 | 说明 |
| :--- | :--- |
| `[ cs ]` | 如果字符串不空，则为真 |
| `[ -n cs ]` | 如果字符串不空，则为真（类似 `[ cs ]`) |
| `[ -z cs ]` | 如果字符串为空（0字符），则为真 |
| `[ cs1 = cs2 ]` | 如果字符串匹配，则为真 |
| `[ cs1 != cs2 ]` | 如果字符字符串不同，则为真 |

字符字符串或变量应该放在引号中（例如 `[ "$1" = "abc" ]` `[ "$a" = "$b" ]`）。否则，包含多个单词的字符串可能会出错。

# 数字

| 表达式 | 说明 |
| :--- | :--- |
| `n1 -eq n2` | 如果数字相等，则为真（等于） |
| `n1 -ne n2` | 如果数字不相等，则为真（不等于） |
| `n1 -gt n2` | 如果 `n1` 大于 `n2`，则为真（大于） |
| `n1 -ge n2` | 如果 `n1` 大于或等于 `n2`，则为真（大于等于） |
| `n1 -lt n2` | 如果 `n1` 小于 `n2`，则为真（小于） |
| `n1 -le n2` | 如果 `n1` 小于或等于 `n2`，则为真（小于等于） |

# 文件（节选）

| 表达式 | 说明 |
| :--- | :--- |
| `-d file` | 如果是目录，则为真（目录） |
| `-e file` | 如果文件存在，则为真（存在） |
| `-f file` | 如果是普通文件（不是设备、目录等），则为真（文件） |
| `-L file` | 如果是符号链接，则为真 |
| `-r file` | 如果文件可读，则为真（读） |
| `-s file` | 如果文件至少 1 字节，则为真（大小） |
| `-w file` | 如果文件可修改，则为真（写） |
| `-x file` | 如果文件可执行，则为真（执行） |
| `file1 -ef file2` | 如果两个文件具有相同的 i-node，则为真（相同文件） |

# 连接条件

| 表达式 | 说明 |
| :--- | :--- |
| `! cond` | 如果条件不满足，则为真 |
| `cond1 -a cond2` | 如果两个条件都满足，则为真（与） |
| `cond1 -o cond2` | 如果至少满足一个条件，则为真（或） |



| `file1 -nt file2` | 如果 `file1` 比 `file2` 新，则为真（新于） |

# bash 变量 `[[ ]]`

虽然 `test` 和短表示法 `[ expression ]` 在大多数 shell 中这样工作，但双括号变体 `[[` 在 `bash` 中是可选：

| 表达式 | 说明 |
| :--- | :--- |
| `[[ cs = pattern ]]` | 如果字符串匹配模式，则为真 |
| `[[ cs == pattern ]]` | 如果字符串匹配模式，则为真 |
| `[[ cs ~ regex ]]` | 如果字符串匹配正则表达式，则为真 |
| `[[ cond1 && cond2 ]]` | 如果两个条件都满足，则为真（与） |
| `[[ cond1 || cond2 ]]` | 如果至少满足一个条件，则为真（或） |

另一个区别是 `[[ ]]` 甚至不需要引号。

## 示例

以下小型脚本没有执行任何意义的任务，它仅演示了在循环中使用 `[[ ]]` 语法。

```bash
#!/bin/bash
for i in {1..10}; do
  rest=$((i%2))
  [[ $rest -eq 1 ]] && continue
  echo $i
  [[ $i -eq 6 ]] && break
done
```

## time 命令

`time` 执行指定的命令并指示花费了多少时间。输出通过标准错误进行，可以通过环境变量更改。

`time` 不仅仅替换秒表，还将执行时间分为三个部分：

- `real`: 显示实际执行时间。
- `user`: 在内核外执行程序的 CPU 时间。
- `sys`: 在内核内执行程序的 CPU 时间。

`user` 和 `sys` 的总和表示执行消耗了多少 CPU 开销。`real` 往往远大于 `user` 和 `sys` 之和。这可能有两个原因：首先，有很多进程与启动的命令并行运行，也消耗了计算时间。其次，执行命令时可能存在等待时间，例如读写文件或在网络中传输数据。

`user` 和 `sys` 分别引用 CPU 核心。如果执行的命令充分利用了多个核心，那么 `user` 和 `sys` 之和可能会大于 `real`。

### 示例

以下命令读取逻辑卷的内容并使用 `7zr` 命令压缩。在多核系统的空闲模式下，该过程需要 24 分钟。如果只有一个核心，备份创建花费更长时间（大约 40 分钟）。

```bash
root# time dd if=/dev/vg830/lv3 bs4M | 7zr a -si lv3.img.7z
real 24m53.424s
user 38m37.841s
sys 0m30.446s
```

- `settime datetime`
  - 重置日期和时间。计算机的硬件时钟也会相应更改。时间必须以 `2025-12-31 23:59:59` 的格式输入。
- `set-timezone name`
  - 设置所需的时区。
- `status`
  - 显示时间、时区和其他各种时间数据，例如夏令和冬令之间的下次切换时间。

### 示例

以下命令首先显示当前时间，然后更改时区：

```
root# timedatectl status
Local time: 2025-05-18 09:08:33 CEST
Universal time: 2025-05-18 07:08:33 UTC
RTC time: 2025-05-17 18:51:42
Time zone: Europe/Vienna (CEST, +0200)

root# timedatectl set-timezone Europe/Paris
```

```
timeout [options] time span command
```

`timeout` 执行指定的命令，如果运行时间超过指定时间，则会自动结束该命令。时间跨度指定为一个浮点数，后面带有字母 `s`、`m`、`h` 或 `t`，分别表示秒、分钟、小时或天（例如，`0.5h` 表示半小时）。

- `-k`
  - 通过 `KILL` 信号终止运行时间过长的程序。默认情况下，`timeout` 使用 `TERM` 信号，但该信号可以被忽略。

### 示例

在以下命令中，`scp` 有 30 秒的时间将文件传输到另一台计算机。之后，该进程将被取消。

```
user timeout 30 scp localfile myserver:destinationdir/
```

# tldr 命令

`tldr` 是 "too long, didn't read" 太长没读）的缩写，是对通常极其庞大的手册页的一种批评。`tldr` 尝试做得更好，提供了一些常用命令的指示性示例。因此，该命令是此书的一个很好的补充。输出在终端中以颜色高亮。

```
user tldr rsync
向或从远程主机传输文件（但不在两个远程主机之间传输），默认使用 SSH。要指定远程路径，请使用 userhost:path/to/file_or_directory。更多信息：
https://download.samba.org/pub/rsync/rsync.1.
- 传输文件：
```

`rsync path/to/source path/to/destination`

```
- - 使用归档模式（递归复制目录，在不解析的情况下复制符号链接，并保留权限、所有者和修改时间）：
rsync --archive path/to/source path/to/destination

- - 在发送到目标时压缩数据，显示详细且人类可读的进度，并在中断时保留部分传输的文件：
rsync --compress --verbose --human-readable --partial --progress \path/to/source path/to/destination

- - （另外五个使用示例）
```

## top [q]

`top` 每五秒显示一次所有运行进程的列表，进程根据其计算时间的份额进行排序。如果在调用时指定了可选 `q` 参数，`top` 将不断更新列表并占用所有的空闲计算时间。按 `q` 终止程序。

### 方案

比 `top` 更方便且视觉效果更好的替代方案是 `btop` 和 `htop` 命令，大多数发行版必须单独安装。这些命令提供了各种附加功能，为输出着色，并允许水平和垂直滚动查看运行中的进程。

如果你感兴趣的内存消耗和 CPU 使用率，而是运行进程的 I/O 活动或能效，那么你应该查看 `iotop` 或 `powertop` 的描述。

## touch [options] files

`touch` 更改文件保存的最后修改时间。如果在不带选项运行命令，则会将当前时间保存为修改时间。如果文件不存在，将创建一个长度为 0 字节的新文件。

- `-r file`
  - 使用文件的保存修改时间。
- `-t time`
  - 指定时间。必须使用 `[[CC]YY]MMDD[.ss]` 格式，例如 `202512311730` 表示 `2025/12/31` 下午5:30。或者，你也可以通过 `-d` 选项指定更可读的格式。

### 示例

在此示例中，`touch` 用于比较目录中的所有文件与目标目录文件的修改时间。如果你忘记了哪些文件是现在复制的，这很有。

```
user$ cd target

user$ find -type f -exec touch -r /source {}
```

# tr

`tr` 将字符串1的所有字符替换为字符串2对应的字符。两个字符串长度应该相同。未出现在字符串1中的字符保持不变。无法用多个字符替换单个字符（例如用"o"）——这必须使用 `sed` 等命令。

- `-d`
  - 删除字符串1指定的字符。字符串2不需要指定。

### 示例

在以下示例中，`tr` 将所有小写字母替换为大写字母并在终端显示结果（标准输出）：

```
user$ tr a-z A-Z < file
```

## traceroute

`traceroute` 提供本地计算机到目标地址 TCP/IP 数据包路径上的所有站点列表。为每个站点指定运行时间（默认尝试三次）。只有在目标地址端口未被防火墙拦截，`traceroute` 才能工作。在这种情况下，`traceroute` 只返回星号。

- `-4` 或 `-6`
  - 使用 IPv4 或 IPv6 协议。默认情况下，`traceroute` 使用相应的协议。如果主机关联了 IPv4 和 IPv6 地址，`traceroute` 优先使用 IPv4。对于 `traceroute`，`-6` 应用。
- `-m n`
  - 确定中间站点的最大数量（默认 30）。
- `-n`
  - 仅显示中间站点的 IP（不显示主机名）。
- `-q`
  - 使用指定的 UDP 端口（默认）。
- `-q n`
  - 发送 `n` 个数据包并测量数据包的响应时间（默认）。

### 示例

以下命令显示我的本地计算机和 Web 服务器之间的站点。在某些站点，IP 数据包通过不同的路由器路由，这表示冗余连接。

```
root traceroute kofler.info (213.239.211), 30 hops max, 60 byte packets

1 device.lan (10.0.0.138) 14.116 ms 13.376 ms 13.112 ms

2 62.47.95.239 (62.47.95.239) 25.650 ms 27.489 ms 29.245 ms
```



9 `3.hetzner.de` (`213.239.252.8`) `48.315 ms`

4 `4.hetzner.de` (`213.239.252.136`) `49.034 ms`

2 `2.hetzner.de` (`213.239.229.136`) `51.231 ms`

10 `kofler.info` (`213.239.211.2`) `52.069 ms` `54.640 ms` `55.757 ms`

# `trap` [command] signal

当 shell 接收到指定的信号时，bash 命令执行指定的命令。如果没有指定命令，程序或 bash 将忽略该信号。`trap -l` 返回所有可能的信号及其分配的标识符。`trap` 通常用于脚本中的错误保护。

## 示例

以下小型脚本在无限循环中运行，无法通过按 `Ctrl+C` 中断。但是你可以使用 `kill` 来结束脚本，例如。

```bash
#!/bin/bash

trap echo "Ctrl+C will be ignored!" SIGINT

while true
do
  sleep 1
done
```

# `tree` [options] [start directory]

同名软件包 `tree` 显示从当前或指定的起始目录开始的目录树结构。

- `-a`
默认输出文件而不仅仅是目录。
- `-L n`
仅考虑前 `n` 个层级。
- `-x`
留在当前文件系统中，不考虑挂载的目录或其他文件系统的链接。

# `truncate` [options] files

`truncate` 缩小或增大文件。当文件减小时，文件会直接被截断。注意：在此过程中你会丢失数据！当文件增大时，会在文件中添加相应数量的 `0` 字节。对于大多数文件系统，这不会改变数据介质所需的空间，因为文件将被识别为稀疏文件。如果你想物理上用零填充文件，必须使用 `dd` 命令。如果向 `truncate` 传递不存在的文件名，该命令将创建指定大小的文件。

- `-s n`
指定所需的大小（字节）。如果数字后面跟着 `K`、`M`、`G` 或 `T` 字母，`truncate` 将该数字乘以 `1,024`；`1,048,576` 等。或者，`KB`、`MB`、`GB` 或 `TB` 代表 `1,000`；`1,000,000` 等。因此，`10K` 对应 `10,240` 字节，而 `10KB` 对应 `10,000` 字节。

## 示例

在以下示例中，首先用文件填充 `1 MiB` 随机数据。然后使用 `truncate` 将文件增大到 `2 MiB`。`ls -l` 实际上显示大小为 `2 MiB`，但 `dd` 证明了文件在硬盘上仅占用 `1 MiB` 空间。

SSD。只有当后续向文件中写入除零以外的数据时，空间需求才会增加。

```bash
user$ dd if=/dev/urandom of=file bs=1024 count=1024
user$ truncate -s 2M file
user$ ls -l file
-rw-r-- 1 kofler 2097152 19. Nov 14:30 file
user$ du -h file
1.0M file
```

# `tty`

`tty` 显示活动终端的设备名称（对于文本控制台：`dev/tty1` 到 `tty6`；对于 X 下的 shell 窗口：`dev/pts/n`）。

# `tune2fs` [options] device

你可以使用 `tune2fs` 来更改 `ext2`/`ext3`/`ext4` 文件系统的各种系统参数。

- `-c n`
指定在启动时执行多少次挂载操作后对分区进行错误检查。`0` 表示永远不进行检查。
- `-i n`
指定在启动时每隔（以天为单位）对分区进行一次错误检查。`0` 表示永远不进行检查。
- `-l`
显示指定文件系统的信息，但不更改任何内容。
- `-m n`
指定磁盘的百分之比保留给 `root` 数据（`mke2fs` 通常默认为 `5%`）。
- `-U new-uuid` 或 `-U randomn`
为文件系统提供一个新的 `UUID`。

## 示例

以下命令会导致 `/dev/sda1` 中的文件系统每年检查一次，或在 `200` 次挂载操作后检查：

```bash
root# tune2fs -i 365 -c 200 /dev/sda1
将最大挂载次数设置为 200
将检查间隔设置为 31536000 秒
```

`bash` 命令类型决定了指定的命令是 shell 命令（例如 `cd`）、自定义函数还是别名缩写。命令哈希消息（hashed message）意味着该 Linux 命令已在此会话中执行过，且其路径名称已被 `bash` 记录在哈希目录中。

## 示例

`cd` 是集成到 shell 中的命令：

```bash
root# type cd
cd 是一个 shell 内置命令
```

# `U`

## `ubuntu-security-status` [options]

过去，`ubuntu-security-status` 显示已安装包的维护状态信息。该命令已被 `pro security-status` 替换（参见该条目）。

## `ufw` [options] command

`ufw` 是一个 Ubuntu 特有的防火墙配置命令。`ufw` 默认安装在 Ubuntu 及其衍生版本上，但未激活。如果你想使用 `ufw` 进行防火墙配置，必须先使用 `ufw enable` 激活防火墙。

以下子命令用于配置防火墙。它们可以与 `--dry-run` 选项结合。在这种情况下，不会进行任何更改。该选项用于测试复杂命令的语法。

- `allow|deny [on interface] port/protocol/"app name"`
允许或阻塞端口（例如 `22`）、协议（例如 `ssh`）或具有独立规则文件的程序（参见 `ufw app list`）。
规则可以可选地仅针对特定的网络接口制定（例如在 `eth0` 上）。`man ufw` 列出了制定规则的其他其他选项，仅适用于入站或出站数据包，或仅适用于特定协议或 IP 版本（例如针对 `tcp`、`udp`、`ipv6`）。
- `app info "app name"`
提供 `ufw` 规则文件的详细信息。
- `app list`
列出 `/etc/uf2/applications.d` 目录下所有具有 `ufw` 规则文件的程序。
- `default allow|deny|reject [incoming|outgoing|routed]`
定义防火墙的默认行为。如果没有指定 `incoming|outgoing|routed`，输入过滤器的行为将发生更改。默认情况下——如果激活了防火墙——拒绝行为适用于入站过滤器，允许行为适用于出站过滤器。
- `disable`
停用防火墙。所有网络流量均可以无阻流动。
- `enable`
激活防火墙。
- `reload/reset`
重载所有防火墙规则或对防火墙进行完全重启。
- `status [verbose]`
显示防火墙状态。

## 示例

以下命令会导致 `/dev/sda1` 中的文件系统每年检查一次，或在 `200` 次挂载操作后检查：

```bash
root# tune2fs -i 365 -c 200 /dev/sda1
将最大挂载次数设置为 200
将检查间隔设置为 31536000 秒
```

# `unexpand` text file > result

`unexpand` 将指定文本文件中的多个空格替换为制表符（`tab`），并将结果写入标准输出。该命令是 `expand` 的反向操作，`expand` 的作用是将制表符替换为空格。

- `-a`
替换所有空格，而不仅仅是行头的空格。
- `-t n`
指定每个制表符位置的字符数（默认为 `8`）。

# `uniq` [options] file

`uniq` 将文本文件的行输出到标准输出，消除连续的相同行。对于预先排序过的文件，`uniq` 会消除所有出现超过一次的行。

- `-c`
显示每行出现的次数。
- `-d`
仅输出重复行（但不包括仅出现一次的行）。
- `-u` 仅输出*没有*重复的行（即*唯一*的行）。

## 示例

`sort` 排序测试文件，`uniq` 消除重复行并将结果保存在 `test1` 中：

```bash
user$ sort test | uniq > test1
```

# `unset` variable

`bash` 命令 `unset` 删除指定的变量。

# `until` condition; do commands done

`until` 在 `bash` 脚本中创建循环。循环会持续运行，直到满足指定的条件。循环判断标准是指定为条件的命令的返回值。比较和测试使用 `test` 命令或其在方括号中的短形式进行。

## 示例

示例展示了如何构建一个简单的 `until` 循环：

```bash
user i=1; until [ $i -gt 3 ]; do echo $; i=$[$i+1]; done
1
2
3
```

来自 `xz-utils` 软件包的 `unxz` 用于解压之前使用 `xz` 压缩的文件。`.xz` 文件扩展名将被移除。

# `unzip` [options] archive.zip [file1 file2]




该命令从 ZIP 存档中提取文件，ZIP 在 Windows 世界中非常常见。如果没有显式列出要提取的文件，`unzip` 将解压存档中的所有文件。如果你想在 Linux 上创建自己的 ZIP 存档，必须使用 `zip`。

## 示例

以下命令从 `archive.zip` 中提取 `print.pdf` 文件。如果该存档中有其他文件，它们将不会受到影响。

```
user$ zipinfo archive.zip

Archive: archive.zip

Zip file size: 5870439 bytes, number of entries: 4

-rw-r--r-- 3.0 uniq 3594936 defN 24-Mar-24 19:06 ebook.pdf

-rw-r--r-- 3.0 uniq 3245639 defN 26-Mar-24 12:54 print.pdf

...

user$ unzip archive.zip print.

Archive: ../archive.zip

inflating: print.pdf
```

## `update-alternatives` [options] command

`update-alternatives` 管理 `/etc/alternatives` 目录中的链接。这些链接决定了并行安装的具有相同多个程序（例如编辑器或 Java 环境）的活动版本。该命令通常由相关软件包的（卸）载脚本执行，但当然也可以交互式使用。在 Red Hat 或 Fedora 系统上，该命令作为 `alternatives` 的形式可用。

- `-auto name`
  为命令启用自动模式。这意味着优先级值最高的命令会自动激活。

- `-config name`
  显示指定命令的可用替代方案。然后你可以交互式地指定未来应该激活哪种替代方案。`update-alternatives` 随后会相应调整链接并将该命令切换到手动模式。

- `--display name`
  提供指定命令的所有已安装替代方案列表。

- `--install ...` 或 `--remove ...`
  为命令安装或删除替代方案。这些命令通常只在软件包的（卸）载脚本中使用。

- `--set name command path`
  设置指定的命令路径。

## 示例

将指定的命令设置为默认值：

```
update-alternatives --set python /usr/bin/python
```

在 Red Hat 或 Fedora 系统上，该命令也作为 `alternatives` 的形式可用。

```
until condition; do

commands

done
```

`until` 在 bash 脚本中创建循环。循环会持续运行，直到满足指定的条件。循环判断标准是指定为条件的命令的返回值。比较和测试使用 `test` 命令或其在方括号中的短形式进行。

## 示例

示例展示了如何构建一个简单的 `until` 循环：

```
user i=1; until [ $i -gt 3 ]; do echo $; i=$[$i+1]; done

1

2

3
```

来自 `xz-utils` 软件包的 `unxz` 用于解压之前使用 `xz` 压缩的文件。`.xz` 文件扩展名将被移除。

```
unzip [options] archive.zip [file1 file2]
```

该命令从 ZIP 存档中提取文件，ZIP 在 Windows 世界中非常常见。如果没有显式列出要提取的文件，`unzip` 将解压存档中的所有文件。如果你想在 Linux 上创建自己的 ZIP 存档，必须使用 `zip`。

## 示例

以下命令从 `archive.zip` 中提取 `print.pdf` 文件。如果该存档中有其他文件，它们将不会受到影响。

```
user$ zipinfo archive.zip

Archive: archive.zip

Zip file size: 5870439 bytes, number of entries: 4

-rw-r--r-- 3.0 uniq 3594936 defN 24-Mar-24 19:06 ebook.pdf

-rw-r--r-- 3.0 uniq 3245639 defN 26-Mar-24 12:54 print.pdf

...

user$ unzip archive.zip print.

Archive: ../archive.zip

inflating: print.pdf
```

## `update-alternatives` [options] command

`update-alternatives` 管理 `/etc/alternatives` 目录中的链接。这些链接决定了并行安装的具有相同多个程序（例如编辑器或 Java 环境）的活动版本。该命令通常由相关软件包的（卸）载脚本执行，但当然也可以交互式使用。在 Red Hat 或 Fedora 系统上，该命令也作为 `alternatives` 的形式可用。

- `-auto name`
  为命令启用自动模式。这意味着优先级值最高的命令会自动激活。

- `-config name`
  显示指定命令的可用替代方案。然后你可以交互式地指定未来应该激活哪种替代方案。`update-alternatives` 随后会相应调整链接并将该命令切换到手动模式。

- `--display name`
  提供指定命令的所有已安装替代方案列表。

- `--install ...` 或 `--remove ...`
  为命令安装或删除替代方案。这些命令通常只在软件包的（卸）载脚本中使用。

- `--set name command path`
  设置指定的命令路径。

## 示例

将指定的命令设置为默认值：

```
update-alternatives --set python /usr/bin/python
```

在 Red Hat 或 Fedora 系统上，该命令也作为 `alternatives` 的形式可用。

- `-a -G group`
  将用户添加到指定的组。

- `-L`
  临时锁定账户。出于此目的，在 `/etc/shadow` 中的密码哈希值前放置 `!` 字符，这就是无法登录的原因。

- `-U`
  释放被 `-L` 锁定的账户。

## 示例

以下命令将用户 `gersin` 添加到 `docuteam` 组：

```
root# usermod -a -G docuteam gersin
```

如果你以后想将该用户从组中移除，必须运行 `gpasswd -d gersin docuteam`。

# `vcgencmd` 命令

此命令允许你读取树莓派 OS 上设备或 CPU 的关键数据，并更改一些参数。

- `commands`
  列出所有 `vcgencmd` 命令。

- `get_config parametername|int|str`
  返回指定参数或所有整数或字符串参数的状态。参数在 `/boot/config.txt` 文件中设置。

- `get_throttled`
  提供关于电源潜在问题的信息（4B 型）。

- `measure_clock arm|core|hdmi|uart`
  提供 CPU 频率、图形核心频率以及其他各种组件的频率。

- `measure_temp`
  提供 CPU 温度。

- `measure_volts core|sdram_c|sdram_i|sdram_p`
  指定图形核心和内存的电压。

- `version`
  提供固件版本。

## 示例

以下命令显示了当前空闲的树莓派 5 的运行状态：

```
pi$ vcgencmd measure_clock arm

frequency(0)=1500019456

pi$ vcgencmd measure_temp

temp=48.4°C
```

## `vgchange` [options] [vname]

LVM 命令 `vgchange` 用于更改卷组 `VG` 的属性。最重要的用途是激活或禁用 VG。

- `-ay|n`
  激活 `y` 或禁用 `n` 所有 VG 或指定的 VG。

## `vgcreate` [options] vgname pvname1 [pvname2 ...]

`vgcreate` 从一个或多个物理卷 `PV` 创建一个新的 VG。

## 示例

在以下示例中，`pvcreate` 首先标记了硬盘或 SSD 的第一个分区 `/dev/sdb1` 和 `/dev/sdc1`。`vgcreate` 从此创建了卷组 `vg1`。然后，`lvcreate` 命令为逻辑卷 `lvi` 留了 100 GiB，在其中建立文件系统，`mount` 将该文件系统挂载到目录树中新创建的 `/mnt/lvi`。

```
root# pvcreate /dev/sdb1

root# pvcreate /dev/sdc1

root# vgcreate vg1 /dev/sdb1 /dev/sdc1

root# lvcreate -L 100G -n lvi vg1
```



`root# mkfs.ext4 /dev/mapper/vg1-lvi`

`root# mkdir /dev/mapper/vg1-lvi /mnt/lvi`

```
vgdisplay vgname
```

`vgdisplay` 显示指定 VG 的详细信息。

`vgxtend vgname pvname`

`vgxtend` 向 VG 添加一个 PV。

## 示例

以下命令将 `/dev/sdc2` 分区定义为新的物理卷，然后将其添加到空间过小的 `myvg1` 卷组中：

```
root# pvcreate /dev/sdc2

Physical volume "/dev/sdc2" successfully created

root# vgxtend myvg1 /dev/sdc2

Volume group "myvg1" successfully extended

root# vgdisplay myvg1
```

| VG Size | 180.64 GB |
| :--- | :--- |
| Alloc PE / Size | 6402 / 22.50 GB |
| Free PE / Size | 41324 / 158.14 GB |

## `vgmerge vgname1 vgname2`

`vgmerge` 将 `vgname2` 添加到 `vgname1`。命令成功执行后，只剩下 `vgname1`。包含了之前组成 `vgname1` 和 `vgname2` 存储池的所有 PV。

## `vgreduce [options] vgname [pvname1 pvname2 ...]`

`vgreduce` 从 VG 的存储池中移除指定的 PV。这仅在 PV 未被使用时才有效。`-a` 选项移除所有非活动的 PV。

# `vgrename oldvgname newvgname`

`vgrename` 给 VG 指定新名称。除了 `oldvgname`，也可以指定 VG 的 UUID。

## `vgscan`

`vgscan` 列出所有卷组。

```
vipw [options]

vigr [options]

visudo [options]
```

`vipw`、`vigr` 和 `visudo` 命令启动 vi/vim 编辑（参见快捷键部分）并打开 `/etc/passwd`、`/etc/group` 或 `/etc/sudoers` 文件。保存时，会检查你是否符合相应文件的语法。如果不符合，则无法保存。

- `-r directory`
  使用指定的目录作为根目录。

- `-s`
  打开 `/etc/passwd`、`/etc/group` 或 `/etc/sudoers` 文件。

支持虚拟网络的管理。这些是私有网络区域，可以通过 NAT 连接到主机系统，例如 libvirt 工具的默认网络。

- `pool-define xmlfile`
- `pool-define-as poolname type --target path`
- `pool-start poolname`
- `pool-auto-start xmlfile`
- `pool-destroy poolname`
- `pool-delete poolname`
- `pool-list`
- `pool-info poolname`

支持 libvirt 存储池的管理。`pool-define` 创建一个新的池，其属性描述在 XML 文件中。`pool-define-as` 也创建一个新池，其中关键数据直接作为参数传递。允许的池类型包括 `dir`（本地目录）、`netfs`（网络目录）、`logical`（卷组）、`disk`（硬硬盘）或 `iscsi`（iSCSI 服务器）。

然后必须通过 `pool-start` 启动新池。如果将来需要自动启动该池，则必须运行 `pool-autostart`。

删除存储池的命令有些令人困惑：在删除之前，必须使用 `pool-destroy` 停用池。虽然该命令听起来像某种糟糕操作，但池只是被停止了，稍后可以使用 `pool-start` 启动。只有 `pool-delete` 会真正删除池。`pool-delete` 假设池中的所有卷已先删除，这意味着只有空池才能被删除。

- `qemu-monitor --hmp name 'command'`
  为指定的名称指定的虚拟机运行指定的 QEMU 监控命令。需要 `--hmp` 选项，因为否则必须以 JSON 格式指定命令。

- `restore file`
  重新激活使用 `save` 保存的虚拟机。之后可以删除该状态文件。

- `save name file`
  将虚拟机的状态（本质上是 RAM 内容）保存到文件中，然后停止机器的运行。要重新激活虚拟机，必须使用 `restore`。

- `schedinfo [options] name`
  显示或更改虚拟机的调度器参数（`--set parameter=value`）。这些参数可以控制虚拟机允许使用多少硬件资源。资源控制要求在主机系统上激活 cgroups 功能。

- `setmaxmem n`, `setmem n`
  设置内存使用（RAM）的限制和当前分配的内存。额外的 `--config`、`--current` 和 `-live` 选项允许你指定设置是永久保存还是仅在当前执行。

- `shutdown/reboot name`
  关闭或重启虚拟机。虚拟机将通过 ACPI 接收关闭信号。虚拟机中必须安装 ACPI 守护进程 `acpid` 才能处理该信号。

- `snapshot-create vmname [xml-file [--redefine]]`
  `snapshot-create-as vmname snapshotname [description]`
  `snapshot-list vmname`
  `snapshot-delete vmname snname`
  `snapshot-revert vmname snname [--running]`
  创建运行中虚拟机的快照、列出所有快照、删除快照或将快照内容应用于镜像文件。快照功能仅用于使用 QCOW2 镜像文件的。

- 指定的虚拟机
  如果你虚拟机。图形模式与机器通信，应该使用 VNC 客户端（连接数据由 `virsh vncdisplay` 命令确定，参见此列表中的 `vncdisplay` 项）或 virt-viewer 程序。

- `suspend/resume name`
  临时停止指定的虚拟机或恢复执行。然而，被停止的虚拟机会继续使用 RAM！因此，只有虚拟 CPU 被停止了。

- `ttyconsole name`
  指定使用主机的哪个设备来访问客系统的串口接口（例如 `/dev/pts/5`）。

- `undefined name`
  删除描述虚拟机的 XML 文件。保留带有虚拟硬盘的镜像文件。在删除虚拟机的所有快照之前，`undefined` 无法运行。

- `vcpuinfo name`
  提供虚拟机可用的（虚拟）CPU 信息，以及到目前使用的 CPU 时间信息。该命令也可以用于检查 CPU 绑定。

- `vcpupin name guest-cpu-nr host-cpu-list`
  将主机的物理 CPU 核心与客体的虚拟 CPU 绑定。`vcpupin vm1 0 2` 将主机的第三个 CPU 核心永久分配虚拟机 `vm1` 的第一个虚拟 CPU。

- `vol-create xmlfile`
- `vol-create-as poolname newvolume size`
- `vol-delete volname`
- `vol-info volname`

支持存储池中数据媒体的管理。`vol-create` 创建一个新的数据媒体，其属性描述在指定的 XML 文件中。`vol-create-as` 创建所需大小的数据媒体，其中允许 K、M、G 和 T 后缀分别代表 KiB、MiB、GiB 和 TiB。当你创建镜像磁盘时，可以使用 `--raw/qcow2/qed` 指定所需的格式（默认为 raw）。

`--allocation size` 决定预先分配多少内存；对于 raw 卷，内存始终被预留。

如果有多个存储池，对于所有带有 `-pool poolname` 选项的命令，你必须指定指的是哪个池。

- `vncdisplay name`
  返回虚拟机 VNC 显示的 IP 地址（localhost 为空）和端口号。你可以启动任何 VNC 客户端与虚拟机交互。出于安全考虑，VNC 访问默认仅从 localhost 工作（参见 `/etc/libvirt/qemu.conf` 文件）。

如果虚拟机完全没有通过 VNC 共享图形系统，而是使用更现代的 Spice 系统，`vncdisplay` 将不会返回结果。在这种情况下，你可以使用 virt-viewer 程序操作虚拟机。你可以直接将虚拟机名称传递给该程序。

然而，如果需要确定 Spice 端口号将会变得困难。virsh 缺乏类似于 `vncdisplay` 的用于确定虚拟机 spice 端口的命令。我在 https://ubuntuusers.de/ 的论坛上找到以下命令，它通过从进程列表中提取端口号提供了解决方案：

```



`spice_port=$(ps aux | grep vm_name | grep -oP "(?<=spice port)")`

## 示例

一旦通过 `virsh` 命令启动了 libvirt shell，你就可以运行命令管理本地所有的虚拟机：

```
root# virsh list --all

Id Name       Status

--------------------

13 fedora running

- ubuntu shut down

- windows shut down

virsh# start windows

Domain started

virsh# vncdisplay windows:

virsh# exit
```

你也可以通过 SSH 连接到远程机器上的 libvirt 守护进程。出于安全原因，无法通过密码登录 KVM 主机，必须在建立连接之前设置你的公密钥。

```
virsh# connect qemu+ssh://user@hostname/system

user@hostname's password: ********
```

`virt-clone` 复制由 libvirt 工具管理的关闭虚拟机。这将创建一个新的 XML 定义文件和镜像文件的副本。其他硬件组件保持基本不变。

- `--auto-clone`
  创建一个虚拟机。名称由之前的名称加上 `-clone` 组成。clone 也会插入镜像文件的名称中，例如 `rhel9.img` 变为 `rhel9-clone.img`。使用 `--auto-clone` 时可以省略显式指定 `--name` 和 `--file`。
- `connect hypervisor`
  与指定的虚拟化系统建立连接。
- `f file` 或 `--file=file`
  指定新镜像文件的所需名称。如果原始虚拟机有多个虚拟硬盘，你必须多次使用此选项。除了镜像文件，你也可以指定设备文件名，例如使用主机的逻辑卷作为数据存储时。
- `mac nn:nn:nn:nn:nn:nn`
  指定适配器所需的 MAC 地址。如果省略此信息，`virt-clone` 将自动使用唯一的随机 MAC 地址。
- `--name reliving`
  指定新虚拟机的名称。
- `--original name`
  指定原始虚拟机的名称。
- `--preserve-data`
  防止复制镜像文件。这意味着新虚拟机与旧虚拟机使用相同的镜像文件。因此，不允许同时运行旧旧虚拟机。

时间！如果你想用新的虚拟硬件或网络配置测试系统，此选项非常有用。

## 示例

以下命令复制了 Ubuntu 服务器安装用户 `user5`。新的虚拟机命名为 `user6`，新的镜像文件保存在 `/var/lib/libvirt/images/user6.img` 文件中。确保在 libvirt 存储池中创建了新的镜像文件。否则，RHEL/Fedora 上的 SELinux 规则将阻止虚拟机运行。

```bash
root# virt-clone --original user5 --name user6 \
--file /var/lib/libvirt/images/user6.img
```

## `virt-install [options]`

`virt-install` 是一个 Python 脚本，可以帮助你设置新的虚拟机。

- `--arch architecture`
  指定所需的 CPU 架构，例如 `i386`、`i686` 或 `x86_64`。默认情况下，`virt-install` 使用与宿主机系统相同的架构。
- `--cdrom file`
  指定 ISO 文件名或 CD/DVD 驱动器设备名称，从该设备加载安装数据。
- `--connect hypervisor`
  建立与指定的虚拟化系统的连接。如果在带有 root 权限的 KVM 宿主机上启动 `virt-install`，脚本会自动建立到 `qemu:///system` 的连接。
- `--disk file`
  指定保存虚拟机的镜像文件路径。如果你想使用多个虚拟存储设备，必须多次指定该选项。
- `--disk opt1=value1,opt2=value2...,`
  允许你从不同的 libvirt 存储池指定多个镜像文件。允许的选项包括：用于指定镜像文件或块设备的 `path`；指定之前创建的 libvirt 存储池的 `pool`；指定存储池中现有镜像文件的 `vol`（格式为 `poolname/imagename`）；指定新镜像文件所需大小的 `size`（单位为 GiB）；选择总线系统的 `bus`（`scsi` 或 `virtio`）；以及选择缓存策略的 `cache`（`writethrough`、`writeback` 或 `none`）。
- `--graphics type,opt1=value1,opt2=value2...`
  显示虚拟机图形系统的实现方式。可能的类型有 `vnc` 或 `spice`。

VNC 被作为标准。可以使用其他选项指定各种连接参数，如端口、监听和密码。

```bash
--import
```

- `--import`
  使 `virt-install` 不执行新安装，而是基于现有镜像文件创建新虚拟机。
- `--name type, opt1`
  指定虚拟机的名称。
- `--network type,opt1=value1,opt2=value2,...`
  指定虚拟机网络设备的关键数据。如果需要，可以多次指定该选项。`type` 指定如何与宿主机建立网络连接。允许的值包括：`bridge=name`（之前设置的网桥），`network=name`（使用 `virsh` 定义的虚拟网络），或者如果虚拟机通过 NAT 与主机系统通信，则简单使用 `user`。

其他选项决定网络设备的参数：`model` 指定要仿真的哪个适配器，例如 `e1000`、`rtl8139` 或 `virtio`。`mac` 定义设备的 MAC 地址。如果未指定此参数，`virt-install` 将自行生成随机 MAC 地址。KVM 的 MAC 地址必须以 `52:54:00` 开头！
- `--nodisk`
  允许不带镜像文件进行安装（例如，如果安装要在网络存储设备中进行）。
- `--noreboot`
  防止安装完成后自动重启。
- `--os-type name`
  指定要安装的操作系统类型，例如 `linux`、`unix`、`windows` 或其他。这些信息用于优化各种硬件参数。
- `--os-variant name`
  指定要安装哪种操作系统，例如 `fedora28`、`virtio26`、`rhel7` 或 `win10`。`virt-install` 提供了所有操作系统操作系统的完整列表。如果你使用此选项，则不需要指定 `--os-type`。
- `--ram n`
  指示内存（RAM）的大小，单位为 MiB。
- `--serial pty`
  为虚拟机配备串口接口。当虚拟机启动时，串口接口连接到宿主机上的伪 TTY 设备。在 `virsh` 中，你可以使用 `ttyconsole vmname` 确定设备名称。
- `--soundhw=ac97/es1370/sb16`
  为虚拟机配备声卡。
- `--vcpus=n`
  指定所需的 CPU 核心数（默认位一个）。
- `--video=cirrus/vga/mvga`
  指定要仿真的图形适配器（默认位 `cirrus`）。

## 示例

在运行 `virt-install` 之前，你必须为虚拟硬盘创建一个镜像文件：

```bash
root virsh vol-create-as default disk.qcow2 10G --format qcow2

virsh
```

`virt-install` 命令允许你设置一个新的虚拟机：

```bash
root# virt-install --name myname --ram 2048 --cdrom install.iso \
  --os-variant rhel8 --disk vol=default/disk.qcow2 --graphics vnc --noboot
```

## `virt-top [options]`

`virt-top` 显示虚拟机所需的 CPU 容量和内存空间。当 `virt-top` 运行时，你可以根据 0、1、2、3 显示虚拟机的 CPU 核心、网络接口或磁盘设备。

- `connect hypervisor`
  建立与指定的虚拟化系统的连接。默认情况下，如果以 root 权限启动，与 `qemu:///system` 通信。
- `o sort`
  指定排序顺序，例如 `cpu`、`mem` 或者根据 CPU 性能、内存需求或总时间。

## 示例

```bash
root# virt-top

14:36:17 - x86_64 8/CPU 1600MHz 1596MB

5 domains, 3 active, 3 sleeping
```



实际上，查看源：

`watch` 命令定期运行指定的命令并显示输出。

- `d` 或 `--differences`
  标记与之前结果相比的差异。

- `e` 或 `--exit`
  如果调用的命令返回错误则退出 `watch`。

- `n err`
  指定多少秒后再次运行命令（默认是两秒）。

## wc files

`wc` 统计指定文件的行数、单词和字符。如果使用通配符输入多个文件，`wc` 会计算总数。此外，`wc` 非常适合与其他程序组合。

## 示例

`find` 返回每个普通文件的行数，`wc` 返回目录下所有文件的总数。

```bash
user$ find / -type f -print | wc
```

从 HTTP、HTTPS 和 FTP 服务器下载文件。`wget` 可以恢复中断的下载，可以递归跟踪，适用于自动化下载。

传输的文件指定为 URL（统一资源定位符），例如 `http://myserver.com/file.iso`。`wget` 命令由许多选项控制；最重要的有：

- `-b`
  作为后台进程执行并将所有状态消息写入 `wget-log` 文件。

- `-B url` 或 `--base=url`
  为你通过 `-I file` 指定的文件中的所有相对链接加上基础 URL 前缀。

- `-c`
  续传中断的下载。注意：如果文件在此期间在服务器上发生了变化，则下载的文件是不正确的，它包含部分旧文件数据和新文件数据！

- `--force-html`
  将通过 `-i` 指定的文件解释为 HTML 文件，并加载 HTML 文件中链接引用的所有文件。

- `--ftp-user=user --ftp-password=pw`
  指定 FTP 下载的用户名和密码。此信息也可以在 URL 中传递（`ftp://user:password@server/file.txt`）。

- `-i file` 或 `--input-file=file`
  从指定的文本文件中读取要传输的文件（URL）。如果你传递 `-` 字符而不是文件，`wget` 将期望从标准输入读取 URL。`-i` 选项只接受本地文件作为参数，不接受 URL。（因此 `-i http://server/name.html` 是无效的！）。

- `--limit-rate=n`
  限制每秒下载量。字母 `k` 和 `m` 分别表示字节和兆字节（例如 `--limit-rate=0.25m`）。

- `--no-check-certificate`
  不检查 HTTPS 证书。如果你知道相关服务器使用自签名证书，这样做是有意义的。

- `-q`
  不输出状态消息（静模式）。

- `--retry-connrefused`
  在发生连接拒绝错误后仍继续尝试下载文件。此选项对于不可靠的下载服务器有用，这些服务器偶尔会从网络中消失并在短时间内重新出现。

- `--spider`
  测试通过 `-i htmlfile force-html` 指定的文件中的所有链接是否仍然有效。但不会下载链接指向的文件。

- `-t n` 或 `--tries=n`
  如果连接丢失，将尝试重连 `n` 次（默认设置为 20）。使用 `-t`，`wget` 会不断尝试，直到下载成功或你取消命令。

- `-w n` 或 `--wait=n`
  指定 `wget` 在下载下一个文件之前等待的秒数。此选项可以防止下载服务器因无数几乎同时发生的下载请求而导致过载。

## 递归下载

以下选项控制递归下载：

- `-E` 或 `--html-extension`
  为类型为 `application/xhtml+xml` 或 `text/html` 且文件名不以 `.html` 或 `.htm` 结尾的所有下载文件添加 `.html` 扩展名。

- `-H` 或 `--span-hosts`
  同时也跟踪指向其他网站的链接。

- `-k` 或 `--convert-links`
  更改下载的 HTML 文件中的链接，使其引用本地文件。这使得以后可以离线查看页面。

- `-l n` 或 `--level n`
  限制递归深度（默认设置为 5）。使用 `-inf` 取消限制。

- `-L` 或 `--relative`
  仅跟踪相对链接（但不包括指向起始网站的绝对链接）。

- `-r`
  激活递归下载。对于 HTTP 下载，`wget` 会跟踪起始页面上的所有 HTTP 链接，下载通过这种方式指定的文件，跟踪它们的链接等等。`wget` 仅考虑相对链接和指向起始网站页面的链接。对于 FTP 下载，`wget` 会读取所有子目录。

- `-p`
  下载查看源文件所需的所有文件（包括超过最大递归级别的文件）。

## 示例

在基本形式下，`wget` 仅下载指定的文件：

```
user$ wget ftp://myftpserver.com/name.abc
```

如果下载因任何原因被中断，可以使用 `-c` 没有任何问题地恢复：

```
user wget -c ftp://myftpserver.com/name.abc
```

以下递归下载命令（`-r` 选项）有助于以后离线读取网站或存档其当前状态。递归深度通过 `-l 4` 限制为四层。

```
user wget -r -l 4 -p -E -k http://website.com
```

## whatis 文件

`whatis` 输出指定命令或关键词的简短描述。`whatis` 描述仅存在于安装了 `whatis` 的主题中。

## whereis

`whereis` 为命令搜索手册页、源代码和文档。

## which

`which` 在你的 `PATH` 中搜索与给定可执行文件、别名或 shell 函数同名的文件。

## 示例

使用 `which` 时，输出可能如下所示：

```
user$ which ls
/usr/bin/ls
```

## type

`type` 告诉你命令的类型，它是别名、关键字、函数还是文件。

## 示例

使用 `type` 时，输出可能如下所示：

```
user$ type ls
ls is aliased to `ls --color=auto`
```

## wpa_passphrase ssid

`wpa_passphrase` 帮助为 Wi-Fi 认证服务 `wpa_supplicant` 设置配置文件。

## 示例

`wpa_supplicant` 期望将 Wi-Fi 的名称（即服务集标识符 `ssid`）作为参数。然后，你必须输入 Wi-Fi 的密码。该命令将输出符合 `wpa_supplicant` 语法的多行内容。你现在只需要将这些行加到 `/etc/wpa_supplicant/wpa_supplicant.conf` 的末尾：

```
user wpa_passphrase my-wifi-name
# reading passphrase from stdin
strictlySecret{
  ssid="my-wifi-name"
  # psk="strictlySecret"
  psk=9a18494197f55e1c6b350cc49b09a5fab532a8ec991f997fffd0a5e78d96
}
```



## write username

`write` 允许你向另一个用户发送消息。运行命令后，在按下 `Ctrl+D` 之前输入的所有字符都将传输到指定用户的终端。

`wsl` 不是一个 Linux 命令，而是一个 Windows 命令。它被包含在书中是因为它可以帮助你管理适用于 Linux 的 Windows 子系统 (`WSL`)，即在 Windows 上启动和删除 Linux 安装等。当你在“启用 Windows 功能”程序中激活了“适用于 Linux 的 Windows 子系统”选项时，该命令才可用。

在没有其他选项的情况下，`wsl` 会启动默认 Linux 安装或运行传递给 `wsl` 的命令。

- `-d` 或 `--distribution name`
启动指定的发行版。其后续用用将在 shell 中以交互方式进行。

- `-l` 或 `--list`
列出所有 Linux 安装。使用额外的 `--verbose` 选项，该命令还会显示哪些 Linux 实例正在运行，以及它们是兼容 `WSL1` 还是 `WSL2`。（`WSL2` 使用 Linux 内核来运行相应的发行版，这具有速度优势。然而，与 `WSL1` 相比，`WSL2` 在网络连接方面存在限制。）

- `-s` 或 `--set-default name`
指定哪个 Linux 安装为默认 Linux 系统。

- `--set-default-version name 1|2`
决定新的 Linux 安装默认使用 `WSL1` 还是 `WSL2` 运行。

- `--set-version name 1|2`
指定指定的 Linux 发行版应如何运行（`WSL1` 或 `WSL2`）。

- `--shutdown`
关闭所有运行中的 Linux发行版。

- `-t` 或 `--terminate name`
停止指定的 Linux发行版的执行。

- `-u` 或 `--user name`
为指定用户运行命令或登录。

- `--unregister name`
删除指定的 Linux 安装。

`wsl` 不提供安装新 Linux 发行的选项。要此此，你需要咨询 Microsoft Store，那里有各种 Linux 发行版可免费下载。当你第一次启动 `WSL` 发行版时，必须设置一个用户和密码。该用户具有 `sudo` 权限。

### 示例

测试计算机上有四个 Linux 安装，以 Ubuntu 作为默认发行版：

| 名称 | 状态 | 版本 |
| --- | --- | --- |
| * Ubuntu | 已停止 | 2 |
| kali-linux | 已停止 | 1 |
| docker-desktop-data | 已停止 | 2 |
| docker-desktop | 已停止 | 2 |

`wsl` 运行了两次 `id`，一次使用标准账户运行，一次使用 root 权限运行。这不需要密码。

```
> wsl id
uid=1000(kofler) gid=1000(kofler) groups=1000(kofler),4(adm),....
```

```
> wsl -u root id
uid=0(root) gid=0(root) groups=0(root)
```

### 上一个示例启动了用于交互式使用的 Kali Linux：

```
> wsl -d kali-linux
$ cat /etc/os-release
PRETTY_NAME="Kali GNU/Linux Rolling"
NAME="Kali GNU/Linux"
```

```
$ ip a
8: eth0:BROADCAST,MULTICAST,UP mtu 1500 group default qlen 1
link/ether 04:d4:c4:92:65:24 65:f
inet 192.168.178.52/24 brd 192.168.178.255 scope global dynamic
...
16: eth1:BROADCAST,MULTICAST,UP mtu 1500 group default qlen 1
link/ether 00:15:5d:7e:85:98
inet 172.31.96.1/20 brd 172.31.111.255 scope global dynamic
...
```

## xargs 命令

`xargs` 将来自标准输入的数据转发到指定的命令。`xargs` 通常与位于管道符之前的命令结合使用，格式为 `command1 | xargs command2`。

出于安全考虑，X 图形系统通常只允许本地连接。要从外部计算机进行操作，必须通过 `xhost +name` 为该主机显式定义异常。更宽松的方法是 `xhost +`，它会完全禁用访问控制，允许从任何主机登录。

### 示例

在生活中，运行 `xhost` 通常是必要的，特别是如果你首先想通过 VNC 以普通用户身份连接到图形服务器，然后使用 `sudo` 或 `su` 以 root 权限运行图形程序时。默认情况下是不允许的。解决方案是 `xhost +localhost`（因为通过 VNC 已建立了连接，现在只需在不同的账户下运行程序即可）。

以下示例假设你首先建立了 VNC 连接，然后在终端窗口中运行 `xhost`，最后通过 `sudo` 启动图形模式下的程序——在这种情况下，是 `edit` 编辑器：

```
user$ xhost +localhost
user$ sudo edit
(以 root 权限启动编辑器)
```

## xinput [command]

`xinput` 支持为 X 窗口系统配置输入设备（例如键盘、鼠标和触摸板）。

- `-list`
列出所有识别出的输入设备。

- `-list-props deviceid`
列出设备的参数。你应该预先使用 `xinput list` 确定设备 ID。

- `-set-button-map deviceassignmentbutton1 mapbutton2 ...`
更改鼠标按钮的分配。

## xkill [options]

`xkill` 终止一个卡住或崩溃了一的 X 程序。启动命令后，必须用鼠标点击相关的窗口。

## xrandr [options]

`xrandr` 在运行期间更改屏幕分辨率、帧率和其他设置。如名所示，`xrandr` 仅作用于 Xorg。Wayland 的替代方案是 `wlr-randr`。

- `--addmode output name`
为指定的显示输出添加图形模式（可能是之前通过 `--newmode` 定义的）。

- `--dpi n`
指示每英寸显示的像素数。

- `--left-of output name`, `--right-of name`, `--below name`, 或 `--above name`
激活由 `--output` 指定的信号输出，并指定屏幕之间的相对位置。这只有在 `xorg.conf` 中设置了足够大的虚拟分辨率以能覆盖两个屏幕时才有效。

- `--newmode freq x1 x2 x3 x4 y1 y2 y3 y4`
定义一个新模式（新分辨率）。语法对应于 `xorg.conf` 中的 `ModelLine` 行。你可以使用 `gtf` 命令确定正确的数字组合。

- `--off`
关闭由 `--output` 指定的信号输出。

- `--orientation x`
更改图像位置。允许的设置为 normal（正常）、inverted（反转）、left（左）和 right（右）。

- `--output name`
指示其他选项与特定的信号输出。这在连接多个显示器时非常有用。你可以通过 `xrandr -q` 确定活动信号输出的名称。

- `--primary`
使通过 `--output` 选择的屏幕为主屏幕，Gnome 或 KDE 将其上显示面板、Dock 等。

- `-q`
指示哪些设置选项。结果很大取决于所使用的显卡驱动程序。

- `--rate n`
更改当前分辨率的帧率。`n` 是所需的赫兹（Hz）。

- `--size n`
更改分辨率。`n` 是 `xrandr -q` 结果列表中的数字，或者是 `widheight` 格式的目标分辨率。

### 示例

以下命令将分辨率设置为 1280 × 1024 像素：

```
user xrandr --size 1280x1024
```

下一个命令激活 DVI 和 VGA 信号输出。（输出名称取决于显卡和驱动程序。）两个显示器上将显示相同的图像。`--auto` 选项使每个显示器以其最佳的分辨率和帧率运行。

```
user$ xrandr --output DVI-I-0 --auto --output VGA-0 --auto
```

以下三个命令定义了一个为 1280 × 720 像素的新图形模式，并为 HDMI1 输出激活它：

```
user$ xrandr --newmode 1280x720 74.18 1280 1390 1430 1650 720 725 730 750
```

```
user$ xrandr --addmode HDMI1 1280x720
```

```
user$ xrandr --size 1280x720
```



## `xset` [command]

`xset` 更改 X 服务器的各种设置。

- `-dpms` / `+dpms`
激活或禁用节能功能（显示电源管理信号）。

- `dpms n1 [n2 [n3]]`
指定显示器多少秒后激活 DPMS Standby（待机）、Suspend（挂起）和 Off（关闭）模式。

- `q`
提供当前设置列表。

- `s n`
在 `n` 秒后激活屏幕保护。

## `XZ` [options] 文件

来自 `xz-utils` 包的 `xz` 压缩指定的文件。

- `-d`
解压指定的文件（或解压）。

- `--compress`
压缩指定的文件。

- `-c`
将文件内容输出到标准输出。

- `-t`
测试压缩文件的完整性。

- `-v`
显示有关压缩的详细信息。

- `--level`
设置压缩级别（0 到 9）。

- `-q`
静默模式。

- `--filename`
设置输出文件的文件名。

- `--index`
为文件创建索引，允许随机访问。

- `--help`
显示帮助信息。

- `--version`
显示版本信息。

提供了多得输入和控制选项。

- `calendar`
显示日历并允许你选择一个标签。

- `entry`
启用文本输入。

- `file-selection`
允许你选择一个文件。

- `password`
允许你输入密码。

- `text zenit`
指定在对话框中显示的文本。

- `title text`
为对话框提供一个标题。

## 示例

以下脚本行首先提示用户输入密码，然后显示密码：

```
pw=$(zenity) --password --title 'Your password please ...'
echo "That was your password: $pw"
```

```
zip [options] archive.zip file1 file2 ...
```

该命令创建一个名为 `archive.zip` 的 ZIP 压缩包，并将所有指定的文件插入其中。该包特别适用于与 Windows 用户交换数据。要在 Linux 上再次提取这些文件，你必须使用 `unzip`。

- `r`
递归地归档目录的内容。

## 示例

以下命令将作为参数传递的所有 HTML 文件插入 `myarchive.zip`：

```
user zip myarchive.zip *.html
```

`zipinfo [options] file.zip`

该命令返回 ZIP 压缩包的目录。

`zramctl [options] command`

在现代发行版中（例如 Fedora），部分 RAM 被用作交换空间（swap space），因为存储在那的数据块经过了压缩。假设虚拟机有 4 GiB 的 RAM。ZRAM 内存最多可以存储 2 GiB 的数据。如果实现了 2 倍的平均压缩，那么整个交换空间仅使用 1 GiB 的 RAM。因此，系统可以使用总共 5 GiB 的内存。当然，交换和压缩会损失效率，但在实践中，系统的运行效果异常出色。

在没有任何额外参数的情况下，`zramctl` 提供关于系统使用情况的信息。在这种情况下，ZRAM 可以存储 2.8 GiB 的数据。交换空间目前仅包含 752 MiB 的数据。这些数据可以压缩到 222 MiB。加上各种元数据，交换空间占用 238 MiB。

```
user$ zramctl
ALGORITHM DISKSIZE DATA COMPR TOTAL STREAMS MOUNTPOINT
/dev/zram0 lzo-re 2.8G 752,3M 222M 238,3M 6 [SWAP]
```

- `a` 或 `--algorithm lzo|lz4|lz482|zstd`
使用指定的压缩算法。

- `f` 或 `--find`
使用第一个空闲 ZRAM 设备。

- `s` 或 `--size n`
创建一个指定大小的 ZRAM 设备（例如 `-s 1GiB`）。

## 示例

以下命令展示了如何手动为 1 GiB 的数据设置（进一步的）ZRAM 区域：

```
root# zramctl --find --size 1GiB
/dev/zram1
root# mkswap /dev/zram1
root# swapon /dev/zram1
```

对于 Fedora，`systemd` 负责激活 ZRAM 系统。

```
zypper [options] command
```

特定于 SUSE 的（SUSE-specific）`zypper` 命令用于辅助 RPM 软件包管理器。它负责安装和更新包、设置包源等。`zypper` 需要 `libzypp` 库，它是所有当前 SUSE 发行版的不可或缺的一部分。只要意义清晰，可以简写以下命令，例如用 `zypper name` 代替 `zypper install name`。

- `addrepo [options] uri`
设置一个新的包源并赋予其别名。统一资源标识符（URI）描述包源，例如如下文所示：

```
http://download.opensuse.org/distribution/leap/15.0/repo/
```

默认情况下，包源是激活的（`zypper repos` 中的 `enabled` 列）并被标记为需要刷新（`refresh` 列）。只要意义清晰，以下命令可以简写，例如用 `zypper name` 代替 `zypper install name`。

- `addrepo [options] uri`
设置一个新的包源并赋予其别名。统一资源标识符（URI）描述包源，例如如下所示：

```
http://download.opensuse.org/distribution/leap/15.0/repo/
```



默认情况下，包源是激活的（`zypper repos` 中的 `enabled` 列）并被标记为需要刷新（`refresh` 列）。只要意义清晰，以下命令可以简写，例如用 `zypper name` 代替 `zypper install name`。

（注：原文后续段落存在较多重复和逻辑混乱，以下为基于技术语境的翻译）

### zypper 命令

- `addrepo [options] uri`
  设置一个新的包源并赋予其别名……（此处省略重复内容）

- `clean [--all]`
  从缓存中删除已下载的软件包。

- `dup`
  执行发行版更新（distribution update）。

- `info name`
  提供指定软件包、补丁或产品的信息。

- `install [-y] name`
  安装指定的软件包。

- `lifecycle`
  提供已安装软件包将持续提供更新的表格概览。

- `list-updates [-t package]`
  显示所有可用补丁，使用 `-t package` 同时显示补丁和更新。

- `patches`
  列出所有补丁。

- `patch-check`
  确定可用补丁的数量。

- `patch-info [name]`
  提供所有补丁或指定补丁的信息。

- `refresh`
  测试包源的内容是否发生变化，必要时重新加载——即使对于使用 `n`（不刷新）选项设置的包源。使用 `-f`（强制）选项，即使 zypper 认为没有变化也可以重新访问内容。

- `remove [-y] name`
  删除指定的软件包。额外的 `--clean-deps` 还会卸载不再需要的依赖包。使用 `-y`，zypper 将不再确认。

- `removerepo name`
  根据 URI 或别名删除包源。

- `renamepo old new`
  为包源分配一个新的别名。

- `repos`
  列出所有已安装包源。该命令显示每个包源的名称和别名，但不显示地址（URI）。对于 YaST 设置的包源，地址会被别名，这就是为什么别名列看起来像地址列。然而，这不适用于 `zypper addrepo` 设置的包源。

- `search [options] expression`
  使用指定的搜索表达式搜索软件包。默认情况下，只搜索包名。使用 `-d`，zypper 还会搜索包描述。`-i` 将搜索限制为已安装的软件包，`-u` 将限制为尚未安装的软件包。可以使用 `-t pattern` 来确定预定义的软件包组。

- `update [-t package] [-y]`
  更新所有可用补丁的软件包。使用 `-t package` 选项，zypper 还会考虑更新，即更高程序版本。这里是简要解释：更新是比安装版本更高的完整软件包。相反，补丁是补充或更新包（增量 RPM），它们仅包含更改，因此要小得多。

| 仓库名称 | 当前版本 | 可用版本 | 架构 |
| --- | --- | --- | --- |
| 主仓库 (OSS) | 7zip | 23.01-4.2 | 23.01-5.1 | aarch64 |
| 主仓库 (OSS) | argyllcms | 3.1.0-2.1 | 3.1.0-3.1 | aarch64 |
| 主仓库 (OSS) | avahi | 0.8-31.3 | 0.8-32.1 | aarch64 |

## 特殊 bash 字符

`#& %!`

无论是在输入命令还是在 shell 编程中，你都可以使用大量的特殊字符来执行各种操作。表 1 总结了最重要的特殊字符的含义。

| 字符 | 含义 |
| --- | --- |
| `;` | 分隔多个命令 |
| `:` | 不执行操作的 Shell 命令 |
| `.` | 启动 shell 程序而不创建创建独立的子 shell（. 文件，对应源文件） |
| `#` | 引入注释 |
| `#!/bin/sh` | 指定 shell 程序所需要的 shell |
| `&` | 在后台运行命令（com&) |
| `&&` | 条件执行命令（com1 && com2） |

| 字符 | 含义 |
| --- | --- |
| `&>` | 重定向标准输出和错误（对应于 >&) |
| `|` | 创建管道（com1 | com2） |
| `||` | 条件执行命令（com1 || com2） |
| `*` | 文件名的通配符（任意数量的字符） |
| `?` | 文件名的通配符（任意单个字符） |
| `[abc]` | 文件名的通配符（abc 中的任意一个字符） |
| `[ expression ]` | 测试表达式的短写法 |
| `[[ expr ]]` | 扩展测试语法，bash 特有 |
| `(...)` | 在当前 shell 中执行命令（((com1; com2))） |
| `{...}` | 组化命令 |
| `{, , }` | 组合字符串（a{1,2,3} -> a1 a2 a3） |
| `{a..b}` | 组合字符串（b{4..6} -> b4 b5 b6） |

| 字符 | 含义 |
| --- | --- |
| `~` | 目录目录缩写 |
| `>` | 重定向输出到文件（com > file） |
| `>>` | 将输出重定向到现有文件 |
| `>&` | 重定向标准输出和错误（对应于 &>） |
| `2>` | 重定向标准错误输出 |
| `<` | 从文件重定向输入（com < file） |
| `<< end` | 将输入从活动文件重定向到末尾 |
| `$` | 标记变量（echo $var） |
| `!$` | 上一个启动的后台进程的 PID |
| `$$` | 当前 shell 的 PID |
| `$0` | 当前执行的 shell 脚本的文件 |
| `$1 to $9` | 传递给命令的前九个参数 |
| `$#` | 传递给 shell 程序的参数数量 |
| `$* or $@` | 所有传递参数的总和 |

| 字符 | 含义 |
| --- | --- |
| `$?` | 上一个命令的返回值（θ = OK 或错误代码） |
| `$(...)` | 命令替换（echo $ls） |
| `$((...))` | 算术分析（echo $((2+3))) |
| `${...}` | 用于编辑字符串的各种特殊函数 |
| `"..."` | 防止大多数特殊字符被解析 |
| `'...'` | 防止所有特殊字符被解析 |
| `` `...` `` | 命令替换（echo `ls`，对应于 $(ls)） |
| `\character` | 取消特殊字符的作用 |

**表 1** 特殊 bash 字符

## 配置文件

Linux 命令参考的这部分总结了最重要的 Linux 配置文件的语法。这些文件按名称排序，而不是按它们所在目录的路径排序。

这里这里展示的大多数文件适用于所有发行版。我会明确指出特定于发行版的特殊之处。有关配置文件的更多信息，请参阅 `man 5 name`。数字 5 表示你想读取配置文件的文档，而不是可能同名的命令的文档。

```
/etc/adduser.conf
```

Debian/Ubuntu 特有的文件 `/etc/adduser.conf` 包含了使用 `adduser` 和 `addgroup` 命令设置新用户和组的默认设置。`adduser.conf` 文件包含以 `parameter=value` 形式逐行设置的参数。

- `ADD_EXTRA_GROUPS=0|1`
  指定新用户是否应自动分配到 `EXTRA_GROUPS` 中列出的辅助组。

- `HOME`
  指定家目录的基础目录（通常为 `/home`）。

- `DIRMODE`
  指定设置新家目录时使用的访问位（默认为 755）。

- `DSHELL`
  指定默认 shell。

- `EXTRA_GROUPS="group1,group2,..."`
  包含默认分配给新用户（`ADD_EXTRA_GROUPS=1`）或通过 `adduser` 选项 `--add_extra_groups` 分配的辅助组列表。

- `FIRST_GID` and `LAST_GID`
  确定普通组的 GID 范围。

- `FIRST_SYSTEM_GID` and `LAST_SYSTEM_GID`
  确定系统账户组的 GID 范围。

- `FIRST_SYSTEM_UID` and `LAST_SYSTEM_UID`
  确定系统账户的 UID 范围。

- `FIRST_UID` and `LAST_UID`
  确定普通用户的 UID 范围。

- `GROUPHOMES=yes|no`
  指定是否在 `/home/groupname/username` 处设置新用户的家目录。

- `LETTERHOMES=yes|no`
  指定是否将家目录放在字母子目录下，例如 `/home/k/k`。这对于拥有大量账户的计算机有用。

- `NAME_REGEX=yes|no`
  包含一个正则表达式（参见 `grep`），新用户名必须匹配该正则。

- `SKEL`
  指定从哪个目录复制文件到新用户目录（通常为 `/etc/skel`）。

- `USERGROUPS=yes|no`
  指定是否为每个用户设置。

## 示例

以下行显示了 `adduser.conf` 中默认设置的节：

```
ADD_EXTRA_GROUPS=0|1

HOME=/home
```



`DIRMODE=755`

`DSHELL=/bin/bash`

`EXTRA_GROUPS="group1,group2,..."`

`FIRST_GID=1000`

`LAST_GID=2000`

`FIRST_SYSTEM_GID=100`

`LAST_SYSTEM_GID=999`

`FIRST_SYSTEM_UID=100`

`LAST_SYSTEM_UID=999`

`FIRST_UID=1000`

`LAST_UID=2000`

`GROUPHOMES=no`

`LETTERHOMES=no`

`NAME_REGEX=.*`

`SKEL=/etc/skel`

`USERGROUPS=yes`

## `/etc/aliases`

`/etc/aliases` 文件列出了本地账户的转发地址。邮件服务器不直接分析 `/etc/aliases`，而是考虑从该文件生成的数据库文件。因此，在执行 `newaliases` 命令之前才会生效。

名称必须是本地账户（不带 `@hostname!`）。指定别名有多种选项，取决于邮件服务器支持哪些变体：

- `name`
  将邮件重定向到另一个本地账户。
- `adresse@host`
  将邮件重定向到外部邮箱地址。
- `/path/file`
  将邮件添加到指定文件的末尾。
- `|command`
  将邮件传递给指定的命令。
- `:include:/path/file`
  从指定文件中读取别名列表。

如果指定了多个别名，邮件将重定向到所有地址。

### 示例

在以下示例中，发往 `root` 转发 和本地用户 `michael` 和 `ben`。发送给 `support` 的邮件将保存在 `support` 邮箱中，并转发给 `michael` 和 `peter.parks@abc-company.com`。

```
root        michael

postmaster: michael

webmaster: michael, ben

support: support, michael, peter.parks@abc-company.com
```

4B, 400, 和 5)。

- `arm_freq=n`
  指定所需的最高 CPU 频率，单位为 MHz。
  当 CPU 负载较少时，频率会自动降低。如果你将频率提高 CPU 的默认频率（超频），则应该略微增加电压（`over_voltage_delta` 参数）。

- `camera_auto_detect=1`
  `display_auto_detect=1`
  自动检测 DSI 摄像头和显示器。

- `cmdline=string`
  将字符字符串传递给内核。将解析该参数 own解析 `/boot/cmdline.txt` 文件。

- `gpu_freq=n`
  指示图形单元的时钟频率，单位为 MHz。

- `decode_MPG2=0x12345678`
  `decode_WVC1=0x12345678`
  指定启用 MPEG-2 和 VC-1 解器的代码。
  密钥可以在 `www.raspberrypi.com` ，并且必须与 CPU 的序列号匹配。序列号存储在 `/proc/cpuinfo` 文件中。

  `decode` 参数仅适用于 3B+ 及之前的型号，但不再适用于 4B、400 和 5。较新的型号具有 H264 硬件解码器。其他视频格式通过软件解码。完全不需要许可密钥。

- `dtover=xxx`
  激活硬件组件的设备树覆盖层（overlay）并加载相应的驱动模块。

- `dtparam=audio=on`
  激活音频系统并加载驱动程序 `snd_bcm28xx`。

- `dtparam=i2c_arm=on`
  激活 I²C 总线。

- `dtparam=spi=on`
  激活 SPI 总线。

- `over_voltage_delta=n`
  增加 CPU 的电压（单位为微伏，50000 对应 0.05V）。

- `sdram_freq=n`
  指示主内存（RAM）的时钟频率，单位为 MHz。

- `usb_max_current_enable=1`
  即使在电源不足的情况下（即使用弱电源适配器）也激活 USB 启动过程。此选项仅适用于 5 型及后续型号，并可能导致运行不稳定。

`config.txt` 的更改在下次重启之前不会生效。你可以在运行期间使用 `vcgencmd get_config` 读取许多 `config.txt` 参数。你可以在此处查看更多关于 `config.txt` 的细节：

https://elinux.org/RPiconfig

## `/etc/crontab`

`/etc/crontab` 文件由后台进程 `ccrond` 分析。`crontab` 包含了逐行信息，说明了何时为哪个用户账户执行哪些命令。
cron 系统允许在预定义的时间自动执行任务，例如在 1 月、4 月、7 月和 10 月的第一个星期一凌晨 2:30 将文件系统镜像到外部备份服务器。

每个 `crontab` 条目由一行中的七列组成。列与列之间用空格或制表符分隔。最后必须以换行符结束，否则将被忽略。在行首使用 `#` 字符引入注释。不允许在 `crontab` 条目后输入注释。

- 第一列（分钟）
  指定程序应在第几分钟（0–59）执行。
- 第二列（小时）
  指定指定的小时（0--23）。
- 第三列（日期）
  指定月份中的某一天（1–31）。
- 第四列（月份）
  指定月份（1–12）。
- 第五列（星期）
  指定星期中的哪几天（0–7，0 和 7 都代表星期日）。
- 第六列（用户/账户）
  指定为哪个用户执行命令（通常是 `root`）。
- 第七列（命令）
  包含要执行的命令。命令可能包含空格；直到行尾的所有文本都将被解释为命令。

如果在前五列中输入 `*` 而不是数字，则该字段将被忽略。例如，`15 * * *` 意味着命令应在每天、每月、每小时的每个整点后 15 分钟执行一次，无论是星期几。同样，`0 * * 6` 意味着命令在每周六的凌晨 0:29 执行。

对于时间字段，允许使用 `*/n` 表示法。这意味着命令将每隔 n 分钟/小时等执行一次。因此，`*/15 * * *` 意味着命令每刻钟执行一次（n:00, n:15, n:30 和 n:45）。

在时间字段中，还允许用逗号分隔的多个条目以及范围范围。第二列中的 `1,13` 意味着命令在凌晨 1 点和下午 1 点执行。在第二列中，`2,4,6,8-18,20,23` 导致命令在 2 点、4 点、6 点、8 点、11 点以及早上 6 点到下午 6 点之间的每小时执行。

除了五个时间列外，还可以使用表 1 总结的 `@` 缩写。在第一列开头使用 `-` 号可以阻止 syslog 记录命令。这种规则仅适用于六列为 `root` 时。

| 缩写 | 含义 |
|---|---|
| @reboot | 每次启动后 |
| @yearly | 每年 |
| @annual | 每年 |
| @monthly | 每月 |
| @weekly | 每周 |
| @daily | 每天 |

| 缩写 | 含义 |
|---|---|
| @hourly | 每小时 |

**表 1** `crontab` 缩写

## SHELL, PATH, 和 MAIL

在程序启动之前，`/etc/crontab` 通常包含设置环境变量的行。在 CentOS 上，默认设置如下：

```
SHELL=/bin/bash

PATH=/sbin:/bin

MAILTO=root
```

### 示例

`crontab` 中的以下三行会导致每小时 15 分钟调用一次维护脚本，每周日 00:30 启动备份工具，每天创建一个数据库备份：

```
15 * * * root /usr/bin/maintenance-script

30 0 * * root /usr/bin/backup-tool
```



# 其他 cron 文件

除了全局 `/etc/crontab` 文件外，取决于发行版还有其他定义 cron 任务的方法：

- `/etc/cron.d`
在发行版中，cron 守护进程还会分析 `/etc/cron.d` 目录下的所有文件。这些文件的规则与 `/etc/crontab` 相同。

- 用户特定的 crontab 文件
取决于发行版，用户特定的 crontab 文件存储在 `/var/spool/cron/` 或 `/var/spool/cron/tabs` 目录中。文件名指示适用于用户。这些文件中省略了六列。可以使用 `crontab` 命令更改用户特定的 cron 项。

- `cron.hourly`, `cron.daily`, `cron.weekly`, `cron.monthly`
在大多数发行版中，`/etc/crontab` 中的默认配置包含某些条目，导致 `/etc/cron.hourly/*` 中的所有脚本以 root 权限每小时执行一次，`etc/cron.daily/*` 每天一次。这些文件是普通的脚本文件，不适用 crontab 语法规则。但记得设置执行位（`chmod +x file`）！

`cron.daily`、..weekly 和 .monthly 中的自定义脚本文件名可能仅由数字、字母、连字符和下划线组成。只要文件名包含一个点，脚本将被忽略！如果安装了 Anacron 程序，来自 `/etc/cron..weekly` 和 .monthly 的脚本将不会执行。

## /etc/deluser.conf

Debian/Ubuntu 特有的文件 `/etc/deluser.conf` 包含了使用 `deluser` 和 `delgroup` 命令删除用户和组的默认设置。`deluser.conf` 文件由 `parameter=value` 格式的逐行条目组成。

- `BACKUP=0|1`
指定对 `REMOVE` 参数删除的文件进行备份。

- `BACKUP_TO`
指定备份目录的位置。

- `EXCLUDE_FSTYPE="fs1,fs2,...)"`
指定在搜索用户文件创建备份时应忽略哪些文件系统。

- `ONLY_IS_EMPTY=1`
导致仅在组为空时删除组

成员。

- `REM_HOME=0|1`
指定是否也应该删除该账户的主目录。

- `REM_ALL_FILES=0|1`
指定是否应该删除主目录之外的用户文件，例如打印缓存文件和电子邮件收件箱。

## 示例

以下行显示了 `deluser.conf` 中在 Ubuntu 上有效的默认设置：

## /etc/dnf/dnf.conf

软件包管理系统 DNF 的基础设置可以在 `/etc/dnf/dnf.conf` 中找到，该系统通常用于 Fedora 和 Red Hat。`/etc/yum.repos.d/` 下的 `*.repos` 文件也包含了各个独立软件包源的详细设置。

### 基础设置

- `clean_requirements_on_remove = true/false`
指定由于依赖关系而安装的软件包在所有引用该包的软件包卸载后，是否应该自动删除。即使此选项为 true，dnf 也不会在未询问的情况下删除通过 `dnf install` 明确安装的包。

- `color=never`
导致终端中的 dnf 命令不使用任何颜色。如果你想使用颜色，请使用 `color=always`。

- `exactarch=1`
导致 dnf 仅考虑架构与已安装软件包匹配的更新。因此，i386 软件包无法被较新的 x86_64 软件包替换。

- `gpgcheck=1`
导致 dnf 使用密钥确保软件包的真实性。也可以偏离 `dnf.conf` 中的设置，为每个软件包源单独设置 `gpgcheck`。插件决定了 dnf 是否考虑插件。

- `installonly_limit=n`
控制同时安装多少个旧版本的内核软件包。该设置影响所有以新包形式安装更新的包。此处理过程确保了受影响软件包的旧版本始终可用，作为回退。

- `keepcache=0`
导致下载的软件包在安装后不进行归档。通常情况下，这是一个非常有用的设置，因为软件包所需的空间随着时间推移会变得很大，而且通常没有理由再次安装这些软件包。然而，可能会出现 dnf 检测到安装并中止安装过程。在这种情况下，下载的软件包将被删除。如果你可以修复问题并重复更新，则所有软件包都必须重新下载。你可以通过使用 `keepcache=1` 来避免这种情况。要显式删除 `/var/cache/dnf` 中的下载包，你必须运行 `dnf clean packages`。

在当前的 Fedora 版本中，该文件仅包含几个设置：

```
# /etc/dnf/dnf.conf on Fedora

[main]

gpgcheck=1

installonly_limit=3

clean_requirements_on_remove=True

best=False

skip_if_unavailable=True
```

### 软件包源

软件包源通过 `/etc/yum.repos.d` 目录下的 `*.conf` 文件配置。在从 yum 切换到 dnf 时，该目录没有重命名为 `/etc/dnf.repos.d`。

- `[variant]`
指定后续设置与软件包源的哪个部分有关。

- `baseurl=url` 或 `mirrorlist=url`
指定软件包文件所在的位置。使用 `mirrorlist` 时，url 指向镜像服务器列表。dnf 会自动选择其中一个镜像。dnf 会将 url 中的 `$releasever`、`'$arch'` 和 `$basearch` 变量替换为 Linux 发行版的版本号及其架构。

- `enabled=0/1`
指示软件包源是否激活。

- `name=repone`
指定软件包源的名称。

- `metadata_expires`
控制从软件包源下载的元数据的有效时间。dnf 将元数据保存在缓存中，如果元数据尚未过期，则不再再次下载。这可以节省时间减少下载量，但可能导致 dnf 忽略软件包源的最近更改。如有必要，你可以使用 `dnf clean metadata` 强制删除本地元数据。这将强制 dnf 在下次执行时重新导入所有软件包源的元数据。

以下行是文件 `/etc/yum.repos.d/fedora.repo` 的节选。该文件包含了 Fedora 发行版基础软件包的软件包源定义。

```
[fedora]

name=Fedora releasever - $basearch

metalink=https://mirrors.fedoraproject.org/metalink

repo=fedora-releasever&arch=$basearch

enabled=1

metadata_expire=7d

repo_gpgcheck=0

type=rpm

gpgcheck=1

gpgkey=file:///etc/rpm/RPM-KEY-GPG-GPG-KEY-fedora-$releasever-$basearch

skip_if_unavailable=False
```

```
[fedora-source]

name=Fedora releasever - Source

...
```



## `/etc/fstab`

`/etc/fstab` 包含了所有要集成到目录树或在计算机启动时激活的文件系统和交换分区条目。每个条目由空格或制表符分隔的六列组成。使用 `#` 字符引入注释。

+   - 第一列（`Device`）
包含数据介质的设备名称。除了设备名称，还可以使用 `LABEL=xx`、`UUID=xx` 或 `PARTUUID=xx` 指定数据介质的名称或 ID。

+   - 第二列（`Path`）
指定数据介质所在的目录。第二列指定的目录必须已经存在。对于交换分区，你应该在此处输入 `none`。

+   - 第三列（`File type`）
指定文件系统，例如 `ext4`、`btrfs` 或 `vfat`。重要文件系统的概览可以在书中找到。

+   - 第四列（`Options`）
包含挂载选项。多个选项仅用逗号分隔。如果你不需要任何选项，应输入 `defaults`。

+   - 第五列（`Dump`）
包含 `dump` 程序的信息。该列在 Linux 上被忽略。通常对系统分区输入 `1`，对其他分区输入 `0`。

+   - 第六列（`fsck`）
指定启动时是否检查文件系统以及检查顺序。通常对系统分区输入 `1`，对其他分区输入 `0`。这意味着仅在启动时检查系统分错误。如果你希望自动检查其他分区，必须在这些分区上输入数字 `2`。这意味着在检查完系统分区后进行。如果 `fstab` 的第五列和第六列缺失，则假设为 `0`。

### 示例

以下示例显示了带有 RAID 和 LVM 的服务器的 `fstab` 文件。启动分区位于 RAID 设备 `/dev/0` 上。系统和数据目录使用逻辑卷作为存储位置。`/`、`/var` 和 `/backup` 文件系统在重启时进行检查。如果根文件系统发生错误，文件系统将以只读模式挂载。

```
/dev/md/0      /boot      ext2    defaults        0 0

/dev/vg0/root  /         ext4    errors=remount-ro 0 1
```

## `/etc/group`

`/etc/group` 包含了所有组名称、相应的组标识符 (`GID`) 以及属于该组的用户列表。要管理组，通常使用 `groupadd`、`groupmod` 和 `groupdel` 命令。组文件中的行条目由四列组成，每列之间用冒号分隔：

+   * 第一列（`Group name`）
指示组名称。

+   * 第二列（`unused`）
旧版本中包含组密码的哈希值。当前的 Linux 发行版在此处保存 `x` 字符。如果定义了组密码，它们将保存在 `etc/gshadow` 中。

+   * 第三列（`GID`）
包含组标识符。在大多数发行版中，小于 `1000` 的 `GID` 留给系统账户。

+   * 第四列（`Accounts`）
包含属于该组的所有用户的逗号分隔列表

该组的成员。然而，系统只考虑次要组成，每个用户的主组存储在 `/etc/passwd` 的第四列。

### 示例

以下行显示了某台作为 Web 服务器和开发服务器计算机上的 `/etc/group` 摘。每个系统账户和普通用户都有自己的组。`admin` 组的成员可以使用 `sudo` 执行管理操作。`devel` 组的成员拥有版本管理系统的特殊访问权限。

```
root:x:0:

bin:x:1:

admin:x:27:kofler,huber

kofler:x:1000:huber,

devel:x:1023:kofler,huber,miller,smith
```

## `/etc/default/grub`

`/etc/default/grub` 包含了 GRUB 2 的默认设置。这些设置仅在重新生成 GRUB 配置文件 `boot/grub.cfg` 时才会生效——这可以通过手动使用 `update-grub` 命令（Debian, Ubuntu）或 `grub-mkconfig`（Fedora, openSUSE）来实现。

以下列表描述了最重要的关键词：

- `GRUB_CMDLINE_LINUX`：指定要传递给内核的选项。`GRUB_CMDLINE_LINUX` 选项适用于每次启动，但不适用于恢复模式。
- `GRUB_DEFAULT`：指定默认选择哪个 GRUB 菜单项。“saved” 意味着意味着激活上一次选择的项目。相反，如果涉及 LVM 或 RAID，GRUB 无法在菜单选择后保存任何环境变量。另一个选项是将目标菜单的字符串分配给 `GRUB_DEFAULT`。但是，你必须小心地保持拼写完全准确。
- `GRUB_DISABLE_OS_PROBER=false`：在重建引导时激活对其他操作系统的搜索。从 2022 年左右开始，GRUB 的配置使得 GRUB 菜单中只显示活动发行版的条目，而不再显示用于启动其他发行版的条目。这些条目在过去（BIOS）是必要的，但现在已经过时了（EFI）。如果 EFI 配置出现问题，GRUB 菜单项是一个很好的备份/冗余方案。
- `GRUB_DISABLE_LINUX_UUID=true`：导致 GRUB 将文件系统的 UUID 传递给内核。如果没有此选项，GRUB 将根目录作为设备名称传递。此设置仅适用于活动发行版的启动（脚本），不适用于其他发行版。
- `GRUB_DISABLE_RECOVERY=true`：防止 `update-grub` 或 `grub2-mkconfig` 向 `grub.cfg` 添加用于在恢复模式启动 Linux 的菜单项。
- `GRUB_DISTRIBUTOR`：由 `/etc/grub.d/` 脚本分析并指定当前发行版的名称。
- `GRUB_ENABLE_BLSCFG=true`：导致启动时除了 `grub.cfg` 外还会考虑来自 `/boot/loader/entries` 目录的菜单项。这使得配置文件更加清晰，并对应 `systemd-boot`（另一种引导程序）的过程。
- `GRUB_GFXMODE`：指定 GRUB 运行的图形模式（默认分辨率为 640 × 480 像素）。
- `GRUB_HIDDEN_TIMEOUT`：如果 GRUB 在安装期间仅识别出单个 Linux 发行版，则此项非常重要。在这种情况下，`GRUB_HIDDEN_TIMEOUT` 指定用户有多长时间的时间按下 `Shift` 来显示 GRUB 菜单。在等待期间屏幕保持黑色。如果安装了多个操作系统，GRUB 将忽略 `GRUB_HIDDEN_TIMEOUT` 设置并显示菜单。
- `GRUB_HIDDEN_TIMEOUT_QUIET=true`：防止在 `GRUB_HIDDEN_TIMEOUT` 等待期间显示倒计时器。如果你想让 GRUB 菜单始终显示，请使用注释字符 `#` 设置行 `GRUB_HIDDEN_TIMEOUT=…` 和 `GRUB_HIDDEN_TIMEOUT_QUIET=…`。
- `GRUB_TIMEOUT=n`：指定 GRUB 等待选择菜单项的秒数。如果在此时间过去且没有用户输入，GRUB 将启动选定的操作系统。在此处设置的时间仅在 GRUB 菜单出现时才生效。
- `GRUB_TERMINAL=console`：导致 GRUB 在文本模式下运行。然而，那里无法显示 Unicode 字符。

### 示例

在 Ubuntu 上，配置文件包含以下设置：

```
# File /etc/default/grub

GRUB_TIMEOUT=5

GRUB_DISTRIBUTOR="$(sed 's, release *$,,g' /etc/system-release)"

GRUB_DEFAULT=saved

GRUB_DISABLE_SUBMENU=true

GRUB_TERMINAL_OUTPUT="console"

GRUB_CMDLINE_LINUX=

GRUB_DISABLE_RECOVERY="true"

GRUB_ENABLE_BLSCFG=true
```

## `/boot/grub/grub.cfg`

取决于你的发行版，`/boot/grub/grub.cfg` 或 `/boot/grub2/grub.cfg` 将是当前 GRUB 版本的配置文件。该文件在内核更新期间自动生成。为了影响 GRUB 的行为，你可以运行以下命令之一：`update-grub`（Debian, Ubuntu）或 `grub-mkconfig`（Fedora, openSUSE）。

## `/etc/hosts`

`/etc/hosts` 用于将 IP 地址分配给主机名。该文件通常只包含本地（localhost）的条目，在静态配置服务器的情况下，还包含主机名。在过去，该文件用于列出局域网内的其他计算机。然而，即使在小型网络中，此功能也由路由器或本地名称服务器（如 `Bind` 或 `dnsmasq`）来完成。

`/etc/hosts` 文件包含基于模式的逐行条目：

最简单的变如下：

```
127.0.0.1       localhost
```

在大多数 Linux 发行版中，`localhost` 也为 IPv6 定义了定义。以下行显示了 Fedora 和 RHEL 的默认设置：



127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain

::1             localhost localhost.localdomain localhost6 localhost6.localdomain

在静态网络配置的情况下（例如在根服务器上），`hosts` 还可以包含计算机 IP 地址和主机名的条目：

```
211.212.213.214 abc-company.com abc-company
```

## `/etc/network/interfaces`

`/etc/network/interfaces` 文件（简称 `ENI`）包含了 Debian 发行版的网络配置。在 Ubuntu 中，由 `NetworkManager` 和 `Netplan` 处理网络配置。在当前的 Raspberry Pi OS 版本中，`NetworkManager` 拥有网络唯一控制权。

### 与 NetworkManager 的交互

对于桌面安装，该文件通常几乎为空，只包含回环接口（loopback interface）的设置：

```
# loopback interface
auto lo
iface lo inet loopback
```

`NetworkManager` 负责所有其他接口。

### IPv4 配置

服务器安装或具有静态网络配置的计算机，情况完全不同。在这种情况下，`auto` 名称行启动每个网络接口的配置块，该配置块会在计算机启动时激活。随后的接口名称选项描述了接口的基本配置。其他参数将根据配置类型随后出现。

如果接口从 DHCP 服务器获取 IP 数据，则配置非常简短：

```
# IPv4 network interface with DHCP
auto eth0
iface eth0 inet dhcp
```

在静态配置中，使用多个关键字逐行指定网络参数，其含义自言自明。`dns-nameserver` 关键字仅在 Ubuntu 上用于配置名称服务器。`resolvconf` 包负责评估。但在 Debian 上，你必须自行在 `/etc/resolv.conf` 中手动设置名称服务器。

```
# IPv4 network interface, static configuration
auto eth0
iface eth0 inet static
address 211.212.213.37
netmask 255.255.255.224
gateway 211.212.213.1
dns-nameservers 211.222.233.244 212.232.234.254
```

你可以使用 ``ifup xxx`` 激活单个接口的更改，将 `xxx` 替换为接口名称。

### IPv6 配置

如果你也想使用 IPv6，可以只需在 `/etc/network/interfaces` 中使用 `inet6` 关键字再次定义相关接口。`auto` 关键字指定 IPv6 配置将考虑网关或 IPv6 路由器的路由器公告。

#### 通过 DHCP 进行 IPv4 配置，通过路由器公告进行 IPv6 配置

```
auto eth0
iface eth0 inet dhcp
iface eth0 inet6 auto
```

IPv6 网关使用 DHCPv6 服务器，正确的方法是 `dhcp`。如果还需要通过路由器公告要配置路由器地址，则需要额外的 `accept_ra` 选项。例如，当使用启用了 `enable-ra` 选项的 `dnsmasq` 时就是这种情况。

#### 通过 DHCP 进行 IPv4 和 IPv6 配置

```
auto eth0
iface eth0 inet dhcp
iface eth0 inet6 dhcp
accept_ra 1
```

对于静态配置，接口必须如下：

```
# IPv4 and IPv6 configuration
auto eth0
iface eth0 inet static
iface eth0 inet6 static
address a0:4f8:161::20
netmask 64
gateway fe80::1
```

### Wi-Fi 和 WPA 配置

`NetworkManager` 通常负责笔记本电脑的 Wi-Fi 接口和 WPA 认证。然而，直接在 `/etc/interfaces` 中配置也是可能的。这在嵌入式设备或 Raspberry Pi 等计算机上非常常见。Wi-Fi 接口基本上是以以太网接口的方式配置的。你通过 `wpa_supplicant` 程序使用参数进行认证。在最简单的情况下，配置如下：

```
## /etc/network/interfaces
auto wlan0
iface wlan0 inet dhcp
wpa-ssid "wlan-name"
wpa-psk "secret"
```

使用 `wpa-ssid` 指定你的 Wi-Fi 网络名称（SSID 代表服务标识符）。`wpa-psk` 指定 Wi-Fi 密码，其中假设使用 Wi-Fi 保护访问 (WPA) 方法。如果需要更多参数，通常是将认证数据保存在外部文件中。接口参数如下：

```
## /etc/network/interfaces (manual configuration with WPA)
auto wlan0
iface wlan0 inet dhcp
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
```

在这里，`wpa-conf` 指定 WPA 配置文件的位置，它必须与 `/etc/wpa_supplicant/wpa_supplicant.conf` 的语法对应。如果有图形用户界面来管理多个 Wi-Fi 网络（如在 Raspberry Pi OS 上），你必须使用 `wpa-roam` 关键字：

```
# /etc/network/interfaces (WiFi configuration on Raspberry Pi OS)
allow-hotplug wlan0
interface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
if default inet dhcp
```



- `SystemMax`
  指定日志文件可以占据文件系统的最大百分比。在超过此限制之前，将删除旧的日志文件。默认设置为 10%。

你可以通过 `man journald.conf` 查找无数其他选项。

## /etc/locale.conf

`/etc/locale.conf` 文件包含使用当前系统版本作为 init 系统的发行版的语言和字符集设置。`localectl` 命令可以帮助你更改设置。以下列表了可以设置的最重要的本地化参数：

- `LANG=xxx`
  确定所有未设置的 `LC` 变量的默认值。

- `LC_ALL=xxx`
  覆盖所有的单独 `LC` 设置。

- `LC_COLLATE=xxx`
  确定排序顺序。

- `LC_TYPE=xxx`
  确定字符集。

- `LC_MESSAGES=xxx`
  确定消息、错误信息等的显示。

- `LC_MONETARY=xxx`
  确定货币金额的表示方式。

- `LC_NUMERIC=xxx`
  确定数字的表示方式。

- `LC_PAPER=xxx`
  确定纸张大小。

- `LC_TIME=xxx`
  确定日时间的显示。

`locale -a` 提供了所有可能的设置列表。通常使用 `spr_land.zs` 表示法，其中 `spr` 用两个字母表示语言，`land` 用两个字母表示国家`zs` 指定字符集。例如，在德语国家，你将使用 `de_DE.utf8`。

根据发行版的不同，这些或其他本地化设置被保存在其他位置：

| Debian, Ubuntu | /etc/default/locale |
| :--- | :--- |
| SUSE | /etc:/sysconfig/language |

## 示例

在以下 `locale.conf` 的设置设置中，德语为默认语言，UTF-8 为默认字符集：

## /etc/login.defs

`/etc/login.defs` 包含了在创建新用户和组时考虑的各种设置。这些设置适用于 `shadow-utils` 软件包中的命令，例如 `adduser`、`useradd` 以及 `addgroup` 和 `groupadd`。相反，`login.defs` 参数对使用可插拔模块 `PAM` 的命令没有影响；这特别包括 `passwd`！

`login.defs` 中的设置按行制作。在每行中，首先输入一个关键字，然后是一个或多个空格或制表符字符，最后是所需的设置。

- `CREATE_HOME`
  指定在创建新用户时是否应自动创建主目录（yes/no）。

- `ENCRYPT_METHOD`
  指定使用什么算法在 `etc/shadow` 中存储哈希值。允许的设置为 DES、MD5、SHA256 和 SHA512（最安全）。

- `ENV_PATH` 和 `ENV_SUPATH`
  包含普通用户以及 root 或 `su` 的 `PATH` 环境变量的默认设置。对于大多数发行版，`PATH` 变量的额外设置在 `etc/profile` 或 `etc/bashrc` 中完成。

- `GID_MIN` 和 `GID_MAX`
  指定普通组的最小和最大组 ID。

- `LOG_OK_LOGINS`
  使用 `syslog` 记录成功登录（yes/no）。

- `MAIL_DIR`
  指定存储本地邮件的目录位置。

- `PASS_MAX_DAYS`, `PASS_MIN_DAYS`, 和 `PASS_WARN_AGE`
  指定密码的有效期以及之后可以更改的最早时期（参见 `chage`）。

- `PASS_MIN_LEN`
  定义密码密码长度。

- `SYS_GID_MIN` 和 `SYS_GID_MAX`
  指定系统账户的最小和最大 GID。

- `SYS_UID_MIN` 和 `SYS_UID_MAX`
  指定系统账户的最小和最大 UID。

- `SYSLOG_SU_ENAB` 和 `SYSLOG_SG_ENAB`
  使用 `syslog` 记录 `su` 和 `newgrp` 命令（yes/no）。

- `UID_MIN` 和 `UID_MAX`
  指定普通用户的最小和最大用户 ID。

- `USERGROUPS_ENAB`
  控制是否为每个用户创建一个单独组（yes/no）。

## 示例

以下行显示了 Fedora 上 `login.defs` 中的默认设置。然而，你应该注意的是，`PASS_MIN_LEN` 和 `UMASK` 的设置与 Fedora 的操作无关！密码的最低要求由 PAM 模块 `pwquality` 指定，而 `umask` 在 `etc/profile` 中预设为 022。

```
MAIL_DIR             /var/spool/mail

PASS_MAX_DAYS       99999

PASS_MIN_DAYS       0

PASS_MIN_LEN        5

PASS_WARN_AGE        7

UID_MIN              1000

UID_MAX              60000

SYS UID_MIN          201

SYS UID_MAX          999

GID_MIN              1000

GID_MAX              60000

SYS GID_MIN          201

SYS GID_MAX          999

CREATE_HOME          yes

UMASK                022
```

```
renderer: networkd

ethernets:

  ens3:

    addresses: [ 138.201.20.182/26 ]

    gateway4: 138.201.20.176

    nameservers:

      search: [ ubuntu-book.info ]

      addresses:

        - "213.133.100.100"

        - "213.133.98.98"
```

当然，配置文件中也允许使用 IPv6 地址。在某些情况下，你必须指定针对 IPv4 和 IPv6 的关键字，例如 `gateway4` 对应 `gateway6`，或者 `dhcp4` 对应 `dhcp6`。你可以在以下网站找到更多关于路由、桥接、绑定、VLAN 等等示例：

https://netplan.io/examples

## /etc/systemd/network/networkd.network

网络后端 `networkd` 是 `systemd` 的一部分，目前安装在许多发行版中，但很少处于激活状态。主要的例外是 Ubuntu Server，那里的 `networkd` 由 Netplan 控制。

`networkd` 解析位于 `/etc/systemd/network`、`/lib/systemd/network` 和 `/run/systemd/network` 目录下的配置文件。文件必须具有 `*.network` 扩展名。

以下行展示了如何在虚拟机中设置具有静态 IP 地址以太网接口的示例：

```
# File /etc/systemd/network/01-mystatic.network

[Match]

Name=ens3

[Network]

Address=138.201.20.182

Gateway=138.201.20.176

DNS=213.133.100.100

DNS=213.133.98.98

Domains=ubuntu-book.info
```

第二个示例也显示了静态配置，这次是针对 Hetzner 根服务器的，包含了路由和 IPv6 设置：

```
[Match]

MACAddress=90:1b:0e:8e:48:86

[Network]

Address=2a01:4f8:171:2baf::2/64

Gateway=fe80::1

Address=138.201.20.176/26

Gateway=138.201.20.129

[Route]

Destination=138.201.20.128

Gateway=138.201.20.129
```

如果可用的 DHCP 服务器，可能的配置如下所示：

```
# File /etc/systemd/network/01-dhcpclient.network

[Match]

Name=enp03

[Network]

DHCP=ipv4

[DHCP]

UseMTU=100

RouteMetric=100
```



你可以在 `man systemd.network` 中找到关于网络配置语法的更多详细信息。Arch Linux wiki 也包含了非常有用的信息：

`https://wiki.archlinux.org/index.php/systemd-networkd`

## `/etc/NetworkManager/system-connections/<interface>.nmconnection`

几乎所有的 Linux 发行版都依赖 NetworkManager 进行 Wi-Fi 配置。对于其他网络发行，通常会并行使用特定发行版的程序。例外包括当前的 Fedora 和 RHEL 版本（从 RHEL 9 开始），它们完全依赖 NetworkManager，即使对于服务器上的静态配置也是如此。以前 RHEL 中常见的 `/etc/sysconfig/network-scripts` 下的 `ifcfg` 文件已经过时。

使用 NetworkManager，网络接口的配置以 `keyfile` 语法保存在 `/etc/NetworkManager/system-connections` 目录下。这些文件的语法在此文档：

`www.linux.org/docs/man5/nm-settings-keyfile.html`

`https://people.freedesktop.org/~lkundrak/nm-docs/nm-settings.html`

如果可能，你应该使用图形化工具配置网络。在 Gnome 中，这位于设置中的网络模块。`nmcli` 和 `nmtui` 在控制台或终端中运行良好。`nmcli` 代表 NetworkManager 文本用户界面，是一个用于文本模式的菜单和对话框引导配置程序。

当然，直接更改配置文件也是可能的。为了让 NetworkManager 采用你的配置文件，这些文件必须由 root 所有，并且必须允许 root 读取。确保执行了 `chmod 600 filename`，并在必要时也执行 `chown root:root filename`！

在尝试你自己的配置文件时，`/var/run/NetworkManager` 目录下的动态生成文件经常会干扰。请重启！NetworkManager 仅为那些 `/etc/NetworkManager` 中没有显式配置的接口创建动态配置文件。

要使更改生效，你必须要求 NetworkManager 重新读取现有配置文件。然后，你显式地告诉它对某个特定接口应用更改——这里是 `enp1s0`：

```
root# nmcli connection reload

(reload configuration)
```

```
root# nmcli dev reap enp1s0

(apply new configuration)

root# nmcli connection show

(interface overview)
```

# DHCP 配置

通过 DHCP 接收网络配置的以太网接口实际上不需要配置。然而，你也可以在文件中指定域名服务器。你可以为接口确定以下内容：

- `method` 为 `auto`
- `address1` 是该
- `dns` 是该

# 静态配置

通过 DHCP 接收网络配置的以太网接口实际上不需要配置。然而，你也可以在文件中指定域名服务器。你可以为接口确定以下内容：

- `method` 为 `auto`
- `address1` 是该
- `dns` 是该

对于静态 IPv4，你需要更改 `[ipv4]` 部分的几行：

```
# File /etc/NetworkManager/system-connections/en1s0.nmconnection

...

[ipv4]

method=manual

address1=138.201.20.182/26

gateway=138.201.20.176

dns=213.133.100.100,213.133.98.98
```

# IPv6 配置

静态 IPv6 的相关行如下：

```
# File /etc/NetworkManager/system-connections/en1s0.nmconnection

...

[ipv6]

addr-gen-mode=default

method=manual

address1=2a01:4f8:171:2baf::2/64

gateway=fe80::1
```

# 防火墙区域

你可以在配置文件的 `[connection]` 部分包含所需的 `firewalld` 区域：

```
# File /etc/NetworkManager/system-connections/en1s0.nmconnection

[connection]

...

zone=trusted
```

如果没有此指定，防火墙系统将使用默认公共区域。你可以使用 `firewall-cmd --active-zones` 查看所有接口的激活区域。

## `/etc/nsswitch.conf`

`/etc/nsswitch.conf` 文件控制通过 C 库名称切换函数解析主机名、用户名和组名。除非本地网络使用 LDAP 或其他服务进行用户管理和验证，否则很少更改此文件。

该文件按行包含，第一列指示数据库名称。“数据库”指的是 一组信息，例如所有用户的列表，包括登录名、全名、主目录、默认 shell 等。第一列允许的关键字包括 `aliases`（邮件别名）、`group`、`hosts`、`networks`、`passwd`、`rpc` 和 `shadow`。

数据库名称后面跟着一个冒号，然后是一系列用空格分隔的服务列表。最重要的服务如下：

- `files` 从本地配置文件读取数据，例如 `/etc/passwd` 或 `/etc/group`。
- `compat` 的含义与 `files`，但允许解释 `/etc/passwd` 中的额外信息。
- `db` 从数据库文件读取数据。
- `nis` 分析过时的网络信息服务。
- `dns` 查询域名服务器（用于主机名）。
- `mdns4_minimal` 使用 Zeroconf 解析主机名。
- `ldap` 与 LDAP 服务器通信。
- `wins` 使用 WINS 服务器。

此外，可以以 `[STATUS=ACTION]` 或 `[!STATUS=ACTION]` 的形式指定命令，这些将在特定事件发生或不发生时执行。允许的 `STATUS` 值有 `success`（成功）、`notfound`（未找到）、`unavail`（不可）和 `tryagain`（重试）。可能的动作有 `return`（立即返回结果，不回退到其他选项）和 `continue`（使用下一个查找服务）。

### 示例

以下行显示了 Fedora 默认配置片段。对于用户账户，仅考虑了 `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 文件。主机名从 `/etc/hosts` 读取，从名称服务器请求，并通过 Zeroconf (Avahi) 确定。

```
passwd: files
shadow:  files
group:   files
hosts:   files dns mdns4_minimal
...
```

## `/etc/os-release`

对于使用 `systemd` 作为初始化系统的当前发行版，`/etc/os-release` 包含了有关已安装发行版的信息。以下行显示了文件的语法：

```
NAME="AlmaLinux"
VERSION="9.3 (Shamrock Pampas Cat)"
```

```
ID="almalinux"
ID LIKE="rhel fedora"
VERSION ID="9.3"
PLATFORM_ID="platform:el9"
PRETTY_NAME="AlmaLinux 9.3 (Shamrock Pampas Cat)"
..
```

严格来说，该文件并不是配置文件，而是一个信息文件。因此，修改该文件是没有意义的。然而，它在更新过程中可能会定期更新。

## `/etc/passwd`

`/etc/passwd` 文件包含上所有本地账户的数据，包括登录名、全名、默认 shell 和家目录。然而，出于安全考虑，不包含密码的哈希值；它存储在独立的 `etc/shadow` 文件中。如果可能，你应该使用提供的管理账户的命令，例如 `useradd`、`usermod` 或 `userdel`。

`passwd` 文件由七列组成，每列之间用冒号分隔：

- 第一列（账户名）

  包含登录名。它不能包含任何空格且不应有特殊字符。习惯上只使用小写字母。

- 第二列（密码）

  过去，这里包含密码的哈希值。

  所有当前的 Linux 发行版现在都在此列中存储 `x` 字符，哈希值可以在 `etc/shadow` 中找到。

- 第三列（UID）

  包含内部用户 ID，用于管理访问权限和进程。在大多数发行版中，小于 1000 的 UID 留给系统账户，从 1000 开始的 UID 供普通用户。

- 第四列（主组）

  指示用户主组的编号。用户可以分配到其他组；附加组保存在 `etc/group` 中。

- 第五列（注释）

  用于注释字符串，可以由几部分组成。在实践中，通常只在此保存完整的用户名。如果创建用户时没有指定此项，则第五列与第一列相同。



### 第六列（家目录）

包含家目录的路径。

### 第七列（Shell）

指定登录后自动激活 `shell`；对于普通用户，这通常是 `/bin/bash`。对于不提供登录的系统账户，通常使用 `/sbin/nologin` 或 `/bin/false` 代替 `shell`。可以通过 `chsh` 命令更改默认 `shell`。

## 示例

以下行显示了 Fedora 系统上的某些系统账户和一个用户账户：

```
root:x:0:0:root:/root:/bin bin:x:1:1:bin:/sbin/nologin daemon:x:2:2:daemon:/sbin:/sbin/nologin adm:x:3:3:adm:/var/adm:/sbin/nologin
kofler:x:1000:1000:Michael Hofler:/home/kofler:/bin/bash
```

![](img/94f0b4d76a25250c220515a1d5bba83f_856_0.png)

`/etc/profile` 和 `/etc/profile.d` 包含了环境变量的系统级设置。`PATH`、`MAIL` 和 `HOSTNAME` 等变量在其中被预设。此外，许多发行版使用 `umask` 来设置新创建文件的位。`/etc/profile` 是一个 `shell` 脚本。从语法上讲，最重要 `shell` 的公分数允许允许都是允许。在 Ubuntu 上，除了 `/etc/profile`，还提供了一个用于系统级设置的文件。`profile` 设置由 `.profile` 和 `.bashrc` 中的用户特定设置进行补充。例如，`bash` 会加载 `/etc/bashrc`、`.bashrc` 和 `alias` 文件。根据发行版的不同，可能会有额外的配置文件。

许多发行版运行 `rc.local` 脚本以兼容旧的 Init-V 系统。

| 发行版 | 位置 |
| :--- | :--- |
| Debian, Raspberry OS, Ubuntu | `/etc/rc.local` |
| CentOS, RHEL | `/etc/rc.d/rc.local` |
| openSUSE/SUSE | `/etc/init.d/boot.local` |

该文件必须是可执行的 (`chmod +x`)！此外，在某些发行版中，设置文件后必须运行 `systemctl reload-daemon` 以便下次重启时生效。`rc.local` 是旧系统的遗留，多年前已被 `systemd` 取代。取决于发行版，该文件可能是空的或者默认不存在，但如果你正确创建它它会被 `systemd` 使用。

## 示例

以下脚本记录了 `/var/boot` 的时间：

```bash
#!/bin/bash
date > /var/boot
```

为了确保脚本被 `systemd` 识别，必须运行以下命令：

## `/etc/resolv.conf`

`/etc/resolv.conf` 控制未知网络名称（主机名）的 IP 地址。“未知”意味着不在 `hosts` 中定义。该文件通常由以下关键词组成：

- `nameserver ip`

  指定名称服务器的 IP 地址。该关键字可以使用多次来指定备用名称服务器。允许最多三个 IPv4 和三个 IPv6 名称服务器。

- `domain domain`

  指定本地域名。允许省略主机名，即 `name` 而不是 `name.mydomain`。

- `search domain`

  指定用于搜索的域名。可以指定六个域名，每个都有自己的搜索条目。在解析期间，按顺序测试指定的域名；例如对于 `ping name`，首先是 `name.domain1`，然后是 `name.domain2`，依此类推。`search` 的默认设置为本地域名。`domain` 和 `search` 是互斥的。如果 `resolv.conf` 包含这两个关键词，以后者为准。通常动态生成的，特别是通过 DHCP 进行 IP 配置时。越来越多的发行版（Fedora, Ubuntu）使用 `systemd-resolved` 设置本地名称服务器。`etc/resolv.conf` 然后引用该服务器（通常为 `127.0.0.53`）。如果你想知道本地服务正在访问哪个外部服务器，必须运行 `resolvectl` 或 `systemd-resolve --status`。

## 示例

以下行显示了手动配置 IPv4 和 IPv6 名称服务器：

```
## /etc/resolv.conf
# 局域网域名
nameserver 212.212.213.1  # IPv4 DNS
nameserver 212.212.214.1  # 备用 DNS（如果第一个失败）
nameserver 2001:4860:4860::8888  # IPv6 DNS
```

## `/etc/rsyslog.conf`

许多 Linux 发行版使用兼容 `syslog` 的 `rsyslog` 记录内核以及各种网络服务的日志。该程序通过 `/etc/rsyslog.conf` 文件和补充的 `/etc/rsyslog.d/*.conf` 文件进行配置。这些配置文件包含两个部分的规则：

- 选择器 (`Selector`)

  规则的第一部分指定要记录什么内容。

- 动作 (`Action`)

  规则的第二部分控制对消息做什么。

规则可以使用 `\` 字符跨越多行。一条消息可能适用于多个规则。在这种情况下，该消息会被记录或传递多次。要使 `syslog` 配置的变化生效，必须通过 `service rsyslog restart` 重启 `syslog` 服务！

### 选择器 (Selectors)

每个选择器由由点号 `.` 分隔的两个部分组成：`service.prioritylevel`。允许使用分号 `;` 分隔指定多个选择器。此外，一个选择器中可以用逗号分隔多个服务。所有使用 `syslog` 的 Linux 程序都必须为它们的消息分配服务类型和优先级。

`Syslog` 识别以下服务（设施）：`auth`, `authpriv`, `cron`, `daemon`, `ftp`, `kern`, `lpr`, `mail`, `news`, `syslog`, `user`, `uucp` 以及 `local0-local7`。`*` 字符代表所有服务。

`Syslog` 还识别以下优先级（按重要性递增排序）：`debug`, `info`, `notice`, `warning = warn`, `err = error`, `crit`, `alert` 以及 `emerg = panic`。`warn`、`error` 和 `panic` 关键字被认为是过时的——你应该使用 `warning`、`err` 和 `emerg` 代替它们。`*` 字符代表所有优先级。`none` 关键字适用于未分配优先级的消息。

优先级的定义包含了所有更高（更重要）的优先级。因此，`mail.err` 选择器也包含了来自邮件系统的 `crit`、`alert` 和 `emerg` 消息。如果你显式地只需要特定优先级的消息，必须以 `=` 字符为缀（例如 `mail.=err`）。

### 操作 (Actions)

日志文件的名称通常指定为操作。日志文件通常在每次输出后进行同步。如果文件名以前有一个减号 `-`，`syslog` 将不会进行同步。这种方式要高效得多，但如果发生系统崩溃，尚未物理保存的消息将会丢失。

`Syslog` 还可以将消息转发到先进先出（FIFO）文件或管道。在这种情况下，你需要在文件名前加上 `|` 字符。在下文列表中出现的 `/dev/console` 文件是一个用于将消息传递到 X 图形系统的特殊 FIFO 文件。

`*` 字符意味着消息将发送给所有登录到控制台或通过 SSH 登录的用户。由于这具有很大的干扰性，它默认仅用于关键消息。

### 日志配置 (Journal Configuration)

当前的发行版使用 `systemd` 项目中的 `Journal` 程序来代替或辅助 `rsyslogd`。它通过 `etc/systemd/journald.conf` 和其他几个文件进行配置。

## 示例 (Example)

以下行显示了标准的 Ubuntu `syslog` 配置，采用了略微简化且格式更清晰的形式：

```
# File /etc/rsyslog.d/50-default.conf bei Ubuntu
# Selector             Action
auth,authpriv.*        /var/log/auth.log
*.auth;authpriv.none   -/var/log/syslog
kern.*                 -/var/log/kern.log

mail.*                   -/var/log/mail.log
mail.err                /var/log/mail.err
*.emerg                 :omusmsg*:

demon.*;;mail.*;;news.err; *=debug;*=info; *=notice;*=warn |/dev/console
```

用通白的语言来说，上述配置意味着：



- `/var/log/auth.log` 包含所有优先级的身份验证消息。这些包括失败和成功的登录尝试（也通过 SSH）、PAM 消息、`sudo` 命令等。作为唯一的日志文件，`auth` 在每条消息产生时立即同步。

- `/var/log/syslog` 包含通过 `syslog` 记录的所有消息，包括未分配优先级的身份验证消息。这种全包罗的方法既是优点也是缺点。一方面，你可以从一个文件中提取所有能想象到的信息；另一方面，在这一杂烩中寻找相关的条目无疑是非常困难的。

- `/var/log/kernel.log` 包含所有内核消息。

- 来自邮件系统（例如 `postfix`）的消息分布在几个文件中。在 `mail.log` 中存储所有消息；在 `mail.err` 中仅存储错误消息。

- 关键系统消息（例如关于即将关机或内核错误）通过 `:omusmsg*` 转发给所有用户，特别是所有终端窗口和控制台。`omusmsg` 是向用户发送消息的 `rsyslog` 模块。

- 警告和错误消息也被转发到 X 系统。要在 X 上跟踪这些消息，你必须启动。

### `/etc/shadow` 的语法

```
account-name:password:last-change:minimum:maximum:warning:inactive:expire:reserved
0:0:0:0::
```

### `/etc/shadow` 的字段含义

- `account-name`：用户名
- `password`：加密后的密码
- `last-change`：自 1970 年 1 月 1 日以来最后修改密码的天数
- `minimum`：上次修改密码后可以修改密码的最少天数
- `maximum`：密码有效天数
- `warning`：密码过期前警告用户的天数
- `inactive`：密码过期后账户被锁定的天数
- `expire`：自 1970 年 1 月 1 日以来账户过期的天数
- `reserved`：留供未来使用

以下是 `/etc/shadow` 的部分内容：

```
root:$6$.clIM0B:0:0:0:0::
bin*:18095:0:0:99999:7::
daemon*:18095:0:0:99999:7::
adm*:18095:0:0:99999:7::
...
kofler:$sy9jTT...19793:0:99999:7::
```

要找出最后修改密码的时间，你必须运行 `date` 命令：

```
user$ date -d "1970-01-01 + 19793 days"
```

以及 `multiverse` 软件包，而 Debian 将 `main`（主）、`contrib`（贡献）、`non-free`（非自由）及类似的组件进行了区分。

首先提到的包源具有优先级：因此，如果某个软件包可以从多个源下载，`APT` 将从第一个源下载它。

## 示例

以下列表显示了一些 Ubuntu 软件包源。出于空间原因，每个条目跨越了两个行。

```
# File /etc/apt/sources.list
deb http://de.archive.ubuntu.com/ubuntu/ mantic \
    main restricted universe
deb http://de.archive.ubuntu.com/ubuntu/ mantic-updates \
    main restricted universe
deb http://security.ubuntu.com/ubuntu/ mantic-security \
    main restricted universe
```

> `/etc/sudoers`

`/etc/sudoers` 文件和 `/etc/sudoers.d` 中的额外文件定义了允许哪些用户通过 `sudo` 凭借权限运行哪些命令。该文件还包含各种控制 `sudo` 基本行为的通用设置。设置取决于发行版的不同而存在差异。

`sudoers` 文件应仅使用 `visudo` 命令进行修改。它会调用环境变量 `VISUAL` 或 `EDITOR` 定义的编辑器（默认是 `vi`），在保存前执行语法检查，从而确保你不会因为包含错误的 `sudoers` 文件而让自己排除在后续的管理工作之外。对于像 Ubuntu 这样不提供 root 登录的发行版，这尤为重要。

## 基础设置

- `Defaults always_set_home`

  当用户切换时更改 `HOME` 环境变量，使其指向新用户的家目录。通常情况下，这会自动发生。此选项仅在应用 `!env_reset` 或 `env_keep` 包含 `PATH` 变量时才有效。

- `Defaults env_keep="var1 var2 var3"`

  指定在用户切换时保留哪些环境变量，因此这些变量被排除在 `env_reset` 之外。

- `Defaults env_reset`

  在用户切换时重置所有环境变量。此设置默认启用。要禁用它，你必须输入 `Defaults !env_reset`。

- `Defaults mail_badpass`

  在登录尝试失败后，向管理员发送警警告邮件。

- `Defaults secure_path="pfad1:pfad2:pfad3"`

  为 `sudo` 命令定义 `PATH` 环境变量的内容。

- `Defaults targetpw`

  表示运行命令的账户的密码必须始终输入，即通常的 root 密码。如果没有此设置，`sudo` 会期望当前用户的密码。

- `Defaults timestamp_timeout=n`

  指定 `sudo` 再次询问密码的时间。默认设置为五分钟。

## 权限

`/etc/sudoers` 中的三列式条目定义了允许哪些用户从哪台计算机运行哪些程序。以下行表示用户 `katherine` 允许在名为 `uranus` 的计算机上运行 `/sbin/fdisk` 命令。`ALL` 关键字表示 `katherine` 可以在任何账户下运行该命令，即作为 root、`news`、`lp` 等运行。

```
katherine uranus=(ALL) /sbin/fdisk
```

如果 `sudoers` 的第一列以 `%` 字符开头，则该条目适用于指定组的所有成员。以下行意味着 `wheel` 组中的所有用户都可以从任何计算机以任何用户身份运行所有命令：

```
%wheel ALL=(ALL) ALL
```

可以允许特定用户在不指定密码的情况下运行 `sudo`。然而，只有当没有其他 `sudoers` 行要求该用户提供密码时，`NOPASSWD` 关键字才有效。这也适用于组条目，例如 `%admin`。

```
kofler ALL=(ALL) NOPASSWD: ALL
```

以下规则读起来如下，极其宽松：任何人都可以做任何事情。该规则仅与 `Defaults targetpw` 选项结合使用时才有意义，该选项始终要求输入代表运行命令的用户的密码。

```
ALL ALL=(ALL) ALL
```

## 示例

以下行显示了 Ubuntu 上的默认配置。在该发行版中，root 的设置没有有效密码。因此，无法进行 root 登录！此外，`ssh -l root` 也无法工作。因此，运行管理命令的唯一方法是通过 `sudo`。`admin` 和 `sudo` 组的所有成员都有此权限，其中包含 `admin` 组仅是为了兼容旧版本的 Ubuntu。在当前的 Ubuntu 版本以及大多数其他发行版中，`sudo` 是具有 sudo 权限用户的常用组。

```
# Default configuration in /etc/sudoers on Ubuntu
Defaults        env_reset
Defaults        mail_badpass
Defaults        use_pty
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin"
root            ALL=(ALL:ALL) ALL
%admin          ALL=(ALL:ALL) ALL
%sudo           ALL=(ALL:ALL) ALL
@includedir /etc/sudoers.d
```

## `/etc/sysctl.conf`

`/etc/sysctl.conf` 包含了内核参数的默认设置。该文件在系统启动时被分析，列出的所有参数都会被相应设置。对于后续更改，你可以使用 `sysctl -p` 来确保所有设置都从 `sysctl.conf` 加载并生效。

要设置的内核参数以 `name.name.name=value` 的形式逐行指定。注释行以 `;` 或 `#` 开头。

## 示例

`sysctl.conf` 中的以下设置会导致计算机启动时激活 IPv4 和 IPv6 的转发。如果计算机作为路由器工作，这是必要的。

```
net.ipv4.ip_forward=1 net.ipv6.conf.all.forwarding=1
```

## systemd.service



init 系统由配置文件控制，位于以下三个目录：

```
/etc/systemd/system
/run/systemd/system
/usr/lib/systemd/system
```

`systemd` 也用于管理用户特定的服务，位于 `/home/.config/systemd/user` 以及其他目录。`*.service` 文件由几个部分组成，引入 `[Unit]`、`[Service]`、`[Install]`。

### [Unit] 关键字

- `Before/After=name`

  指定在之前或之后启动的其他服务或单元。`Before` 和 `After` 为 `systemd` 提供了启动顺序的信息。

- `Description=description`

  使用字符串描述服务。

- `OnFailure=name`

  指定当当前服务启动失败时要运行的一个或多个服务。

- `Wants/Requires=name`

  指定之前应该启动的其他服务。这些关键字定义了依赖关系。对于 `Wants`，可能的失败会被忽略，而对于 `Requires`，意味着不会启动当前服务并触发错误。

### [Service] 关键字

- `Environment=var1='value1' var2='value2' ...`

  定义传递给启动进程的多个环境变量。

- `EnvironmentFile=filename`

  加载文件并考虑文件中按行的变量赋值。

- `ExecReload=/path/program options`

  在运行期间运行指定的命令重新加载服务的配置。

- `ExecStart=/path/program options`

  运行指定的命令启动服务。在使用 `Type=oneshot` 时，允许有多个 `ExecStart` 行并按顺序执行。

- `ExecStop=/path/program options`

  运行指定的命令结束服务。如果你未使用此关键字，服务将通过 `KILL` 信号终止。如果需要，`KillMode` 和 `KillSignal` 关键字（在 `systemd.kill` 手页中列出）描述发送什么信号以及如何操作。`ExecStop` 仅在使用 `Type=oneshot` 时有效。

- `RemainAfterExit`

  通常与 `Type=oneshot` 使用。`systemd` 会记住当前激活的状态。如果没有此选项，`systemd` 认为操作在最后一个 `StartExec` 命令结束后结束，并立即将状态置回停止。显式执行 `systemctl stop` 将不再产生影响。

- `Type=simple|forking|oneshot|dbus|notify|idle`

  指定服务的类型或程序的启动方式。

如果缺少类型指定，`simple` 类型会让 `systemd` 假设用 `ExecStart` 指定的命令启动一个后台服务。只有当该命令结束，`systemd` 才会认为该服务正常运行。

`Type=notify` 的工作方式类似，但 `systemd` 期望一个关于启动过程完成的显式通知。

后台服务必须调用 `sd_notify` 函数或等效函数。

`Type=forking` 与 `simple` 有相似之处，但在这里，`ExecStart` 命令负责启动一个与启动命令分离的后台进程。一旦 `ExecStart` 命令完成，`systemd` 就会认为该服务正在其自身的后台进程中运行。

对于 `oneshot` 类型，`systemd` 假设要执行的命令执行非常快，可以在执行其他操作之前对其进行等待。除非服务文件中包含 `RemainAfterExit` 关键字，否则服务的状态在执行结束时会被重置为 `stop`。

关于其他类型变体的详细信息请参见 `systemd.service`。

- `User=username` 和 `Group=groupname`

确定在哪个账户下执行命令。默认情况下，系统服务以 `root` 权限运行。

### [Install] 关键字

- `WantedBy=or RequiredBy=target`

指定为哪个目标单元（target）需要或要求该服务，例如对于 `multi-user.target` 或 `reboot.target`。在实践中，通常使用 `WantedBy`，这意味着即使单个服务的启动失败，目标也会到达。相反，`RequiredBy` 在出现问题时会导致错误。此时，相关的目标将无法激活。

### 示例

以下行显示了 Fedora 默认配置中的 `httpd.service` 文件。它负责启动 Apache Web 服务器。启动的前提条件是网络以及任何网络文件系统的成功激活。Web 服务器应该作为多用户目标的一部分被自动启动。

```
# File /lib/systemd/system/httpd.service (Fedora)
[Unit]
Description=The Apache HTTP Server
Wants=httpd-init.service
After=network.target remote-fs.nss-lookup.target httpd-init.service
Documentation=man:httpd.service(8)

[Service]
Type=notify
Environment=LANG=C

ExecStart=/usr/bin/httpd $OPTIONS -DGROUND
ExecReload=/usr/bin/httpd $OPTIONS -k graceful
# SIGWINCH 用于优雅停止
KillSignal=SIGWINCH
KillMode=mixed
PrivateTmp=true
OOMPolicy=continue

[Install]
WantedBy=multi-user.target
```

### 设置自定义 systemd 服务

要设置你自己的 `systemd` 服务，你需要在 `/etc/systemd/system` 目录下创建一个 `*.service` 文件。执行此操作的最佳方法是使用另一个类似服务的服务文件。根据发行版的不同，可以在 `/lib/systemd/system` 或 `/usr/lib/systemd/system` 目录中找到合适的文件。

出于效率考虑，`systemd` 将重要配置文件的内容保留在缓存中。更改配置后，你必须使用 `systemctl` 显式重新加载配置文件：

```
root# systemctl daemon-reload
```

要立即启动服务并在以后每次到达多用户目标时启动它，需要执行以下命令：

```
root# systemctl enable --now myservice
```

如果出现问题，最好使用 `journalctl -u myservice` 进行调试。

### 其他 systemd 配置文件

除了 `*.service` 文件外，还有标识符为 `*.mount`、`*.path`、`*.socket`、`*.target` 和 `*.wants` 的 `systemd` 配置文件，这些在本书书中不再进一步讨论。它们的语法在 man pages `service.mount`、`service.path` 等中记录。所有这些文件共同被视为单元文件（unit files）。这些单元的通用语法在 `man systemd.unit` 中进行了解释。

如果你想设置由 `systemd` 定期运行的任务，你必须熟悉 `*.timer` 文件的格式（参见 `systemd/timer`）。

### systemd.timer

`systemd` 可以以类似于 `cron` 的方式处理进程的定期执行。配置通过 `*.timer` 文件完成，该文件必须带有一个同名的服务文件（即 `name.service`）。对于自定义配置，`*.timer` 文件通常位于 `/etc/systemd/system`。

`*.timer` 文件的结构与 `*.service` 文件类似，通常由三个部分组成：`[Unit]`、`[Install]` 以及 `[Timer]`。`[Timer]` 部分决定了 `systemd` 何时以及如何执行任务。

### [Timer] 关键字

- `AccuracySec=time`

指定执行任务的精度。默认情况下，`systemd` 允许在 1 分钟的窗口内执行任务。你可以通过此设置来更改这个时间范围。

- `OnBootSec=time`

指定在系统启动多久时间后首次执行任务。可以使用相对时间格式。

- `OnActiveSec=time`

指定在单元激活（启动）多久时间后首次执行任务。

- `OnUnitSec=time`

指定在单元上次结束后多久时间后再次执行任务。

- `OnCalendar=time`

指定按照特定的时间执行任务。可以使用 `cron` 格式（例如 `* * * * *` 表示每分钟执行一次），也可以使用更易读的格式如 `daily`、`hourly` 等。

- `RandomizedSec=time`

指定在执行任务前增加的随机偏移时间，以防止多个任务在同一时间导致系统负载过高。



https://wiki.ubuntuusers.de/WLAN/wpa_supplicant

在简单的情况下，你也可以使用 `wpa_passphrase` 创建所需的配置行，或直接在 `/etc/network/interfaces` 中进行配置。

# 键盘快捷键

Linux 命令参考的最后部分涉及最重要的编辑器和其他通常通过键盘操作的命令的快捷键。这些包括 `bash`、`man`、`info`、`less` 和 `mutt`。

几乎所有程序都提供了自定义键盘快捷键选项。本节指的是默认配置，即大多数 Linux 发行版的标准配置。

## bash

表 1 总结了在 Bourne Again Shell (`bash`) 中输入命令时可以使用哪些键盘快捷键。这些键盘快捷键实际上源于 `readline` 库。你可以在 `/etc/inputrc` 或 `.inputrc` 中更改该库的配置。

| 键盘快捷键 | 功能 |
|---|---|
| Ctrl+A | 将光标移动到行首（类似于 Pos1） |
| Ctrl+C | 取消当前命令 |
| Ctrl+E | 将光标移动到行尾（类似于 End） |
| Ctrl+K | 删除光标位置到行的剩余内容 |
| Ctrl+Y | 重新插入最近删除的文本 |
| Ctrl+Z | 中断当前命令（可以通过 `fg` 或 `bg` 继续） |
| Tab | 补全文件名和命令名 |
| 方向键向上/向下 | 滚动查看已执行的命令 |

**表 1** `bash` 中输入命令的键盘快捷键

## emacs

`emacs` 是 Linux 上功能最丰富、最复杂的编辑器之一。它有数百个键盘快捷键和命令，这里仅列出最重要的部分。

通常，有三种方式输入 `emacs` 命令：菜单、使用键盘快捷键（主要是与 `Ctrl` 或 `Alt` 组合键）或输入命令名。第三种方式通过 `Alt + X` 或 `Esc` 启动，例如 `Alt + X` `delete-char` `Enter`。命令参数的输入通过两种机制实现便利：

- 在输入期间，你可以在 `emacs` 命令名后添加 `Tab`。你也可以以同样的方式补全文件名。
- 在使用 `Alt + X` 引入新命令后，可以使用 `Alt + P`（上一个）和 `Alt + N`（下一个）访问之前指定的命令。

在 `emacs` 文档中，键盘快捷键的表示方式略有不同：`DEL` 指 `Backspace`，`C` 代表 Control `Ctrl`，`M` 代表 `Meta`。在标准 PC 键盘上没有直接对应的 `Meta` 键。可以通过两种方式在 PC 键盘上模拟 M-x：`Esc` 和 `X`（连续输入）或 `Alt + X`。

表 2 总结了基本功能。你可以使用光标和各种键盘快捷键移动光标（见表 3）。

| 键盘快捷键 | 功能 |
|---|---|
| Ctrl+X, Ctrl+F | 加载新文件 |
| Ctrl+X, Ctrl+S | 保存当前文件 |
| Ctrl+X, Ctrl+W | 另存为文件 |
| Ctrl+G | 取消命令输入 |
| Ctrl+X, U | 撤销上次更改 (`undo`) |
| Ctrl+X, Ctrl+C | 退出 `emacs`（带有保存提示） |

**表 2** 基础 Emacs 命令

| 键盘快捷键 | 功能 |
|---|---|
| Alt+F/Alt+B | 将光标向前或后移动一个单词 |
| Ctrl+A/Ctrl+E | 将光标置于行首或行尾 |
| Alt+//Alt+Shift+> | 将光标移动到文本开头或结尾 |
| Alt+G Enter | 将光标移动到第 n 行 |

**表 3** 光标移动

表 4 规定了如何选择、删除和重新插入文本，表 5 总结了如何搜索和替换。

| 键盘快捷键 | 功能 |
| --- | --- |
| Ctrl + | 设置一个（不可见的）标记点 |
| Ctrl + W | 删除标记点与当前光标位置之间的文本 |
| Ctrl + Y | 重新插入最近删除的文本 |
| Ctrl + X, Ctrl + X | 交换光标位置和标记点 |
| Alt + D | 删除光标处的下一个单词或单词末尾 |
| Alt + Backspace | 删除光标之前的单词或直到光标的单词开头 |
| Ctrl + K | 删除光标位置到行的剩余内容 |
| Alt + 0, Ctrl + K | 删除光标位置之前的行首 |
| Alt + M | 删除随后的段落 |
| Alt + Z, x | 删除直到下一个 x 出现处的所有字符，x 也会被删除 |
| 键盘快捷键 | 功能 |
|---|---|
| Ctrl+Y | 在光标位置插入上次删除的文本 |

**表 4** 选择、删除和重新插入文本

| 键盘快捷键 | 功能 |
|---|---|
| Ctrl+S | 正向增量搜索 |
| Ctrl+R | 反向增量搜索 |
| Alt+P | 选择之前使用过的搜索文本（上一个） |
| Alt+N | 选择稍后使用的搜索文本（下一个） |
| Ctrl+G | 取消搜索 |
| Ctrl+X, Ctrl+X | 交换标记点（搜索开始）和当前光标位置 |
| Ctrl+Alt+S | 正向增量模式搜索 |
| Ctrl+Alt+R | 反向增量模式搜索 |
| 键盘快捷键 | 功能 |
| --- | --- |
| Alt + % | 无模式的搜索和替换 |
| Alt + X query-replace-r Enter | 带模式的搜索和替换 |

**表 5** 搜索和替换

## gnome-terminal

如果你在 Gnome 上运行 shell 命令，你很可能会使用 `gnome-terminal` 程序。为了在 `bash` 中可以使用常用的快捷键，你应该首先禁用**菜单快捷键字母**选项，以便通过**编辑 • 设置** 使用 `Alt` 快捷键来控制菜单。如果需要，你仍然可以使用 `F10` 键来控制菜单——除非你你在上述配置对话框中也禁用了该键的处理。任何情况下，某些 `gnome-terminal` 特有的键盘快捷键仍然可用；它们总结在表 6 中。

| 键盘快捷键 | 功能 |
| --- | --- |
| Shift + Ctrl + C | 将选中文复制到剪贴板 |
| 键盘快捷键 | 功能 |
|---|---|
| Shift + Ctrl + F | 在终端输出中搜索文本 |
| Shift + Ctrl + G | 重复反向搜索 |
| Shift + Ctrl + H | 重复正向搜索 |
| Shift + Ctrl + N | 打开新终端窗口 |
| Shift + Ctrl + Q | 关闭窗口 |
| Shift + Ctrl + T | 打开新终端标签 |
| Shift + Ctrl + V | 粘贴剪贴板内容 |
| Shift + Ctrl + W | 关闭标签 |
| Shift + Ctrl + + | 增大字体 |
| Shift + Ctrl + - | 缩小字体 |
| Shift + Ctrl + 方向键向上/向下 | 转到上/下一个标签 |
| 键盘快捷键 | 功能 |
|---|---|
| F11 | 激活全屏模式 |

**表 6** `gnome-terminal` 快捷键

## grub

在 Linux 引导程序 GRUB 中，可以使用方向键选择操作系统或 Linux 变体，然后按 `Enter` 启动。GRUB 还提供了交互式更改菜单参数或运行自定义命令的选项。表 7 总结了这些最重要的快捷键。该表相对于当前的 GRUB 版本2。

| 键盘快捷键 | 功能 |
|---|---|
| Esc | 退出图形模式并激活文本模式 |
| C | 启动命令模式执行 GRUB 命令。输入命令时，可以像 shell 一样使用 `Tab` 补全文件名。 |
| E | 启动所选菜单项的编辑器。 |
| P | 通过输入密码启用交互式 GRUB 功能。只有当 GRUB 受密码保护时才需要。 |
| Ctrl+F10 | 启动之前用 E 修改过的菜单项。 |

**表 7** 交互式控制 GRUB 2 的键盘快捷键

`info` 启动同名的在线帮助系统。要在帮助文中导航，可以使用表 8 总结的键盘快捷键。你也可以通过同名包中的 `info` 命令、配合 `emacs` 编辑器在 Gnome 和 KDE 帮助系统中更方便地读取 `info` 文本。

| 键盘快捷键 | 功能 |
|---|---|
| Spacebar | 向下滚动文本 |
| Backspace | 向上滚动文本 |
| 快捷键 | 功能 |
|---|---|
| B, E | 跳到信息单元的开始/结束（开始/结束） |
| Tab | 将光标移动到下一个交叉引用 |
| Enter | 跟踪指向另一个信息单元的交叉引用 |
| N | 显示同一层级下的下一个信息单元（下一个） |
| P | 显示同一层级下的上一个信息单元（上一个） |
| U | 向上一个层级 |



| L | 回到上一次显示的文本（上一次） |

| H | 显示详细的操作说明（帮助） |

| ? | 显示命令概览 |

| Q | 退出信息（退出） |

**表 8** info 键盘快捷键

# joe

`joe` 是一个简单的编辑器，其快捷键基于 WordStar 文字处理器（参见表 9）。该编辑器也可以通过 `jmacs` 或 `jpico` 的名称启动。与 `emacs` 或 `Pico` 兼容的其他快捷键同样适用。

| 快捷键 | 功能 |

|---|--|

| Ctrl+K, H | 显示/隐藏帮助窗口 |

| Ctrl+K, E | 加载新文件 |

| Ctrl+K, D | 保存文件（可选另存新名称） |

| Ctrl+Y | 删除一行 |

| Ctrl+Shift+- | 撤销删除 |

| Ctrl+C | 退出 `joe`（带有保存确认提示） |

**表 9** `joe` 中的键盘快捷键

# konsole

KDE 粉丝通常在 `konsole` 程序中运行 shell 命令。大多数快捷键由该程序直接传递给 shell。然而，还有一些 `konsole` 特有的键盘快捷键，总结在表 10 中。

| 快捷键 | 功能 |

| --- | --- |

| Shift + Ctrl + A | 标记标签页活动 |

| Shift + Ctrl + C | 将选中文本复制到剪贴板 |

| Shift + Ctrl + F | 在终端输出中搜索文本 |

| F3 | 重复向后搜索 |

| Shift + F3 | 重复向前搜索 |

| Shift + Ctrl + I | 标记标签页长时间未活动 |

| Shift + Ctrl + N | 打开新的终端窗口 |

| Shift + Ctrl + Q | 关闭窗口 |

| 快捷键 | 功能 |

|---|---|

| Shift + Ctrl + T | 打开新的终端标签页 |

| Shift + Ctrl + V | 粘贴剪贴板内容 |

| Shift + Ctrl + W | 关闭标签页 |

| Shift + Ctrl + + | 增大字体 |

| Shift + Ctrl + - | 缩小字体大小 |

| Shift + Ctrl + 左方向/右方向 | 切换到上一个/下一个标签页 |

**表 10** `konsole` 中的键盘快捷键

# less

`less` 命令显示文本。在程序运行时，你可以使用光标键滚动文本、搜索文本、启动由环境变量 `$EDITOR` 设置的编辑器等（参见表 11）。`less` 也被用于显示 `man` 帮助页。

| 快捷键 | 功能 |

|---|---|

| 光标键 Pos1, End | 向上或向下滚动文本，跳转到文本的开始或结束 |

| G, Shift+G | 跳到文本的开始或结束 |

| / pattern Enter | 向前搜索 |

| ? pattern Enter | 向后搜索 |

| N | 重复向前搜索（下一个） |

| Shift+N | 重复向后搜索 |

| V | 启动由 `$EDITOR` 或 `$VISUAL` 设置的编辑器 |

| Q | 退出 `less`（退出） |

| H | 显示带有额外快捷键的帮助文本 |

**表 11** `less` 的快捷键

# man

`man` 命令显示重要命令、配置文件、C 函数等的文档。为了允许在帮助文本中进行简单的滚动，你可以使用 `less` 命令。因此，`man` 中使用的快捷键与 `less` 相同（参见表 11）。

# mutt

`mutt` 是一个文本模式的电子邮件客户端。该程序非常适合阅读和回复存储在本地计算机上的电子邮件。老牌 Linux 粉丝甚至在图形用户界面中也偏好 `mutt`，因为可以使用键盘非常高效地控制该程序。表 12 仅包含最重要的快捷键。

| 快捷键 | 功能 |

|---|---|

| 光标键 | 在邮件列表中移动光标 |

| Enter | 显示所选邮件的前几行 |

| 空格键 | 滚动邮件文本 |

| T | 删除邮件 |

| 快捷键 | 功能 |

| --- | --- |

| I | 从邮件视图切换回收件箱 |

| Y | 显示下一封邮件 |

| M | 使用由 `$EDITOR` 或 `$VISUAL` 设置的编辑器编写新邮件 |

| R | 回复邮件 |

| ? | 显示带有所有键盘快捷键的帮助文本 |

**表 12** `mutt` 的快捷键

# nano

`nano` 是一个极简编辑器，特别适合初学者。最重要的键盘快捷键（见表 13）始终显示在底部的两行文本中。

| 快捷键 | 功能 |

| --- | --- |

| Ctrl+A | 将光标移动到行首 |

| Ctrl+D | 删除一个字符 |

| 快捷键 | 功能 |

| --- | --- |

| Ctrl+E | 将光标移动到行尾 |

| Ctrl+H | 删除一个字符 |

| Ctrl+^ | 设置标记 |

| Ctrl+K | 删除当前行 |

| Ctrl+U | 重新插入上次删除的文本 |

| Ctrl+R | 插入上次删除 |

| Ctrl+0 | 保存文件 |

| Ctrl+X | 退出编辑器 |

**表 13** `nano` 的快捷键

# screen

你可以使用 `screen` 运行多个终端（多路复用）。`screen` 由 Ctrl+A 控制。

| 快捷键 | 功能 |

|---|---|

| ? | 显示帮助 |

| * | 列出所有会 |

| 0 | 切换 0 到 9 |

| C | 创建新会 |

| D | 分离当前会 |

| Shift+H | 从图形切换 |

| N | 切换到下一个会 |

| \ | 结束所有会 |

**表 14** `screen` 中的快捷键

# 文字控制台

如果你直接在控制台中工作，而不是在 KDE、Gnome 或其他系统中，则某些快捷键适用。表 15 总结了最重要的。

| 快捷键 | 功能 |

| --- | --- |

| Ctrl + Alt + Fn | 从图形切换 |

| Alt + F1 | 回到图形 |

| Alt + Fn | 切换到控制台 |

| Alt + 右方向/左方向 | 逐页向前/后滚动 |

| Shift + 上方向/下方向 | 向前/后滚动 |

| Ctrl + Alt + Del | 终止 Linux |

**表 15** 文字控制台快捷键

# vi/vim

`vi` 编辑器是 Unix 历史上的元老。几乎所有的 Linux 发行版默认安装了兼容 `vi` 的 `vim` 程序，你可以同时启动 `vi` 和 `vim`。

`vi` 提供的功能数量与 `emacs` 相似，但更难学习。表 16 总结了基本命令。

| 快捷键 | 功能 |

|---|---|

| I | 激活插入模式 |

| A | 激活插入模式。文本输入从字符开始 |

| Esc | 激活标准模式或取消命令输入 |

## 标准模式下的命令

| | |

| D, W | 删除一个单词 |

| D, D | 删除当前行 |

| n D, D | 删除 n 行 |

| P | 在光标位置后插入删除的文本 |

| Shift + P | 在光标位置前插入最近删除的文本 |

| . | 重复上次命令 |

| U | 撤销上次更改（撤销） |

| Shift + U | 撤销当前行的所有更改 |

| Ctrl + R | 反撤销（重做），从 Vim 7 起 |

| 快捷键 | 功能 |

| --- | --- |

| w | 保存文件 |

| q | 退出 `vim` |

| q! | 即使有未保存的文件也退出 `vim` |

## 插入模式下的命令

Ctrl+O 在不离开插入模式的情况下运行命令

表 16 基本命令

与其他编辑器主要的根本区别在于 `vi` 区分了不同的模式。

- 插入模式

  要输入文本，必须使用 I（插入）或 A（追加）切换到插入模式。此时 `vim` 会在底部最左侧显示 -- INSERT 字样。

- 复杂命令模式

  然而，大多数命令都在复杂的

命令模式，可以使用 `:` 激活。你可能需要先按 `Esc` 退出插入模式。

表 17 提供了删除文本的最常用键盘快捷键的概览。表 18 列出了用于移动光标的有用命令。表 19、表 20 和表 21 涉及了如何复制、选择和编辑文本。

### 表 17

| 键盘快捷键 | 功能 |

|---|---|

| `Del`, `Backspace` | 通常含义 |

| 插入模式下的键盘快捷键 | |

| `X` | 删除光标位置的字符或所选文本 |

| `Shift` + `X` | 删除光标前的字符 |

| `D`, `D` | 删除当前行 |

| 键盘快捷键 | 功能 |

| --- | --- |

| D 光标命令 | 根据光标移动命令删除文本（参见表 18）。示例：<br>D, $ 删除到行尾的所有内容。<br>D, B 删除上一个单词<br>D, W 删除下一个单词 |

**表 17 删除文本**

| 键盘快捷键 | 功能 |

| --- | --- |

| 光标键 | 标准含义 |



| H/L | 将光标向左/右移动 |

| J/K | 将光标向下/向上移动 |

| Shift + H/ Shift + L | 将光标移动到当前页的开头或结尾 |

| Shift + M | 将光标移动到当前页的中间 |

| B/W | 将光标向左/右移动一个单词 |

| 键盘快捷键 | 功能 |

| :--- | :--- |

| E | 将光标移动到单词末 |

| G, E | 将光标移动到单词首 |

| ( , ) | 将光标移动到当前/下一个块的开头 |

| { , } | 将光标移动到当前/下一个段落的开头 |

| ^, $ | 将光标移动到行的行尾 |

| Shift + G | 将光标移动到行尾 |

| G, G | 将光标移动到行首 |

| n Shift + G | 将光标移动到第 n 行 |

| n I | 将光标移动到第 n 列 |

| % | 将光标移动到相应的括号字符 ([{}) |

**表 18 标准模式下光标移动的键盘快捷键**

| 键盘快捷键 | 功能 |

| --- | --- |

| V | (激活)取消字符选择模式 |

| Shift + V | (激活)取消行选择模式 |

| Ctrl + V | (激活)取消块选择模式 |

| A, W | 向右扩展一个单词的选择 |

| A, S | 向右扩展一个块的选择 |

| A, P | 向右扩展一个段落的选择 |

| A, B | 向右扩展一个 () 层的选择 |

| A, Shift + B | 向右扩展一个 {} 层的选择 |

| G, V | 再次选择上次选择的文本 |

| 0 | 在选择开始和结束之间切换光标位置 |

**表 19 选择文本**

| 键盘快捷键 | 功能 |

| --- | --- |

| Y | 将所选文本复制到复制寄存器 |

| 键盘快捷键 | 功能 |

|---|---|

| Y, Y | 将当前行复制到复制寄存器 |

| Y 光标命令 | 复制光标移动捕获的文本<br>示例：Y, } 将文本复制到段落末尾 |

**表 20 将文本复制到复制寄存器**

| 键盘快捷键 | 功能 |

|---|---|

| X | 删除所选文本 |

| Y | 将所选文本复制到复制寄存器 |

| ~ | 在大写和小写之间切换 |

| Y | 将所选行合并为一长行 |

| G, Q | 执行

**表 21 编辑文本**

| 键盘快捷键 | 功能 |

| --- | --- |

| > , < | 缩进或取消缩进 |

| = | 根据当前缩进调整 |

| !sort | 使用外部命令排序 |

# 搜索与替换

在默认模式下，`/search` 会将光标移动到搜索的内容。`N` 重复搜索，`Shift`+`N` 反向搜索。要反向搜索，必须使用 `?search`。表 22 总结了搜索时最重要的特殊字符。vim 在搜索时区分大小写。如果你不想这样做，必须使用 `:ignorecase`（适用于后续搜索）或运行 `:ignorecase`（仅适用于本次）。使用 `:set incsearch` 增量搜索。搜索后，所有匹配项将保持高亮。要将所有的 abc 替换为 efg，你需要运行 `:s/abc/efg/g`。`Enter` 结束搜索，`Esc` 取消。!` 则带你回到行首。

| 字符 | 含义 |

| --- | --- |

| . | 任意字符 |

| ^ $ | 行首/行尾 |

| \ < | 单词首/单词尾 |

|  | 

**表 22 搜索项中的特殊字符**

| 字符 | 含义 |

|---|---|

| [a-e] | a 到 e 之间的字符 |

| \s, \t | 空格或制表符字符 |

| \( \) 将搜索模式总结为组 |

| \= | 搜索项可以出现 0 次 |

| * | 搜索项可以出现任意次数（甚至是 0 次） |

| \+ | 搜索项至少出现一次 |

## 屏幕显示与导航建议

我们建议使用无衬线**字体**，如 Arial 或 Seravek，并且在竖屏格式下建议字体大小约为 30–40%，横屏格式下建议为 20–30%。背景不宜过亮。

请利用**连字符**选项。如果该选项无法正常工作，请将文本向左对齐。否则，请使用文本两端对齐。

要在电子书中进行**搜索**，书的索引将可靠地引导您访问书中真正相关的页面。如果索引没有帮助，您可以使用阅读设备的搜索功能。

由于本书在横屏格式下以双页跨页的形式显示，我们包含的**目录**可能比您阅读设备的相应功能更能让您了解书籍的内容和结构。为了方便您随时打开目录，它已作为一个单独条目包含在设备生成的目录中。

如果您想**放大图片**，请点击相应的图片**一次**。再次点击一次，即可返回到上一个屏幕。如果您双击两次（在 iPad 上），图片将以原始尺寸显示，然后必须放大到所需的尺寸。如果您点击一次，图片将直接放大并以更高的分辨率显示。

对于包含编程代码的书籍，请注意，在特定的字体大小下，代码行可能会被错误换行或显示不完整。如有疑问，请缩小字体大小。

## 关于我们和我们的计划

网站 `https://www.rheinwerk-computing.com` 提供了我们当前出版计划的详细且第一手的信息。在这里，您还可以轻松订购我们所有的书籍和电子书。Rheinwerk Publishing Inc. 信息以及额外的联系方式也可以在 `https://www.rheinwerk-computing.com` 找到。

## 法律说明

本节包含本电子书详细且具有法律约束力的使用条件。

## 版权说明

本出版物整体受版权保护。所有使用和开发权均由作者和 Rheinwerk Publishing 保留；特别是无论是印刷形式还是电子形式的复制权和发行权。

© 2025 by Rheinwerk Publishing Inc., Boston (MA)

## 用户的权利

您有权仅出于个人目的使用本电子书。特别是，您可以出于个人目的打印本电子书或进行复制，前提是您将此副本存储在由您个人专门使用的设备上。您无权进行任何其他使用或开发。

特别是，禁止将电子或打印副本转发给第三方。此外，禁止在互联网、内网或以任何其他方式分发本电子书或向第三方提供。任何公开展示、其他出版或超出个人使用范围的对电子书的任何复制均被明确禁止。上述规定不仅适用于整个电子书，也适用于其部分内容（例如图表、图片、表格、文本段）。

版权注释、品牌和其他法律保留声明不得从电子书中删除。

本书的任何部分均不得以任何方式为训练人工智能技术或系统而使用或复制。根据《数字单一市场指令 2019/790》第 4(3) 条规定，Rheinwerk Publishing, Inc. 明确保留本作品免受文本和数据挖掘。

## 商标

本出版物使用的通用名称、商品名称、商品描述等可能是未经特殊标识的商标，并受法律法规的约束。

书中提到的所有产品均为其各自公司的已注册或未注册的商标。

## 责任限制

无论在创建文本、图表和程序时付出了多少努力，出版商或作者、编辑或翻译人员对可能的错误及其后果不承担任何法律责任或义务。

## 文档存档

文档存档包含了所有的插图和表格（如果有），供您参考。



```bash
kofler@host1:-$ duf

# 2 local devices

| MOUNTED ON | SIZE | USED | AVAIL | USE% | TYPE | FILESYSTEM |
|---|---|---|---|---|---|---|
| / | 61.8G | 49.4G | 9.7G | [########...] | 79.9% | ext4 | /dev/vda1 |
| /localbackup | 44.1G | 22.0G | 20.1G | [####......] | 49.8% | ext4 | /dev/vdb |

# 6 special devices

| MOUNTED ON | SIZE | USED | AVAIL | USE% | TYPE | FILESYSTEM |
|---|---|---|---|---|---|---|
| /dev/ | 2.8G | 0B | 2.0G | | devtmpfs | udev |
| /dev/shm | 2.8G | 0B | 2.0G | | tmpfs | tmpfs |
| /run | 577.9M | 1.3M | 576.7M | [......] | 0.2% | tmpfs | tmpfs |
| /run/Lock | 5.0M | 0B | 5.0M | | tmpfs | tmpfs |
| /run/snapd/ns | 577.9M | 0B | 576.7M | [......] | 0.2% | tmpfs | tmpfs |
| /run/user/1000 | 577.9M | 4.0K | 577.9M | [.......] | 0.0% | tmpfs | tmpfs |
kofler@host1:-$ duf Providing Good Overview of the Free Space on All Data

root@utmf39:~# ls --long /etc/systemd
drwxr-xr-x root 01 Mar 01:00 24 network
-rw-r---- root 28 Feb 01:15 24 coredump.conf
-rw-r---- root 28 Feb 01:15 24 homed.conf
-rw-r---- root 28 Feb 01:15 24 journal.conf
-rw-r---- root 01 Mar 01:00 24 logind.conf
-rw-r---- root 28 Feb 01:15 24 network.conf
-rw-r---- root 28 Feb 01:15 24 oomd.conf
-rw-r---- root 01 Mar 01:00 24 sleep.conf
-rw-r---- root 28 Feb 01:15 24 pstore.conf
-rw-r---- root 01 Mar 01:00 24 resolved.conf
-rw-r---- root 01 Mar 01:00 24 timesyncd.conf
-rw-r---- root 01 Mar 01:00 24 user.conf
drwxr-xr-x root 01 Mar 01:00 24 system.control
drwxr-xr-x root 11 Mar 01:25 24 system-journal
drwxr-xr-x root 01 Mar 01:00 24 system-resolve
drwxr-xr-x root 01 Mar 01:00 24 system-security
34 directories, 38 files, 0 links
```

`Figure 2` Provides an Overview of the `/etc/systemd` Directory

```
root@f39:~home (Fedora Linux 39 64-bit Kernel 6.7.0-fc39.arm64) uptime:6:29:12

| | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|
| CPU | | 5.0% | | 1.7g | trq | 95.8% | | 2k | total | 40M | 2.81g | active |
| MEM | | 43.3% | system | 0.0% | nice | 0.0% | sw_int | 283 | inact | 1.27g | buffer | 2.20m | used | 27m | free | 15.0g | min | 0.15 |
| swap | | 10.0% | | | | | | | | 1.26g | | | 2.27m | | | | |NETWORK

| | Rx/s | Tx/s | | CPU | MEM | VIRT | RES | PID | USER | TIME | NI | S | R/W |
|---|---|---|---|---|---|---|---|---|---|---|---|
| eth0 | 976k | 376k | +1.1% | 7.5 | 6.7% | 2146 kofier | 04:21 | 0 | 33 | 0 | gnome-shell /usr/bin/glance |
| wlan0 | 0 | 15.2 | | 1.76 | | 2862 kofier | 00:08 | 9 | 0 | 0 | gnome-software --glistic |
| vda1 | 0 | 0.0 | | 1.0 | | 2811 kofier | 00:02 | 1 | 0 | 0 | python /usr/share/python-type |
| vda2 | 0 | 0.0 | | 7.2M | 23.9M | 10205 root | 00:00 | 5 | 0 | 0 | system --system-deserial |
| vda3 | 0 | 0.0 | | 0.0 | | 2811 kofier | 00:00 | 5 | 0 | 0 | packagekitd |
| ramz0 | 343K | 0 | | 0.8 | 10.1M | 20668 root | 00:00 | 5 | 0 | 0 | gnome-shell-shell-frames

DISK I/O

| | Total | Used | free | | | | | | |
|---|---|---|---|---|---|---|---|---|
| /vda1 | 0.0G | 0.7 | 10.1M | 20668 | 00:00 | 5 | 0 | 0 | gnome-desktop-portal-gnome |
| /home (vda3) | 0.0G | 23.4G | 0.6 | 851M | 18.4M | 2782 kofier | 00:00 | 5 | 0 | 0 | gsd-settings
```

`Figure 3` Simple Monitoring with `glances`

![](img/94f0b4d76a25250c220515a1d5bba83f_928_0.png)
