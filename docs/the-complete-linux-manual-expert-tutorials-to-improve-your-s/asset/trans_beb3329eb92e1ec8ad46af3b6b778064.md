

## sinclair
## 48K ZX Spectrum
## The Hobbit

THE HOBBIT 是一款开创性的超级程序，是计算机软件的里程碑。你将在文字和图形中面对危险、激情和冒险。遇见《霍比特人》中的所有角色，并用普通英语与他们交谈！THE HOBBIT 程序带给你未来，带来激动人心且富有挑战性的幻想！

## MELBOURNE HOUSE

霍比特人，1982 年的先进编程杰作。

## Common Coding Mistakes

当你开始做新事物时，你不可避免地会犯错误，这纯粹是由于缺乏经验，而这些错误本身就是很好的老师。然而，即使是专家也会偶尔出现失误。关键在于，尽可能从中吸取教训。

## X=MISTAKE, PRINT Y

程序员需要注意的陷阱有很多，太多无法在此全部列出。能够识别错误并修复它，是你开始进入更高级领域并成为更好的编码者的标志。每个人都会犯错，即使是有三十多年经验的编码者也是如此。从这些基本、常见的错误中学习有助于建立更好的编码基础。

## SMALL CHUNKS

能够像《黑客帝国》电影中的尼奥那样工作真是太好了。只需询问，你的操作员就会将其加载到你的记忆中，你瞬间就能掌握该主题的一切。可惜的是，我们做不到。第一个主要陷阱是有人试图学得太多、太快。所以请以小块的方式学习编码，慢慢来。

![](img/f80199d101da92d953f18eaa6205b48e_143_0.png)

## EASY VARIABLES

对变量进行有意义的命名是消除常见编码错误的关键。字母表中的字母是可以的，但当代码指出 x 变量有问题时会发生什么。给变量命名为 lives、money、player1 等等并不困难。

```
1 var points = 1023;
2 var lives = 3;
3 var totalTime = 45;
4 write("Points: " +points);
5 write("Lives: " +lives);
6 write("Total Time: " +totalTime+ " secs");
7 write("----------------");
8 var totalScore = 0;
9 write("Your total Score is: " +totalScore);
```

## //COMMENTS

使用注释。这是一个简单的概念，但在你下次查看代码时，注释可以节省很多问题。插入注释行可以帮助你快速筛选出导致问题的代码段；如果需要回顾旧代码也很有用。

```
53 orig += 2;
54 target += 2;
55 --h;
56 #endif
57 if (n == 0)
58 return;
59
60 //
61 // Loop unrolling.
62
63
64 // (n & (-3)) is the greatest multiple of 8 r
65 // In the while loop ahead, orig will move ov
66 // increments (4 elements of 2 bytes).
67 // end marks our barrier for not falling outs
68 char const * const end = orig + 2 * (n & (-3))
69
70 // See if we’re aligned for writing in 64 or
71 #if ACE_SIZEOF_LONG == 8 &&
72 //((defined( __amd64__) || defined( __x86_64
```

## PLAN AHEAD

早上醒来决定编写一个经典的文字冒险游戏固然很棒，但如果没有一个好的计划，这并不总是切实可行的。无需太多思考和计划就可以编写小的代码片段，但更长、更深入的代码需要一个良好的工作计划来坚持并帮助消除错误。

![](img/f80199d101da92d953f18eaa6205b48e_143_1.png)

![](img/f80199d101da92d953f18eaa6205b48e_143_2.png)

## USER ERROR

用户输入往往是代码中令人瘫痪的错误。例如，当用户应该输入年龄的数字时，却用字母输入。通常用户可以输入大量内容到输入中，导致某些内部缓冲区溢出，从而导致代码崩溃。注意那些用户输入，并清楚地说明他们需要什么。

```
Enter an integer number
aswdadf
You have entered wrong input
5
You have entered wrong input
f"t"!"!
You have entered wrong input
sdfsf121213123
You have entered wrong input
12342342342342324
You have entered wrong input
12
the number is: 12

Process returned 0 (0x0)   execution time : 21.495 s
Press any key to continue.
```

## BACKUPS

始终备份你的工作，并为你所做的任何更改做二次备份。如果有良好的备份可以恢复，那么错误是可以纠正的，尤其是在出现问题时。继续从你离开的地方开始，要比从头开始容易得多。

![](img/f80199d101da92d953f18eaa6205b48e_144_0.png)

## RE-INVENTING WHEELS

你很容易花费数天时间试图弄清楚一段代码以实现给定结果，这令人沮丧且通常浪费时间。虽然自己解决问题同样令人满意，但通常同样的代码在互联网上的某个地方已经存在。不要试图重新发明轮子，看看是否有人已经先做了。

![](img/f80199d101da92d953f18eaa6205b48e_144_1.png)

## SECURE DATA

如果你编写代码来处理用户名和密码或其他敏感数据，那么请确保数据不是明文。学习如何创建函数来加密敏感数据，然后再将其输入到可能传输或存储它的例程中，以免有人能够查看它。

![](img/f80199d101da92d953f18eaa6205b48e_144_2.png)

## HELP!

寻求帮助是大多数人在过去挣扎过的事情。我们询问的人会嘲笑我们吗？我是在浪费大家的时间吗？有人默默忍受是一个常见的错误。然而，只要你以正确的方式提问，遵守任何论坛规则并保持礼貌，那么你的问题就不是愚蠢的。

![](img/f80199d101da92d953f18eaa6205b48e_144_3.png)

## MATHS

如果你的代码进行多次计算，那么你需要确保其背后的数学是正确的。有成千上万的实例，程序因糟糕的数学编码而提供不正确的数据，这可能产生灾难性的后果，具体取决于代码的用途。总之，请仔细检查你的代码方程。

```
set function v2
set output
max = 5
min = 0

comp = (x, y) = (x, y) + (0, 1)
... [code snippet]
```

## Master Your Tech From Beginner to Expert

要继续了解更多关于你的技术，请访问我们：

www.bdmpublications.com

## FREE Tech Guides

Apple iPhone, iPad, Mac, MacBook & Watch

PC & Windows 10

Samsung & Android

Photography, Photoshop & Lightroom

Coding Python, Raspberry Pi & Linux

## EXCLUSIVE Offers on our Tech Guidebooks

- Print & digital editions
- Featuring the very latest updates
- Step-by-step tutorials and guides
- Created by BDM experts

今天就查看我们的最新标题！

## ultimate photoshop

bdmpublications.com/ultimate-photoshop

购买我们的 Photoshop 指南并免费下载教程图片！只需注册即可发挥创意。

## PLUS SPECIAL DEALS and Bonus Content

订阅我们的月度新闻通讯，获取 BDM 的最新更新、优惠和新闻。我们在这里帮助你掌握你的技术！

## Discover more of our guides today...

![](img/f80199d101da92d953f18eaa6205b48e_146_0.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_1.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_2.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_3.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_4.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_5.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_6.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_7.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_8.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_9.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_10.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_11.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_12.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_13.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_14.png)

![](img/f80199d101da92d953f18eaa6205b48e_146_15.png)

