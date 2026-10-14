

Save before running the program, or anything you've done since you last saved won't be interpreted

![](img/3b256f430f51c98f1315671f6e4eec19_155_0.png)

## 07 修复一个小问题

我们当前使用的 Debian 镜像在 Geany 中存在一个小的配置问题。你可以通过按 F5 键运行程序或进入 Build 菜单并选择 Execute 来判断是否遇到此问题。如果存在该问题，则不会发生任何事情，并且你会看到一条消息提示 'Could not find terminal: xterm'。不用担心，很容易修复。进入 Edit 菜单，然后选择 Preferences。进入 Tools 选项卡，将 Terminal 的值从 xterm 改为 lxterminal。

![](img/3b256f430f51c98f1315671f6e4eec19_155_1.png)

## 08 测试我们的程序

现在我们完成了这部分，为什么不测试一下呢？值得注意的是，你必须在运行程序之前保存，否则自上次保存以来所做的任何更改都不会被 Python 解析。通过按 F5 键运行程序。输入你的名字，输入后按 Enter 键。完成后，你会看到一条欢迎消息。如果程序以代码 0 退出，则表示一切运行成功。按 Enter 关闭终端。

## 09 处理数字

我们将通过基本重复前面几行代码的方式向用户请求一个数字。一旦用户给出数字，我们将对其进行二分、平方和加倍。raw_input 函数返回用户输入的值作为字符串。字符串是基于文本的值，因此我们无法对其执行算术运算。Python 中的 integer 类型只能存储整数，而 decimal 类型可以存储带小数点的数字。我们将执行一种称为类型转换的操作，它基本上是将一种类型的值转换为另一种类型。我们将把数字字符串转换为 decimal 值，因为如果我们要对数字进行二分，很可能会涉及小数。如果数字是 integer 类型，任何小数部分都将被简单地截断，而不会进行四舍五入。这称为截断。

```
numberHalved = number / 2
numberDoubled = number * 2
numberSquared = number * number
```

## 10 执行算术运算

Python 中的主要算术运算符是 + - * /，后两者分别表示除法和乘法。我们创建了三个新变量，名为 numberHalved、numberDoubled 和 numberSquared。请注意，我们不需要指定它们应为 decimal，因为 Python 会根据其初始值的类型为变量赋予类型。number 变量是 decimal 类型，因此对该数字执行算术运算返回的所有值也将是 decimal 类型。

```
# Print out the values we just worked on
# to a string
print("The result of halving that number")
print("The result of doubling that number")
print("The result of squaring that number")
print("")
```

## 11 打印我们的数字

现在我们已经执行了算术运算，我们需要使用 print 函数打印结果。print 函数只接受传递给它的字符串值。这意味着在打印之前，我们需要使用 str() 函数将每个 decimal 值转换为字符串。我们使用引号之间没有任何内容的 print 语句来打印一个空行。这之所以有效，是因为 print 函数在输出末尾总是添加一个新行，除非另有说明，因此打印空字符串只会打印一个新行。

print 函数只接受字符串值，因此将每个 decimal 值转换为字符串

```
# ask the user for a number and square it, double it
number = raw_input("Please enter a number: ")
```

## Program Minecraft Pi

学习如何开始使用 Minecraft Pi，这是一款在 Raspberry Pi 上学习 Python 编程的绝佳工具...

Minecraft 是一款革命性的沙盒游戏，玩家仅被称为 Steve，需要在比地球还大的巨大方块 3D 世界中生存和繁荣。世界的每个一米段都由一个方块表示。该方块可能是众多物品中的任何一个，并且你挖得越深，物品可能越稀有。你的挑战是挖掘、建造并在利用你发现的物品的同时对抗夜间怪物的军队。

Minecraft Pi 去除了游戏的生存元素，让你处于一种乐高建造模式，你拥有游戏中许多物品的无限供应，并且可以自由地用它们建造。Minecraft Pi 也是 Minecraft 的唯一版本，Minecraft 可在几乎所有流通的游戏平台上使用，而该版本积极鼓励玩家使用简单的应用程序编程接口 API 来破解世界。在本教程中，我们将学习基础知识...

## 01 安装 Minecraft Pi

你首先需要在 Raspberry Pi 上安装 Minecraft Pi —— 你可以在 bit.ly/1mgAJ7S 在线找到我们完整的安装指南。如果你知道如何处理 tar 包并且不需要逐步说明，你只需要下载以下文件并将其解压到你的主文件夹中：bit.ly/1pjZ17Z。

## 02 你必须启动 X

在 Pi 上进行编码和玩 Minecraft 时，你需要牢记一些事情。很多人似乎都被游戏无法从命令行运行的事实所困扰。假设你没有将 Pi 设置为这样，你必须使用 startx 启动桌面环境。从终端启动游戏，方法是进入 mcpi 文件夹并输入：

```
./minecraft-pi
```

![](img/3b256f430f51c98f1315671f6e4eec19_157_0.png)

