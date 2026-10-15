
# 第四部分：红帽 Linux 网络和服务器设置

正在进行的 soa 查询：0
查询日志：已关闭 (OFF)
服务器已启动并正在运行

如果您无法通过名称或 IP 地址访问您的 DNS 服务器提供服务的计算机，那么您应该确保每个客户端的地址记录是正确的。您也可以尝试使用完整主机名或 IP 地址 `ping` 每一个客户端和服务器计算机。

# 获取更多关于 BIND 的信息

关于在本章中未描述的其他 BIND 选项，您可以通过以下列表中的几个地方进行参考：

- `/usr/share/doc/bind-*` — 包含 BIND 9 管理员参考手册的 HTML 和 XML 版本。
- 手页 (Man pages) — 输入 `man` 命令，后跟 `named` 或 `named.conf`。这些帮助页包含了与 `named` 守护进程和 `named.conf` 文件相关的选项和变量的描述。
- 互联网软件协会 (www.isc.org/products/BIND) — ISC 网站包含与 BIND 相关的信息和下载。通过该网站，您可以找到指向 BIND 邮件列表、与 BIND 相关的安全公告以及 BIND 历史的链接。

## 总结

将您的红帽 Linux 服务器连接到互联网并不是容易的决定。如果服务器对您的业务至关重要，且维护服务器的工作对您来说难以负担，您应该考虑将您的服务器交给托管商。

如果您决定将您的红帽 Linux 服务器暴露在网上以提供 Web、FTP、邮件或其他类型的服务，您应该仔细考虑安全影响并为此做好准备。通过使用我在书中其他部分描述的红帽 Linux 功能，您可以创建防火墙、监控日志文件并跟踪系统文件的更改，以保护您的计算机。

控制服务器公网暴露的一种方法是获取一个域名并配置您自己的域名系统（DNS）服务器。您可以设置您的 DNS 服务器，为从互联网请求该信息的客户端解析主机名到 IP 地址，同时也为本地私有局域网（LAN）上的用户解析。

# 附录 A
# CD-ROM 中包含的内容

随书附带的 CD-ROM 由三张红帽 Linux 8 安装光组成。安装红帽 Linux 8：

- 遵循第 2 章和 CD-ROM 中包含的说明。
- 参考附录 B 获取完整的红帽软件包列表。

如果由于某些原因您手头没有这些 CD-ROM，可以从红帽 Linux 镜像站下载这些任何一个包（参见 www.redhat.com/download/mirror.html）。RPMfind.net 网站是查找红帽 Linux 额外软件包的极佳资源。RPMfind 可以帮助您找到曾经包含在红帽 Linux PowerTools CD 中的额外、有用的软件包。红帽公司 Inc. 已不再维护 PowerTools。

> **注意：** 所有的 CD-ROM 文件都是只读的。包含源代码的 CD-ROM 是可用的。

## 附录 B：Red Hat Linux RPM 963

- am-utils: 用于自动挂载文件系统的工具。包含 amd 守护进程。
- anaconda: Red Hat Linux 安装程序。
- anaconda-help: anaconda 安装程序中使用的帮助信息。
- anaconda-images: anaconda 安装程序中使用的图形图像。
- anaconda-runtime: 用于构建 Red Hat 介质集。
- anacron: 针对非 24 小时运行机器的周期性命令调度器。
- anonfp: 一个快速的只读匿名 FTP 服务器。
- apel: 用于自定义 emacs 的可移植 emacs 库。
- apmd: 用于监控电池电源的高级电源管理软件。
- ark: 处理各种常见格式归文件的 KDE 工具。
- arpatch: 用于跟踪以太网/IP 地址配对的 archwatch 工具。
- arts: 配合 KDE 3 音频系统使用的模拟实时合成器软件。
- arts-dev: 使用 arts (Bourne) 开发程序所需的库和文档。
- ash: 一个轻量级 shell，类似于 Unix System V 的 sh shell。
- asp2php: 将活动服务器页面转换为 PHP 格式的工具。
- asp2php-gtk: asp2php 应用程序 gtk+ 前端接口。
- spelt: 一组用于多种语言拼写检查的术语。
- aspell-dev: 使用 aspell 开发应用程序所需的库和文档。
- at: at 和 batch 命令便于单次的、时间导向的任务控制。
- atk: 为应用程序添加无障碍支持的一系列接口。
- atk-dev: 用于 atk 的库、头文件和文档。
- at-spi: 允许屏幕阅读器、放大镜或脚本与 GUI 控件交互。
- at-spi-dev: 用于编译 at-spi 的库和头文件。
- attrtr: 用于操作扩展文件系统属性的工具。
- audiofile: 实现 SGI Audio File 库以处理音频文件的工具。
- audiofile-dev: 与音频开发相关的开发工具。
- amumix: 用于调整音频混器设备 (/dev/mixer) 的 amumix 程序。
- amumix-X11: 基于 gtk 的 amumix 程序版本。
- authconfig: 配置系统授权资源的工具。
- authconfig-gtk: 配置系统授权资源的图形化工具。
- autoconf: 创建用于制作移植、可配置源码包脚本的工具。
- autoconf213: 旧版本的 autoconf。

## 964 附录

