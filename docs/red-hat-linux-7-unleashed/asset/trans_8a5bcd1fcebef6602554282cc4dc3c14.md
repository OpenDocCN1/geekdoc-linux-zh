
## 附录 D
### Red Hat Linux RPM 包列表

本附录（包含表 D.1 和表 D.2）是针对本书 CD-ROM 中包含的 Red Hat Linux 软件的交叉参考。表 D.1 列出了单个包名称、其大小及简短描述。表 D.2 列出了 Red Hat 用于组织其发行版所使用的单个包组。这些表格可以帮助你选择包，以便为你的工作站、服务器或便携系统构建和安装自定义配置。

如果你存在资源限制，例如有限的硬盘空间或内存（RAM），表 D.2 可以帮助你构建一个最小化系统（通过仅安装“系统环境/基础”组中的那些包）。查看 Red Hat Linux 中究竟包含了多少编辑器、数据库管理器或游戏也非常方便！如果你不确定某个包是否已安装在你的系统上，你可以使用带有 `query` 或 `-q` 选项的 `rpm` 命令运行快速检查，方法如下：

```
# rpm -q abiword
abiword-0.7.10-3
```

这表明包 `abiword-0.7.10-3` 已安装在你的系统上。然而，如果你使用 `rpm` 命令并得到如下输出：

```
# rpm -q abiword
package abiword is not installed
```

你会从输出中看到该包未安装。

本附录是使用带有各种 `--queryformat` 选项的 `rpm` 命令创建的。你系统的 RPM 数据库（位于 `/var/lib/rpm` 目录下）包含已安装包的索引，你可以对已安装的包或仍在 Red Hat Linux CD-ROM 上的包执行查询。本附录中的表格是使用 `rpm` 命令像这样构建的：

```
# rpm -qa --queryformat '%{NAME}|%{SIZE}|%{SUMMARY}\n' | sort >table.txt
```

## 表 D.1 Red Hat Linux 包列表

