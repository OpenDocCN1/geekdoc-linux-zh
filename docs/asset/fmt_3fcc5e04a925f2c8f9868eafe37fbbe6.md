
# 红帽 Linux Fedora 入门指南

![](img/8c094d1b36276212c03d10d898508a6e_5_0.png)

## 关于作者

**Jon ‘maddog’ Hall** 是 Linux International 的执行董事，这是一个致力于推广 Linux 操作系统使用率的供应商组织。他在计算机行业工作了二十多年（不知怎的，这听起来比仅仅说“25 年”更有影响力），其中过去 18 年一直在使用、编程并赞美 Unix 操作系统。Jon 在康柏电脑公司（Compaq Computer Corporation）工作，致力于帮助制定康柏在 Linux 方面的战略。此前，Jon 曾是哈特福德州立技术学院的计算机科学系主任，他的学生们（希望如此）亲切地给他取了昵称‘maddog’，当时他正在试图教授他们操作系统设计、编译器理论以及如何体面地生活。

1994 年 5 月，当 Jon 在数字设备公司（Digital Equipment Corporation）工作时，‘maddog’ 遇到了 Linus Torvalds，并足够聪明（他的批评者说 ‘maddog’ 只是幸运）地认识到 Linux 操作系统的潜力。Linux 改变了他的生活，主要是让他每天工作 22 个小时。然而，自从 ‘maddog’ 开始使用 Linux 以来，他也开始认识更多的女孩（特别是他的两个教女）。通常你可以在各种 Linux 会议和活动上听到 Jon 演讲（‘maddog’ 只是在吠叫），他还以长途跋涉去当地 Linux 用户组演讲而闻名。

**Paul G. Sery** 是计算机系统工程师，受雇于位于新墨西哥州阿尔伯克基的沙尼亚国家实验室（Sandia National Laboratories）。他是计算机支持单位特别项目部的成员，该部门专门负责管理和排除 UNIX 及 Linux 系统故障。

当他不在系统管理问题上撞得头破血流的时候，Paul 和他的妻子 Lidia 喜欢在里奥格兰德河谷骑行他们的双人自行车。他们还喜欢在整个墨西哥旅行。Paul 是《Linux Network Toolkit》的作者，也是其他几本书的合著者。他拥有新墨西哥州的电气工程学士学位。

## 献词

**Jon ‘maddog’ Hall：** 献给爸爸妈妈（TM），他们对电子产品的厌恶众所周知，而且他们仍然可以称呼他们的儿子为 Jon 而不是 maddog。

**Paul G. Sery：** 献给我的妻子，Lidia Maura Vazquez de Sery。

## 作者致谢

我想感谢我的妻子 Lidia，感谢她的耐心、支持和良好建议，所有这些都使得编写这本书成为可能。没有她，我将仍然是一个戴着护口器、眼镜用胶带粘着、看“星际迷航”、穿着皱巴巴衬衫、在洗碗池里煮意大利面、周六晚上黑客操作的可怜家伙。好吧，我从来就不是“星际迷航”的粉丝，而且我现在周六晚上正在敲击键盘，但我美丽的妻子确实让我成为了一个更好的人。

我还想感谢 Anne Hamilton 和 Laura Lewin，她们给了我写作的机会，特别是写这本书的机会。她们都对我表现出极大的信心和耐心。我非常感激，并祝她们的事业成功。

当然，我想感谢 Wiley Publishing 的职员，他们也提供了大量且必不可少的帮助。Terri Varveris 和 Rebecca Whitney 提供了持续且必不可少的协助。

我要承认，我的狗臭名昭著的 Oso Maloso 在写这本书时完全没有提供帮助；它吃了很多本该早早终结其长期生涯的东西，包括但不限于老鼠药、Advil、万圣节那天许多磅的 Tootsie Rolls、聚会上几袋鸡骨头、啤酒和其他各种物品；逃脱了许多围栏和大门；并且是已故的伟大狗狗 Paunchy（你在本书中随处可见它的名字）和其他当地狗狗的朋友。

Oso 有用吗？嗯，一天晚上在写这本书时，我接到一个电话。我把苹果派留在键盘旁边，下楼去接电话，从他上楼的旁边经过。我应该知道有些不对劲，因为他手里拿着一个手机，而我拿起来接电话时没有人回答。他下楼时我上楼。苹果派不见了。Oso 1 分，人类 0 分。

*— Paul G. Sery*

## 出版商致谢

我们为这本书感到自豪；请通过位于 `www.dummies.com/register/` 的在线注册表格向我们发送您的评论。

