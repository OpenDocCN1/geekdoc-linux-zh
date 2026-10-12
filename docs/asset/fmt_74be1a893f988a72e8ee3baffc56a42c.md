
## ActionsWidget

ActionsWidget 渲染了两个 Material 设计的悬浮操作按钮 (FAB)，让用户可以通过点击相应的按钮阅读示例和或购买书籍。这些按钮是使用 `FloatingActionButton`（`ActionButton` 类）组件实现的。点击每个按钮将启动由 Books API 为给定书籍提供的 URL。启动 URL 使用了 `url_launcher` 插件 (`url_launcher`)。在本文写作时，`url_launcher` 的当前版本为 `'5.4.11'`。请在 `pubspec.yaml` 的 `dependencies` 部分下添加此依赖项。

```yaml
# 以从 BookDetailsPage 打开网页阅读链接和购买链接

url_launcher: ^5.4.11
```

ActionsWidget 位于 `BookDetailsPage` 中 `InformationWidget` 下方。ActionsWidget 顶部有一个 `Padding` 组件。该 `Padding` 组件包含一个 `Row` 组件。该 `Row` 组件水平方向对齐其子组件。该 `Row` 组件具有两个 `FloatingActionButton` 类型或带有扩展变体的 FAB 的子组件。`FloatingActionButton.extended()` 方法允许 FAB 变得更大，并包含图标和标签。`onPressed` 包含了启动 FAB URL 的实现。请参考图 15.4 查看 ActionsWidget 布局的视觉表示。

![](img/ffb84d2e382861a17088a545dbd2b0c6_264_0.png)

### 图 15.4 ActionsWidget 剖析

让我们来看 ActionsWidget 的代码实现：

```dart
class ActionsWidget extends StatelessWidget {
  final BookModel book;
  const ActionsWidget({Key key, this.book}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(8.0),
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: [
          book.accessInfo.webReaderLink == null
            ? FloatingActionButton.extended(
                label: Text("Read"),
                heroTag: "webReaderLink",
                onPressed: () => launch(book.accessInfo.webReaderLink))
            : Container(),
          book.saleInfo.saleability == "FOR_SALE"
            ? FloatingActionButton.extended(
                label: Text("Buy"),
                heroTag: "buy_book",
                onPressed: () => launch(book.saleInfo.buyLink))
            : Container(),
        ]
      ));
  }
}
```

## 第二页 – BookDetailsPage

### DescriptionWidget

`description widget` 是一个简单的组件，用于在 `Text` 组件中渲染书籍描述。这个组件并不需要单独成一个组件。然而，为了保持简单，我将其提取出来。这里是 `DescriptionWidget`：

```dart
class DescriptionWidget extends StatelessWidget {
  final BookModel book;
  const DescriptionWidget({Key key, this.book}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return book.volumeInfo.description != null
      ? Text(book.volumeInfo.description)
      : Container();
  }
}
```

# 252

# 实用 Flutter

![](img/ffb84d2e382861a17088a545dbd2b0c6_268_0.png)

图 16.1 原生实现中 CounterApp 剖析

在每次点击时增加计数器。此应用中总共有七个小组件：

- 1. `Scaffold`: 根小组件。
- 2. `AppBar`: 显示应用标题。
- 3. `Center`: 将子组件对齐在屏幕中心。
- 4. `FloatingActionButton`: 用于增加计数器的悬浮按钮 (FAB)。
- 5. `Column`: 垂直对齐子组件。
- 6. `Text`: 显示信息文本。
- 7. `Text`: 显示更新后的计数器数字。

请参考图 16.1 查看应用小组件的视觉结构。

# 原生模式 (VANILLA PATTERN)

此示例是展示本地状态管理的经典案例。该应用内置了本地状态管理。我们将使用不同的状态管理方法，通过此示例来增加计数器并显示其值。目标是介绍各种状态管理解决方案，并在实现相同目的的同时理解不同方法之间的实现差异。在本章中，我们将关注不带任何额外修饰的基础或“原生”实现。

让我们从 `CounterApp` 自带的默认内置状态管理解决方案开始。它使用 `StatefulWidget` 结合 `setState()` 方法在特定时刻更新并反映小组件的状态。让我们查看下面的应用代码：

# 状态管理简介

```dart
import 'package:flutter/material.dart';
```

```dart
void main() {
  runApp(CounterApp());
}
```

```dart
class CounterApp extends StatelessWidget {
  // 这个小组件是你的应用程序根。
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(title: 'CounterApp (Vanilla)'),
    );
  }
}
```

```dart
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
  final String title;
  @override
  _MyHomePageState createState() => _MyHomePageState();
}
```

```dart
class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;
  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }
  @override
  Widget build(BuildContext context) {
    print("Building _MyHomePageState
```

```dart
//Widget#5
child: Column (
  mainAxisAlignment: MainAxisAlignment.center,
  children: <Widget>[
    //Widget#6
    Text (
```
