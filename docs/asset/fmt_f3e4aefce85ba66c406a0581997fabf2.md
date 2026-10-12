
```dart
void increment() => number++;
void decrement() => number--;
```

```dart
class _MyPageState extends State<MyHomePage> {
  Counter _counter = Counter();
```

```dart
void _increment() {
  setState(() {
    _counter.increment();
  });
}
```

```dart
void _decrement() {
  setState(() {
    _counter.decrement();
  });
}
```

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <
          Text(
            'Counter: ${_counter.number}',
            style: Theme.of(context).textTheme.headline3,
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <
              ElevatedButton(
                key: Key('decrement'),
                onPressed: _decrement,
                child: Icon(Icons.remove),
              ),
              ElevatedButton(
                key: Key('increment'),
                onPressed: _increment,
                child: Icon(Icons.add),
              ),
            ],
          ),
        ],
      ),
    );
  }
}
```

```dart
class MyTextWidget extends StatelessWidget {
  final String textString;
  final TextStyle style;
  final Key myKey;

  const MyTextWidget({this.myKey, this.textString, this.style});

  @override
  Widget build(BuildContext context) {
    // 需要指定方向性，因为这个 widget
    // 将独立进行测试。
    return Text(
      textString,
      style: style,
      textDirection: TextDirection.ltr,
      key: myKey,
    );
  }
}
```

# 集成测试

当 `Text` 是 `Scaffold` 的子组件时，你不需要在 `Text` 中指定 `textDirection`，因为在这种情况下它是隐式提供的。

# 测试对文件

测试对有两个文件，它们位于 `test_driver` 目录中。该目录位于 Flutter 项目的根目录下。

# 插桩应用

第一个文件创建在 `test_driver/` 目录下。你可以随意命名。我认为它应该与本章的名字一致：`test_driver/main_22.dart`。该文件是 API 的插桩版本，并有助于将性能分析等插桩信息记录到集成测试套件中。该文件的内容如下：

```dart
//插桩 CounterApp
import 'package:flutter_driver/driver_extension.dart';
import '../lib/chapter22/main_22.dart' as app;

void main() {
  EnableDriverExtension();
  app.main();
}
```

# 测试套件

第二个文件也存在于同一个目录 `test_driver/`。它的名称与插桩文件相同，后缀为 `_test`。因此，集成测试套件将位于 `test_driver/main_22_test.dart` 文件。

# 编写集成测试

在本节中，我们将编写测试来测试应用的功能和用户界面交互。编写集成测试套件有三个部分。

# 集成测试 311

## 测试套件 (TEST SUITE)

多个集成测试可以根据其相关性分组。在本节中，我们将创建一个组来测试 `CounterApp` 中的递增和减少功能。

```dart
void main() {
  group('关于测试套件的描述', () {
    // 测试用例在这里
  });
}
```

## 设置 (Setting Up)

在此测试中，我们将通过点击按钮来增减数字，并验证屏幕上的数字。我们使用 `find.byKey()` 方法获取这些组件的引用。`Finder` 存储了渲染数字的组件引用。`incrementFinder` 持有用于递增计数器的 `ElevatedButton` 组件的引用。`decrementFinder` 持有用于减少计数器的 `ElevatedButton` 组件的引用。

```dart
final numberTextFinder = find.byKey('N');
final incrementFinder = find.byKey('I');
final decrementFinder = find.byKey('D');
```

接下来，我们将获取 `FlutterDriver`（`flutter_driver` 库）的引用，它将测试套件连接到已插桩的应用程序以验证测试用例。

```dart
FlutterDriver flutterDriver;
// 连接到 test_driver/main_22.dart 中的已插桩应用
setUp(() async {
  flutterDriver = await FlutterDriver.connect();
});
```

## 拆卸 (Tearing Down)

在所有测试用例执行完成后，调用 `tearDownAll()` 函数来关闭应用的连接。

```dart
// 关闭驱动程序与插桩应用之间的连接
tearDownAll(() async {
```

## 312

## 实战 Flutter (Pragmatic Flutter)

```dart
if (flutterDriver != null) {
  flutterDriver.close();
}
```

## 测试用例 (TEST CASE)

在此测试用例中，我们将使用绿色按钮增加计数器数字并减少两次。数字增加一次将在屏幕上显示 '1'。减少两次将显示数字为 '-1'。

用于递增数字的 `ElevatedButton` 组件通过 `flutterDriver.tap(incrementFinder)` 点击。同样，减少数字的按钮通过 `flutterDriver.tap(decrementFinder)` 点击。点击任一按钮都会增加或减少显示的数字。可以使用 `flutterDriver.getText(numberFinder)` 获取此数字。最后，你可以使用 `expect(flutterDriver.getText(numberFinder), '1')` 验证预期行为。在下一个测试用例中，递增按钮被点击一次和两次，减少两次得到 '-1'。'-1' 通过 `expect(await flutterDriver.getText(numberFinder), '-1')` 进行验证。

```dart
test(' 递增与减少计数器', () async {
  // 点击递增计数器
  await flutterDriver.tap(incrementFinder);
```

```dart
// 验证数字是否变为 1
expect (await flutterDriver.getText(numberFinder), '1');
```

```dart
// 点击两次减少计数器
await flutterDriver.tap(decrementFinder);
await flutterDriver.tap(decrementFinder);
```