- **autoconvert**: 用于转换中文 HZ/GB/BIG5 编码的自动转换工具。
- **autoconvert-xchat**: autoconvert-xchat 插件。
- **autofs**: 通过 autount 守护进程自动挂载和卸载文件系统。
- **automake**: automake make 文件生成器。
- **automake14**: 为未更新到兼容新版本 automake 项目包含。
- **automake15**: 为未更新到兼容新版本 automake 项目包含。
- **autorun**: 自动检测并挂载 CD-ROM 的软件。
- **awesfx**: 用于控制 AWE32 音频驱动的工具。
- **balsa**: balsa 邮件阅读器（GNOME 桌面的一部分）。
- **basesystem**: Red Hat Linux 系统的一部分。
- **bash**: GNU Bash (Bourne Again Shell) 2.05b 版本。
- **bash-doc**: GNU Bash shell 的文档。
- **bc**: bc 高精度计算器命令行工具和语言。
- **bdflush**: 用于将脏缓冲区刷回磁盘的 bdflush 内核。
- **beecrypt**: 通用加密库。
- **beecrypt-dev**: 使用 beecrypt 开发应用程序所需的文件。
- **bg5sps**: 将 BIG5 编码转换为可打印 PostScript 的工具。
- **bind**: DNS 协议的伯内核互联网命名域实现。
- **bind-dev**: 用于 BIND 9.x.x DNS 软件开发的头文件。
- **bind-utils**: dig, dnslookup, nsupdate 以及其他 DNS 工具。
- **binutils**: GNU 命令行工具，如 ar, ld, nm, size 等。
- **bison**: GNU bison 解析器生成器（yacc 的替代品）。
- **bitmap-fonts**: 来自 Xfree86 包的、设计用于终端的位图字体。
- **bitmap-fonts-cjk**: anaconda 从 Xfree86 中选的位图字体。
- **blas**: 用于基础线性代数的基本线性代数程序 (BLAS) 库。
- **blas-man**:  blas 包的 man页。
- **bonobo**: GNOME 桌面环境使用的基于 CORBA 的组件系统。
- **bonobo-activation**: 为客户端应用程序启动或加载 Bonobo 组件。
- **bonobo-activation-dev**: 编译使用 bonobo-activation 程序的头文件。
- bonobo-conf: 基于 bonobo 的配置选项系统。
- **bonobo-conf-devel**: 使用 bonobo-conf 开发程序所需的库和文件。

## 附录 B：Red Hat Linux RPM 965

- **bonobo-devel**: 使用 bonobo 文档模型的应用程序库和头文件。
- **bootparamd**: 用于无引导工作站的 bootparamd 启动参数服务器。
- **booty**: 用于 anaconda 的 Python 库。
- **boot-utils**: Linux 系统的引导程序管理工具。
- **boot-utils-devel**: boot-utils 的开发文件。
- **bootx**: x86 系统的引导程序。
- **bdev**: Linux 块设备管理工具。
- **bdev-devel**: bdev 的开发文件。
- **bgm**: Linux 图形库。
- **bgm-devel**: bgm 的开发文件。
- **bind2**: 伯内核互联网命名域服务器。
- **bind2-devel**: bind2 的开发文件。
- **bitset**: 位操作库。
- **bitset-devel**: bitset 的开发文件。
- **bitline**: Linux 位流库。
- **bitline-devel**: bitline 的开发文件。
- **bcurses**: 终端 ncurses 库。
- **bcurses-devel**: bcurses 的开发文件。
- **bcrypt**: Linux 加密库。
- **bcrypt-devel**: bcrypt 的开发文件。
- **bind2**: GNU 汇编语言。
- **bind2-devel**: bind2 汇编器开发文件。
- **blast**: GNU C++ 库。
- **blast-devel**: blast 的开发文件。
- **block**: Linux 块设备工具。
- **block-devel**: block 的开发文件。
- **bluez**: Linux 蓝牙栈。
- **bluez-devel**: bluez 的开发文件。
- **blueray**: Blu-ray 播放器库。
- **blueray-devel**: blueray 的开发文件。
- **blueman**: Linux 蓝牙桌面管理器。
- **blueman-devel**: blueman 的开发文件。
- **blueevil**: Linux 蓝牙音频管理器。
- **blueevil-devel**: blueevil 的开发文件。
- **maild**: Linux 邮件传输代理。
- **maild-devel**: maild 的开发文件。
- **bmail**: Linux 邮件客户端。
- **bmail-devel**: bmail 的开发文件。
- **bprint**: Linux 打印库。
- **bprint-devel**: bprint 的开发文件。
- **brcrypt**: Linux 加密库。
- **brcrypt-devel**: brcrypt 的开发文件。
- **brdev**: Linux 设备库。
- **brdev-devel**: brdev 的开发文件。
- **brutils**: Linux 工具库。
- **brutils-devel**: brutils 的开发文件。
- **brcurses**: Linux curses 库。
- **brcurses-devel**: brcurses 的开发文件。
- **brgraphics**: Linux 图形库。
- **brgraphics-devel**: brgraphics 的开发文件。
- **braudio**: Linux 音频库。
- **braudio-devel**: braudio 的开发文件。
- **brvideo**: Linux 视频库。
- **brvideo-devel**: brvideo 的开发文件。
- **brnetwork**: Linux 网络库。
- **brnetwork-devel**: brnetwork 的开发文件。
- **brnet**: Linux 存储库。
- **brnet-devel**: brnet 的开发文件。
- **brfs**: Linux 文件系统库。
- **brfs-devel**: brfs 的开发文件。
- **brdb**: Linux 数据库库。
- **brdb-devel**: brdb 的开发文件。
- **brusb**: Linux 总线库。
- **brusb-devel**: brusb 的开发文件。
- **brmouse**: Linux 鼠标库。
- **brmouse-devel**: brmouse 的开发文件。
- **brkeyboard**: Linux 键盘库。
- **brkeyboard-devel**: brkeyboard 的开发文件。
- **brinput**: Linux 输入库。
- **brinput-devel**: brinput 的开发文件。
- **broutput**: Linux 输出库。
- **broutput-devel**: broutput 的开发文件。
- **brkey**: Linux 密钥库。
- **brkey-devel**: brkey 的开发文件。

