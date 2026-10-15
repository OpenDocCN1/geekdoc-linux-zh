
## Windows 客户端
要从 Windows 系统访问 Samba 资源，你需要确保你的 Windows 系统已启用 TCP/IP 网络。如果你的 Windows 客户端连接到 Microsoft 网络，这可能已经满足。如果你需要将 Windows 系统直接连接到你的 Linux Samba 服务器所在的 TCP/IP 网络，你应该检查该 Windows 系统是否已启用 TCP/IP 网络。这包括确保安装了 Microsoft 网络客户端和 TCP/IP 协议，并且你的网络接口卡（NIC 适配器）已配置为使用 TCP/IP。这些步骤在 Windows 2000 和 XP 上，以及 Windows 95、98 和 ME 上略有不同。

连接后，你的 Samba 共享和打印机将出现在 Windows 网络窗口中。在 Windows XP 上，你可以选择“我的网络位置”，它会列出你 Linux Samba 服务器上的 Samba 共享。如果你打开“查看工作组计算机”，它将列出你的 Samba 服务器（以及工作组中的任何其他 Samba 或 Windows 系统）。Samba 服务器将具有在 **server string** 选项中赋予的名称，加上 netbios 名称（主机名）。请遵循你特定 Windows 系统上的说明，以访问打印机和目录等远程共享资源。

# 索引

## 数字
- 0-6 级 Linux 软件 RAID 级别，解释，706–708
- 0-6 运行级别，描述，578–579
- 64 位机器，创建 Fedora 发行版，51

## 符号
- - （标准输入）参数，与命令一起使用，210
- ! 运算符，与数据包规则一起使用，426, 430
- \! shell 提示符代码，描述，237
- # （磅号）提示符，使用，194
- # 提示符，解释，58–59
- \# shell 提示符代码，描述，237
- $ （美元符号）
  - 在命令提示符处，解释，58–59
  - 用于引用 shell 脚本的参数，218–219
  - 用于引用变量值，215
  - 与 BASH（Bourne again）shell 一起使用，194
  - 与变量一起使用，197
- \$ shell 提示符代码，描述，237
- $? 特殊变量，示例，219
- $TTL 指令，与区域文件一起使用，841–842
- % （百分号）字段说明符，与 Apache 日志一起使用，502
- % （百分号）提示符，使用，194
- %% （百分号）符号，用于引用后台作业，212
- & （和号）
  - 执行后台作业，212
  - 与 lftp 客户端一起使用，341
  - 与 Mail 实用工具一起使用，314
- && （双和号），与命令一起使用，195
- * （星号）
  - 在 BASH（Bourne again）shell 中使用，203, 207
  - 用于文件名搜索，261
- . （点）命令
  - 与 .bash_profile 脚本一起使用，240
  - 与 .bashrc 文件一起使用，243
- . （点）文件
  - 显示，90
  - 使用，248
- .. 命令，使用，217
- .. 符号，用于引用父目录中的文件，257
- .bash_profile 文件，使用，658
- / （根目录）
  - 在 FHS（文件系统层次标准）中的作用，662–663
  - 使用 chroot 命令设置，49
  - 重要性，250
- / （斜杠），放置在目录名之后，228
- /etc/login.access 文件，内容，605
- /etc/nsswitch.conf 文件，与 DNS（域名服务）的关系，813–815
- ? （问号），在 BASH（Bourne again）shell 中使用，203–204, 207
- @ （at 符号），与主机名一起使用，197
- [] （括号），在 BASH（Bourne again）shell 中使用，204, 207
- \ （反斜杠）
  - 在 BASH（Bourne again）shell 中使用，207
  - 与命令一起使用，194
