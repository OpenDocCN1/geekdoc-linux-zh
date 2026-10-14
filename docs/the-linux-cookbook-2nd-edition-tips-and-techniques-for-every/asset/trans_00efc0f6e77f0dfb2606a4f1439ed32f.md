

## 30. 娱乐

没有关于如何管理额外时间的章节，生产力又是什么？

本章中的配方描述了那些传统上在 UNIX 系统上找到的经典游戏和奇思妙想，现在可在 Linux 上使用。它还包括使用系统解决文字游戏以及其他保证让你忙碌的娱乐的配方。

### 30.1 玩经典 UNIX 游戏

```
Bsd-games
DEB: bsdgames
RPM: bsd-games
WW: ftp://metalab.unc.edu/pub/Linux/games/
```

这是一套久负盛名的纸牌游戏、动作和冒险游戏、棋盘游戏以及屏幕娱乐。

按当代标准来看，它们在感官刺激方面提供的很少。但它们是经典，在过去的年代里曾是大学校园和各地计算机实验室的主流，而且仍然可以在任何终端上游玩。它们可能同样能娱乐儿童和老一辈。

下表列出了此软件包中包含的各种游戏和程序，给出了其系统名称和描述。

| Command | Description |
|---|---|
| adventure | 基于肯塔基州一个名为巨洞的实际洞穴的基于文本的模拟游戏。由 William Crowther 和 Don Woods 在 1970 年代编写，早于 PC 时代的 ZORK。有关此游戏历史的更多信息可在网上查阅 http://www.rickadams.org/adventure/. |
| arithmetic | 对一组基础加法和减法问题进行测验并计时你的答题速度。 |
| atc | 空中交通管制模拟。 |
| backgammon | 一人或两人玩的双陆棋游戏，附带规则。 |
| banner | 以长垂直文本字体输出文本，适合打印大型横幅。（参见 Recipe 16.4 [Outputting Text Banners], page 402. 在 Debian 系统上，banner 包含在 bsdmainutils 软件包中。） |
| battlestar | 具有奇幻主题的基于文本的冒险游戏。由 David Riggle 于 1979 年编写。 |
| bcd | 将文本过滤为纸带打孔卡输出。 |
| boggle | 流行的文字游戏。 |
| caesar | 解密 Julius Caesar 的密码（参见 Recipe 29.6 [Using ROT13 Encryption], page 569）。 |
| canfield | 扑克纸牌接龙的一种变体。 |
| cfscores | 显示你的 canfield 分数。 |
| countmail | 告诉你有多少邮件，但以“相当令人讨厌”的方式。 |
| cribbage | 纸牌游戏 cribbage。 |
| fish | 儿童纸牌游戏 Go Fish。 |
| gomoku | 两人玩的五子棋游戏。 |
| hangman | 经典的“猜词”游戏。 |
| hunt | 多人网络游戏，其目标是猎杀并消灭所有其他玩家。 |
| mille | Mille Bornes，一种双手纸牌游戏。 |
| monop | Monopoly，一种财产管理游戏，类似于著名的棋盘游戏。 |
| morse | 将文本过滤为摩尔斯电码。默认情况下写出“dit”和“daw”这两个词；使用 `-s` 输出点和划而不是单词。要将摩尔斯电码解码为明文，请使用 `-d` 选项。 |
| number | 将阿拉伯数字转换为英文（参见 Recipe 29.5.2 [Converting an Arabic Numeral to English], page 568）。 |
| phantasia | 角色扮演奇幻游戏。 |
| pig | 将文本过滤为 Pig Latin。目前没有可用的反向过滤器。 |
| pom | 告诉你月亮的当前相位。 |
| ppt | 将文本过滤为纸带输出。 |
| primes | 输出质数，从 0 开始，停止在 4,294,967,295 或标准输入中给出的数字；你也可以将起始和停止值作为参数给出。例如，要输出 1 到 10 之间的质数，运行的命令是 primes 1 10。 |
| quiz | 对来自各种主题的事实和琐事进行测验。 |
| rot13 | 加密和解密 ROT13 密码（参见 Recipe 29.6 [Using ROT13 Encryption], page 569）。 |
| rain | 在屏幕上显示雨滴下落的动画。通过将以毫秒为单位的值作为 `-d` 选项的参数来控制延迟。例如，rain -d 160 是一个不错的设置可尝试。 |
| random | 从其输入中输出随机行。 |
| robots | 射击游戏，你在其中与杀人机器人战斗。 |
| sail | 旧式海战角色扮演游戏。 |
| snake | 避开蛇的同时收集金钱。 |
| snscore | 显示 snake 的最高分。 |
| teachgammon | 双陆棋游戏的说明。 |
| tetris-bsd | 著名的俄罗斯电子游戏 Tetris。 |
| trek | 太空冒险游戏。 |