## 988 附录

- **chromium**: 一款街机游戏。
- **chromium-devel**: chromium 的开发文件。
- **cipe**: VPN 守护进程和内核模块。
- **cipe-devel**: cipe 的开发文件。
- **cleanfeed**: 过滤 USENET 垃圾邮件。
- **compat-db**: 伯内核数据库的旧版本。
- **compat-gcc**: Red Hat 7.3 的兼容编译器。
- **compat-gcc-c++**: 为旧版 Linux 系统的 C++ 编译器。
- **compat-gcc-g77**: 为旧版 Linux 系统的 Fortran 77 编译器。
- **compat-gcc-java**: 为旧版 Linux 系统的 Java 编译器。
- **compat-gcc-objc**: 为旧版 Linux 系统的 Objective-C 编译器。
- **compat-libjpeg**: gcc 编译器的 Java 运行时库。
- **compat-libgcc-dev**: gcc java 编译器的静态库和 C 头文件。
- **compat-libstdc++**: GCC C++ 库快实现。
- **compat-libstdc+++**: Red Hat 7.3 的头文件和库。
- **compat-pwdb**: 管理 Linux PAM 用户认证接口的库。
- **compat-slang**: S-Lang 扩展语言的嵌入接口和编程库。
- **comps-extras**: 用于 comps 文件的工具和图像。
- **comsat**: 异步邮件通知客户端和服务器。
- **control-center**: GNOME 桌面配置工具。
- **control-center-devel**: 开发 GNOME 控制中心组件的组件。
- **cplo**: 在多种归档格式与文件、磁盘、磁带之间拷贝。
- **cpp**: C（预处理器）宏处理工具，用于 C 代码的预处理。
- **cproto**: 从 C 源码创建函数原型和变量声明。
- **cracklib**: 需要测试密码“强度”的应用程序库。
- **cracklib-dicts**: CrackLib 测试密码安全性时使用的字典。
- **crontabs**: cron 守护进程用于调度任务的根 crontabs 文件。
- **ctags**: 从 C 源码对象生成标签文件的 c 工具。
- **cups**: 通用打印系统，UNIX 系统的移植打印服务。
- **cups-devel**: CUPS 开发环境。
- **cups-drivers**: CUPS 打印机驱动程序。

## 附 B：Red Hat Linux RPM 967

- cups-drivers-hpijs: 使用优化 hpijs 驱动程序的 HP 打印机 CUPS 驱动程序。
- cups-drivers-pnm2ppa: 用于 PPA（HP兼容 GDI）打印机的 CUPS 驱动程序。
- cups-libs: 允许应用程序原生使用 CUPS 的库。
- curl: 一个功能强大的实用，用于通过各种互联网协议从远程服务器检索文件。
- curl-dev: 构建使用 curl 功能的应用程序所需的文件。
- cvs: 维护文件更改历史。
- cWnn: 一种中文字系统。
- cWnn-common: cWnn 和 tWnn 中文输入系统所需的文件。
- cWnn-dev: 用于 cWnn 或 tWnn 中文字符输入的编程工具。
- cyrus-sasl: 简单认证与安全层 (SASL) 的 Cyrus 版本。
- cyrus-sasl-dev: 开发使用 cyrus-sasl 的应用程序所需的文件。
- cyrus-sasl-gsapi: 支持 GSAPI 认证的 cyrus-sasl 插件。
- cyrus-sasl-md5: 用于 CRAM-MD5 和 DIGEST-MD5 认证的 Cyrus 插件。
- cyrus-sasl-plain: 用于 PLAIN 和 LOGIN 认证方案的 Cyrus-sasl 插件。
- db4: Berkeley Database 第 4 版的 C 库。
- db4-dev: db4 开发的头文件和库。
- db4-java: 用于 Java 开发的 db4 库。
- db4-utils: 管理第4 版 Berkeley 数据库的命令行工具。
- ddskk-cdb: 用于 SKK 日语输入方法的字典调试器。
- ddd: 数据显示调试器，一个与命令行调试器交互的 GUI 界面。
- ddskk: 用于 emacs 的简单假名到汉字转换工具。
- ddskk-emacs: 用于 XEmacs 的简单假名到汉字转换工具。
- dejagun: 一个测试程序的 Expect/Tcl 框架，以标准格式交付输出。
- desktop-backgrounds: 一组用作屏幕背景的图像。
- desktop-backgrounds-extra: 在 desktop-basic 基础上构建背景包。
- desktop-file-utils: 创建并验证用于 KDE 和 GNOME 菜单的 .desktop 文件。
- dev: 常用使用的 Linux 设备文件。
- dev86: 一个 x86 汇编器和链接器。
- dhclient: DHCP 客户端应用程序。

## 968 附录