- \[ shell 提示符代码，描述，237
- \\ shell 提示符代码，描述，237
- {} （花括号），在 BASH（Bourne again）shell 中使用，205
- | （管道符），在 BASH（Bourne again）shell 中使用，207, 209–210
- ~ （波浪号），与用户名一起使用，197
- ~= （赋值）运算符，与变量一起使用，215
- = （等号），与别名一起使用，228
- > （大于号），与 Mail 实用工具一起使用，315
- > 和 >> （重定向运算符），在 BASH（Bourne again）shell 中使用，206–208
- >= 和 2> 符号，在 BASH（Bourne again）shell 中使用，210–211
- ; （分号）
  - 在 wvdial 中的作用，129
  - 用于分隔命令，195
- ' （单引号）
  - 与反引号 (`) 的区别，216–217
  - 与别名一起使用，228–229
- ` （反引号）与单引号 (') 的区别，216–217
- / 目录，功能，253

## A
- A 类型地址，使用，843–844
- AbiWord 文字处理器
  - 描述，288
  - 特性，283
  - 从命令行安装，81
  - 使用 Yum 安装，104
- About Me 首选项对话框，配置，66
- 绝对路径名与相对路径名，252
- accept 和 reject 工具，与 CUPS（通用 Unix 打印系统）一起使用，558
- ACCEPT 目标，与数据包一起使用，424, 426
- 访问控制列表（ACLs），与 Squid 代理服务器一起使用，516–517
- Apache Web 服务器中的访问控制，498
  - 类型，369–371
- 使用 allow 的访问向量规则，在 SELinux 中管理，386–387
- AccessFileName 指令，与 Apache Web 服务器一起使用，497
- Squid 代理服务器中的 acl 条目，模式，519
- ACLs（访问控制列表）
  - 在 DNS（域名系统）中使用，859–860
  - 与 Squid 代理服务器一起使用，516–517
- Acrobat Reader for Linux 文档查看器，描述，284
- 操作和用户，在系统日志中指定，591–592
- 添加新设备类型窗口，显示，126
- AddHandler 指令，与 Apache Web 服务器一起使用，506
- 地址记录，使用，843–844, 848
- 管理访问，控制，572–573
- 管理任务，执行，92
- Advanced Intrusion Detection Environment (AIDE) 工具，使用，367
- Advanced Linux Sound Architecture (ALSA)，网站，296
- Advanced Maryland Automatic Network Disk Archiver (Amanda). 参见 Amanda (Advanced Maryland Automatic Network Disk Archiver)
- Advanced Package Tool (APT)，特性，642–643
- Red Hat Enterprise Linux 的高级平台，特性，6–7
- AFE (Affix Frontend Environment)，网站，117
- Affix Frontend Environment (AFE)，网站，117
- agetty 程序，与终端连接一起使用，741

## AH
- AH (authentication header) 协议，与 IPsec 的关系，396
- AH 有效载荷，在 IPsec 连接中加密，399

## AIDE
- AIDE (Advanced Intrusion Detection Environment) 工具，使用，367

## AIM
- AIM (AOL Instant Messenger)，特性，347

## Alacarte
- Alacarte，在 GNOME 2.x 中使用，142

## alias
- alias 命令，用于创建命令名称，228–229
- Alias 指令，与 Apache Web 服务器一起使用，497

## aliases
- aliases 记录，使用，849
- aliases IP 别名，824
  - 移除，229
  - 在 Sendmail 中的支持，532–533
  - 使用命令名称作为别名，229
  - 与模块一起使用，748
  - 与资源记录一起使用，845

## allow
- allow 访问控制指令，与 Apache Web 服务器一起使用，498
- allow 关键字，在 SELinux 中使用，386–387
- AllowOverride 指令，与 Apache Web 服务器一起使用，497
- allow-transfer 语句，在 DNS 中使用，855–856

## --all-stages
- --all-stages 选项，与 Pungi 一起使用，54

## ALSA
- ALSA (Advanced Linux Sound Architecture)
  - 与声音设备一起使用，742
  - 网站，296

## ALT
- ALT 键。参见键盘快捷键

## Amanda
- Amanda (Advanced Maryland Automatic Network Disk Archiver)
  - 命令，781–782
  - 配置，782–783
  - 在网络上启用，783
  - 特性，781
  - 使用，783–784

## ampersand
- ampersand (&)
  - 执行后台作业，212
  - 与 lftp 客户端一起使用，341
  - 与 Mail 实用工具一起使用，314
- ampersands (&&)，在命令中使用，195

## anacon
- anacon，用于补充 con 服务，578

## Anonymous
- Anonymous 指令，与 Apache Web 服务器一起使用，501

## anonymous
- 匿名 FTP
  - 允许访问，476
  - 特性，475
  - 文件，477
- 匿名登录，使用 .netrc 功能，339–340

## AOL
- AOL Instant Messenger (AIM)，特性，347

## ap
- ap 参数，与 iwconfig 无线工具一起使用，132

## Apache
- Apache 配置工具，使用，508
- Apache Jakarta 项目，重要性，489–490
- Apache Web 服务器
  - 访问控制，498
  - 替代方案，498
  - 认证，500–501
  - 配置文件，491–492
  - 配置操作，493
  - 配置，120, 496
  - 配置无效目录，497
  - 使用的指令，493
  - 特性，489
  - 文件和目录，491
  - 全局配置，494
  - 安装，490
  - 与 IP 寻址，506
  - 日志文件，501–503
  - MPMs (多处理模块)，490
  - 服务脚本，491
  - 启动和停止，490–492
  - 手动停止，453
  - 支持插值字符串，505–506
  - 使用自动目录索引，500
  - 使用 CGI 文件，499–500
  - 使用 MIME 类型，499
  - 使用模块，494–495
  - 使用 URL 路径名，498–499
  - 虚拟主机，503–506
- apache2 控制工具，特性，492
- Apache-SSL Web 服务器，网站，488, 509
- apconfig，在 SELinux 中使用，391

## Appearance
- Appearance 窗格，在 KDE 面板 (Kicker) 中使用，181

## applets
- applets. 另请参阅 GNOME applets
  - 与 GNOME 面板的关系，162
  - 在 KDE 面板 (Kicker) 中的支持，180

## application
- 应用程序启动器
  - 添加到面板，163
  - 在 GNOME 桌面上创建，147–148
  - 使用 Nautilus 文件管理器创建，157
- 应用程序. 另请参阅程序
  - 从 KDE (K Desktop Environment) 访问，182
  - 在抽屉图标下分组，163
  - 在 KDE (K Desktop Environment) 启动时启动，183
  - 在 KDE (K Desktop Environment) 中启动，181
  - 在 Nautilus 文件管理器中启动，156

## APT
- APT (Advanced Package Tool)，特性，642-643

## arch
- arch 选项，用于指定 32 位和 64 位版本，50

## Archive
- Archive Manager，使用，110
- 存档的 tar 文件，使用 gzip 压缩，272

## archives
- archives
  - 压缩，270-271
  - 使用 File Roller 创建，266-267
  - 使用 tar (tape archive) 创建，268
  - 显示内容，268
  - 提取，268-269
  - 提取内容，272
  - 为源代码应用程序提取，110
  - 在 Konqueror 中提取，184
  - 更新，270
  - 使用，247
- 归档到磁带，271

## Area
- Area Code 变量，与 wvdial 一起使用，130

## arguments
- 参数
  - 包含命令名称，229
  - 用于引用 shell 脚本，218-219
  - 在 Linux 命令中使用，72-73

## ARIN
- ARIN (American Registry for Internet Numbers)，网站，802

## Arrangement
- Arrangement 窗格，在 KDE 面板 (Kicker) 中使用，181

## ARRAY
- ARRAY 条目，用于指定 RAID 设备名称，710, 714

## ascii
- ascii 命令，与 ffp 程序一起使用，338

## assignment
- 赋值 (=) 运算符，与变量一起使用，215

## asterisk
- asterisk (*)
  - 在 BASH (Bourne again) shell 中使用，203, 207
  - 与文件名搜索一起使用，261

## at
- at (@) 符号，与主机名一起使用，197
- AT&T Unix Korn shell，描述，227

## ATI
- ATI 驱动程序，软件包，101

## attacks
- 攻击，保护系统免受攻击，111-114

## attribute
- 属性类型定义，与 LDAP 目录数据库一起使用，625

## ATTRS
- ATTRS 键，与 udev 规则一起使用，731

## audio
- 音频 CD，在 Fedora 中播放，70

## audit
- audit2allow 工具，与 SELinux 一起使用，376-377, 380-381
- 审计系统，特性，592-593

## AUTH
- AUTH 命令，与 Sendmail 一起使用，542

## AuthConfig
- AuthConfig 指令，与 Apache Web 服务器一起使用，497

## authentication
- 认证
  - 在 Apache Web 服务器中，500-501
  - 配置，113-114
  - 软件包认证，109
  - 在 Samba 中，84-85
  - 使用 SSH (Secure Shell)，407
  - 使用，111
- 认证头 (AH) 协议，与 IPsec 的关系，396
- 认证头有效载荷，在 IPsec 连接中加密，399

## Authentication
- Authentication 工具，配置 Kerberos，418

## AuthName
- AuthName 指令，与 Apache Web 服务器一起使用，500

## auto
- 自动挂载，实施，676

## Auto Reconnect
- Auto Reconnect 变量，与 wvdial 一起使用，130

## autofs
- autofs 服务，按需挂载 NFS，895

## B
- 反引号 (`) 与单引号 (') 的区别，216-217
- 反斜杠 (\)
  - 在 BASH (Bourne again) shell 中使用，207
  - 与命令一起使用，194
- 备份
  - 使用 dump 和 restore 制作，784-789
  - 记录，786
  - 恢复，787-789
  - 从中还原，789
  - 自动计划，779

## Balsa
- Balsa 邮件客户端，与 GNOME 桌面一起使用，311-312

## BASH
- BASH (Bourne again) shell. *另请参阅* 命令行；BASH (Bourne again) shell 中的作业。
  - 命令行编辑，195-196
  - 条件控制结构，221-223
  - 配置，242-243
  - 配置历史，201
  - 默认提示符，237
  - 定义环境变量，231
  - 描述，227
  - 编辑功能，195
  - 编辑历史事件，200-201
  - 结束进程，214
  - 过滤器和正则表达式，224-226
  - 生成模式，205
  - 维护的历史列表，197-201
  - 初始化和配置文件，244
  - 作业管理操作，211
  - 循环控制结构，223-224
  - 匹配多个字符，203
  - 匹配字符范围，204
  - 匹配 shell 符号，204-205
  - 匹配单个字符，203-204
  - 在字符间导航，195
  - 运算符，207
  - 重定向和管道标准错误，210-211
  - 重定向标准输出，206, 208
  - 重新显示命令，198
  - 引用事件，200
  - 运行后台作业，212
  - 搜索文件，225
  - 用于文件名的特殊字符，201-202
  - 特殊功能，230
  - 标准输入，205-206, 208-209
  - 标准输出，205-206
  - 使用的符号，202
  - 测试运算符，220
  - 使用管道符 (|)，209-210
  - 变量，214-217
- bash 命令，描述，228
- BASH 命令行
  - 命令行补全，196-197
  - 文件名补全，196-197
- 命令行，识别，194
- BASH 配置文件脚本
  - 编辑，239-240
  - 手动重新执行，240
- BASH_ENV shell 变量，指定，236

# 索引

## B

- bash_logout 文件，使用方法，243–244
- bash_profile 文件，重要性，238
- BASH shell 变量，描述，232
- BASH_VERSION shell 变量，描述，232
- .bashrc，使用它配置 BASH（Bourne again）shell，242–243
- bashrc 文件，内容及位置，243
- Nautilus 属性框中的基本面板，说明，157
- Baud 变量，与 wvdial 配合使用，130
- 行为偏好，在 Nautilus 文件管理器中设置，159
- 贝尔实验室，Unix 在其中的流行度，14
- Berkeley Internet Name Domain (BIND)，特性，830–832
- Berkeley Software Distribution (BSD)，开发，14
- Beryl 合成窗口管理器，使用，148
- bg 命令，与作业配合使用，213
- biff 实用工具，邮件通知功能，316
- /bin 目录
  - 内容，584, 663–664
  - 功能，253
- 二进制掩码，与权限配合使用，616–617
- 二进制方法，与所有权权限配合使用，618–619
- BIND (Berkeley Internet Name Domain)，特性，830–832
- BIND 配置语句，描述，836
- BIND 服务器文件，位置，834
- BIND 服务器，启动和停止，832
- BIND 区域类型，描述，836
- bit or rate 参数，与 iwconfig 无线工具配合使用，132
- BitTorrent，使用它下载 ISO 和 DVD 发行版镜像，635–636
- Fedora 的 BitTorrent 文件，位置，28
- 蓝牙
  - 配置，117–118
  - 支持，117
- BlueZ
  - 替代方案，117
  - 特性，118
- 书签，在 Konqueror 中与目录配合使用，186
- boot，使用 title 指定，598
- 启动 CD-ROM，创建，758–759
- /boot 目录，内容，663
- 启动盘
  - 创建，49
  - 放置内核，767
- 启动加载器
  - 配置，767–768
  - 创建，758
  - 安装，43
  - 重新安装，50
- 启动分区，设置，41
- 启动源选项，选择，34–35
- 可启动 CD-ROM，创建，690–691
- 可启动 RAID，配置，714–715
- 从 RAID 设备启动，708
- 启动，故障排除，49
- 方括号（ [ ] ），在 BASH（Bourne again）shell 中使用，204, 207
- 广播地址，使用，804
- Nautilus 中的浏览器视图
  - 说明，153
  - 导航，154
- 浏览器视图，在 GNOME 桌面中使用，62
- 浏览器
  - Epiphany，328
  - Ephesus，325
  - Firefox，326–328
  - Galeon，328
  - Konqueror，328
  - 行模式浏览器，328–329
  - Mozilla 框架，326
  - Nautilus，328
- BSD (Berkeley Software Distribution)，开发，14
- bye 命令，描述，228
- bye 命令，与 ftp 程序配合使用，338
- 字节流，说明，249
- 字节，按字节检查文件，249
- bzip2 实用工具，与压缩文件配合使用，271
- bzip2 实用工具，用于压缩文件，273–274

## C

- 缓存内存，在 Squid 代理服务器中配置，520
- cache_peer，与 Squid 代理服务器配合使用，519
- 缓存，与 Squid 代理服务器配合使用，519–520
- 仅缓存服务器，与 DNS 配合使用，840
- Cairo 图像，符合 TANGO 样式指南，140
- OpenOffice 中的 Calc 程序，特性，280
- case 命令，使用 esc 关键字，221
- cat 命令
  - 效果，253
  - 列出文件，254
  - 使用，197
  - 与父目录配合使用，257
- CD 刻录机和解压机，可用性，302
- cd 命令
  - 在目录间移动，49
  - 导航目录，256–257
  - 与 ftp 客户端配合使用，341
  - 与源代码应用程序配合使用，110
- CDPATH 系统环境变量，描述，232
- CD-ROM 启动盘镜像，位置，35
- CD-ROM 驱动器，设备名称，670–671
- CD-ROM
  - 从 CD 启动 Linux，38
  - 使用 GNOME 卷管理器刻录，150
  - 使用 Gnome 刻录，71
  - 创建启动 CD，49
  - 创建文件系统，685
  - 显示内容，183
  - 弹出，183
  - 从 CD 安装 Fedora，30–31
  - 手动挂载，683–684
  - 获取用于 Fedora 安装，27–28
  - 在 Fedora 中播放，70
  - 手动录制，689–692
  - 卸载，183
- CD-RW 光盘，复制文件到，261
- cdedge 驱动程序，用于播放 Windows 游戏，86
- CentOS (Community Enterprise Operating System)，使用，7
- 证书，在 ipec 中使用，402
- CGI 程序与 PHP，507
- change 命令，使用它指定，605–606
- chaine 命令，使用它指定，423–424
- 链
  - 为防火墙创建，443–444
  - 在 NAT（网络地址转换）中，431–432
  - 与 Netfilter 防火墙的关系，422
- channel 参数，与 iwconfig 无线工具配合使用，132
- 字符
  - 另见在 BASH（Bourne again）shell 中进行特殊字符匹配，203
  - 使用正则表达式匹配，225
- chcon 命令，在 SELinux 中使用，392

## C（续）

- checkmountmude 命令，在 SELinux 中使用，391
- checkpolicy 命令，在 SELinux 中使用，391
- chgrp 命令，使用，614–615
- chkconfig 工具
  - 配置 xinetd 服务以供其使用，461
  - 启用和禁用 xinetd 服务，460, 470–471
  - 功能，461
  - 列出服务，458
  - 管理服务，582–583
  - 选项，459
  - 移除和添加服务，460
  - 启动和停止服务，459
  - 使用，452
  - 与 CUPS (Common Unix Printing System) 配合使用，551
  - 与 Network Manager 配合使用，122
- chown 命令
  - 更改权限，612–613
  - 使用，615–616
  - 使用 -x 选项，217
- chown 命令，使用，614–615
- chroot 命令
  - 与 FTP 服务器的关系，473
  - 设置根目录，49
- chron 命令，与 SELinux 故障排除器配合使用，381
- cron 服务，启动，574
- CIDR (Classless Interdomain Routing)，与子网掩码的关系，798–802
- B 类网络，段，799
- 基于类别的 IP 编址，说明，797–798
- Classless Interdomain Routing (CIDR)，与子网掩码的关系，798–802
- clear 命令，与 .bash_logout 文件配合使用，244
- clearlooks 主题，与 Fedora 桌面配合使用，140
- 时钟小工具，设置偏好，164
- 克隆工具，与 RAID 设备配合使用，715
- close 命令，与 ftp 程序配合使用，338
- CNAME 记录，使用，845
- Coda 分布式网络文件系统，使用，903
- 彩色背景，为 GNOME 中的面板创建，161–162
- COM 端口，与终端设备的关系，741
- 命令历史，在 BASH（Bourne again）shell 中保留，198–200
- 命令行
  - 另见 BASH（Bourne again）shell
  - 从命令行访问 PPP，129–131
  - 编辑操作，198
  - 说明，193
  - 安装 AbiWord，81
  - 安装 MPlayer，82–83
  - 标记开头，194
  - 关闭 Linux，59
  - 启动图形界面，66
- 命令行编辑，在 BASH（Bourne again）shell 中执行，195–196, 200
- 命令行安装，执行，644–651
- 命令行接口
  - 访问 Linux，58
  - 登录和注销，58
  - 使用，72–73
- 命令行邮件客户端
  - Mail 实用工具，314–315
  - Mutt，314
- 命令名称
  - 包含参数，229
  - 用作别名，229
- 命令选项，为软件配置，655
- 命令结果，分配给变量，216–217
- 命令
  - 在几行中键入，194
  - 在后台执行，212
  - 用于调用 shell，228
  - 位置，657
  - 重新显示，73
  - 在 BASH（Bourne again）shell 中重新显示，198
  - 使用 alias 命令重命名，228–229
  - 使用 while 循环重复，223
  - 在同一行运行，195
  - 在命令行内运行，195
  - 在它们之间发送数据，209–210
  - 用分号 (;) 分隔，195
  - 使用别名替换，228–229
  - 使用参数和选项，194
- Common Unix Printing System (CUPS)。参见 CUPS (Common Unix Printing System)
- Community Enterprise Operating System (CENTOS)，使用，7
- 比较，使用 test 命令进行，219–220
- 编译器配置，生成，111
- Compiz 合成窗口管理器，使用，148
- compiz 窗口管理器，特性，60
- compress 命令，使用，273
- 压缩归档
  - 提取，110
  - 从中安装软件，652–656
- 压缩归档，270–271
- 压缩文件，272–274
- 计算机文件夹，内容，69
- Concurrent Versions System (CVS)，说明，658–659
- 条件控制结构，使用，219, 221–223
- 配置目录和文件
  - 描述，586
  - /etc 目录，585
  - /etc/sysconfig，587
- 配置文件
  - 关于编辑的建议，90
  - 创建 Xen 虚拟机，775–776
  - 直接编辑，90
  - 在 home 目录中列出，245
  - 定位，258
  - 位置，585, 665
- 配置。另见系统配置
  - 解决冲突，49
  - 为 Fedora 安装选择，29
- configure 脚本，使用，633
- 连接跟踪模块，与 Iptables 配合使用，429–431
- 控制台，监视器作为，740
- 约束规则，在 SELinux 中管理，387
- 联系人应用程序，在 Office 中的可用性，281
- -context 选项，与 find 命令配合使用，260
- 上下文相关帮助，可用性，73
- KDE 控制中心。参见 KDE 控制中心
- 控制结构
  - 条件控制结构，221–223
  - 功能，221–222
  - 类型，219
- 复制
  - 目录，263
  - 文件，259–262
- cp 命令
  - 效果，261

