
# Solaris 7 参考指南

![](img/ff371d3d858587ebc936ec78efb90a15_0_0.png)

Janice Winsor

![](img/ff371d3d858587ebc936ec78efb90a15_1_0.png)

Janice Winsor

编辑/制作监督：Faye Gemellaro

封面设计总监：Jerry Votta

封面插图：Scott Weiss

制造经理：Alexis R. Heydt

营销经理：Bryan Gambrel

征稿编辑：Gregory G. Doench

技术编辑：Bill Calkins

营销经理：Michael Lloyd Alread

出版者：Rachel Borden

## 前言

Solaris 7 参考手册是您对在线参考文档第 1 节“用户命令”中所有手册页的完整指南（除 FMLI 命令外）。

指南内的所有文档引用均指向官方 Solaris 文档。要访问 Sun Microsystems, Inc. 的在线文档，请访问：

`http://docs.sun.com`。

## 读者群

本书适用于任何 Solaris 系统软件的用户，他们需要参考在线手册页中的第 1 节用户命令进行快速参考或获取更详细的信息。

## 本书使用的约定

下表显示了书中使用的排版约定。

| 字体或符号 | 说明 |
| --- | --- |
| `courier` | 表示命令、文件名、对象名、方法、参数、JavaScript 关键字、HTML 标签、文件内容或代码段。 |
| 字体或符号 | 说明 |
| --- | --- |
| *`courier` 斜体* | 表示您应该用有效值替换的变量。 |
| **courier** | 表示您输入的文本。 |
| *斜体* | 表示定义、强调或 |

## 图标

在本书中，任何在 Solaris 7 中新增或修订的内容将在页边标记有“New!” 图标。

## 本书组织方式

本章节按字母顺序组织命令，以便快速查找。第 1 节用户命令的列表按字母顺序排列，并用星号标记在 Solaris 7 中修订的内容。

## 致谢

Solaris Press 感谢以下人员对本书的贡献：Calkins, Microsystems, Inc. 提供了支持；Borden, SQA Product, 提供了帮助；Gallops, Pyramid Inc., 提供了修订稿；Nohr, Communications, 提供了友谊；Maris, 实现了设计。

## 引言

Solaris 7 参考手册是您对在线参考文档第 1 节“用户命令”中所有手册页的完整指南（除 FMLI 命令外）。指南内的所有文档引用均指向官方 Solaris 文档。要访问 Sun Microsystems, Inc. 的在线文档，请访问：...

## 音频应用 (SUNWaudio)

| | | |
| --- | --- |
| `audioconvert` | 转换音频格式 |
| `audioplay` | 播放音频 |
| `audiorecord` | 录制音频文件 |

## 附带工具 (SUNWBtool)

| | | |
| --- | --- |
| `ar` | 维护归档为随机库 |
| `dis` | 反汇编器 |
| `dump` | 转储对象文件的部分 |
| `elfdump` | 转储对象文件的部分 |
| `gprof` | 显示调用图数据 |
| `lex` | 生成词法分析程序 |
| `lorder` | 归档的排序关系 |

## 2 引言

| | | |
| --- | --- | --- |
| `mcs` | 操作对象的注释部分 |
| `nm` | 打印对象的名称列表 |
| `prof` | 显示分析数据 |
| `ranlib` | 将归档转换为库 |
| `size` | 打印对象节的大小 |
| `strip` | 从对象文件中删除符号表、调试和行号 |
| `symorder` | 符号符号列表 |
| `tsort` | 拓扑排序 |
| `unidef` | 从 C 程序源中解析并删除 ifdef 行 |
| `yacc` | 另一个编译器编译器 |

## 核心 Solaris (Usr) (SUNWcsu)

### 归档命令

| | | |
| --- | --- |
| `cpio` | 进出文件归档 |
| `eject` | 从驱动器中弹出 CD-ROM 和磁盘介质 |
| `fdformat` | 格式化磁盘或 PCMCIA 内存卡 |
| `mt` | 磁带控制 |
| `pax` | 可移植归档交换 |
| `tar` | 创建磁带归档并添加或提取文件 |
| `unzip` | 从 Zip 归文件中列出、测试和提取压缩文件 |
| `zipinfo` | 列出 Zip 归文件的详细信息 |