- **dhcp**: 动态主机配置协议 (DHCP) 服务器和中继。
- **dhcp-devel**: 与 ISC DHCP 服务器接口的库。
- dia: 类似于 Visio 的绘图和绘制程序。
- dialog: 用于在文本模式界面中显示对话框的 dialog 工具。
- dict: dict 客户端，用于从 DICT 服务器访问字典定义。
- difflib: libc 的小型实现。
- diffstat: 从 diff 命令的输出生成统计信息。
- diffutils: 包含用于比较文件的 diff, cmp, diff3 和 sdiff 工具。
- diskcheck: 监控硬盘剩余可用空间的实用程序。
- Distutils: 分发和安装 Python 模块的模块。
- dmalloc: 内存管理例程的透明替换品。
- docbook: 包含 DocBook SGML DTD 和样式表的包集。
- dosunix: 将文本文件从 DOS 转换为 UNIX 格式。
- dosstools: 用于创建和操作 DOS 文件系统的工具。
- doxygen: 从 C 或 C++ 源代码创建文档。
- doxygen-wizard: 用于创建和编辑 oxygen 配置文件的 GUI 前端。
- dtach: 一个模拟 screen 分离功能的简单程序。
- dump: 用于备份和恢复 ext2/3 文件系统的实用程序。
- dvdrecord: 命令行 CD/DVD 录制程序。
- dvgrab: 从连接火线的设备捕捉数字视频。
- e2fsprogs: 用于查找和修复 ext2 文件系统不一致的程序。
- e2fsprogs-devel: 为开发 ext2 文件系统程序提供的库和头文件。
- ed: 行行的文本编辑器（原始的 UNIX 文本编辑器）。
- el2: Eaz 扩展库，适用于 GNOME 的组件和函数集合。
- el2-devel: 开发 eel 的库和包含文件。
- efax: 使用任何类型 1、2 或 2.0 的调制解调器发送和接收传真。
- eject: 弹出 CD、软磁盘、Jazz磁盘或其他媒体。
- ElectricFence: 检测内存分配违规。
- elinks: 支持帧的文本模式 浏览器。
- emacs: 运行 emacs 所需的库。
- emacs-elisp: 与 emacs 文本编辑器配合使用的 emacs-elisp 源程序。
- emacs-leim: 用于国际字符脚本的 Emacs Lisp 代码。

## 附录 B：Red Hat Linux RPM 969

- emacspeak: 允许视障用户使用计算机的语音接口。
- encript: 将 ASCII 文本格式化为 PostScript 输出的打印过滤器。
- eog: Gnome 图片查看器。
- epic: 增强型 cii 聊天客户端。
- eruby: Ruby 解释器。
- eruby-devel: 用于 Ruby 的库和头文件。
- eruby-libs: Ruby 的运行时库。
- esound: 用于查找和修复 ext2 文件系统不一致的程序。
- esound-devel: 为开发 ext2 文件系统程序提供的库和头文件。

# 附录 B：Red Hat Linux RPM 971

- GConf2-devel: 开发 GConf2 所需库文件。
- gconf-editor: GConf2 配置源的编辑器和管理工具。
- gd: 用于创建 JPEG 和 PNG 图像文件的图形库。
- gdb: 命令行驱动的调试器。
- gdbm: Gdb 数据库索引库。
- gdbm-devel: 使用 GNU 图形库开发应用程序的组件。
- gdk-pixbuf: GDK Pixbuf 图像加载库。
- gdk-pixbuf-devel: 与 GDK Pixbuf相关的开发工具。
- gdk-pixbuf-gnome: 用于显示图像的 GNOME 画板。
- gdm: GNOME 显示管理器，维护基于 X 的图形登录。
- gd-progs: 与 gd 图形库相关的实用程序。
- edit: 一个紧凑的、基于 GNOME 的文本编辑器。
- genromfs: 为初始内存磁盘构建 romfs 文件的工具。
- gettext: 用于创建多语言消息的工具和实用程序。
- gftp: 多线程图形 ftp 程序。包含对目录下载和恢复中断的文件传输的支持。
- ggv: Ghostscript 前端，提供对 Ghostscript 的平移和持久化用户设置。
- ghostscript: 显示和打印 PostScript 文件。
- ghostscript-devel: 开发启用 ghostscript 的应用程序的头文件。
- ghostscript-fonts: Ghostscript 程序使用的字体集。
- ghostscript-gtk: 支持 GTK 的后处理文件查看器。
- giftrans: 将 GIF8 文件转换为 GIF89 格式。
- gimp: GNU 图像处理程序。
- gimp-data-extras: 用于 GIMP 的图案、渐变和其他图形元素。
- gimp-devel: 开发 GIMP 插件和扩展所需的库和头文件。
- gimp-perl: 用于在 GIMP 和 GIMP Perl 扩展之间通信的库。
- gimp-print: 在高需求任务期间提供增强打印功能的驱动程序。
- gimp-print-cups: 能、爱普及兼容打印机的原生驱动程序。
- gimp-print-devel: GIMP 打印接口的头文件、库和文档。
- gimp-print-utils: 来自 gimp-print 的实用程序。

# 972 附录

