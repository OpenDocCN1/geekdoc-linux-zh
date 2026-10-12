

## 红帽® Linux® 管理员的必备资源！

![](img/a0884097af3186d9b4f616aaa3f065b0_0_0.png)

## 红帽
LINUX®

### 管理员指南

![](img/a0884097af3186d9b4f616aaa3f065b0_0_1.png)

Kerry Cox

> CD 包含超过
> 1,300 个文件

![](img/a0884097af3186d9b4f616aaa3f065b0_2_0.png)

Heart of Worcestershire College
Redditch Archer, Osprey House & Bromsgrove

书籍应在以下最后日期之前归还或续借。

- 您可以在任意学习中心当面续借：
- 电话续借：
  - Osprey House 01905 725681 - 全年开放
  - Bromsgrove 01527 572555 - 仅在读期间
  - Redditch Archer 01527 572519 - 仅在读期间

或发送电子邮件至：renewals@howcollege.ac.uk

14/6/2004

请注意，借取本物品即表示您同意遵守学院的政策，包括支付逾期罚款。
注意：- 任何物品的丢失或损坏都将收取费用。
逾期归还将收取罚款

- 3 MAY 2017

207361

![](img/a0884097af3186d9b4f616aaa3f065b0_4_0.png)

## 红帽® Linux®

### 管理员
指南

## 在线查看更新

