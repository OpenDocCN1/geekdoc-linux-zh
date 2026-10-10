

# Linux 的安装与管理

第二版

Linda McKinnon
Al McKinnon

![](img/cae5c706c216875d12d4b7d28144cc71_0_0.png)

![](img/cae5c706c216875d12d4b7d28144cc71_1_0.png)

![](img/cae5c706c216875d12d4b7d28144cc71_2_0.png)

# Linux 的安装
与管理

# 第二版

Linda McKinnon
Al McKinnon

QA76.76.063 M39874 2002
McKinnon, Linda.
Linux 的安装与
管理 /
c2002.

Gearhead Press

![](img/cae5c706c216875d12d4b7d28144cc71_2_1.png)

Wiley 计算机出版
John Wiley & Sons 公司

出版人：Robert Ipsen
编辑：Ben Ryan
咨询编辑：Donis Marshall
责任编辑：Angela Smith
文字设计与排版：D&G Limited, LLC

公司用于区分其产品的标识通常被声称为商标。在所有 John Wiley & Sons 公司知悉该声明的情况下，产品名称将以首字母大写或全大写字母显示。然而，读者应联系相关公司以获取有关商标和注册的更完整信息。

本书使用无酸纸印刷。

版权所有 © 2002，Linda McKinnon 和 Al McKinnon 著。保留所有权利。

**由 John Wiley & Sons 公司，纽约出版**

同时加拿大出版。

除根据 1976 年美国版权法第 107 或 108 条许可的情况外，未经出版商事先书面许可，或未经通过向版权许可中心支付适当单本费用获得授权，本出版物的任何部分不得以电子、机械、 photocopying（复印）、录音、扫描或其他方式复制、存储在检索系统中或传输。向出版商申请许可的请求应寄至许可部门，John Wiley & Sons 公司，纽约第三大道 605 号，纽约，纽约 10158-0012，电话 (212) 850-6011，传真 (212) 850-6008，电子邮件：PERMREQ@WILEY.COM。

本出版物旨在提供关于所涵盖主题准确且权威的信息。它基于出版商不从事专业服务这一理解出售。如果需要专业建议或其他专家协助，应寻求合格专业人士的服务。

Gearhead Press 商标是 Gearhead Group Corporation 的独家财产。

*国会图书馆图书在版数据*：

ISBN: 0-471-20884-1

美国印刷

10 9 8 7 6 5 4 3 2 1

## Gearhead Press 致读者

Gearhead Press 致力于出版面向经验丰富的信息技术专业人士的技术书籍——网络工程师、开发人员、系统管理员和其他人员——他们需要更新技能、学习如何更有效地使用技术，或者仅仅是想要一份关于最新技术的高质量参考。

Gearhead Press 源于我对工程师和开发人员专业培训人员的经验：这些人员通过第一手经验真正理解在职专业人士的需求。Gearhead Press 的作者是业内顶尖的培训专家，他们在定义技术革命的公司工作。因此，Gearhead Press 的作者经常与那些通过创新产品改变世界的开发人员和工程师处于同一战壕中。基于在 IT 培训中的这一经验，我们的书籍提供卓越的技术内容，并带有基于实际经验的独特视角。

现在，作为 John Wiley & Sons 公司的一个出版社，Gearhead Press 将继续为读者带来 Wiley 在过去近 200 年中一贯提供的质量水平。

谢谢你。

Donis Marshall
Gearhead Press 创始人
Wiley 计算机出版咨询编辑

![](img/cae5c706c216875d12d4b7d28144cc71_5_0.png)

*出版商
赠礼*

# Gearhead Press 在售图书

（有关当前和即将出版的完整信息，请访问 www.wiley.com/compbooks/）

## Gearhead Press 点对点系列图书

- 迁移到 Microsoft Exchange 2000
作者：Stan Reimer
ISBN 0-471-06116-6

- 使用 Apache 安装和配置 Web 服务器
作者：Melanie Hoag
ISBN 0-471-07155-2

- VoiceXML：启用网站语音功能的 10 个项目
作者：Mark Miller
ISBN 0-471-20737-3

## Gearhead Press 前线实战系列图书

