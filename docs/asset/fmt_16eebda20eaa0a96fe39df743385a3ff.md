
- `sed-2.0-6`
- `quote-1.5-31`
- `vixie-cron-3.0-9`
- `textutils-1.19-2`
- `gawk-3.0.0-5`
- `file-3.20-3`
- `vim-4.2-5`
- `bdbflush-1.5-5`
- `at-2.9-2`
- `fwhois-1.00-5`
- `procinfo-0.9-1`
- `time-1.7-1`
- `kbdconfig-1.3-1`
- `timeconfig-1.4-1`
- `perl-5.003-4`
- `setup-1.5-1`
- `filesystem-1.2-1`
- `adduser-1.2-1`
- `dev-2.3-1`
- `redhat-release-4.0-1`
- `ld.so-1.7.14-4`
- `gdbm-1.7.3-8`
- `modules-2.0.0-4`
- `db-1.85-10`
- `slang-0.99-31`
- `mailcap-1.0-3`
- `readline-2.0-10`
- `lib-2.7.1-4`
- `tmpwatch-1.1-1`
- `crackslib-1.3-1`
- `crontabs-1.3-1`
- `zip-2.1-1`

### 3.2 如何使用 rpm 安装包

使用 `rpm` 时，通过 `--root` 选项指定挂载目录作为安装根。我发现许多包安装失败，是因为安装或后安装脚本由于根目录不同而无法执行，使用 `--nscripts`：

```
rpm --root /omega -i --nscripts package.I386.rpm
```

### 3.3 完成包安装

包安装完成后，还有两个小问题是预/后安装脚本旨在修复的但它们没成功。使用 LILO（从未让它在软盘上运行）进入单用户模式是通过编辑 `/omega/etc/initab` 实现的。修改以下行：

From-- > id:3:initdeaf

# Slack 2.2 安装

设置 id:1:initdefault: 

然后，重启系统。

#### 3.3.1 /etc/ld.so.cache

如果尝试启动，你会收到两个错误信息，第一个将是缺少 `/etc/ld.so.cache` 文件。一旦以单用户模式启动，请运行 `ldconfig` 来创建缓存文件：

```
ldconfig
```

#### 3.3.2 pamconfig

对于那些尝试在多用户模式下启动的人来说，另一个烦恼是，无论你尝试什么登录，你都可以以任何用户登录。要修复这个问题，请在用户模式下运行以下命令：

```
rpm --qf '%{POSTIN}' $(rpm -q --requires pamconfig) | sh -x
```

#### 3.3.3 恢复设置

现在这两件事都处理好了，再次编辑文件 `/etc/initab`，，这样系统将进入多用户模式。

# 4 Slack 2.2 安装

## 4.0.4 要求

- ZIP 磁盘和驱动器（显而见）
- 支持 ZIP 的内核
- ZIP Howto（推荐）
- 1.44" HD 格式软盘
- 1 到 2 小时的时间

## 4.1 安装

好了，现在是有趣的部分：确定哪些文件需要放在系统磁盘上，哪些软件包是你想要（并且可以放入）你的 ZIP 驱动器的。

我决定最简单的开始方法是将 Slack 直接安装到 ZIP 驱动器。我决定这种方法主要是因为 Slack 比 Red Hat 发行版小，更容易删掉我不需要的内容。反正我最后使用的是 Slack 发行版，这显然是一个选择。

将 Slack 安装到 ZIP 驱动器很容易，以 root 身份运行设置程序，将 `/omega` 设置为安装分区，将安装分区设置为 Slack 源所在的位置（cdrom, hardrd, ve 等），选择安装并按照提示操作。

## 4.2 安装什么

最困难的部分是决定添加什么，不添加什么。显然，你需要 'A' 系列（大约 8 兆），其余的取决于你。

我成功地将 Slack 版本精简到了可观的 70 兆安装量，包含了 gcc/g++、X11R6（不是全部）、sendmail、在线文档（去除了所有开发 man 手页，但包含了 howto）以及各种好东西，同时为免费用户留了大约 10 兆。视人而异（YMMV）。

# 5 修改 /etc/fstab（两种发行版均适用）

重启之前需要做的最后一件事是检查那里的 fstab 以确保是根分区。编辑 `/omega/etc/fstab` 文件，使其至少看起来如下：

# 2008 CVII. "ZIP-INSTALL MINI-HOWTO" BY JOHN WIGGINS <JWIGGINS@COMP.UARK.EDU>