- gkermit: 使用 Kermit 协议辅助文件传输。
- gkrelm: 监控 CPU 使用、磁盘活动和网络流量的图表软件。
- glaze: 为 GTK+ 工具包开发快速用户界面的软件。
- glaze2: 用于 GTK+ 2.0 的 glaze 版本。
- glib: 用于提高移植性的常用函数 glib 1.2 版本。
- glib2: 用于提高移植性的常用函数 glib 2 库版本。
- glib2-devel: 用于 glib2 开发的静态库和头文件。
- glibc: 许多程序使用的标准库。
- glibc-common: 二进制文件、区域支持和时区数据库。
- glibc-debug-*: 用于深层调试的各种库。
- glibc-devel: 开发大多数 C 语言程序的标准头文件和对象文件。
- glibc-kernheaders: glibc 提供的 Linux 内核头文件。
- glibc-profile: 创建使用 gprof 进行分析的程序所需的库。
- glibc-utils: 程序调试期间有用的各种工具。
- gl-devel: 支持 GIMP 库的静态库和头文件。
- Glide3:  3DfxVoodoo 显卡的编程接口。
- Glide3-devel: 允许程序使用 3Dfx Interactive Voodoo 中 3D 加器的接口。
- glut: 使用 OpenGL API 的 3D 图形库。
- glut-devel: 开发使用 glut 的应用程序所需的库和头文件。
- gmp: 处理算术和浮点数函数的 MP 库。
- gmp-devel: 创建使用 GNU MP 精度库的程序的组件。
- gnome-applets: 用于 GNOME 桌面的小程序（微型图形应用程序）。
- gnome-audio: 可以在 GNOME 环境中使用的声音。
- gnome-audio-extra: 可用于 GNOME 桌面的声音文件。
- gnome-desktop: GNOME 组件之间共享的代码。
- gnome-desktop-devel: 编译 gnome-desktop 组件的库和头文件。
- gnome-games: GNOME 游戏，如接龙牌、gnothelle 和俄罗斯方块。
- gnome-kerberos: 用于管理 Kerberos 5 票据的 krb5 工具。
- gnome-libs: GNOME桌面环境和应用程序所需的库。

# 附录 B：Red Hat Linux RPM 973

- gnome-libs-devel: 创建在 GNOME 桌面运行的应用程序所需的库。
- gnome-lokkit: 配置简单网络防火墙的 GNOME 工具。
- gnome-media: GNOME CD 播放器和其他多媒体工具。
- gnomemeeting:  MicrosoftMeeting 的 H323 远程会议工具。
- gnome-mime-data: gnome-vfs 的文件类型识别数据文件。
- gnome-panel: 提供桌面管理工具，如菜单和工作区切换器。
- gnome-pilot: 整合 GNOME 和像 Palm Pilot 等 PalmOS 设备所需的文件。
- gnome-pilot-devel: 允许应用程序使用 gnome-pilot 的需库。
- gnome-print-devel: 允许应用程序使用 gnome-pilot 的需库。
- gnome-gtk: 支持 GTK 的后处理文件查看器。
- gimp-print-cups: 能、爱普及兼容打印机的原生驱动程序。
- gimp-print-devel: GIMP 打印接口的头文件、库和文档。
- gimp-print-utils: 来自 gimp-print 的实用程序。
- gnome-session: GNOME 会话管理器。
- gnome-settings: GNOME 设置守护进程组件。
- gnome-terminal: GNOME 终端模拟器。
- gnome-utils: 用于 GNOME 桌面的各种实用程序。
- gnome-viewer: GNOME 媒体查看器。
- gnome-window: GNOME 窗口管理器。
- gnome-writer: GNOME 文本编辑器。

## 附录 B：Red Hat Linux RPM 975

- guppi: 一个基于 GNOME 的数据分析和可视化系统。
- guppi-devel: 开发使用 Guppi 的应用程序所需的头文件和库。
- gv: 用于在 X 窗口中查看 PostScript 和 PDF 文档的轻量级前端工具。
- g-wrap: 为 C 库创建 Scheme 接口的工具。
- g-wrap-devel: grep 开发所需的的文件和库。
- gzip: 数据压缩工具。
- h2ps: 将韩语（Hangul）转换为文本 PostScript。
- hanterm-xf: 用于 X 窗口的韩文终端。
- hdparam: 用于设置和查看硬盘参数的工具。
- hesld: 用于查看 heiosid 数据库的工具和库。
- hesiod-devel: 使用 heiosid 数据库的应用程序所需的库和头文件。
- hexedit: 十进制文件查看器和编辑器。
- hotplug: 用于连接 USB 设备时加载模块的热插拔实用程序。
- hotplug-gtk: 用于 Compaq PCI 热插拔控制器的 GTK 接口。
- hpljs: 优化的 HP 打印机驱动程序集。
- htdig: hdig 索引搜索系统。
- htdig-web: hdig 使用的 CGI 脚本和 HTML 代码。
- htmlview: 应用程序用于显示基于 HTML 的帮助页。
- httpd: Apache Web 服务器配置、文档和守护进程。
- httpd-devel: 用于扩展模块的 Apache 服务器头文件和文档工具。
- httpd-manual: Apache 手册（HTML 格式）。
- hwbrowser: 用于当前系统硬件配置的浏览器。
- hwcrypto: Linux 下与硬件加密加速器接口的库。
- hwdata: 系统硬件的识别和配置数据。
- ImageMagick: 功能丰富的图形显示和编辑工具。
- ImageMagick-c++: 使用 ImageMagick 功能应用程序的 C++ 绑定。
- ImageMagick-c++-devel: 与 ImageMagick 图形库配合 C++ 库。
- ImageMagick-devel: 实现 ImageMagick API 所需的库。
- ImageMagick-perl: ImageMagick 的 Perl 绑定。
- imap: 用于客户端邮件传输的 IMAP 和 POP 协议守护进程。
- imap-devel: 用于与 IMAP 邮件服务器接口的 IMAP 开发工具。

