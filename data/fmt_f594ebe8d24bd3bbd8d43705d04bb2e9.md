
我们现在可以测试我们所做的一切。由于我们没有更改任何用于显示的代码，可以使用它，但要使用上一个问题中提到的 tel 客户端。运行服务器的一个实例并打开两个终端。在其中一个，运行命令：

```
$ tel localhost 9009
```

www.linuxusker.com 49

## Java 教程

![](img/84ab224de9f66d5fe3638204a9a78c1c_49_0.png)

图 2

两个玩家都从同一个方格开始。如果玩家 I 移动，玩家 II 仍然会看到屏幕

（如果你使用了不同的操作系统，请链链端口。在其中一个终端中，运行 `move` 命令，然后运行 `search` 命令并按回车。然后，我们将字母 `O` 直接设置在当前玩家的左侧，这样对立玩家就在另一个终端中运行。）

下一步是设置客户端以读取地图，并通过在地图上放置玩家来与之交互。客户端上的 `ServerOutput` 类使用 `AnimalDecoder.decodeTile` 方法将字符转换为 `Map` 对象。在此方法中添加一些代码，如果字符为 `O`，则向地图上添加一个玩家。然后，我们可以使用以下代码向瓦片中添加玩家：

```
tile.getPlayersTile().add(new Player(I));
```

最后，我们需要确保 GUI 本身能够显示地图上的玩家。`GUIOutputView` 类使用 `MapGrid` 类来显示地图瓦片和其他元素。为了有一种在地图上显示玩家的方法，打开样式表 `src/main/resources/styles/map.css` 并创建一个名为 `opponent` 的新 ID。如果你愿意，可以复制并粘贴玩家 ID 的代码并重命名为 `opponent`，尽管你可能想将 `background-image` 属性更改为 `main_green_33pg.jpg`（随光盘提供），这样我们就可以从当前玩家创建对手。现在，我们可以使用以下代码创建一个带有对手图像的新瓦片：

```
new Map("Opponent")
```

（如果你使用的是提供的代码以前一个版本代码，这可能会有所不同。）查看 `MapGrid.displayMapTile`，在地图上显示蛋瓦片的技术是在地图上相应的方格上显示玩家。你可以使用以下表达式检查瓦片是否有玩家：

```
tile.getPlayersTile().isEmpty()
```

![](img/84ab224de9f66d5fe3638204a9a78c1c_49_1.png)

图 3

由于玩家 I 已经移动，他的客户端通过显示更新后的地图做出响应。当玩家移动时，不要忘记移除对手瓦片。如果我们现在运行游戏，我们应该能够在地图上看到其他玩家。

在图 2 中，我们看到了玩家 I 开始游戏的位置。在图 2 中，玩家 I 已移动到方格，似乎 II 仍然看到图 2 中的视图。在这里，GUI 只有在玩家按下按键时才会响应。

## 处理迭代

当你编写 `nextPlayerTiles()` 方法时，你需要从特定的瓦片返回下一个玩家。如果你这样这样做，我们最终将得到两个循环：一个遍历瓦片，一个遍历玩家。这将产生两个效果：它将清理我们的代码，并且我们避免了执行相同任务的嵌套循环。在 Java 中实现此点的方法是编写一个 `Iterator` 接口的实现。迭代器有两个方法：`hasNext()`，如果存在另一个元素则返回 `true`；以及 `next()`，返回迭代中的下一个元素或 `null`。

如果我们有一个 `Iterator`，就可以用它执行迭代：`forEach()`，在 Lambda 表达式或方法引用中使用将其应用于迭代的每个元素。

我们可以在 `Player` 抽象类中添加一个（具体的）方法：

```java
public void notifyChange() {        setChanged();
    notifyObservers();
}
```

我们需要第二个更改是将 `GameModel` 观察者作为 `Player` 实例添加。在 `EggServer` 方法中添加该行：

- `player.addObserver(gameModel);`

