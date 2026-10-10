
`软件仓库` 存储大量软件包及相关信息，包括描述每个软件包的标头以及提供该软件包依赖的其他软件包信息的标头。通常，Linux 发行版会为其每个版本维护软件仓库。

- 软件包类别：软件包通常被分为几个类别。Ubuntu 使用以下类别：
    - `main`—Ubuntu 支持的开源软件
    - `universe`—社区维护的开源软件
    - `multiverse`—受版权或法律问题限制的软件
    - `restricted`—专有设备驱动程序
    - `backports`—来自较新版本的 Ubuntu 且早期版本不可用的软件包

`apt-get` 工具会根据 `sources.list` 文件中指定的类别，从它搜索的软件仓库中选择合适的软件包。

## `sources.list`：指定 `apt-get` 搜索的软件仓库

`/etc/apt/sources.list` 文件指定了当你要求查找或安装软件包时 `apt-get` 搜索的软件仓库。你必须修改 `sources.list` 文件，以便 `apt-get` 能够从非默认软件仓库下载软件。通常，你不需要配置 `apt-get` 来安装受支持的软件。

`sources.list` 中的每一行描述一个软件仓库，并具有以下语法：

```
type URI repository category-list
```

其中 `type` 为可执行文件软件包的 `deb` 和源文件软件包的 `deb-src`；`URI` 是软件仓库的位置，通常是 `cdrom` 或以 `http://` 开头的 Internet 地址；`repository` 是要搜索的软件仓库的名称；`category-list` 是 `apt-get` 选择软件包所在的类别的空格分隔列表。注释以井号（`#`）开头，可以在行的任何位置出现，并持续到行末。

Ubuntu 系统中 `sources.list` 中的以下行使 `apt-get` 搜索位于 `us.archive.ubuntu.com/ubuntu` 的 `Precise` 存档中可执行文件的 `deb` 软件包。它接受分类为 `main`、`restricted` 和 `multiverse` 的软件包：

```
deb http://us.archive.ubuntu.com/ubuntu/ precise main restricted multiverse
```

将 `deb` 替换为 `deb-src` 以以相同方式搜索源文件软件包。使用 `apt-get source` 命令下载源软件包。

## 默认软件仓库

Ubuntu 系统中的默认 `sources.list` 文件包含诸如 `precise`（最初发布的 `Precise`）、`precise-updates`（`Precise` 发布后的主要错误修复）、`precise-security`（关键的安全相关更新）和 `precise-backports`（较新、测试较少且未经 Ubuntu 安全团队审查的软件）等软件仓库。`sources.list` 中的某些软件仓库可能被注释掉。移除你希望启用的软件仓库行的前导井号（`#`）。修改 `sources.list` 后，执行命令 `apt-get update`（第 1184 页）以更新本地软件包索引。

下一行是添加到 `sources.list` 中的，它启用 `apt-get` 搜索第三方软件仓库（但请参阅以下安全提示）：

```
deb http://download.skype.com/linux/repos/debian/ stable non-free
```

在这种情况下，软件仓库名为 `stable`，类别为 `non-free`。虽然代码是为 Debian 编译的，但它可以在 Ubuntu 上运行，这种情况很常见。

### 使用你信任的软件仓库

有许多软件包仓库。在选择将哪些软件仓库添加到 `sources.list` 时要有所选择。当你添加一个软件仓库时，你是信任管理该仓库的人不会在你可能下载的软件包中放入恶意软件。此外，不受支持的软件包可能会与其他软件包冲突或导致升级失败。

# LPI 和 COMPTIA 认证

## 本附录内容

- Linux 基础知识 . . . . . . . . . . 1190
- 认证考试 1 目标：LX0-101 . . . . . . . . . . 1204
- 认证考试 2 目标：LX0-102 . . . . . . . . . . 1220