### 通信命令

| | | |
| --- | --- |
| `ftp` | 文件传输程序 |
| `login` | 登录系统 |
| `mail`, `rmail` | 读取邮件或向用户发送邮件 |
| `mailcompat` | 提供 Solaris 邮箱兼容性 |
| `mailx`, `mail`, `Mail` | 交互消息处理系统 |
| `mesg` | 允许或拒绝消息 |
| `mconnect` | 连接 SMTP 邮件服务器套字 |
| `on` | 使用本地环境在远程系统上执行命令 |
| `rlogin` | 远程登录 |
- `rsh`, `remsh`, `remote_shell` 远程外壳。1133
- `talk` 与另一个用户通信。1306
- `telnet` 使用 TELNET 协议访问远程系统的用户界面。1324
- `tftp` 简单文件传输程序。1334
- `tip` 连接到远程系统。1342
- `vacation` 自动回复邮件。1451
- `write` 向另一个用户写入内容。1502

### 文件管理命令

- `cat` 合并并显示文件。121
- `cd`, `chdir`, `pushd`, `popd`, `dirs` 更改工作目录。127
- `chgrp` 更改文件组所有权。133
- `chmod` 更改文件的权限模式。138
- `chown` 更改文件所有者。142
- `cksum` 写入文件的校验和和大小。145
- `cmp` 比较两个文件。147
- `cp` 复制文件。163
- `crypt` 编码或解码文件。183
- `exportfs` 将导出选项转换为 share/unshare 命令。334
- `file` 确定文件类型。354
- `getfac` 显示任意访问文件信息。432
- `head` 显示文件的前几行。466
- `kill` 终止信号处理进程。577
- `ln` 为文件创建硬链接或符号链接。692
- `ls` 列出目录内容。740
- `mkdir` 创建目录。825
- `more`, `page` 浏览或分页查看文本文件。830
- `mv` 移动文件。842
- `pathchk` 检查路径名。983
- `pg` 文件查看过滤器。1004
- `ps` 报告进程状态。1081
- `pwd` 返回工作目录名称。1094
- `rcp` 远程文件复制。1098

## 4 介绍

| `rdist` | 远程文件发布程序。 | 1100 |
| `rm`, `rmdir` | 删除目录项。 | 1119 |
| `setfacl` | 修改文件或多个文件的访问控制列表 (ACL)。 | 1208 |
| `tail` | 交付文件的最后部分。 | 1303 |
| `tee` | 复制标准输出。 | 1322 |
| `touch` | 修改文件的访问和修改时间。 | 1355 |
| `type` | 命令类型的描述。 | 1390 |
| `umask` | 获取或设置文件模式创建掩码。 | 1398 |
| `which` | 定位命令；显示其路径或别名。 | 1492 |

### Kerberos 命令

| `chkey` 更改用户的安全 RPC 密钥对。 | 136 |
| `kdestroy` | 销毁 Kerberos 票据。 | 570 |
| `kerberos` | Kerberos 安全系统介绍。 | 572 |
| `keylogin` | 使用 keyserv 解密并存储机密。 | 574 |
| `keylogout` 使用 keyserv 删除存储的机密。 | 576 |
| `kinit` | Kerberos 登录命令。 | 581 |
| `klist` 列出当前持有的 Kerberos 票据。 | 583 |
| `ksrvtgt` 使用服务密钥获取并存储 Kerberos 票据授予票。 | 638 |

### 本地化命令

| `dumps` 显示当前区域的字符集表。 | 274 |
| `gettext` 从消息数据库中检索文本字符串。 | 445 |
| `iconv` 字符集转换工具。 | 481 |
| `is` 显示此平台的原生指令集。 | 527 |
| `localedef` 定义区域环境。 | 702 |
| `xstr` 从 C 程序中提取字符串。 | 1514 |

另见第 17 页的“系统本地化 (SUNWloc)”。

### 杂项

| `Intro`, `intro` 命令和应用程序的介绍。 | 498 |
