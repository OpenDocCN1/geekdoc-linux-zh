
你可以在 `HumanPlayer` 内部选择想要使用的特定集合类型。如果你将 `getSet()` 改为 `ArrayList`，项目将保持顺序。

跨 `HumanPlayer` 的库存的可读输出并不适合通过套接字发送。更完整的方案是：

### 图 3

![](img/3eaaaaf4dd2065fe8f3d6fb19ba774d3_48_0.png)

上方：当我们通过 `socket` 发送地图瓦片时，在移动端上打印玩家并不是更好。

其次，`BufferedReader.readline()` 方法一次从 `socket` 读取一次输入。正如图 3 所示，客户端将读取八行独立的输入。我们需要告诉客户端服务器已完成工作，因此在打印完消息后结束 `socket` 是一个好主意。最后，我们需要刷新 `PrintWriter()`，因为从性能角度考虑，通过 `socket` 发送大块文本比发送许多行行单独的行要好得多。调用 `PrintWriter.flush()` 方法可以确保每条消息都发送到客户端。

# 多态允许我们在相同功能的不同实现之间进行切换，并将它们相互替换

我们可以在辅助方法内部构建此功能，例如：

```java
private void endMessage() {
  server.printInput("end");
  server.flush();
}
```

下一步是设置服务器，使其能够从 `socket` 读取输入。由于服务器运行在单线程上，它似乎需要 `loadeggs` 包中的 `ConsoleInputController`，以便它能读取来自 `System` 以外的输入。将类重命名为 `StreamInputController` 并添加一个名为 `reader` 的调用字段以确保万无一失。如果提供了构造函数，在此字段中添加额外代码。添加构造函数来设置此字段的值：

```java
public StreamInputController(InputStream in) {
  reader = new BufferedReader(new InputStreamReader(in));
}
```

更改类的构造函数会破坏 `loadeggs.App` 类（即游戏版本的主类），因此我们必须修复。更改如下：

```java
ConsoleInputController = new ConsoleInputController();
StreamInputController = new ConsoleInputController(System.in);
```

最后一步是为服务器创建主类。在 `EggsServer` 中创建一个带有 `main()` 方法的类。我们使用来自 `loadeggs.App` true的模型。区别在于：

- 我们使用 `ConsoleOutput` 的 `Handler`。
- 我们使用 `StreamInputController` 来初始化 `System.in` 的输入 `socket`。

为了实现这一点，我们需要向服务器添加代码。目前，选择该端口的 `ServerSocket` 并编写代码创建它。如上一节所示，添加一行代码调用 `ServerSocket` 实例的 `accept()` 方法并返回该实例。我们使用该实例初始化服务器和 `StreamWriterController` 来处理对象。

一旦设置好服务器，我们几乎可以复制 `load eggs` 中 `main` 方法get代码。将 `ConsoleOutput` 替换为 `ServerHandler` 以初始化 `StreamInputController`。再次，多态允许我们在类的不同实现之间进行切换并将它们相互替换。

## 设置客户端

创建客户端的工作量与创建服务器一样大。然而，我们正在做相同的事情；将我们的 GUI 输入和类连接到 `socket`，而不是连接到服务器。

最后，创建一个新的客户端类并将其添加到 `loadeggs.GameInteger` 类中。该类将替换我们类中的 `StandardGameModel`。它负责监听来自 GUI 的输入命令，并通过 `socket` 将它们发送到服务器。此类类应该有一个 `PrintWriter` 类型的字段，该字段在构造函数中进行设置：

```java
public MessagePrinter(OutputStream output)
```

# Java 教程

- 重用你的代码

确保你查阅寻找可以避免重复代码的方法。例如，如果你使用提供的代码从文件读取游戏地图，你可以在翻译器中改进并使用它。你可能需要重写原始类，以抽象出可以在其他地方使用的代码。

```java
{
  out = new PrintWriter(outputStream);
}
```

或者，`MessagePrinter` 类可以继承 `MessagePrinter` 类（此处原文可能可能有误）并在其构造函数中调用父类构造函数。

`MessagePrinter` 类还应该实现 `Observer`，例如 `StandardGame` 类。这意味着它需要实现 `update()` 方法来响应来自所观察者的消息。在我们的情况下，我们将此类作为内部类，接收形式为 `move` 的消息，并在接收到它们时将这些消息直接传递给 `socket`。因此，例如 `update()` 方法可能如下：

### 图 4

```java
switch (messages.get(i).charAt(j)) {
  case '.':
    mapTiles[i][j] = new LandTile();
    break;
  case 'E':
    mapTiles[i][j] = new LandTile();
    SimpleEmptyTile(null, 0);
    break;
}

out.printMessage(message);
out.flush();
```

// `message` 是来自服务器的接收。

我们将创建的下一个类是 `ServerListener`。该类继承 `Observable` 类。它的作用是监听来自服务器的的消息，将它们封装成单独的命令发送到程序的其余部分。我们将在下一节编写此代码。`ServerListener` 类将有一个 `Socket` 类型的字段，应在其构造函数中初始化。它也将实现 Server 接口。

此循环应该负责将服务器输入封装成 `Collections`（`ArrayList` 或 `LinkedList`），然后将这些传递给观察者以便它们处理。在我们的情况下，`ServerListener` 类应该反复从 `socket` 读取消息，如果进入 "move"，它应该调用 `setChanged(true)` 和 `notifyObservers()`，以便程序的其他部分处理它。

- 跨客户端

为了显示它，不需要知道原始类是什么，创建一个空。下面的代码是 `run()` 方法，我们在线程中运行。我们将编写此方法，使其包含一个从服务器读取行的循环：

```java
public void run() {

  String serverMessage;

  while (server.readLine() != null) {

    // 执行某些操作

  }

}
```

在将其整合之前，我们将创建的最后一个组件是对于渲染非常重要的类。我们将在 `udgame.network` 中创建一个类来存储瓦片信息。该类将实现 Server 接口，其 `update()` 方法应该处理由 `ServerListener` 提供的块。

- 写客户端

在 Listener 类中添加一个 `Output` 类型的字段。在此，编写构造函数使其接受 `outputView` 作为参数并使用它设置字段。`update()` 方法应该读取由 `ServerListener` 提供的字符串集合，然后调用视图的所有所有方法。首先，我们写一个 `switch` 语句查找集合中的第一个字符串，并确定我们处理的是地图还是物品。我们需要编写代码来处理收到的消息。注意 `updateTiles()` 方法接收 `MapGrid` 对象数组，如图 3 所示，我们需要将其转换为 `MapGrid`。图 4 显示了瓦片。但是如果瓦片字符

- 下一个

### 图 5

| `@Override` |
| :--- |
| `public void displayMapTiles(MapTile[] grid)` |
| `Platform.runLater(() -> {` |
| `MapView mapArea = gui.getMapArea();` |
| `mapArea.displayMapGrid(grid);` |
| `});` |
| `});` |

# 对象流

使用 `ObjectInputStream` 和 `ObjectOutputStream` 类，我们可以通过 `socket` 发送对象而不是文本。你可以轻松地通过 `socket` 发送对象。

```java
ObjectInputStream in = new ObjectInputStream(socket);

ObjectOutputStream out = new ObjectOutputStream(socket);
```