## 976 附录

- imlib: X 窗口系统的图像加载和渲染库。
- imlib-cfg: 用于控制 imlib 如何渲染图像的 imlib_conf 程序。
- imlib-devel: 使用 Imlib 图像和渲染库开发程序的组件。
- im-sdk: 互联网/内网输入法框架。
- indent: 用于美化 C 语言代码的 indent 工具。
- indexhtml: 安装 Red Hat Linux 后看到的 Red Hat 欢迎网页。
- inews: 将 Usenet 新闻文章同步到本地新闻服务器。
- info: 用于显示 textinfo（读作 "tech-info"）文件的文本浏览器。
- initscripts: 启动时和运行级别的初始化脚本。
- inn: 用于在 Linux 中创建和维护新闻服务器的 InterNews 服务器。
- inn-devel: 开发使用 InterNews 系统应用程序的组件。
- ipchains: 在 IP 网络上实现防火墙和 IP 伪装的组件。
- iproute: 用于路由 IP 流量的 ip 命令及相关工具。
- iptables: 高级数据包过滤工具。
- iptables-ipv6: 用于 IPv6 网络的高级数据包过滤工具。
- iptraf: 基于控制台的网络监控工具。
- iputils: 各网络监控工具，包括 ping 和 rdisc。
- ipxutils: 用于配置和操作 Novell IPX 网络的工具集。
- ipvsadm: 用于管理带有 Linux 虚拟机服务器补丁的服务器虚拟 IP 服务工具。
- irb: 交互式 Ruby，一种基于终端的 Ruby 表达式评估器。
- irda-utils: 用于与红外设备通信的 IrDA 工具。
- isci: 用于 IP 网络分布式磁盘访问的 ISCI 守护进程和实用程序。
- isdn4k-utils: 配置 ISDN 子系统的工具。
- isdn4k-utils-devel: 开发 capi 应用所需的库和头文件。
- isdn4k-utils-vboxgetty: 用于 ISDN 语音箱的 vboxgetty 和 vboxtty。
- isolcom: 加 Multitech 智能串口内部数据文件的工具。
- itcl: Tcl 语言的对象对象扩展。
- jadetex: 用于处理 DSSSL 文档的 jadetex 和 pdfadetex 命令。
- jcode.pl: 用于日语字符编码转换的 perl 库。

## 附录 B：Red Hat Linux RPM 977

- jdkgcj: Sun Java SDK 的免费实现。
- jed: 基于 slang 屏幕库的 jed 文本编辑器。
- jfsutils: 管理 JFS 文件系统的工具。
- jisksp14: 14 点辅助汉字字体。
- jisksp16-1990: 16 点 jis 辅助汉字字体。
- joe: 使用 Borland WordStar 键位绑定的无行文本编辑器。
- joystick: 用于连接和配置操纵杆的工具。
- jpllot: 用于 Palm Pilot 的桌面整理应用程序。
- kaboodle: 一个 KDE 媒体播放器。
- kakasi: 将汉字转换为平假名、片假名或罗马字的日语字符转换器。
- kakasi-devel: 开发使用 Kakasi 应用程序的头文件和库文件。
- kakasi-dict:  Kakasi 字典。
- camera: 为 KDE 增加数码相机支持的程序。
- kappa20: 20 点的日语字体。
- karm: 跟踪用户在不同任务上花费时间的工具；适用于计费。
- kbd: kbd: 用于配置系统控制台的工具。
- kbdconfig: 用于配置键盘映射的 kbdconf.ig 命令。
- kcale: KDE 口袋计算器。
- kce: 汉字编码转换器。
- charselect: KDE 字符选择器。
- ktextcolor: KDE 调色板编辑器和颜色选择。
- kdb: GNU 调试器 (gdb) 的 KDE 图形前端。
- kde2-compat: 用于 KDE 桌面面的各种兼容库。
- kdeaddons: Kate 文本编辑器的插件。
- kdeaddons-kicker: KDE 面板的插件和额外组件。
- kdeaddons-newsticker: 扩展 KDE 面板的脚本。
- kdeaddons-conquer: 扩展 KDE 面板的插件。
- kdeaddons-noatum: 扩展 KDE 面板的插件。
- kdeaddons-noat: 扩展 KDE 面板的插件。
- kdeaddons-color: 扩展 KDE 面板的插件。
- kdeadmin: 扩展 KDE 面板的插件。
- kdeartwork: 扩展 KDE 面板的插件。
- kdeartwork-kclock: 扩展 KDE 面板的插件。
- kdeartwork-color: 扩展 KDE 面板的插件。

## 978 附录