以下是一些帮助这本书推向市场的人员：

- **收购、编辑和媒体开发**
  - 项目编辑：Rebecca Whitney
  - 收购编辑：Terri Varveris
  - 技术编辑：Korry 和 Susan Douglas
  - 编辑经理：Carol Sheehan
  - 版权编辑：Laura Moss
  - 媒体开发专家：Angela Denny
  - 媒体开发经理：Laura VanWinkle
  - 媒体开发主管：Richard Graves
  - 编辑助理：Amanda M. Foxworth
  - 卡通：Rich Tennant (`www.the5thwave.com`)

- **制作**
  - 项目协调员：Erin Smith
  - 排版和图形：Carrie Foster, Joyce Haughey, Kristin McMullan, Mary Gillot Virgin, Shae Lynn Wilson
  - 校对员：Laura Albert, Carl William Pierce, Charles Spencer, Ethel M. Winslow
  - 索引编制：TECHBOOKS 制作服务

**技术 Dummies 系列的出版和编辑**

Richard Swadley，副总裁兼执行群出版社

Andy Cummings，副总裁兼出版社

Mary C. Corder，编辑总监

**消费者 Dummies 系列的出版**

Diane Graves Steele，副总裁兼出版社

Joyce Pepple，收购总监

**排版服务**

Gerry Fahey，制作服务副总裁

Debbie Staley，排版服务总监

# 引言

*Red Hat Linux Fedora 傻瓜入门*旨在帮助你安装和使用 Red Hat Linux。这本书向你展示了如何用 Red Hat Linux 执行有趣且引人入胜——甚至是有用的——任务。这本书也被设计成一个有效的门垫或咖啡杯垫。无论你用它做什么，我们希望你能享受乐趣。

## 关于本书

这本书被设计成一个帮手式教程。它提供了一个寻求帮助和慰藉的地方，就在那种时刻：当你花了两小时试图让网络连接工作，而你的狗撞了一下线缆，它却神奇地开始工作了。

**注意：** 在付印时，Red Hat 将其 Linux 产品更名为 Fedora 项目。在整本书中，我们通常称该产品为 Red Hat Linux。你可能会在新闻、网络上或其他地方看到该产品被称为 Fedora 项目，但请放心，书中使用的不同术语指的是同一个产品。

我们尽力在这本书中填充了你需要了解的内容，例如如何：

* 安装 Red Hat Linux
* 使用宽带 DSL 和电缆调制解调器或老式拨号调制解调器连接到互联网
* 连接到你的局域网 (`LAN`)
* 构建简单但有效的防火墙
* 构建互联网和 LAN 服务，例如 Web 页面和打印服务器
* 使用 Red Hat Linux 播放 CD 和收听互联网广播电台
* 使用 GNOME 桌面环境
* 利用有用且可用的应用程序，例如 OpenOffice 桌面生产力套件、Evolution 桌面组织者和电子邮件客户端，以及流媒体多媒体播放器 MPlayer
* 使用 OpenOffice 桌面生产力套件来满足你的文字处理、电子表格和演示需求
* 升级你的计算机和网络安全
* 知道去哪里寻求帮助
* 管理你的 Red Hat Linux 工作站

你会在整本书中看到故障排除提示，第 18 章专门致力于此主题。并不是说 Red Hat Linux 有那么大的麻烦，但我们希望你有准备，以防你遇到坏运气。

本书中的指令旨在适用于你在随附 DVD 上找到的 Red Hat Linux 版本；我们还描述了如何下载几个未在 DVD-ROM 上找到的软件包。尽管你可以自由使用其他版本的 Red Hat Linux 甚至其他 Linux 发行版，但请注意，我们的指令可能不精确或不适用。祝你好运！

![](img/8c094d1b36276212c03d10d898508a6e_21_0.png)

## 愚蠢的假设

你知道人们做假设时说的话，但如果我们没有做一些假设，这本书就不会被写出来。如果你是以下情况，这本书适合你：

* **想要构建一个 Red Hat Linux 工作站：** 你想使用 Linux 操作系统来构建你的个人工作站。惊喜！本书后面的 DVD-ROM 包含 Red Hat Linux 发行版。
* **有一台计算机：** 这只是一个技术细节，但你需要一台计算机，因为本书描述了如何在计算机上安装 Red Hat Linux。
* **没有强力胶带：** 你想将 Red Hat Linux 操作系统和计算机组合在一起，而使用强力胶带没有奏效。
