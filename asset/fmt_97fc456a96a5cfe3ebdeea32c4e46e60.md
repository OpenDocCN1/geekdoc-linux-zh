
# Widget 测试

## 在线源码

此示例的完整源代码（第 21 章：Widget 测试）可以在 GitHub 上找到。

`CounterApp` 的代码可以在此处获取（第 21 章：Widget 测试）。

# 运行 Widget 测试

可以使用与单元测试相同的命令来运行 widget 测试。

```
$ flutter test test/main_21_test.dart
```

# 输出

执行所有测试所花费的总时间显示为 `00:04`。`+6` 代表执行的测试数量。

最后一部分 `All tests passed!` 显示了测试运行的状态。

```
00:04 +6: All tests passed!
```

# 结语

在本章中，你学习了如何为 `CounterApp` 编写 widget 测试。你学习了使用

`flutter_test` 包来编写测试以验证 widget 的行为。你使用了 `WidgetTester`、`testWidgets()`、`Finder` 和 `Matcher` 来测试 widget 的行为。`WidgetTester` 帮助构建交互式 widget 测试。`testWidgets()` 方法用于编写验证 getter 行为的测试代码。`Finder` 类用于在测试应用中查找 widget。`Matcher` 类帮助验证 `Finder` 类是否可以在环境中定位给定的 widget。

## 参考文献

- Dart Dev. (2020, 11 30). test. Retrieved from pub.dev: https://pub.dev/packages/test

- Flutter Dev. (2020, 11 30). Finder class. Retrieved from api.flutter.dev: https://api.flutter.dev/flutter/flutter_test/Finder-class.html

- Flutter Dev. (2020, 11 30). Key class. Retrieved from api.flutter.dev: https://api.flutter.dev/flutter/foundation/Key-class.html

- Flutter Dev. (2020, 11 30). Matcher class. Retrieved from api.flutter.dev: https://api.flutter.dev/flutter/package-matcher/Matcher-class.html

- Flutter Dev. (2020, 11 30). MediaQuery class. Retrieved from api.flutter.dev: https://api.flutter.dev/flutter/widgets/MediaQuery-class.html

- Flutter Dev. (2020, 11 30). pump method. Retrieved from api.flutter.dev: https://api.flutter.dev/flutter/flutter_test/TestWidgetsBinding/pump.html

- Flutter Dev. (2020, 11 30). pumpWidget method. Retrieved from flutter.dev: https://api.flutter.dev/flutter/flutter_test/WidgetTester/pumpWidget.html

- Flutter Dev. (2020, 11 30). tap method. Retrieved from api.flutter.dev: https://api.flutter.dev/flutter/flutter_test/WidgetController/tap.html

- Flutter Dev. (2020, 11 30). testWidgets function. Retrieved from api.flutter.dev: https://api.flutter.dev/flutter/flutter_test/test/testWidgets.html

- Flutter Dev. (2020, 11 30). WidgetTester class. Retrieved from api.flutter.dev: https://api.flutter.dev/flutter/flutter_test/WidgetTester-class.html

- Flutter Team. (2020, 11 27). flutter_test. Retrieved from flutter.dev: https://flutter.dev/docs/cookbook/testing/widget/introduction#1-add-the-flutter-test-dependency

- Google. (2020, 11 30). Widget Testing. Retrieved from flutter.dev: https://flutter.dev/docs/cookbook/testing/widget/introduction

- Tyagi, P. (2020, 11 30). Chapter 21: Widget Testing. Retrieved from Pragmatic Flutter GitHub Repo: https://github.com/ptyagicodecamp/pragmatic_flutter/blob/master/test/main_21_test.dart

- Tyagi, P. (2021). Chapter 21: Unit Testing. In P. Tyagi, Pragmatic Flutter: Building Cross-Platform Mobile Apps for Android, iOS, Web & Desktop. CRC Press.

# 22 集成测试

在上一节关于单元测试（第 20 章：单元测试）中，你学习了如何测试函数、类和方法的逻辑。随后，在 Widget 测试章节（第 21 章：Widget 测试）中，你学习了如何测试 widget。在本章中，你将学习如何在真实设备上测试应用，同时与其他系统级组件进行交互。集成测试允许将多个部分组合在一起。对于测试应用在真实硬件上的性能非常有用。

集成测试是通过使用两个被称为“测试对”（test pair）的文件完成的。第一个文件部署插桩应用（将应用插桩到测试设备，可以是真实设备，也可以是模拟器）。第二个文件包含测试用例，用于驱动应用执行应用的操作。

## 软件包依赖

集成测试需要两个文件组成的测试对。`flutter_driver`（`flutter_driver` 库）需要包含在 `pubspec.yaml` 文件中。该包提供了创建测试对的工具。你需要在 `pubspec.yaml` 配置文件的 `dev_dependencies` 部分下添加以下包。

```
dev_dependencies:
  flutter_test:
    sdk: flutter

flutter_driver:
  sdk: flutter
```

## CounterApp 代码预览

在本节中，我们将为带有两个按钮的 `CounterApp` 编写集成测试。供你参考的来自单元测试章节（第 20 章：单元测试）的应用代码如下：

```
void main() {
  runApp(CounterApp());
}
```

```
class CounterApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
```

```
debugShowCheckedModeBanner: false,
theme: ThemeData(
  primarySwatch: Colors.blue,
  visualDensity: VisualDensity.adaptivePlatformDensity,
  home: MyHomePage(title: 'My Counter App'),
);
```

```
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
```

```
final String title;
```

```
@override
  _MyPageState createState() => _MyHomePageState();
```

```
class Counter {
  int number = 0;
```
