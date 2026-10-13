
# Sams 24小时自学Unix系统管理（Sams 24小时自学系列）

## 关于作者

DAVE TAYLOR 是一位专注于商业和技术问题的知名作家、教师和演讲者。他是 The Internet Mall 和 iTrack.com 的创始人，自 1980 年起就参与 Unix 和互联网工作，曾创建了流行的 Elm Mail System 和 Embot 邮件自动回复程序。作为多产的作者，他最近的书籍包括 Learning Unix for Mac OS X、Sams Teach Yourself Unix in 24 Hours、Creating Cool HTML 4.0 Web Pages、Dynamic HTML Weekend Crash Course 和 The e*Auction Insider。

之前的职位包括 HP 实验室的研究科学家以及 SunWorld 杂志的高级评论编辑。他为 Berkeley Unix (BSD) 官方 4.4 版本贡献了软件，他的程序存在于所有版本的 Linux 及其他流行的 Unix 变体中。

Dave 拥有计算机科学学士学位、教育计算硕士学位，并正在攻读 MBA。他通过科罗拉多大学博尔德分校教授商业和技术相关课程，同时也在凤凰大学在线授课。他的电子邮件地址已有 15 多年未变：taylor@intuitive.com。

当不疯狂地在他的 Mac 键盘上打字时，Dave 要么和妻子 Linda 以及两个可爱的孩子 Ashley 和 Gareth 玩耍，要么在博尔德骑自行车兜风。

## 致敬

*献给我在天空中闪耀的三颗明星...*

## 致谢

这个项目相当复杂，需要处理多个操作系统、安装和配置。幸运的是，我很幸运有一群 Unix 和系统专家在帮助我。因此，我想感谢 Andy Lester 帮助我进行经常低效的 Perl 编码，Westley Annis 帮助澄清神秘的 DNS 世界，以及 Max Horn 对 Darwin Fink 项目的有益更正。Gideon Shaanan、Richard Blum、Cedric Higgins、Tim Hicks、Dave Ennis、Brian Bilbrey、Eugene Lee 以及 Tyler 和 Rima Regas 也都通过他们的评论和帮助提供了帮助。

我无法用言语表达对 Dee-Ann LeBlanc 和 David Ennis 的赞美，他们是本书的技术编辑。他们是挑剔的大师，但最终您遇到的任何错误可能都是我的。（但请，提交勘误报告，以便我们在下一版中修复！）特别是，Dee-Ann 在我的理智开始滑坡时总是可以进行深夜的即时消息会话。谢谢！我也很幸运能与我在其他书籍中使用的同一支 Sams 团队合作，尤其是 Katie Purdum、Heather Goodell 和 Elizabeth Finney。他们都由我的老朋友 Mark Taber 领导。

最后，如果没有我妻子和孩子们的宽容，我就无法完成这本书。非常感谢 Linda、Ashley 和 Gareth。为什么爸爸总是坐在电脑前可能并不完全清楚，但偶尔会有成品！

## 我们希望听到您的声音！

作为本书的读者，您是我们最重要的批评者和评论者。我们重视您的意见，并想知道我们做得对的地方、可以改进的地方、您希望我们出版的领域以及您愿意分享的其他智慧之言。

您可以直接通过电子邮件或写信告诉我您喜欢或不喜欢这本书的内容——以及我们可以如何让我们的书籍变得更好。

*请注意我无法帮助您解决与本书主题相关的技术问题，并且由于我收到的邮件数量很大，我可能无法回复每一条消息。*

当您写信时，请务必包括本书的标题和作者以及您的姓名、电子邮件地址和电话号码。我会仔细审阅您的评论并与本书的作者和编辑分享。

E-mail: opensource@samspublishing.com

邮寄：

Mark Taber

副出版人

Sams Publishing

800 East 96th Street

Indianapolis, IN 46240 USA

## 读者服务

有关本书或另一本 Sams 书籍的更多信息，请访问我们的网站 www.samspublishing.com。在搜索字段中输入 `ISBN`（不含连字符）或书籍标题即可找到您要查找的页面。

## Introduction

欢迎阅读 *24小时学会Unix系统管理*！本书的设计对初学者系统管理员和已有Unix经验的人都很有帮助。此书既可作为指南，也可作为教程。本书的读者被假定为聪慧，并至少对Unix有基本熟悉程度。如果你想在深入阅读本书之前复习一下Unix，我建议阅读配套书目 *24小时学会Unix*，这是一本畅销的入门书，能让你比说出“supercalifragilisticexpialidocious!”更快地掌握Unix的复杂性！（或者输入它，同样如此！）

### What This Book Isn't

我想在你还在书店浏览时就说明一下本书的意图：本书并非打算成为你唯一学习的系统管理资料。事实上，本书源于我教授的一门课程，即Unix系统管理的 *介绍*。之所以有此区别，是因为市面上有多部关于管理的优秀参考著作（通常为800–1,100页），它们提供的是“如果这里出错，就这样修复”的 cookbook 方法。这非常有帮助，我的参考书架上就有这些书，但它们并不会教你 *如何以Unix的方式