| 设备 | 挂载点 | 类型 | 选项 | dump | pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/sda` | `/` | ext2 | defaults | 1 | 1 |
| `/dev/sda2` | none | swap | sw | | |
| none | `/proc` | proc | defaults | 1 | 1 |

保存文件，使用新制作的启动软重启并享受吧！

（特别感谢 Mike 提醒我这个非常重要且关键的步骤。- John）

# 索引

- 81
- to begin 命令选项, 77
- `.bash.profile`, 101
- `.bashrc`, 243
- `.bashrc`, 101
- `.bashlogin`, 340
- `.plan`, 261
- `.profile`, 341
- `.profile`, 101
- `.project`, 261
- `.tcshrc`, 101
- 在路径中的, 72
- 根目录, 72
- `/bin`, 105
- `/bin`, 298, 302, 304, 324
- `/bin/bash`, 81
- `/bin/csh`, 381
- `/bin/sh`, 320
- `/bin/tcsh`, 81
- `/bin/tcsh`, 303
- `/boot`, 303
- `/dev`, 296, 303, 304, 324
- `/dev/MAKDEV`, 304
- `/dev/MAKDEV`, 304
- `/dev/console`, 79
- `/dev/cua`, 79
- `/dev/fdi0`, 310
- `/dev/sdH440`, 310
- `/dev/fdi1`, 310
- `/dev/hd`, 79
- `/dev/hda`, 319
- `/dev/hda1`, 319
- `/dev/hda2`, 319
- `/dev/hdb`, 319
- `/dev/hdc`, 310
- `/dev/hdd`, 310
- `/dev/ip`, 79
- `/dev/null`, 79
- `/dev/pty`, 79
- `/dev/sda`, 308, 310
- `/dev/sdb`, 310
- `/dev/sdb7`, 315
- `/dev/tty`, 79
- `/dev/ttys`, 79
- `/etc`, 298, 303, 324, 347
- `/etc`, 79
- `/etc/image`, 105
- `/etc/csh.rc`, 304
- `/etc/csh.login`, 101
- `/etc/fetchboot`, 321
- `/etc/fdisk`, 310
- `/etc/fstab`, 319, 320, 325, 328
- `/etc/fstab`, 15
- `/etc/getty`, 118
- `/etc/group`, 303, 341
- `/etc/group`
- format 的, 109
- `/etc/host.conf`, 139
- `/etc/hosts`, 138
- `/etc/init`, 118
- `/etc/initab`, 303
- `/etc/initd`, 118
- `/etc/issue`, 303, 339
- `/etc/localtime`, 350
- `/etc/login.defs`, 354
- `/etc/magic`, 303
- `/etc/modf`, 303, 340
- `/etc/motd`, 189
- `/etc/mtab`, 303
- `/etc/networks`, 319
- `/etc/nlog`, 340
- `/etc/passwd`, 303, 340
- `/etc/passwd`, 155
- `/etc/passwd`, 198
- `/etc/procmp`, 304
- `/etc/profile`, 341
- `/etc/profile`, 101
- `/etc/rc`, 303
- `/etc/rc`, 118
- `/etc/rc`, 403
- `/etc/rc.local`, 118
- `/etc/rcd`, 303
- `/etc/resolv.conf`, 131
- `/etc/restore.conf`, 139
- `/etc/quotary`, 341
- `/etc/shadow`, 303, 340
- `/etc/shadow.group`, 341
- `/etc/shells`, 304
- `/etc/termcap`, 246
- `/etc/termcap`, 246
- `/etc/image`, 305
- extra-swap, 328
- `/home`, 298, 301, 303, 318, 319, 325
- `/home`, 79
- `/home/staff`, 302
- `/home/students`, 202
- `/lib`, 298, 303, 324
- `/lib`, 79
- `/lib/modmap`, 303
- `/mnt`, 303
- `/mnt/dosa`, 303
- `/mnt/ext3`, 303
- `/proc`, 303, 305, 306, 317
- IPX, 1085
- `/proc`, 799
- mounting 的, 116
- `/proc/1`, 305
- `/proc/cpuinfo`, 305
- `/proc/devices`, 305
- `/proc/dma`, 305
- `/proc/filesystems`, 305
- `/proc/interrupts`, 305
- `/proc/ioports`, 305
- `/proc/kore`, 305, 317, 347
- `/proc/kmsg`, 305
- `/proc/ksyms`, 305
- `/proc/loadavg`,
- `/proc/meminfo`, 306, 329
- `/proc/modules`, 306
- `/proc/net`, 306
- `/proc/net`, 405
- `/proc/self`, 306
- `/proc/stat`, 306
- `/proc/utime`, 306
- `/proc/version`, 306
- `/root`, 303
- `/sbin`, 302
- `/sbin/79`, 79
- `/sbin/getty`, 296
- `/sbin/init`, 296, 335
- `/sbin/update`, 330
- `/tmp`, 296, 303, 305, 319, 324
- `/tmp`, 79
- `/var`, 298, 301-304, 319, 324
- `/usr`, 80
- `/usr/X11RK`, 304
- `/usr/X11RK/lib/X11/XF86Config`, 125
- `/usr`, 304
- `/usr/X386`, 80
- `/usr/adm/messages`, 312
- `/usr/bin`, 304
- `/usr/doc`, 304
- `/usr/etc.`, 80
- `/usr/include`, 80
- `/usr/include`, 84
- `/usr/include`, 304
- `/usr/info`, 304
- `/usr/lib`, 304
- `/usr/lib/libc.a`, 302
- `/usr/lib/zoneinfo`, 350
- `/usr/local`, 304, 305
- `/usr/local.`, 80
- `/usr/focal/bin`, 304
- `/usr/man`, 304
- `/usr/man/cat*`, 305
- `/usr/man/man*`, 305
- `/usr/sbin`, 304
- `/usr/src`, 80
- `/var`, 302
- `/var`, 298, 301-303, 305, 319, 347
- `/var`, 80
- `/var/adm`, 80
- `/var/adm/messages`, 302
- `/var/lib`, 305
- `/var/libf`, 305
- `/var/lock`, 305
- `/var/log`, 305
- `/var/log/messages`, 305
- `/var/log/wtmp`, 305, 340
- `/var/spool`, 305
- `/var/spool`, 80
- `/var/spool/mail`, 298, 305
- `/var/tmp`, 296, 303, 305, 319, 324

# 2012

# 索引

- 缓冲区缓存 (buffer cache), 295, 333, 335, 336
- 索尼 (Sony), 773
- 错误 (bugs), 28
- CDROM
- 告示板 (bulletin board), 401
- 可录制的 (recordable), 797
- 总线鼠标 (busmouse)
- cdwniz, 1630
- 引导程序配置 (bootstrap configuration), 776
- 集中式计算 (centralized computing), 297
- 集中邮件处理器 (centralized mail handler), 494, 496, 497
- C, 236
- cdfsk, 314
- C 编译器 (C compiler), 295
- 挑战握手身份验证协议 (Challenge Handshake Authentication Protocol), 439, 445–447
- C 新闻 (C News), 144, 529, 533–554
- 农 (Channon), 171
- 活动文件 (active file), 533–535, 537–538
- CHAP, 见挑战握手身份验证协议
- 归档 (archiving), 759
- 字符集 (character set), 498
- 批量参数 (batch parameters), 538–539
- 批处理 (batching), 533, 536–539
- 退格键 (backspace), 1159–1162
- 压缩 (compressing), 533
- 删除 (delete), 1159–1162
- 创建初始配置 (create initial configuration), 534
- 充电 (chargin), 449
- 交换新闻 (exchanging news), 535
- 排除站点 (excluding sites), 535
- PPP, 441
- 过期 (expiring), 531–541
- SLIP, 433
- 主机名别名 (hostname aliases), 535
- 聊天 (chat), 441–442
- 聊天脚本 (chat scrip), 441
- haveinline, 539
- 域网 (LAN), 544
- UUCP, 478
- 馈源限制 (limit of feed), 536, 541
- 分组控制消息 (checkgroups control message), 542
- 日志文件 (log files), 542
- 审核组 (moderated groups), 541
- ARP 表 (ARP tables), 417
- 新闻管理员 (newsmaster), 535
- 以太网接口 (Ethernet interface), 417
- NNTP 支持 (NNTP support), 536, 549
- 主机 (host names), 425
- 接收新闻 (receiving news), 533–535
- IP 路由表 (IP routing table), 411
- relnews, 533
- 域名服务器 (name server), 425
- 发送新闻 (sending news), 536–539
- 网络配置 (network configuration), 409, 411
- 网络连接 (network connections), 406, 419
- 网络接口 (network interface), 409, 416
- 系统文件 (sys file), 534–537
- 待办 (todo), 537
- NIS, 460, 461
- 更新活动文件 (update active file), 542
- NNTP, 542
- 更新低水位 (update low water mark), 552
- PPP, 442
- Usenet (usenet), 535
- 可达性 (reachability), 409, 411
- UUCP, 533, 539
- sendmail, 523–535
- C  Shell (csh), 21
- 缓存 (cache), 335
- 缓存 (BIND 选项), 423
- 仅缓存网络消息 (caching-only network message), 542
- 取消控制消息 (cancel control message), 542
- 检查文件系统 (checking a filesystem), 335
- 标准主机名 (canonical hostname), 390, 424
- chfn, 109
- 区分大小写 (case-sensitive), 193
- cmdod, 222
- cat, 1522
- chroot, 87
- cat., 193, 194, 215, 224
- cat, 78
- 选择 NIS 域 (choosing a NIS domain), 458