- Windows 2000 自动化部署
作者：Ted Malone, Rolly Perreault 和 Mike Young
ISBN 0-471-06114-X

- 强健的 Linux：确保高可用性
作者：Iain Campbell
ISBN 0-471-07040-8

- 为 Windows 2000 编程目录服务
作者：Donis Marshall
ISBN 0-471-15216-1

- 编程 ADO.NET
作者：Richard Hundhausen 和 Steven Borg
ISBN 0-471-20187-1

- 使用 ADO.NET 和 XML 设计 .NET Web 服务
作者：Richard Hundhausen 和 Steven Borg
ISBN 0-471-20186-3

- 为 Microsoft .NET 平台进行无线和移动开发
作者：Steven Juntunen
ISBN 0-471-21494-9

- 让 Win32 应用程序移动化：移植到 Windows CE
作者：Nancy Nicolaisen
ISBN 0-471-21618-6

- 编程 Windows CE 无线应用程序
作者：Barry Shilmover 和 Derek Ball
ISBN 0-471-21469-8

# 目录

- 引言 xiii
- 致谢 xx
- 作者简介 xxii
- 第 1 章 Linux 的起源 1
    - UNIX 简史 1
    - Linux 的历史 7
    - Linux 的特性 8
- 第 2 章 从 CD-ROM 安装 Linux 13
    - 在 IDE 系统上安装 Linux 14
    - 启动 Linux 安装 16
- 第 3 章 开始使用 Linux 系统 47
    - 登录和注销 47
    - 创建用户帐户和密码 49
    - 命令语法 55

![](img/cae5c706c216875d12d4b7d28144cc71_8_0.png)

Linux 和 UNIX 命令的在线信息 56

查看日期：date 和 cal 命令 64

请求已登录用户的数据 67

发送和接收邮件：mail 命令 70

向屏幕发送消息：write 和 wall 命令 75

在线交谈：talk 命令 77

屏蔽消息和对话：mesg 命令 78

其他工具：clear、echo、banner 和 wc 命令 79

练习 83

测验 90

# 第 4 章 Linux 中的文件和目录 93

文件系统结构和层次结构 94

导航目录结构 99

管理目录 101

格式化和访问软盘 110

练习 117

测验 119

# 第 5 章 在 Linux 中使用文件 121

文件和目录：快速回顾 121

Linux 文件名指南 122

创建和更新文件：touch 命令 123

链接文件：In 命令 125

查看文件内容 127

复制、移动和删除文件 130

mtools 实用程序 138

打印文件：lp、lpq 和 lprm 命令 140

练习 149

测验 154

# 第 6 章 Linux 文件权限 157

ls-l 命令回顾 157

权限 159

创建个人目录 168

命令及其所需权限的示例 171

- 练习 171
- 测验 175

## 第 7 章 Shell 基础 179
    - Linux/UNIX Shell 180
    - Linux/UNIX Shell 的类型 181
    - 命令行解析 184
    - 元字符和通配符 185
    - 引用元字符以禁用 Shell 解释 193
    - 标准文件：重定向和管道 195
    - 使用管道连接命令 207
    - 使用分号进行命令分组 212
    - 使用反斜杠进行行续接 213
    - Shell 历史命令 213
    - 练习 217
    - 测验 222

## 第 8 章 基本 Linux 实用程序 225
    - 在目录中搜索文件：find 命令 226
    - 定位命令：whats、whereis 和 which 命令 234
    - 在文件中定位数据：grep 命令 237
    - 排序输出：sort 命令 246
    - 显示文件的部分：head 和 tail 命令 250
    - 练习 253
    - 测验 256

## 第 9 章 高级 Linux 实用程序 257
    - 最大化每个命令的工作量：xargs 257
    - Linux/UNIX 快捷方式：alias 命令 264
    - 比较 find 功能和 Shell 功能 268
    - 确定文件类型：file 命令 273
    - 比较文本文件：diff 命令 276
    - 比较所有类型的文件：cmp 命令 283
    - 压缩文件：gzip、gunzip 和 zcat 命令 285
    - 显示不可打印字符：cat 命令选项 288