本书被许多大学课程用作指定教材。由于选修这些课程的学生通常寻求 LPI 或 CompTIA 认证，教师们要求将认证目标与本书涵盖的内容进行映射。本书完全覆盖了 LPI Linux 基础知识认证的学习目标，并广泛覆盖了 CompTIA Linux+ 考试的目标。本附录将这些学习目标和考试目标映射到本书的相应页面。全书中使用以下图标来标记讨论学习目标和考试目标的地方。

`LE` 此图标表示覆盖 LPI Linux 基础知识认证学习目标中的某个主题。

`LPI` 此图标表示覆盖 CompTIA Linux+ 考试目标中的某个主题。

`LE+` 此图标表示覆盖 CompTIA Linux+ 考试目标中的某个主题以及 LPI Linux 基础知识认证学习目标中的某个主题。

## 更多信息

LPI Linux 基础知识：`www.lpi.org/linux-certifications/introductory-programs/linux-essentials`

LPI 认证考试：`www.lpi.org/linux-certifications/programs/lpic-1`

CompTIA 考试：`certification.comptia.org/getCertified/certifications/linux.aspx`

CompTIA 和 LPI 合作伙伴关系：`www.lpi.org/linux-certifications/partnership-programs/comptia`

# LINUX 基础知识

# 主题 1：LINUX 社区与开源职业

## 1.1 LINUX 演变和流行操作系统

描述：了解 LINUX 开发及主要发行版

关键知识领域

- 开源理念
    - 开源软件与许可协议 第 6 页
- 发行版
    - 发行版 第 6 页
- 嵌入式系统
    - 嵌入式和移动 Linux 第 6 页
- 常用文件、术语和实用程序部分列表
    - `Android`
        - 嵌入式和移动 Linux 第 6 页
    - `Debian`
        - 发行版 第 6 页
    - `CentOS`
        - `CentOS` 第 33 页

## 1.2 主要开源应用程序

描述：了解主要应用程序及其用途

关键知识领域

- 桌面应用程序
    - 桌面应用程序 第 1151 页
- 服务器应用程序
    - `DHCP`：配置网络接口 第 491 页
    - 第 13 章：使用 `CUPS` 进行打印 第 555 页
    - 第 18 章：`OpenSSH`：安全的网络通信 第 685 页
    - 第 19 章：`FTP`：跨网络传输文件 第 713 页
    - 第 20 章：`sendmail`：设置邮件服务器、客户端及其他 第 739 页
    - 第 21 章：`NIS` 和 `LDAP` 第 769 页
    - 第 22 章：`NFS`：共享目录层次结构 第 801 页
    - 第 23 章：`Samba`：Linux 和 Windows 文件及打印机共享 第 827 页
    - 第 24 章：`DNS`/`BIND`：跟踪域名和地址 第 851 页
    - 第 26 章：`Apache` (`httpd`)：设置 Web 服务器 第 931 页
- 移动应用程序
    - 嵌入式和移动 Linux 第 6 页
- 开发语言
    - 第 27 章：Bourne Again Shell (`bash`) 编程 第 981 页
    - 第 28 章：Python 编程语言 第 1081 页
    - 第 29 章：MariaDB SQL 数据库管理系统 第 1113 页
- 包管理工具和存储库
    - 第 12 章：查找、下载和安装软件 第 531 页
    - 附录 D：使用 `apt-get` 保持系统最新 第 1183 页

常用文件、术语和实用程序部分列表

- `OpenOffice.org`, `LibreOffice`, `Thunderbird`, `Firefox`, `Blender`, `Gimp`, `Audacity`, `ImageMagick`
    - 桌面应用程序 第 1151 页
- `Apache`, `MySQL`, `PostgreSQL`
    - 第 26 章：`Apache` (`httpd`)：设置 Web 服务器 第 931 页
    - 第 29 章：MariaDB SQL 数据库管理系统 第 1113 页
    - 编程语言 第 1152 页