- kdeartwork-screensavers: KDE 额外的屏幕保护程序。
- kdebase: 基础 KDE 窗口管理器、kfm 文件管理器和终端。
- kdebase-devel: 开发应用程序的头文件。
- kdebindings: 包含 KDE/C++ 的包。
- kdegames: KDE 游戏，如 kaasteroids、blackbox 和 ksmilektris。
- kdegames-devel: 支持创建游戏的库。
- kde-l18n: 提供各种人类语言支持的包集。
- kdilibs: KDE 环境所需的库。
- kdilibs-devel: 开发 KDE 应用程序的工具和文档。
- kdemultimedia-arts: RT 声音系统的额外功能。
- kdemultimedia-devel: 开发 kdemultimedia 应用程序的工具。
- kdemultimedia-file: 让 KFile 操控音频格式的库。
- kdemultimedia-libs: KDE 多媒体应用使用的库。
- knetwork-devel: 开发 KDE 网络应用程序的库。
- knetwork-libs: 执行网络功能和 MIME 编码/解码的库。
- kdepassword: 用于更改密码和其他用户数据的 KDE 前端程序。
- kdeplim: 用于 KDE 桌面的个人信息管理 (PIM) 工具集。
- kdeplim-cellphone: KDE 与手机同步数据的支持。
- kdeplim-devel: 开发使用 kdeim 应用程序所需的头文件和库。
- kdeplim-pilot: KDE 与 Palm Pilot 或兼容 PDA 同步数据的支持。
- kdeskd-gimp: 用于 GIMP 创建低色 KDE 图标的标准 KDE 调色板。
- kdeskd-kapptemplate: 创建 KDE 应用程序框架的工具。
- kdeskd-kbabel: 辅助翻译的工具。
- kdeskd-kbugbuster: KDE 调试工具。
- kdeskd-kmtrace: 用于 KDE 的 malloc (内存分配) 调试器。
- kdeskd-compare: 用于 KDE 的文件比较工具。
- kdeskd-kspy: Qt/KDE 应用程序状态增强工具。
- kdessh: 用于 ssh 安全外壳应用程序的 KDE 前端。
- kdetoys:实用程序，如 kmoon（月相）和 kclock（时区查看）。
- kdeutils-laptop: 用于管理笔记本电脑的各种程序。

## 附录 B：Red Hat Linux RPM 979

- **kdevelop**: 用于创建具有一致 KDE 界面应用程序的开发工具。
- **kdf**: 监控可用磁盘空间的应用程序。
- **kdlet**: 用于 KDE 的 DICT（网络字典）客户端。
- **kdoc**: 用于交叉引用 C++ 头文件中文件中格式化注释的 kdoc2 程序。
- **kdvi**: TeX 输出文件查看器。
- **kedit**: 一种易于使用的文本编辑器器。
- **keduca**: 测试与考试。
- **kernel-2.4.*: 为各种类型 CPU 配置的 Linux 内核。
- **kernel-bigmem**: 用于配备 4 GB 或更多内存机器的 Linux 内核精简版。
- **kernel-BOOT**: 用于放置在启动磁盘上的 Linux 内核精简版。
- **kernel-doc**: Linux 内核源码部分的文档文件。
- **kernel-pcmcia-cs**: 支持 PCMCIA 设备（通常用于笔记本电脑）的软件。
- **kernel-smp-*: 适用于各种 CPU 的对称多处理 Linux 内核版本。
- **kernel-source**: 用于构建 Red Hat Linux 内核的源码文件。
- **kernel-uml**: 编译为独立程序以作沙箱使用的内核。
- **kernel-utils**: 若干控制 Linux 内核或计算机硬件的实用。
- **kfax**: KDE 传真查看器。
- **kfile-pdf**: 允许 KFile 应用读取 PDF 文件信息的工具。
- **kfile-png**: 允许 KFile 应用读取 PNG 文件信息的工具。
- **kformat**: 以 ext2 或 DOS 格式格式化软盘的工具。
- **kfract**: 用于 KDE 分形生成器。
- **kgeo**: 用于 KDE 的交互式几何包。
- **kghostview**: PostScript 和 PDF 文件查看器。
- **khexedit**: 允许编辑二进制文件的十六进制编辑器。
- **kiconedit**: 用于 KDE 的图标编辑器。
- **kinput2-canna-wan6**: 需要 Canna 或 Wnn6 日文文本的 X 程序的服务器。
- **kit**: 用于 KDE 的 AOL 即时通讯 (AIM) 客户端。
- **kjots**: 放置在桌面上的虚拟笔记本记。
- **klettres**: 法语字母辅导。
- **kjettool**: 用于 HP LaserJet 及兼容打印机的配置工具。
- **kipq**: 用于管理打印队列的 KDE 工具。
- **klprfax**: 用于 KDE 的传真传输支持，允许应用程序打印到传真接口。

# 980 附录

- **kmail**: 用于 KDE 的电子邮件客户端。
- **kmessedwords**: 一种字母排序游戏。
- **kmid**: MIDI 音频文件播放器。
- **kmidi**: 在播放前将声音转换为数字音频的 MIDI 音频文件播放器。
- **kmix**: 用于 KDE 的音频混合器应用程序，支持音量控制。
- **knewsticker**: 显示所选网站新闻的程序。
- **knm_new**: 一种叶名朝字体。
- **knode**: 用于 KDE 的新闻组 (NNTP) 阅读器。
- **knotes**: 允许将笔记放置在桌面上的应用程序。
- **koffice**: 一套办公生产力应用程序集。
- **koffice-devel**: 开发 KOffice 插件所需的文件。
- **kon2**: 用于台的汉字模拟器。
- **kon2-fonts**: 用于 kon 的字体。
- **koncd**: 用于刻制和刻录 CD-ROM 的图形前端。
- **kooka**: 控制图像扫描仪的 KDE 应用程序。
- **korn**: 一个多文件夹 KDE 邮件监控器，可显示新消息数量。
- **kpaint**: 用于 KDE 的简单绘画程序。
- **kpf**: 用于 KDE 的公共文件服务器。
- **pppp**: 用于 KDE 的 PPP 网络应用程序。
- **kppload**: 用于视觉化监控 PPP 连接负载的 kppload 工具。
- **krb5***: 提供 Kerberos 认证方法支持的包。
- **krbafs**: krbafs 库，支持带有 Kerberos 5 凭据的 AFS令牌。
- **kgexpeditor**: 正则表达式编辑器。
- **kgexpeditor-devel**: kgexpeditor 的开发文件。
- **kruler**: 屏幕尺和颜色测量工具。
- **kscd**: 用于 KDE 的音频 CD 播放器。
- **ksire**: 用于 KDE 的 IRC 客户端。
- **ksnapshot**: 用于捕获桌面或单个窗口图像的 KDE 应用程序。
- **kstars**: 桌面行星馆。
- **ksymoops**: 将内核错误信息转换为有用符号和偏移量的工具。
- **ktalkd**: 用于 KDE 支持 Talk 协议的程序。
- **kterm**: kterm 汉字终端模拟器。