| 包名称 | 大小（字节） | 描述 |
|---|---|---|
| abiword | 8840772 | 一种文字处理器。 |
| adjtimex | 48535 | 用于调整内核时间变量的实用工具。 |
| Amanda | 457009 | 支持网络的磁带备份解决方案。 |
| Amanda-client | 306525 | Amanda 磁带备份系统的客户端组件。 |
| Amanda-server | 562912 | Amanda 磁带备份系统的服务器端。 |
| am-utils | 1492186 | 自动挂载实用工具。 |
| anaconda | 6516899 | Red Hat Linux 安装程序。 |
| anaconda-runtime | 5997770 | 仅用于全新安装的 Red Hat Linux 安装程序部分。 |
| anacron | 56411 | 一种类似 cron 的程序，可以运行在停机期间错过的任务。 |
| anonftpd | 1772916 | 一个快速、只读的匿名 FTP 服务器。 |
| apache | 1179253 | 互联网上使用最广泛的 Web 服务器。 |
| apache-devel | 403592 | Apache Web 服务器的开发工具。 |
| apache-manual | 1492008 | Apache Web 服务器的文档。 |
| apmd | 92957 | 用于笔记本电脑的高级电源管理 (APM) BIOS 实用工具。 |
| arpwatch | 140762 | 用于跟踪网络上 IP 地址的网络监控工具。 |
| ash | 462099 | Bourne shell (sh) 的较小版本。 |
| asp2php | 105178 | 将 VBScript/Active Server Pages (ASP) 转换为 PHP 的工具。 |
| asp2php-gtk | 17972 | asp2php 转换器的 GUI 前端。 |
| aspell | 7972944 | 一种拼写检查器。 |
| aspell-ca | 7734941 | aspell 的加泰罗尼亚语文件。 |
| aspell-cs | 64434227 | aspell 的捷克语文件。 |
| aspell-da | 13396490 | aspell 的丹麦语文件。 |
| aspell-de | 10277107 | aspell 的德语文件。 |
| aspell-devel | 2711586 | 用于 aspell 开发的静态库和头文件。 |
| aspell-en-ca | 139452 | aspell 的加拿大词典。 |
| aspell-en-gb | 139448 | aspell 的英国词典。 |
| aspell-eo | 23179323 | aspell 的esperanto（世界语）文件。 |
| aspell-es | 15876306 | aspell 的西班牙语文件。 |
| aspell-fr | 7005038 | aspell 的法语文件。 |
| aspell-it | 1597499 | aspell 的意大利语文件。 |
| aspell-nl | 7110712 | aspell 的荷兰语文件。 |
| aspell-no | 11497743 | aspell 的挪威语文件。 |
| aspell-pl | 35622968 | aspell 的波兰语文件。 |
| aspell-sv | 4381827 | aspell 的瑞典语文件。 |
| at | 76032 | 作业池化工具。 |
| audiofile | 334641 | 用于访问各种音频文件格式的库。 |
| audiofile-devel | 646171 | 开发 audiofile 应用程序所需的库、包含文件和其他文件。 |
| aumix | 120433 | 基于 ncurses 的音频混合器。 |
| aumix-X11 | 45728 | aumix 声音混合器的 GTK+ GUI 界面。 |
| autoconfig | 151177 | 用于设置 NIS 和 shadow 密码的文本模式工具。 |
| auth_ldap | 93355 | 一个用于使用 LDAP 对 HTTP 客户端进行身份验证的 Apache 模块。 |
| autoconf | 597534 | 用于自动配置源代码的 GNU 工具。 |
| autofs | 661056 | 用于自动挂载和卸载文件系统的工具。 |
| automake | 905153 | 用于自动创建 Makefile 的 GNU 工具。 |
| autorun | 63762 | 一个 CD-ROM 挂载实用工具。 |
| awesfx | 314567 | AWE32 声音驱动程序的实用程序。 |
| basesystem | 0 | 定义 Red Hat Linux 系统的骨架包。 |
| bash | 1216755 | GNU Bourne Again shell (bash) 版本 1.14。 |
| bash-doc | 2520970 | GNU Bourne Again shell (bash) 版本 2.04 的文档。 |
| bc | 104008 | GNU 的 bc（一种数值处理语言）和 dc（一种计算器）。 |
| bdfhush | 9141 | 启动将脏缓冲区刷回磁盘守护进程。 |
| bind | 5285346 | 一个 DNS（域名系统）服务器。 |
| bind-devel | 1572427 | bind DNS 开发所需的包含文件和库。 |
| bind-utils | 1813123 | 用于查询二进制名称服务器的实用工具。 |
| binutils | 3256936 | GNU 二进制工具集。 |
| bison | 158146 | GNU 通用解析器生成器。 |
| blt | 5829766 | 一个 Tk 工具包扩展。 |
| bootparamd | 18062 | 为无盘客户端提供引导信息的服务器进程。 |
| bug-buddy | 724703 | 用于 GNOME GUI 桌面的 GUI 错误报告工具。 |
| byacc | 59513 | 一个公共领域的 yacc 解析器生成器。 |
| bzip2 | 151702 | 一个文件压缩实用工具。 |
| bzip2-devel | 84138 | 开发将使用 bzip2 的应用程序所需的文件。 |
| caching-nameserver | 8557 | 用于设置缓存名称服务器的配置文件。 |
| cdda2wav | 243450 | 用于从数字音频 CD 采样/复制 .wav 文件的实用工具。 |
| cdcl | 68551 | C/C++ 函数声明的编解码实用工具。 |
| cdp | 37509 | 一个用于播放音频 CD-ROM 的交互式文本模式程序。 |
| cdda-paranoia | 198634 | 一种紧凑光盘数字音频 (CDDA) 提取工具。 |
| cdda-paranoia-devel | 138483 | 用于 libcdda_paranoia (Paranoia III) 的开发工具。 |
| cdrecord | 672463 | 一个命令行 CD/DVD 录制程序。 |
| cdrecord-devel | 293953 | libschsy SCSI 用户级传输库。 |
| chkconfig | 128905 | 用于维护 /etc/rc.d 层级的系统工具。 |
| chkfontpath | 11069 | 用于编辑 X 字体服务器字体路径的实用工具。 |
| cipe | 100713 | 用于 VPN 的内核模块和守护进程。 |
| cleanfeed | 76856 | Usenet 新闻服务器的垃圾邮件过滤器。 |
| compat-egcs | 126752 | 用于 Red Hat Linux 5.2 向后兼容性的 C 编译器。 |
| compat-egcs-c++ | 4864671 | 用于 Red Hat Linux 5.2 向后兼容 C 编译器的 C++ 支持。 |
| compat-egcs-g77 | 4468108 | 用于 Red Hat Linux 5.2 兼容 C 编译器的 Fortran 77 支持。 |
| compat-egcs-objc | 2015471 | 用于 Red Hat Linux 5.2 兼容 C 编译器的 Objective C 支持。 |
| compat-glibc | 6909510 | 用于 Red Hat Linux 5.2 向后兼容性的 GNU libc。 |
| compat-libstdc++ | 3468701 | 用于 Red Hat 6.2 向后兼容 C++ 编译器的标准 C++ 库 |
| consat | 15576 | 邮件检查客户端和 consat 邮件检查服务器。 |
| console-tools | 2698298 | 用于配置控制台的工具。 |
| control-center | 2483111 | GNOME 控制中心。 |
| control-center-devel | 43364 | GNOME 控制中心开发环境。 |
| control-panel | 184859 | 用于 X 的 Red Hat 系统管理实用程序启动器。 |
| cpio | 68153 | GNU 归档程序。 |
| cpp | 270465 | GNU C 兼容编译器预处理器。 |
| cproto | 86966 | 从 C 代码生成函数原型和变量声明。 |
| cracklib | 91786 | 一个密码检查库。 |
| cracklib-dicts | 875815 | 标准的 CrackLib 词典。 |
| crontabs | 17351 | 用于安排程序执行的 Root crontab 文件。 |
| ctags | 170918 | 一种 C 编程语言索引和/或交叉引用工具。 |
| cvs | 2540907 | 一个版本控制系统。 |
