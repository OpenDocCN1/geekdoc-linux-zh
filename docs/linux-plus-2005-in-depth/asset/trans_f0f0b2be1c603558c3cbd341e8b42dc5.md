

## Linux+ 2005 深入解析

Jason W. Eckert
M. John Schicka

**《Linux+ 2005 深入解析》**，作者为 Jason W. Eckert 和 M. John Schicka

- 完全映射到 CompTIA 的 2005 年 Linux+ 认证考试
- 您的完整认证解决方案——涵盖安装、管理和系统管理
- 包含详尽的章节摘要和关键术语，以及测试您知识的复习题
- 为系统管理员和程序开发人员提供综合信息

### 版权声明

© 2005 年，Thomson Course Technology PTR 版权所有。本书任何部分未经 Thomson Course Technology PTR 书面许可，不得以任何形式或任何手段（包括电子或机械方式，如复印、录音或任何信息存储和检索系统）复制或传播，但在评论中包含简短引用除外。

Thomson Course Technology PTR 标志及相关商业装潢是 Thomson Course Technology PTR 的商标，未经书面许可不得使用。

所有其他商标均为其各自所有者的财产。

> **重要提示：** Thomson Course Technology PTR 无法提供软件支持。如需帮助，请联系相应软件制造商的技术支持热线或网站。

Thomson Course Technology PTR 和作者在本书中已尽力通过遵循制造商使用的大写风格，将专有商标与描述性术语区分开来。

本书中的信息由 Thomson Course Technology PTR 从据信可靠的来源获取。然而，由于我们的来源中可能存在人为或机械错误，Thomson Course Technology PTR 或其他方面，出版方不保证任何信息的准确性、充分性或完整性，并对使用此类信息产生的错误或遗漏及结果概不负责。读者应特别意识到，互联网是不断变化的实体。自本书出版以来，一些事实可能已经发生变化。

有意购买多本副本或寻求本书授权的教育机构、公司和组织应联系出版方以获取批量折扣信息。培训手册、CD-ROM 以及本书的部分内容也可单独购买或根据特定需求进行定制。

ISBN: 1-59200-728-7
图书馆会编目卡片编号: 2004116287
美国印制
05 06 07 08 09 BH 10 9 8 7 6 5 4 3 2 1

### Course Technology PTR 出版人及总经理

- **Stacy L. Hiquet** (Technology PTR)
- **William Pitkin III** (执行编辑)
- **Manyu Chylianski** (产品经理)
- **Dave George** (发展编辑)
- **Elena Montillo, Megan Belanger, Elizabeth Furbish** (制作编辑)
- **Laura Burns** (高级制造协调员)
- **Burt LaFountain** (技术编辑)
- **Sarah O'Donnell** (高级市场经理)
- **Heather Hurley 和 Kristin Eisenzopf** (市场经理)
- **Jordam Casey** (市场协调员)
- **Heather Talbot** (编辑服务经理)
- **Mike Tanimack** (封面设计)
- **William Hartman** (排版员)
- **Sharon Shock** (索引编制员)

### 致谢

首先，我们要感谢 Course Technology 的职员团队，让我们有一本采用与传统书籍根本不同方法的 Linux 书籍的整体愉快写作体验。具体而言，我们要感谢我们的项目经理 Manya Chylinski 的协调和见解，以及我们的发展编辑 Dave George 和制作编辑 Elena Montillo，感谢他们投入大量时间将所有内容整合在一起，将文本转化为目前的状态。此外，我们要感谢 Digital Content Factory 的 Moirag Haddad 提供的建议和指导，以及 TRIOS College 的 Frank Gerenser，感谢他让我们有时间写这本书，并持续鼓励我们通过写书来补充教学。

**Jason W. Eckert：** 我必须借此机会感谢我的合著者 M. John Schitka 在这本书上付出的辛勤工作、长时间的工作和奉献精神。同样，我感谢 Starbucks Coffee 让我保持进度，最重要的是感谢我的女儿 Mackenzie，她为我提供了本书中使用的许多示例，并教会我打篮球的乐趣比写书更重要。