- `GameModel` 和 `player` 对象已经创建。现在当我们调用 `notifyChange()` 时，它将导致游戏模型返回列表。

现在我们已经准备好，我们需要进入 `StandardGame` 类并修改该方法，每当移动或拾取命令时，程序化位于可见范围内的玩家并调用 `notifyChange()`。

```java
public void notifyOtherPlayers() {
    for (int i = 0; i < players.size(); i++) {
        if (players.get(i) != this) {
            players.get(i).notifyChange();
        }
    }
}
```

启动服务器实例，然后启动实例和其中一个玩家的实例。

## 图 4

![](img/84ab224de9f66d5fe3638204a9a78c1c_50_0.png)

幸运！当玩家按下按钮时，GUI 做出了响应。当只有 I 向南移动时，I 出现在他/她的新位置。这是一个更严肃的应用，那么当一个玩家移动时，它可以通知地图上的每个玩家。

`Player` 对象的集合使我们很容易找到足够近的玩家，以通知所有玩家原始瓦片和他们移动到的瓦片。为了对所有这些玩家进行搜索，我们需要访问 `GameModel`。

一种方法是添加对 `GameModel` 接口的引用，允许 `Player` 类调用 `GameModel` 的方法。如果两个类互相引用，是设计糟糕的标志。这破坏了我们的设计，`Player` 作为一个抽象类不应该知道底层的 `GameModel`。这在 `GameModel` 和 `Player` 之间创建了双向依赖，这是一个糟糕的设计。

有一个更优雅的解决方案，而且很容易实现。例如，如果我们在 `GameModel` 类中创建一个接口并让 `Player` 类实现它，并在接口中添加一个方法。那么当 `GameModel` 检测到它需要重新加载游戏时，它会通知其观察者。

由于接口不允许扩展类，我们需要将 `Player` 接口更改为抽象类以便扩展 `Observable` 类，这意味着 `Player` 类中的所有方法都需要 `abstract` 关键字，并且我们需要更改 `HumanPlayer` 类，使其扩展而不是实现我们在这里做的 `Player` 类。

## 图 5

| Refactor | Navigator | Search | Project Window | Help |

|---|---|---|---|---|

| Debug Type Hierarchy (1) [Application] | | | | |

| EggServer (1) Debugging EggServer at localhost:8080 | | | | |

| Thread (main) | | | | |

| Thread (1) [Suspended] only at method in egg.StandardGameModel | | | | |

| Thread (2) [Stopped] only at method in egg.StandardGameModel | | | | |

| StandardGameModel.java:line 67 | | | | |

| StandardGameModel.java:line 166 | | | | |

| StandardGameModel.update:line 233 | | | | |

| StandardGameModel.update(Object):line 233 | | | | |

Eclipse 中的调试面板允许我们通过点击方法名在挂起的线程之间切换。如果你在其他玩家的周围移动，太棒了！现在是调试你的代码以找出它为什么不起工作了。

## 修复同步错误

在这一点，我们拥有了一个运行良好的游戏，尽管似乎还有很多工作要做。并发是一个微妙的领域，而且很难今天就修复所有的错误。

www.luxuker.com 

## Java 教程

## 死锁

同步可以消除错误，但也可以引起错误。如果你尝试同步整个方法，可能会导致程序死锁。通过使用 `Hashtable`，一个线程调用同步方法，然后调用另一个。但如果另一个线程也在移动，那么它们都启动了，这意味着哪个都无法运行（图 7）。

同步中常见的错误来源是同步错误。例如，在以下代码中（while 循环）：

```java
while (true) {
    if (it.hasNext()) {
        Egg e = it.next();
        // process egg
    }
}
```

如果两个线程访问相同的数据，它们将得到 `ConcurrentModificationException`。我们需要使用 Java 虚拟机来处理此：该方法是

（此处应有图 7 的图片）

上述我们使用 Eclipse 中的调试面板来检测共享数据何时变化。并发是一个微妙的主题，很难一眼看到程序中所有的错误。

