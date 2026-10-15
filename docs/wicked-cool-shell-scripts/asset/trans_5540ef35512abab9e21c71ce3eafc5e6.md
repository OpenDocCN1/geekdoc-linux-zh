

在 © 处，是时候展示发牌结果了。最后一步是展示牌，检查花色是否匹配（如果是，我们将跳过让用户决定是否下注的提示），然后测试第三张牌是否介于前两张之间。此测试在 © 处的代码块中完成。

最后，下注结果比较棘手。如果你押注抽到的牌会在前两张牌之间并且确实如此，或者你押注它不会在之间并且确实不在，你就是赢家。否则你就输了。此结果在最终代码块中计算得出。

## 运行脚本

指定任何起始参数，游戏就会给你一个关于如何玩的简要说明。否则，你就直接开始。

让我们看一下第 12-15 节中的介绍。

## 结果

```
$ aceydeucey intro

Welcome to Acey Deucey. The goal of this game is for you to correctly guess whether the third card is going to be between the two cards I'll pull from the deck. For example, if I flip up a 5 of hearts and a jack of diamonds, you'd bet on whether the next card will have a higher rank than a 5 AND a lower rank than a jack (that is, a 6, 7, 8, 9, or 10 of any suit).

Ready? Let's go!

I've dealt:

3 of Hearts
King of Diamonds

The spread is 10. Do you think the next card will be between them? (y/n/q) y

I picked: 4 of Hearts

You bet that it would be between the two, and it is. WIN!

I've dealt:

8 of Hearts
10 of Clubs

The spread is 2. Do you think the next card will be between them? (y/n/q) n

I picked: 6 of Diamonds

You bet that it would not be between the two, and it isn't. WIN!

I've dealt:

3 of Clubs
10 of Spades

The spread is 7. Do you think the next card will be between them? (y/n/q) y

I picked: 5 of Clubs

You bet that it would be between the two, and it is. WIN!
```

I’ve dealt:
5 of Diamonds
Queen of Spades
The spread is 7. Do you think the next card will be between them? (y/n/q) q

You played 3 games and won 3 times.

第 12-15 节：玩 aceydeucey 脚本游戏

## 脚本黑客

仍然存在一个悬而未决的问题，即使用阈值 10 洗牌是否足够；这绝对是可以改进的一个方面。也不清楚显示点差（两张牌的点数差）是否有益。肯定在真正的游戏中不会这样做；玩家需要自己算出来。

再说，你也可以反其道而行之，计算在两个任意牌值之间抽到一张牌的几率。让我们想想：抽到任意一张特定牌的几率是 52 分之一。如果两张牌已经被发出去，牌堆里还剩 50 张牌，那么抽到任意一张特定牌的几率就是 50 分之一。由于花色无关紧要，任意不同点数出现的几率是 50 分之 4。因此，某个给定点差的几率是（该可能点差中的牌数 × 4）除以 50。如果发出了 5 和 10，点差为 4，因为可能的获胜牌是 6、7、8 或 9。所以获胜的几率是 4 × 4 除以 50。你明白我们的意思了吗？

最后，和所有基于命令行游戏一样，界面也可以改进。我们就留给你了。我们也会留给你一个问题：用这个方便的扑克牌函数库还能探索哪些其他游戏。

## 13

## 使用云

![](img/4ffb1cc24a1b24b49254839643abedb2_330_0.png)

过去十年中最重大的变化之一是互联网作为一种家电的兴起，最显著的是基于互联网的数据存储。起初它只是用于备份，但随着移动技术的同步兴起，基于云的存储对日常磁盘使用变得有用。使用云的应用程序包括音乐库（iTunes 的 iCloud）和文件归档（Windows 系统上的 OneDrive 和 Android 设备上的 Google Drive）。

一些系统现在完全围绕云构建。一个例子是 Google 的 Chrome 操作系统，一个完全围绕网络浏览器构建的完整工作环境。十年前，这听起来会很荒唐，但当你想到你现在花在浏览器上的时间……嗯，库比蒂诺或雷德蒙德的没人再笑得出来了。

云非常适合 shell 脚本的扩展，所以让我们开始吧。本章中的脚本主要集中在 OS X 上，但这些概念可以轻松复制到 Linux 或其他 BSD 系统上。