若要查看与本本书和/或 CD-ROM 相关的更新或更正，请访问我们在 [http://www.prima-tech.com/updates](http://www.prima-tech.com/updates) 上的更新页面。

## 向我们发送您的意见

若要对本书或任何 PRIMA TECH 书目发表评论，请访问我们在 [http://www.prima-tech.com/comments](http://www.prima-tech.com/comments) 上的读者反馈页面。

## 如何订购

有关批量折扣的信息，请联系出版商：Prima Publishing, P.O. Box 1260BK, Rocklin, CA 95677-1260; (916) 787-7000。请在您的信头中包含关于书籍预期用途以及您想购买数量的信息。

![](img/a0884097af3186d9b4f616aaa3f065b0_6_0.png)

## 红帽® Linux®
管理员
指南

Kerry Cox

PRIMA PUBLISHING 旗下分部

© 2000 年 Prima Publishing 所有。版权所有。未经 Prima Publishing 书面许可，不得以任何形式或任何手段（包括电子或机械方式，如 photocopying、录音或任何信息存储或检索系统）复制或传输本书的任何部分，但在书评中引用简短引文除外。

![](img/a0884097af3186d9b4f616aaa3f065b0_7_0.png)

Prima Publishing 旗下分部
Prima Publishing 和 colophon 是 Prima Communications, Inc. 的注册商标。PRIMA TECH 是 Prima Communications, Inc. 的商标，加州 Roseville 95661。

Linux 是 Linus Torvalds 的注册商标。Linux 企鹅 Tux 的使用已获 Larry Ewing (lewling@isc.tamu.edu) 许可。Ewing 使用 The GIMP (www.gimp.org) 创建了该图像。对 Tux 的修改由 Jim Thompson 完成。

Red Hat、Red Hat “Shadow Man” 标志、RPM、Maximum RPM、RPM 标志、Linux Library、PowerTools、Linux Undercover、Rhemberer、Rhmember More、Rough Cuts、Rawhide 以及所有基于 Red Hat 的商标和标志均为 Red Hat software, Inc. 在美国和其他国家的商标或注册商标。

Microsoft、Windows、Internet Explorer、Notepad、VBScript、ActiveX 和 FrontPage 是 Microsoft Corporation 的商标或注册商标。Netscape 是 Netscape Communications Corporation 的注册商标。

重要提示：Prima Publishing 无法提供软件支持。请联系相应软件制造商的技术支持热线或网站以获取协助。

Prima Publishing 和作者已尽力在本书中通过遵循制造商使用的大小写风格来区分专有商标和描述性术语。

本书中包含的信息是 Prima Publishing 从被认为可靠的来源获取的。然而，由于来源、Prima Publishing 或他人可能出现人为或机械错误的可能性，出版商不保证任何信息的准确性、充分性或完整性，且对使用该信息导致的任何错误、遗漏或结果概不负责。读者应特别意识到互联网是一个不断变化的实体。自本书付印以来，某些事实可能已经改变。

ISBN: 0-7615-2157-7
美国国会图书馆编目卡号：99-64753
在美国印刷

00 01 02 03 04 1H 10 9 7 6 5 4 3 2 1

| 角色 | 姓名 |
| :--- | :--- |
| 出版人 | Stacy L. Hiquet |
| 市场经理 | Judl Tylor |
| 市场协调员 | Jennifer Breece |
| 编辑总监 | Sandy Doell |
| 图书采购编辑 | Lynette Quinn |
| 高级编辑 | Kevin Harrelld |
| 技术审阅者 | Charles Cofling |
| 文字编辑 | Andrew Saff |
| 内部排版 | Marlan Hartsough |
| 封面设计 | Prima Design Team |
| 索引编制者 | Sherry Massey |

## 献词

*我愿将本书献给我亲爱的妻子，她提供了持续的支持和鼓励。*

*如果没有她，我绝对无法完成这本书。*

## 致谢

特别感谢 Laine Berghout，是她第一次向我展示了一台 Linux 机器并展示了其潜力。我还要感谢 Bruno Browning 和 Read Gilgen 在威斯康星大学麦迪逊分校提供的帮助，以及他们为我提供了一个职业环境，使我不仅专注于学位，还能学习 Linux。Bruno 对我无数无尽的查询表现出了极大的耐心。我要感谢整个 Linux 社区以及许多耐心回答我新闻组帖子的人。他们一次又一次地证明了开源软件是可行的。我只能希望我自己的互助之手能协助他人。还要感谢 Brad Parker 为丰富的管理知识做出的贡献。感谢 John York 和 Dan Gentry 对我编写的许多用户手册及他们继承的大量说明书提供的反馈。Troy Bowman 在自定义 Linux 方面提供了额外的技巧和提示，帮助巨大。我还要感谢 Andrew Bunker 在编程方面的专业知识。我从未认为自己是一名程序员，Andrew 证明了这一点，但他依然极其耐心和乐于助人。

我还要感谢 KSL 的优秀人士，他们对我能力的信心以及他们创造的绝佳工作环境。我非常感谢 Owen Smoot、Mark Fenton、Hal Whitlock，尤其是 Greg James 的帮助和友谊。还要感谢 Pat Neilson 和 Kim Hake 对我无尽的问题和请求的耐心。

我要感谢 Prima Publishing 的各位在使这本书得以出版方面提供的帮助。特别感谢 Lynette Quinn 的支持和鼓励。还要感谢我出色的编辑们，他们帮助我成为了一名比我自己认为所能达到的更好的作家。感谢 Kevin Harrell、Charles Coffing 和 Andy Saff。我相信，我们组队并最终使这本书得以出版，不仅仅是靠运气。

## 作者简介

**Kerry Cox** 正在攻读德国文学博士学位，会说德语、葡萄牙语和俄语。他曾在德国生活两年，最初作为交换生，后来作为获得奖学金的研究人员在 Bayer Industries 从事杀菌剂研究。他还曾在巴西生活两年进行人道主义服务。Kerry 在人文领域凭借其书面材料获得过多个奖项，并出版过文学批评分析和短篇小说。他还开发了互联网上关于德国文学领域的一些初步研究内容。他是 Paul Celan 网站的共同编辑，并开发了国际布莱希特协会的首页。

Kerry 使用 Linux 已有近五年时间，目前是位于犹他州盐湖城的 KSL 广播电视台的系统管理员。他管理着一个由 Linux 和 Solaris 机器组成的大型网络，为美国西部大部分地区提供互联网连接。他此前曾是一家大型互联网服务提供商（也位于盐湖城）的系统管理员，并管理着另一家通过双向卫星传输提供全球访问的 ISP 系统。

他的其他事业包括 GNUware.com，这是一家小公司，提供一张 CD 上包含 1,300 个 Linux 程序的合集。该产品面向希望尝试大量 Linux 应用程序的低速连接用户。

Kerry 现在与妻子和两个小男孩（分别 5 岁和 2 岁）住在犹他州 West Jordan。家中拥有八台联网计算机，他的儿子们已经开始熟悉 Linux。他是一位热衷户外的人，每当有机会就会在 Uinta 山脉徒步和钓鱼。

