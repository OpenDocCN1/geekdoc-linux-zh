

building, 187  
loading, 188

MIT, 230

mkswap, 133

modules

PAM, 141

Mosberger-Tang, David, 206

Motif, 232, 233

mouse, 29

selection, 62, 71

nameserver

selecting, 110

network

interface

aliasing, 110

network configuration, 32, 110

adding device, 112

networking, 112

NFS, 74

exporting, 75

install, see install/NFS

mounting, 75

NIS+, 76

NIS/NYS, 76

not documented, see not supported

not supported, see doesn't exist

Novell, 230

NTFS, 190

O'Reilly & Associates, 72, 74, 76, 233

OS/2, 7, 35

OSF, 232

overview, x

PAM, 141

Paradis, Jim, 206

partitioning, 9

Alpha, 43

recommended, 10

passwords

shadow, 144

PLIP, 9

PPP, 9, see network configuration, adding SLIP/PPP

printer configuration, 105

local, 107

remote, 108

SMB, 108

test page, 109

quickstart, 2

rarp, 47

Rasmussen, Eric, 206

rawrite, 42, 187

Red Baron, 74, 83

Red Hat Software

contacting

email, 233

ftp, 233

mailing lists, 84

axp-list, 85

redhat-announce-list, 85

redhat-devel-list, 85

redhat-digest, 85

redhat-list, 76, 85

rpm-list, 85

sparc-list, 85

www, 84, 233

RISC, 171

root password, 34

rootdisk, see raidisk

RPM, 87

rpm, 87

determining file ownership with, 95

installing, 89

locating documentation with, 95

querying, 92, 95, 96

uninstalling, 90

upgrading, 91

verifying, 93

*Running Linux*, 233

Samborg, Ellen, 206

SCSI, 14, 21

sendmail, 72

aliases, 72

masquerading, 72

with UUCP, 72

services

PAM, 142

setenv, 99

shadow passwords, 144

shutdown, 133, 148

SILO, 50

SLIP, 9, *see* network configuration, adding SLIP/PPP

SPARC

booting

from floppy, 46

from network, 47

disk partitioning, 50

installation

network, 48

supported hardware, 45

unsupported hardware, 46

X Windows, 50

SRM, 42, 192

Stallman, Richard, 230

swapon, 81, 133

swapon, 80, 81, 133

Tylor, Grant, 76

tcpd, 73

tesh, 99

TFTP, 48

TGA, 42

time

setting, 115

Torvalds, Linus, ix, xi, 206, 233

University of California at Berkeley, 230

upgrading, 3

Usenet, 85

user accounts

adding, 100

deactivating, 103

editing, 100

removing, 102

user groups

creating, 103

editing, 104

Video Adapter, 59

Diamond, 153

ET4000, 153

S3, 59, 153

Welsh, M., 233

Windows NT, 188

WordPerfect, 232

World's Greatest Programmer, *see* Torvalds, Linus

WWW, 83

browser, *see* Arena, Netscape

server, *see* Apache

X Constructor, 231

Xconfigurator, 60

XFree86, 231, 234

configuration, 58

Xconfigurator, 58, 59

xf86config, 58

server chart, 59

yp, 76

ypbind, 77

yppasswd, 77

yps, 77

## 红帽 Linux 发行版 4.1

“官方”红帽 4.1 包含所有最新的 Linux 工具和实用程序，包括最新 2.0 内核改进的网络和硬件支持。

本手册是您红帽 Linux 系统安装和管理的“官方”手册。无论您是从互联网上的某个站点下载了红帽 Linux，还是从红帽软件公司购买了红帽 Linux，或作为其他产品或 CD-Rom 套装的一部分，本手册都将使您使用这项先进技术变得更加简单和愉快。

“红帽最大的优势在于，其众多软件包和工具几乎不需要配置……从整体上看，红帽是 Linux 最复杂且最具商业性的发行版。” *Inforworld 杂志*。

这款基于 POSIX 的高级易管理操作系统能让您的 PC 作为 UNIX 工作站有效地、可靠地执行高级计算任务。它非常适合从建立互联网 Web 或 FTP 服务器、互联网应用程序、研究工作、软件开发，甚至高级电脑游戏等各种应用。

### 易于安装和管理。

借助 RHPM 的打包系统和模块化内核，操作系统的安装从未如此简单。只需选择一个或多个配置选项，您的安装即可用于以下用途：

- C 和 C++ 开发  
- NFS 服务器  
- 匿名 FTP/ Gopher 服务器  
- 新闻服务器  
- 网络管理  
- 工作站  
- Dialog 工作站  
- 游戏机  
- X 窗口系统  
- Web 服务器  
- 打印机服务器  
- 网络化工作站  
- DOS-Windows  
- 连接  
- 多媒体机器  
- 文本文档格式化  
- 或使用手动配置选项，根据您的需求和喜好安装和配置您的 Linux 计算机。

许多强大的高级图形化工具为高级用户节省了数小时的时间，并让新手系统管理员能够根据自己的需求定制和配置系统。这些软件工具涵盖了 TCP/IP、PPP、SLIP、文件系统、用户和组、软件包等的配置。

RPM 打包系统是一个日益壮大的 Linux 标准，使系统的升级和维护变得简单且无忧无虑。现在的 4.1 版本引入了“软件包依赖项”，消除了猜测，并在安装、卸载和升级软件包时防止重大系统故障。

### 高级系统和网络安全功能。

RPM 系统的灵活性使红帽 Linux 赢得了最安全操作系统之一的声誉。几乎每当在互联网上发现安全问题时，红帽软件就会发布新的或更新的软件包以应对新的威胁，为您节省时间并降低被入侵的可能性。

红帽 Linux 4.1 发行版支持标准的“UNIX”密码认证，以及用于增强安全的“影子”密码。可插拔认证模块（PAM）系统允许编写额外的认证方法并将其动态添加到系统中，以满足您的特殊安全需求。

### 从早期版本升级。

由于红帽 Linux 4.1 发行版是基于高级 RPM 技术构建的，您的系统永远不会过时。当有新版本发布时，您可以使用简单的升级程序将任何或所有组件升级到最新版本，该程序会为您完成所有工作。红帽 Linux 2.0、2.1 和 3.0 (Picsos) 用户可以简单且安全地升级到 4.1 版本。

### 革命性的软件开发和许可模式。

红帽 Linux 4.1 发行版是一个完整的基于 POSIX 的操作系统，拥有数百项在价格为十倍之高的 UNIX 操作系统中找不到的功能。

红帽 Linux 提供了整个操作系统的完整源代码，包括所有编译器、库、实用程序和 X 窗口系统。

这项先进操作系统技术惊人价值背后的源泉是红帽 Linux 技术的协作开发。GNU 和 Linux 技术受 GPL 版权保护，该协议排除了对全球软件开发贡献的商业控制权和限制。

- 有关这一迷人主题的更多内容，请参阅本书内部。

![](img/3d09de050edc8aef2a604e36a4127b47_267_0.png)

