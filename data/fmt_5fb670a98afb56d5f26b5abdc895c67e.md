
# Python 核心参考指南

![](img/45e4e9c5e19cc2479075c7f2c42810ef_0_0.png)

面向编程专业人士的必备参考书

Developer’s Library 系列书籍旨在为实践型程序员提供其在日常工作中使用的编程语言和技术的独特、高质量的参考和教程。

Developer’s Library 的所有书籍均由专家技术从业者编写，他们非常擅长通过组织和呈现信息，使其对其他程序员有用用。

核心书目包括其主题领域内最优秀、最广受誉的书籍：

- PHP and MySQL Web Development

  Luke Welling & Laura Thomson

  ISBN 978-0-672-32916-6

- MySQL

  Paul DuBois

  ISBN-13: 978-0-672-32938-8

- Linux Kernel Development

  Robert Love

  ISBN-13: 978-0-672-32946-3

- Python Essential Reference

  David Beazley

  ISBN-13: 978-0-672-32866-6

- Programming in Objective-C

  Stephen G. Kochan

  ISBN-13: 978-0-321-56615-7

- PostgreSQL

  Korrry Douglas

  ISBN-13: 978-0-672-33015-5

Developer’s Library 系列书籍可在大多数零售和在线书店购买，也可以通过 Safari Books Online 在 `safari.informit.com` 进行订阅。

策划编辑

Mark Taber

开发编辑

Michael Thurston

主编

Patrick Kanouse

项目编辑

Seth Kerry

文稿编辑

Lisa Thibault

索引员

David Beasley

校对

Megan Wade

技术编辑

Noah Goft

Kurt Grandis

出版协调

Vanessa Evans

书籍设计

Gary Airy

音乐制作

Bronkella Publishing

*献给 Paula, Thomas 以及他们即将出生的兄弟。*

20 线程 413

点运算符 `.` 75

程序结构 81

内置异常 86

- 安装第三方库 154

- 读取命令行选项 157

- 解释器选项与环境 173

- 每个用户的 site 软件包 177

- 启用未来特性 178

- 程序终止 179

- 单元测试与 `unittest` 模块 183

- 调试器命令 187

- 程序性能分析 190

- 反汇编 193

- 调优策略 194

- 内置函数与类型 201

- 内置警告 216

## 13 Python 运行时服务 219

- copy 219

- 注释 222

- marshal 226

- sys 229

- 注释 242

- 注释 256

## 15 数据结构、算法与代码简化 257

- collections 262

- contextlib 267

- heappq 269

- 低层 codecs 接口 277

- 模式语法 281

- 函数 283

- 匹配对象 285

- 有用函数 290

- 打包与解包函数 290

- 格式代码 291

- 关系数据库 API 297

- 游标 298

- 连接对象 305

- 示例 316

- 注释 317

- 注释 336

- 示例 348

- 日志级别 355

- 其他函数 366

- msvcrt 372

- os 378

- 异常 396

- 示例 401

- 注释 407

- winreg 408

- multiprocessing 415

- 管理对象 428

- Lock 对象 438

- RLock 438

- 锁的使用 442

- asyncore 455

- 何时考虑异步网络 467

- 地址族 470

- 注释 486

- ssl 486

- 注释 538

- 注释 558

- hashlib 559

- 示例 560

- qupropri 567

- XML 示例 minidom 570

- xml.dom.minidom.etree.ElementTree 573

    - 嵌入模板 608

- 工具函数 617

- 高级扩展与嵌入 619

# 附录 Python 3 621

- 谁应该使用 Python？ 621

    - 将代码移植到 Python 2.6 634

- 使用 2to3 工具 635

# 索引 639

# 关于作者

David M. Beazley 是一位资深 Python 爱好者，自 1996 年起一直参与 Python 社区。他广为人知的可能可能是他对 SWIG 的工作，这是一项用于将 C/C++ 程序与其他编程语言（包括 Python、Perl、Ruby、T 和 Java）集成的流行软件包。他还编写了许多其他编程工具，包括 PLY（它是 lex 和 yacc 的 Python 实现）。Dave 在洛斯阿拉马国家实验室的理论物理学部工作了七年，在那里他帮助开了 Python 在大规模并行超级计算机上的使用。之后，Dave 去当了一名“恶魔教授”，在那里他享受学生们各种疯狂的编程项目。然而，他此后意识到了自己的错误，现在在芝加哥作为独立软件开发人员、顾问、Python 培训师和兼职爵士乐手。可以通过 http://www.dabeaz.com 与他联系。

# 关于技术编辑

Noah Gift 是《Python For UNIX and Linux System Administration》（O'Reilly）的合著者，并正在编写《Google App Engine In Action》（Manning）。他曾是作家、演讲者、顾问和社区领袖，曾为 IBM developerWorks、Red Hat Magazine、O'Reilly 和 MacTech 等出版物撰稿。他的咨询网站是 http://www.gifts.com，他的大部分写作作品可以在 http://noahgift.com 找到。你也可以在 Twitter 上关注 Noah。

Noah 拥有洛杉矶州立大学的计算机信息科学（CIS）硕士学位和加州州立大学圣路易斯波波校的营养科学学士学位，是 Apple 和 LPI 认证的系统管理员，曾在加州、迪士尼特效动画、Sony Imagerworks 和 Turner Studios 等公司工作过。他目前在新西兰的 Weta Digital 工作。在空闲时间里，他喜欢与妻子 Leah 和儿子 Liam 一起过时光，为钢琴作曲，跑马拉松并虔诚地锻炼。

# 致谢

本书的出版如果没有许多人的支持将是不可能的。首先，我要感谢 Noah Gift 加入项目并对第四版提供了极佳的反馈。Kurt Grandis 也为许多章节提供了有用的意见。我还要过去的技术评审员 Timothy Boronczyk、Paul Dubois、Mats Wichmann、David Asher 和 Tim Bell，他们宝贵的意见和建议使早期版本的成功。Guido van Rossum 在 1999 年酷热的夏天接待留了我几周，为第一版提供了巨大的帮助。最后，但同样重要的是，如果没有我从读者那里收到的所有反馈，这本书将是不可能的。感谢的人太多无法逐一列出，但我尽力吸收了你们的建议以使本书更好。我还要感谢 Addison-Wesley 和 Pearson Education 的所有同事，他们对项目的持续投入和帮助。Mark Tabor、Michael Thurston、Seth Kerney 和 Lisa Thibault 帮助这一版得以圆满出版。特别要感谢 Robin Drake，他在编辑之前的版本时付出的巨大努力使得第三版的成为可能。最后，我要感谢我了不起的妻子和伴侣 Paula Kamen，感谢她所有的鼓励、魔鬼般的幽默和爱。

# 我们想听听你的意见！

作为本书的读者，你是我们最重要的评论家和评价者。我们重视你的意见，并想知道我们做得好的地方、哪些地方可以改进、你希望我们出版的领域以及你的任何建议。你可以直接邮件至 feedback@informit.com。请务必在写信时提供你的姓名和电子邮件，因为我可能无法回复每条信息。

# 读者服务

访问我们的网站并在 informit.com 注册本书，以便获取更新、下载或错误。

邮件：Mark Taber

主编辑

800 East 96th Street

Indianapolis, IN 46240

本书旨在作为 Python 语言的简洁参考。本书假设读者具有 C 或 Java 等语言的编程经验。此外，对系统编程（例如操作系统概念）的通用熟悉对理解库的部分内容有所帮助。
