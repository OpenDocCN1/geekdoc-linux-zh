
| `poor [options] filename` | 贫穷文件 |
| `strong [options] filename` | 强文件 |
| `weak [options] filename` | 弱文件 |
| `young [options] filename` | 年轻文件 |
| `alive [options] filename` | 活着文件 |
| `dead [options] filename` | 死亡文件 |
| `happy [options] filename` | 快乐文件 |
| `sad [options] filename` | 悲伤文件 |
| `right [options] filename` | 正确文件 |
| `wrong [options] filename` | 错误文件 |
| `true [options] filename` | 真文件 |
| `false [options] filename` | 假文件 |
| `possible [options] filename` | 可能文件 |
| `impossible [options] filename` | 不可能文件 |
| `easy [options] filename` | 容易文件 |
| `hard [options] filename` | 困难文件 |
| `simple [options] filename` | 简单文件 |
| `complex [options] filename` | 复杂文件 |
| `certain [options] filename` | 确定文件 |
| `uncertain [options] filename` | 不确定文件 |
| `good [options] filename` | 好文件 |
| `bad [options] filename` | 坏文件 |
| `better [options] filename` | 更好文件 |
| `worse [options] filename` | 更差文件 |
| `first [options] filename` | 第一个文件 |
| `last [options] filename` | 最后一个文件 |
| `best [options] filename` | 文件 |
| `worst [options] filename` | 最糟糕文件 |

# 关于作者

Jon “maddog” Hall 是 Linux International 的执行董事，这是一家致力于推广 Linux 操作系统使用的供应商组织。他在计算机行业已经工作了四个世纪（不知道为什么，这听起来比单纯的“25 年”更有分量），在过去的 18 年里，他一直在使用、编程和崇拜 Unix 操作系统。Jon 目前在康柏公司（Compaq Corporation）工作，帮助康柏构其基于 Linux 的战略。在此之前，Jon 曾哈特福州立技术学院（Hartford State Technical College）计算机科学系主任，当他试图教学生操作系统设计、编译器理论以及如何过上尊严的生活时，学生们亲切地给了他“maddog”这个绰号。

1994 年 5 月，在数字设备公司（Digital Equipment Corporation）工作期间，“maddog”结了 Linux·托瓦尔斯（Linux Torvalds），并且足够聪明（他的批评者说“maddog”只是运气好）而识别出了 Linux 操作系统的潜力。Linux 改变了他的生活，主要是为他提供了每天工作 22 小时的机会。然而，自从“maddog”开始接触 Linux 以来，他也遇到了更多的女孩（特别是他的两个孙女）。你通常可以在各种 Linux 会议和活动上看到 Jon 演讲（“maddog”只是在吠叫），他还以长途跋涉为当地 Linux 用户小组演讲而闻名。

Paul G. Sery 是在位于新墨西哥州阿尔伯克基市的桑迪亚国家实验室（Sandia National Laboratories）工作的计算机系统工程师。他是特殊项目计算机支持单元的成员，专门负责 Unix 和 Linux 系统的管理和故障排除。

当不在与系统管理问题作斗时，Paul 和他的妻子 Lidia 喜欢骑着双人自行车穿过里奥格兰德河谷。他们还喜欢在整个墨西哥旅行。Paul 是《Linux 网络工具包》的作者，以及其他几本书书的合著者。他拥有新墨西哥大学的电气工程学士学位。

# 献

Jon "maddog" Hall：献给爸爸和妈妈™，他们对电子产品的厌恶众所周知，而且他们仍然称呼他们的儿子 Jon 而不是 maddog。

Paul G. Sery：献给我的妻子 Lidia Maura Vazquez de Sery。

# 作者致谢

我想感谢我的妻子 Lidia，她的耐心、支持和良好的建议，这一切让这本书的编写成为可能。没有她，我可能仍然是一个在衬衫里插着口袋保护套、用胶带粘着破损眼镜、狂看《星际迷航》、穿着皱巴巴衬衫、在水槽上架着锅吃面条、周六晚上黑客代码的可怜自怜的哥们儿。好吧，我其实从不迷《星际迷航》，而且我正坐在这个周六晚上敲敲敲打字，但我那奇妙而美丽的妻子确实让我变成了一个更好的人。

当然，我还要感谢威立出版社（Wiley Publishing）的员工，他们也提供了大量且重要的帮助。Terri Varver 和 Rebecca Whitney 提供了持续且关键的协助。他们对我的耐心至关重要。

我感谢 Laura Lewin，她给了我协助编写这本书的机会。她对我充满了信心。我也欠 Anne Hamilton 的（现在是为了……呃，另一位仁士了），她给了我第一份 Linux 工作。我由衷感激，并祝他们在新事业中取得成功。

我还要感谢我的狗，那只臭名昭著的 Oso Maloso；它吃过许多本该早早结束它漫长生涯的东西，包括但不限于：蚂鼠药、芬那林（Advil）、整个万圣节期间几磅吐司卷、某次派对期间几袋鸡骨头、啤酒和其他杂物；逃脱了许多栅栏和门；它还是已故伟大的 Paunchy（阿尔伯克基的前任半神）的朋友。

Oso 有什么用吗？嗯，有一天晚上当我正在写这本书时，我接到一个电话。我把我的苹果派留在键盘旁边，下楼接电话，正好遇到它正在上楼。我本应该知道事有蹊跷，因为它带着一部手机，而当我拿起接电话时没人回答。我上了楼，而它下了楼。苹果派不见了。Oso 1，人类 0。

— Paul G. Sery

# 第一部分：安装 Red Hat Linux

## 第1章：在另一个角落……一只企鹅？

### 世界历史——呃，Linux – 第二部分

### 了解你可以用 Red Hat Linux 做什么

#### 提升你的个人工作站

#### 使用 Linux 网络工具和服务

# 第2章：为 Red Hat Linux 准备

## 为 Red Hat Linux 准备你的硬盘

### 我是胖了还是只是 NTFS？

### 硬盘磁盘碎片整理

### 让路，Windows —— Linux 来了

#### 调整 Windows 9x 和 Windows Me 的尺寸

#### 带有 FIPS 的 FAT 分区

#### 调整 Windows NT、Windows 2000 和 Windows XP NTFS 分区的大小