**M. John Schitka：** 首先，我想感谢我的导师和合著者 Jason W. Eckert，感谢他在创作这本书的漫长小时和深夜里给予的见解、耐心和智慧。更重要的是，我必须感谢我的家人，我的妻子 Jill，以及孩子们 Kyra、Luke 和 Noah，感谢他们在写这本书期间给予的支持、宽容和耐心。希望读者能发现这本书具有启发性，并在他们的教育旅程中有所受益。

最后，我们要感谢同事 Mitch Mijailovic 和 Tonio Mladine 的鼓励；如果没有他们，我怀疑我们今天不会像现在这样热爱 Linux 操作系统。

读者被鼓励通过电子邮件向作者发送关于 *Linux+ 2005 深入解析* 的评论、问题和建议：

- Jason W. Eckert: jasonec@trios.com
- M. John Schitka: johnsc@trios.com

### 内容概览

- 引言 ... xv
- 第 1 章：Linux 简介 ... 1
- 第 2 章：准备安装 Linux ... 43
- 第 3 章：Linux 安装与使用 ... 73
- 第 4 章：探索 Linux 文件系统 ... 113
- 第 5 章：Linux 文件系统管理 ... 159
- 第 6 章：Linux 文件系统管理（行政） ... 199
- 第 7 章：高级安装 ... 245
- 第 8 章：使用 BASH Shell ... 281
- 第 9 章：系统初始化和 X Windows ... 325
- 第 10 章：管理 Linux 进程 ... 373
- 第 11 章：常见管理任务 ... 407
- 第 12 章：压缩、系统备份和软件安装 ... 445
- 第 13 章：故障排除和性能 ... 489
- 第 14 章：网络配置 ... 523
- 第 15 章：配置网络服务和安全 ... 563
- 附录 A：认证 ... 597
- 附录 B：GNU 公共许可协议 ... 605
- 附录 C：在互联网上寻找 Linux 资源 ... 613
- 附录 D：章节复习题答案 ... 617
- 词汇表 ... 623
- 索引 ... 655

### 目录

**引言** ... xv

**第 1 章：Linux 简介** ... 1
- 操作系统 ... 2
- Linux 操作系统 ... 4
- Linux 操作系统的版本 ... 5
- 识别内核版本 ... 5
- Linux 的授权 ... 7
- Linux 的优势 ... 10
- Linux 的历史 ... 17
    - UNIX ... 17
    - 黑客文化 ... 18
    - Linux ... 19
- Linux 发行版 ... 21
- Linux 的常见用途 ... 25
    - 互联网服务器 ... 26
    - 文件和打印服务器 ... 31
    - 应用服务器 ... 32
    - 超级计算机 ... 33
    - 科学/工程工作站 ... 34
    - 办公工作站 ... 35
- 章节摘要 ... 35
- 关键术语 ... 36
- 复习题 ... 40

**第 2 章：准备安装 Linux** ... 43
- 理解硬件 ... 44
    - 中央处理器 (CPUs) ... 44
    - 物理内存 ... 46
    - 磁盘驱动器 ... 48
    - 主板和外围组件 ... 52
- 视频适配卡和监视器 ... 55
- 键盘和鼠标 ... 56
- 收集安装前信息 ... 56
    - 收集硬件信息 ... 59
    - 收集软件信息 ... 62
- 章节摘要 ... 64
- 关键术语 ... 65
- 复习题 ... 70

**第 3 章：Linux 安装与使用** ... 73
- 安装 Linux ... 74
    - 安装方法 ... 74
    - 执行安装 ... 75
- 基本 Linux 使用 ... 95
    - Shell、终端和内核 ... 95
    - 基本 Shell 命令 ... 99
    - Shell 元字符 ... 101
    - 获取命令帮助 ... 102
    - 关闭 Linux 系统 ... 107
- 章节摘要 ... 108
- 关键术语 ... 109
- 复习题 ... 110

**第 4 章：探索 Linux 文件系统** ... 113
- Linux 目录结构 ... 114
- 更改目录 ... 115
- 查看文件和目录 ... 118
    - 文件类型 ... 118
    - 文件名 ... 119
    - 列出文件 ... 120
    - 通配符元字符 ... 126
- 显示文本文件的内容 ... 127
- 显示二进制文件的内容 ... 134
- 在文件中搜索文本 ... 135