## 在调试器内部模拟 bug

为了让自己相信同步问题是一个 bug，你可能需要亲手发现它。首先，在重置开始时，调用 `Map` 类中的 `reset()`，然后启动两个线程。在正常模型下，两个玩家都会出现在地图上。当两个玩家都站立时，按下其中一个玩家的“向上”键，这应该触发我们的断点。

在 Eclipse 中点击“Step over”（单步跳过）来执行第一行代码。如果发生异常，点击客户端并再次按下“向上”键。切换到第二个客户端，对该线程也点击“Step over”，直到到达断点。

效果将是两个玩家都捡起了蛋，如图 1 所示。

在另一次同步后，情况也是一样的。`SampleGame()` 中方法的关键在于，此时将抛出异常，因为我们执行了两个同步方法的非法交替执行。当我们正常运行时，我们就可以确定自己免受此类同步问题的困扰。

线程可能会抛出 `InterruptedException`，因此我们需要处理它。调用 `Thread.sleep()` 应该始终放在 `try` 块中，否则将非常容易添加一个新的 `catch` 块来处理异常。

在这种情况下，错误代码的左侧会出现一个红标记。点击此标记并添加一个 `catch` 子句将代码封装在 `try` 块中即可处理 `InterruptedException`。

如果我们重复实验，会注意到游戏移动变慢了，而且游戏对另一个玩家再次有响应。然而，如果我们用 Ctrl+C 杀死客户端，玩家仍然会出现在地图上。这是因为即使只有几毫秒，客户端仍在向套接字推送更多命令。在我们睡眠时，忽略所有命令更合逻辑。

```
while (reader.ready()) {
  reader.readLine();
}
```

注意，这会导致客户端显示新内容。原因是当我们按下按钮时，客户端会发送：向被按下的按钮发送移动或捡取命令、向重绘地图发送搜索命令，以及发送刷新界面的库存命令。在我们做的更改下，这些操作中只有第一个会在服务器上执行。

解决此问题的变方法是在 `Player` 类的 `notifyChanges()` 方法中、在搜索命令之后立即添加对库存的调用。由于库存只在我们执行的操作中发生变化，每当他们移动或执行命令时，我们必须使用服务器将库存发送给客户端。

## 处理中途退出的玩家

如果在游戏过程中关闭会话，玩家消失后，相应的玩家仍然出现在地图上。我们可以为 `GameModel` 添加一个新方法 `leave()`。该方法的实现位于：

![](img/84ab224de9f66d5fe3638204a9a78c1c_52_0.png)

![](img/84ab224de9f66d5fe3638204a9a78c1c_52_1.png)

在 Eclipse 中向现有代码添加一个新的 `catch` 子句很快。

`StandardGameModel` 将使用 `getMap().removePlayer()` 将玩家从地图中移除。我们需要修改 `StandardGameModel` 类中的代码，使 `executeCommand()` 方法在接收到 `leave` 命令时调用 `leave()` 方法。我们应该确保收到的 `notifyInventoryPlayer()` 方法会将离开的玩家从玩家地图上移除。

一旦我们实现了 `leave` 命令，我们需要确保停止从该玩家的客户端程序接收输入。我们可以通过在 `InputController` 类内部的 `try` 语句中添加一个 `finally` 子句来实现：

```
setChanged();
notifyObservers("leave");
```

同步会导致两个人都捡起同一个蛋，这可不……

如果我们然后运行客户端，它会正常关闭，或者抛出异常……

## TensorFlow 功能

![](img/84ab224de9f66d5fe3638204a9a78c1c_53_0.png)

## 使用 TENSORFLOW 构建智能项目

Joey Bernard 演示了如何为你自己的软件开发项目添加前沿的机器智能。

