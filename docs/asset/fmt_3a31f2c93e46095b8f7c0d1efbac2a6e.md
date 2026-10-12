
# 实战 Flutter

## Source Code Online

此示例（Flutter App Structure: App 剖#2）的源代码可以在 GitHub 上找到。

## Managing State with StatefulWidget

我们希望通过点击微笑表情悬浮按钮来更改问候语。首先，我们需要将所有问候语存储在一个列表中。其次，我们需要启用悬浮按钮，使其能够从列表中选取下一个可用字符串。

我们需要 `StatefulWidget` 来跟踪所选问候语的当前状态。让我们创建一个 `StatefulWidget`，比如 `MyHomePage`。该 widget 被分配为 `MaterialApp` 的 `home` 属性。

```dart
class HelloBooksApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyHomePage(title: 'Hello Books'),
    );
  }
}
```

### StatefulWidget: MyHomePage

当屏幕的一部分需要用新信息更新时，`Stateful widgets` 是非常有用的。在我们的应用中，我们希望在更新问候文本的同时，保持屏幕的其他部分不变。`MyHomePage` 扩展了 `StatefulWidget` 并接受一个参数。该 widget 拥有可变状态，并使用类 `_MyPageState` 表示。

```dart
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
  final String title;
  @override
  _MyPageState createState() => _MyPageState();
}

class _MyPageState extends State<MyHomePage> {
```

### State Widget: MyPageState

每当从 `setState` 方法请求状态更改时，widget 就会重新构建。

每当从 `setState` 方法 方法请求状态更改时，widget 就会重新构建。让我们看看在 `HelloBooksApp` 中是如何实现的。当用户点击 `FloatingActionButton` 时，它会更新屏幕上当前选中的问候语。

```dart
class _MyPageState extends State<MyHomePage> {
  int index = 0;
  final List<String> greetings = [
    'Hello Books',
    'Hola Libros',
    'Ciao Libri',
    'हिंदी किताब',
  ];

  void updateGreeting() {
    setState(() {
      index = greetings.length - 1 ? 0 : index + 1;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
```

```dart
class HelloBooksApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          title: Text('Hello Books'),
        ),
        body: Center(
          child: Text(
            'Hello Books',
            style: Theme.of(context).textTheme.headline4,
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {},
          tooltip: 'Greeting',
          child: Icon(Icons.insert_emoticon),
        ),
      )
    );
  }
}
```

## COMPLETE CODE

```dart
void main() {
  runApp(HelloBooksApp());
}
```

```dart
style: Theme.of(context).textTheme.headline4,
),
),
floatingActionButton: FloatingActionButton(
onPressed: () {},
tooltip: 'Greeting',
child: Icon(Icons.insert_emoticon),
),
)
);
}
}
```
