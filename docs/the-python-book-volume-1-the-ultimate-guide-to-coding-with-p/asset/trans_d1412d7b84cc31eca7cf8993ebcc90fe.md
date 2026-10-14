

## 拆解

**01** 我们需要在此处从头开始指定 Python 解释器的路径。这样可以让我们在终端内或在 IDLE 之类的特定 Python IDE 之外运行程序。请注意，对于此特定脚本，我们使用的是 Python 2 而不是 Python 3，这需要在代码中指定，以确保它从系统中调用正确的版本。

**02** 我们在标准 Python 代码之上导入了两个额外的模块，以便在整个代码中使用一些额外功能。我们将使用 random 模块来确定计算机将出什么招，以及 time 模块在关键点暂停代码的运行。time 模块也可以用于利用日期和时间，要么显示它们，要么用于其他用途。

**03** 我们将每个出招设置为特定数字，以便一旦玩家在游戏中做出选择，它将被等同于该特定变量。这使得后面的代码稍微容易一些，因为我们不需要为此特定功能解析任何文本。如果你愿意，可以添加额外的出招，这将从那里开始。

```
01
#!/usr/bin/env python2

# Linux User & Developer presents: Rock, Paper, Scissors: The Video Game

02
import random
import time

03
rock = 1
paper = 2
scissors = 3

04
names = { rock: "rock", paper: "paper", scissors: "scissors" }
rules = { 1: rock, scissors: paper, paper: rock }

05

06
player_score = 0
computer_score = 0
```

**04** 在这里我们指定游戏的规则，以及代码其余部分中每个出招的文本表示。当被调用时，我们的脚本将打印出三种出招中的任何一种的名称，主要是为了告诉玩家计算机出了什么招。这些名称仅在需要时才与这些变量相等——这样，每个出招分配的数字在需要时得以保持。

**05** 与文本名称的变量定义和使用方式类似，规则也是以这样的方式完成的，即在比较结果时，我们的变量会暂时被修改。代码中更下方我们会正确解释发生了什么，但基本上在确定是否有平局后，我们会查看计算机的出招是否会输给玩家的出招。如果计算机出招等于玩家出招的输招，则获胜。

**06** 非常简单，这创建了一个变量，可以在整个代码中使用来跟踪分数。我们现在需要将其设为零，以便它存在，否则如果我们在函数中定义它，它将只存在于该函数内部。代码根据回合结果为计算机或玩家加分，尽管在此特定版本中平局游戏没有得分。

| Python 模块 |  |
|---|---|
| 你可以使用基本 Python 导入其他模块。右侧显示了一些主要模块。Python 标准自带还有许多更多模块。 | string | 执行常见的字符串操作 |
|  | datetime and calendar | 与时间相关的其他模块 |
|  | math | 高级数学函数 |
|  | json | JSON 编码器和解码器 |
|  | pydoc | 文档生成器和在线帮助系统 |

## 07

在这里我们定义了代码的实际开始部分，使用我们称之为 'start' 的函数。它很简单，向玩家打印问候语，然后启动一个 while 循环，让我们可以按我们希望的次数继续玩游戏。pass 语句允许 while 循环在我们完成后停止，并且如果需要，可以用于执行许多其他任务。如果我们停止玩游戏，则会调用 score 函数——我们将在到达那里时介绍它所做的事情。

## 08

我们保持 game 函数相当简单，以便我们可以更轻松地在代码中分解每一步。它由 start 函数调用，首先通过调用下面的 move 函数来确定玩家出招。一旦确定，它就设置计算机出招。它使用 random 模块的 randint 函数获取 1 到 3 之间的整数（1, 3）。然后它将玩家和计算机出招作为整数传递给 result 函数，我们使用它来找到结果。

```
def start():
    print "Let's play a game of Rock, Paper, Scissors."
    while game():
        pass
    scores()
```

```
def game():
    player = move()
    computer = random.randint(1, 3)
    result(player, computer)
    return play_again()
```

```
def move():
    while True:
        print
        player = raw_input("Rock = 1\nPaper = 2\nScissors = 3\nMake a move: ")
```

```
try:
    player = int(player)
    if player in (1,2,3):
        return player
except ValueError:
    pass
print "Oops! I didn't understand that. Please enter 1, 2 or 3."
```

![](img/3b256f430f51c98f1315671f6e4eec19_28_0.png)

## 09

我们通过将其放入 while 循环来开始 move 函数。move 的全部目的是从玩家那里获取 1 到 3 之间的整数，因此 while 循环允许我们应对玩家做出不受支持的输入的情况。接下来，我们将 player 变量设置为由玩家的输入通过 raw_input 创建。我们还打印了相应的说明文本。我们在文本中使用的 '\n' 添加了换行符；这样，说明会以列表形式出现。

## 10

try 语句用于清理代码并处理错误或其他异常。我们通过使用 int() 将其转换为整数来解析玩家输入的内容。我们使用 if 语句检查它是否为 1、2 或 3——如果是，move 将此值返回给 game 函数。如果它抛出 ValueError，我们使用 except 什么也不做。它打印一条错误消息，然后 while 循环重新开始。这将一直持续到做出可接受的出招为止。