- `NFS`, `Samba`, `OpenLDAP`, `Postfix`, `DNS`, `DHCP`
    - 第 22 章：`NFS`：共享目录层次结构 第 801 页
    - 第 23 章：`Samba`：Linux 和 Windows 文件及打印机共享 第 827 页
    - `LDAP` 第 786 页
    - `Postfix` 第 742 页
    - 第 24 章：`DNS`/`BIND`：跟踪域名和地址 第 851 页
    - `DHCP`：配置网络接口 第 491 页
- `C`, `Perl`, `shell`, `Python`, `PHP`
    - 第 27 章：Bourne Again Shell (`bash`) 编程 第 981 页
    - 第 28 章：Python 编程语言 第 1081 页
    - 编程语言 第 1152 页

## 1.3 理解开源软件及许可

描述：开放社区以及开源软件的商业许可

关键知识领域

- 许可
    - 开源软件与许可协议 第 6 页
- 自由软件基金会 (`FSF`)、开源促进会 (`OSI`)
    - `GNU` 项目 第 3 页
    - Linux 不仅仅是内核 第 6 页
    - `FOSS`/`FLOSS` 第 7 页
    - `GNOME` 和 `KDE` 第 17 页

常用文件、术语和实用程序部分列表

- `GPL`, `BSD`, 知识共享 (`Creative Commons`)
    - ▶ `GPL` 第 5 页
    - ▶ 伯克利 UNIX (`BSD`) 第 3 页
    - ▶ 知识共享 (`Creative Commons`) 第 1245 页 (术语表)
- 自由软件、开源软件、`FOSS`、`FLOSS`
    - ▶ `FOSS`/`FLOSS` 第 7 页
- 开源商业模式
    - ▶ 赚钱 第 7 页

## 1.4 ICT 技能及在 LINUX 中工作

描述：基础信息通信技术 (`ICT`) 技能以及在 LINUX 中的工作

关键知识领域

- 桌面技能
    - ▶ 第 4 章：Fedora 和 Red Hat Enterprise Linux 简介 第 89 页
- 进入命令行
    - ▶ 使用命令行工作 第 119 页
    - ▶ 第 7 章：Linux 实用程序 第 215 页
- Linux 的行业应用、云计算和虚拟化
    - ▶ 第 17 章：在本地和云中设置虚拟机 第 659 页

常用文件、术语和实用程序部分列表

- 使用浏览器、隐私问题、配置选项、搜索网络以及保存内容
    - ▶ `Firefox`: `www.mozilla.org/en-US/firefox/central`
    - ▶ `Chrome`: `www.google.com/intl/en/chrome/browser/features.html`
    - ▶ `Opera`: `www.opera.com`
- 终端和控制台
    - ▶ 使用虚拟控制台 第 121 页
- 密码问题
    - ▶ 用户：更改账户类型和密码 (`GUI`) 第 112 页
    - ▶ 密码安全 第 136 页
    - ▶ `passwd`：更改密码 (`CLI`) 第 137 页
    - ▶ 密码 第 625 页
- 隐私问题及工具
    - ▶ 在网络上搜索 `浏览器隐私`
    - ▶ `Mozilla`: `support.mozilla.org/en-US/kb/private-browsing-browse-web-without-saving-info`
    - ▶ `lifehacker.com/the-best-browser-extensions-that-protect-your-privacy-479408034`
- 在演示文稿和项目中使用常见的开源应用程序
    - ▶ 桌面应用程序 第 1151 页

# 主题 2：在 LINUX 系统中寻找方向

## 2.1 命令行基础

描述：使用 LINUX 命令行的基础知识

关键知识领域

- 基本 `Shell`
    - ► 使用命令行工作 第 119 页
    - ► 第 5 章：`Shell` 第 141 页
- 格式化命令
    - ► 命令行 第 144 页
- 使用选项
    - ► 选项 第 145 页
- 变量
    - ► 参数和变量 第 352 页
    - ► 变量 第 1031 页
- 通配符
    - ► 文件名生成/路径名扩展 第 165 页
    - ► 路径名扩展 第 412 页