## 附录 C

## 运行网络服务

由于 Red Hat Linux 能够提供许多不同的服务（提供 Web 页面、打印机、文件和其他资源），很容易忘记这些服务。假设你安装了 Red Hat Linux 的所有软件软件包。你如何知道哪些服务器将自动启动，以及哪些需要特殊配置才能工作？你该从哪里开始查找配置文件、启动脚本和守护进程？你如何知道你的防火墙配置是否阻止了对服务的访问？

本附录提供了 Red Hat Linux 附带的网络服务的快速参考。其目的是对其他章节中详细描述的这些服务提供概述。你可以将此附录作为如何让服务运行的提醒，或者作为帮助你调试需要修复的服务的指南。

> 注意：你的计算机向能够通过网络访问它的用户提供的任何服务都构成了潜在的安全威胁。有关安全信息，请参考第 14 章以及书中详细描述每个功能配置的章节。

## 运行网络服务的检查清单

随着计算机黑客和病毒的猛袭，安全问题日益增加，操作系统（如 Red Hat Linux）正转向更安全而非更易用的方向。仅仅安装服务器软件不足以让服务运行。

如果服务无法工作，请检查下面列出的项目以找出问题：

- 1. **软件软件包已安装吗？** 每个服务由一个或多个软件软件包表示。如果你进行的是工作站安装或自定义安装，大多数网络服务器可能根本没有安装在你的计算机上。检查表 C-1 以查看运行服务需要哪些软件包。（可能还有其他软件包依赖关系，当你尝试安装软件包时会收到提示。）然后使用 `rpm` 命令从其中一个安装光盘安装软件。
- 2. **防火墙允许访问该服务吗？** Red Hat Linux 安装程序允许你配置防火墙。如果你选择默认（中等安全级别）防火墙，大多数服务将无法在你的本地计算机之外可用。请参考第 14 章，了解如何更改你的防火墙配置以打开提供不同服务的端口。
- 3. **启动脚本已设置为自动启动该服务吗？** 大多数网络服务从启动脚本启动，这些脚本导致守护进程持续监听网络请求。参见“网络服务守护进程”部分如何查找启动脚本并让它们自动启动。
- 4. **是否为该服务创建了配置文件？** 即使守护进程正在监听网络服务，在接受请求之前，可能有一个或多个与该服务相关的配置文件需要设置。表 C-1 列出了每种类型服务器的配置文件。
- 5. **配置文件允许访问该服务吗？** 在服务的配置文件中，可能有几级权限，用户必须通过这些权限才能获得服务的权限。例如，配置文件可能允许从特定计算机访问服务，但拒绝特定用户的访问。
- 6. **对服务共享是否还有其他限制？** 某些标准的 Linux 安全措施可能会阻止对本可以开放共享的服务的访问。例如，你可以使用 NFS 或 FTP 服务器共享 Linux 目录，但本地文件权限可能会阻止对该目录或共享目录内文件的访问。

本附录的其余部分提供了 Red Hat Linux 附带的网络服务相关的守护进程、启动脚本、配置文件和软件包的概述。

## 网络服务守护进程

作为 Red Hat Linux 如何启动网络服务（以及其他服务）的快速回顾，包含文件的两个主要域定义了服务如何启动：

- `/etc/xinetd.d`: 包含 xinetd 守护进程使用的配置文件
- `/etc/init.d`: 包含链接到 `/etc/rc?.d` 目录的启动脚本，以便它们可以在不同的运行级别启动

处理网络服务的这些方法每种都在下面的章节中描述。

> 注意：某些 Red Hat Linux 配置工具还把配置信息存储在 `/etc/sysconfig`目录中。例如，`/etc/sysconfig` 中有 ipchains 和 sendmail 的配置文件。如果你在 `/etc/init.d` 目录的脚本中搜索 `sysconfig` 单词，你将看到有多少服务在那个目录中查找配置信息。

## xinetd 超服务器

xinetd 守护进程被称为超级服务器。它根据 `/etc/xinetd.d` 目录中单独文件中的信息监听对服务的入站请求。当 xinetd 守护进程接收到对服务的请求（针对特定端口号）时，xinetd 通常会启动一个守护进程来处理该请求。它不需要为每个网络服务运行独立的守护进程，只需要运行 xinetd 守护进程 —— 加上每个当前正在使用的服务额外运行一个守护进程。

要查看特定服务是由 xinetd 处理的开启还是关闭，请进入 `/etc/xinetd.d` 目录并使用文本编辑器打开代表该服务的文件。文件顶部的默认行指示该服务默认是开启还是关闭。`disable` 行实际上设置了该服务当前是否被禁用。以下是 `/etc/xinetd.d/ipop3` 文件的示例：

```
```