Google 在机器学习能力方面投入了大量的开发者时间和精力。这项工作已应用于公司的人工智能应用。由 Brain 团队开发的工具之一最初是为机器学习和神经网络应用设计的，但它使用通用语言编写，允许许多其他机器智能应用。TensorFlow 被编写成一个 API 层，以 Python 模块的形式提供。低级 API 和其他 API 构建在此层之上，使常见的编程任务变得更简单，而 TensorFlow 层提供了所有功能。TensorFlow 的张量（tensor）部分描述了所使用的数据结构，即张量。在这种情况下，张量被定义为任意维度的元素数组，其中形状（shape）是定义每个维度大小的列表。TensorFlow 的流（flow）部分是计算部分。

常量节点（constant node）不接受输入并返回单个张量。你可以使用下面的代码创建节点。

```
import tensorflow as tf
node_a = tf.constant(6)
node_b = tf.constant(?)
```

使用 TensorFlow 进行计算需要两个步骤。第一步是创建图，我们已经做了。第二步是运行图和所需的处理。这由名为 session（会）的对象处理。下面的示例作为一个基本的会运行图：

```
session_a = tf.Session()
print(session_a.run(node_a, node_b))
```

常量节点返回其内容，因此当你运行会时，你会得到值 7 并打印出来。这本身并没有那么用。我们可能想对这些张量应用操作，而这些操作也被定义为节点。有很多内置操作可用。通过下面的代码，你将找到生活的答案：

```
node_ans = tf.multiply(node_a, node_b)
print(session_a.run(node_ans,node_ans))
```

这将打印答案 42。节点可以在非常复杂的集合中连接以执行任何需要。这就是为什么 TensorFlow 成为机器学习应用程序的标准工具包。

有许多不同类型可以用于各种计算。TensorFlow 使用计算图，其中节点是计算步骤。有许多不同类型可以用于各种计算。你可以创建非常复杂的计算图来处理数据流。通常情况下，节点接受零或

![](img/84ab224de9f66d5fe3638204a9a78c1c_53_0.png)

（注：提供的 OCR 文本包含大量的重复/重叠部分。我已将唯一内容合并到下面的逻辑流中。）

你之前创建的（内容内容），以及在训练中使用的许多步骤。通过这种方式，你可以将编写这些估算器所花费的所有程序员时间转化为你的优势。我们编写了一些关于如何运行估算器以跨多个节点或使用 GPU 的最佳实践。

我们到为止所看到的许多函数在你需要时并没有以预期的形式可用。某些情况下，你可能对线程有更多控制。在这些情况下，TensorFlow 包含了可以并行执行的队列（Queue）。有几种内置队列可用，例如随机洗牌队列。下面的示例显示了它的样子：

```python
min_after_dequeue=int(0.9),
shapes=shape.shape, dtypes=shape.dtype
```

## 快速提示

安装修复取决于你尝试安装 TensorFlow 的位置，你可能无法轻松地安装它。在某些情况下，提供了包含所有所需内容的 Docker 镜像。

上述，source 是一个正在处理的输入数据对象。然后你需要创建一个运算符来逐个入队：

- `enqueue = queue.enqueue(source)`

通过此，你可以创建一个队列运行器，它将启动线程并从下面的代码中读取：

一旦创建了 Queue 对象，你就需要注册它，以便 TensorFlow 知道

```python
num_threads = 4
queue_runner = tf.train.QueueRunner(queue,[enqueue]=num_threads)
```

```python
queue = tf.RandomShuffleQueue(capacity=capacity,
```

## 如何操作

## 安装 TensorFlow

```bash
$ bernard@localhost:~$ virtualenv --system-packages venv
$ source venv/bin/activate
Installing TensorFlow...
$ pip install --upgrade pip
Installing Pip...
$ pip install tensorflow
Installing TensorFlow... 
$ bernard@localhost:~$ $
```

### 01 创建虚拟环境

推荐的第一步是创建一个虚拟环境，你可以在可以在其中安装 TensorFlow，而不会受到其他 Python 模块的干扰：

### 03 更新 pip

要安装 TensorFlow，你需要一个非常新的 pip 版本。你可以通过以下命令来确认：