- 引号
    - ► 特殊字符 第 142 页
    - ► 引用 `$` 第 354 页
    - ► 引号 第 412 页

常用文件、术语和实用程序部分列表

- `echo`
    - ► `echo`：显示参数 第 219 页
    - ► `echo -c` 第 1009 页
- `history`
    - ► 历史记录 第 376 页
- `PATH` 环境变量
    - ► 在 `.bash_profile` 中设置 `PATH` 第 331 页
    - ► `PATH`：`Shell` 查找程序的位置 第 359 页
- `which`
    - ► `which` 第 255 页

了解即可

- 替换
    - ► 命令替换 第 410 页
- `ll`, `&&.`, 和 `;` 控制运算符
    - ► 列表 第 162 页
    - ► `;` 和 `&&` 分隔命令 第 341 页
    - ► `&&` 和 `||` 布尔控制运算符 第 343 页

## 2.2 使用命令行获取帮助

描述：运行帮助命令并导航各种帮助系统

关键知识领域

- `man`
    - `man`：显示系统手册页 128
- `info`
    - `info`：显示关于实用程序的信息 页 131

常用文件、术语和实用程序的部分列表

- `man`
    - `man`：显示系统手册 页 128
- `info`
    - `info`：显示关于实用程序的信息 页 131
- `man` 页
    - `man`：显示系统手册 页 128
- `/usr/share/doc`
    - `/usr/share/doc` 页 134
- `locate`
    - `locate`：搜索文件 页 256

了解即受益

- `apropos`, `whatis`, `whereis`
    - `apropos`：搜索关键字 页 130
    - `whatis` 页 130
    - `whereis` 页 255

## 2.3 使用目录和列出文件

描述：导航主目录和系统目录，并在各种位置列出文件

关键知识领域

- 文件、目录
    - 普通文件和目录文件 页 177
- 隐藏文件和目录
    - 隐藏文件名 页 180
- 主目录
    - 您的主目录 页 143
- 绝对路径和相对路径
    - 绝对路径名 页 181
    - 相对路径名 页 182

常用文件、术语和实用程序的部分列表

- `ls` 的常用选项
    - 选项 页 221

### 递归列表

- 递归 页 222

### `cd`

- `cd`：切换到另一个工作目录 页 185

### `.` 和 `..`

- `.` 和 `..` 目录条目 页 186

### `home` 和 `~`

- 您的主目录 页 143
- 路径名中的 `~`（波浪号） 页 182
- 波浪号 (`-`) 页 359
- 波浪号扩展 页 407

## 2.4 创建、移动和删除文件

描述：在主目录下创建、移动和删除文件和目录

关键知识领域

- 文件和目录
    - 普通文件和目录文件 页 177
- 大小写敏感性
    - 大小写敏感性 页 179
- 简单通配符和引号
    - 文件名生成/路径名扩展 页 165
    - 路径名扩展 页 412
    - 特殊字符 页 166
    - 引号括起 `$` 页 394
    - 引号 页 452

常用文件、术语和实用程序的部分列表

- `mv`, `cp`, `rm`, `touch`
    - `mv`：移动目录 页 188
    - `mv`：重命名或移动文件 页 237
    - `mv`, `cp`：移动或复制文件 页 187
    - `cp`：复制文件 页 224
    - `rm`：删除链接 页 208
    - `rm`：删除文件（删除链接） 页 222
    - `touch`：更改文件修改和访问时间 页 243
- `mkdir`, `rmdir`
    - `mkdir`：创建目录 页 184
    - `rmdir`：删除目录 页 186

# 主题 3：命令行的强大功能

## 3.1 在命令行上归档文件

描述：在用户主目录中归档文件

关键知识领域

- 文件、目录
    - 普通文件和目录文件 页 177
- 归档、压缩
    - 压缩和归档文件 页 245

常用文件、术语和实用程序的部分列表

- `tar`
    - `tar`：将文件存储到/从归档文件中提取 页 249
    - `tar`：归档文件 页 603
