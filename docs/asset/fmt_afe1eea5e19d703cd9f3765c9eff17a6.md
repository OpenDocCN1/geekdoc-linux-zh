
```bash
flutter run -d <device>
```

```bash
flutter run -d all
```

# Flutter 项目结构

![](img/ffb84d2e382861a17088a545dbd2b0c6_60_0.png)

**图 4.12** 在 Android 模拟器上运行的 Hello Books（FloatingActionButton）

## 在线源代码

`hello_books` 项目的源代码可以在 GitHub 上找到（第 04 章：[Flutter 项目结构](hello_books））。

## 有用的命令

最后，让我们通过以下命令在连接的设备上运行 Flutter：

| `flutter` 命令 | 说明 |
| :--- | :--- |
| `flutter build` | 构建应用。 |
| `flutter analyze` | 分析项目。 |
| `flutter attach` | 附加调试。 |
| `flutter build` | 构建构建制品。 |
| `flutter clean` | 清理。 |
| `flutter config` | 配置。 |
| `flutter create` | 创建新项目。 |
| `flutter list` | 列出安装的包。 |
| `flutter doctor` | 显示信息。 |
| `flutter upgrade` | 升级 Flutter 到最新版本。 |
| `flutter run` | 运行项目。 |
| `flutter emulators` | 列出并启动模拟器。 |
| `flutter install` | 在设备上安装应用。 |
| `flutter pub` | 显示包。 |
| `flutter precache` | 填充 Flutter 工具缓存。 |
| `flutter run` | 在连接的设备上运行。 |
| `flutter screenshot` | 获取连接设备的截图。 |
| `flutter symbolize` | 符号化崩溃堆栈。 |
| `flutter test` | 运行 Flutter 测试。 |

**图 4.13** 可用命令

- `flutter build`：构建应用。
- `flutter run`：在连接的设备上运行。它提供了选择连接设备的选项。
- `flutter help`：你可以在命令行运行 `flutter help` 来列出所有可用命令。可用命令的截图如图 4.13 所示。

# 5 Flutter 应用结构

在本章中，你将通过上一章节中的 `HelloBooksApp`（第 04 章：Flutter 项目结构）来深化对 Flutter 应用结构的理解。该应用会在设备屏幕中心显示问候文本“Hello Books”。此应用将以不同的语言显示此问候：西班牙语（Hola Libros）、意大利语（Ciao Libri）和印地语（है हिन्दी），除了默认的英语之外。其他三个问候都存储在一个名为 `greetings` 的列表 (`List<E>`) 数据结构中。

```dart
final List<String> greetings = {
  'Hello Books',
  'Hola Libros',
  'Ciao Libri',
  'है हिन्दी',
};
```

应用在右下角有一个微笑图标的圆形悬浮按钮，用于从列表中选择下一条消息。图 5.1 显示了从英文文本到下一个西班牙语文本的过渡。点击微笑按钮都会获取列表中的下一条消息。到达列表中的最后一条消息后，它将从 `greetings` 列表第一个消息开始恢复。

![](img/ffb84d2e382861a17088a545dbd2b0c6_63_0.png)

图 5.1 完成的 HelloBooksApp

## FLUTTER 组件

### StatelessWidget (无状态组件)

`Stateless` (`StatelessWidget` 类) 组件是不可变的。一旦创建，就无法更改。它不保留自己的状态。无状态组件只被创建一次，在之后不会被重新构建。无状态组件的 `build()` 方法只会被调用一次。

让我们使用 `Container` (`Container` 组件) 来理解如何创建一个自定义的 `StatelessWidget`。`Widget` 是一种便利组件，它结合了常见的绘制、定位和尺寸调整组件。

下面的代码段演示了如何以无状态的方式创建 `Container` 组件。此组件只被创建一次。

```dart
class MyStatelessWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

无状态组件不跟踪其状态。一旦创建，其值就无法更改。如果需要更改无状态组件的值，则需要创建带有更新后值的新组件。以下是部分无状态组件：

- `Text` 组件 (`Text Widget`)：它包含不可变的字母字符串。
- `Icon` 组件 (`Icon Widget`)：`Icon` 组件是不可变的，不用于交互。
- `Card` 组件 (`Card Widget`)：它是一个材料设计卡片，用于显示相关信息。

图 5.2 显示了 `StatelessWidget` 的几个示例。

![](img/ffb84d2e382861a17088a545dbd2b0c6_64_0.png)

图 5.2 StatelessWidget 示例

## Flutter 应用结构

### STATEFULWGET (有状态组件)

`Stateful` (`StatefulWidget`) 组件是可变的。它跟踪状态。它在生命周期内会重建多次。`Stateful` 组件的 `build()` 方法会被调用多次。

```dart
class MyStatefulWidget extends StatefulWidget {
  @override
  _MyStatefulWidget createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

以下是部分 `Stateful` 组件的示例。它们用于跟踪自己的状态。

- `Checkbox` (`Checkbox` 类)：跟踪复选框是否被勾选的状态。
- `Radio` (`Radio<T>` 类)：需要记住它是否被选中的状态。
- `TextField` (`TextField` 类)：`TextField` 组件允许用户输入文本。这意味着它需要跟踪用户已经输入的内容。

图 5.3 显示了 `StatefulWidget` 的示例。

在 `HelloBooksApp` 中，我们将使用 `StatefulWidget` 来实现“微笑”圆形按钮，以更改问候的的文本。

## 显示‘HELLO BOOKS’ 文本

我们将从显示“Hello Books”文本开始构建 `HelloBooksApp`。该应用利用了材料设计 (`Material Design`)。`MaterialApp`

![](img/ffb84d2e382861a17088a545dbd2b0c6_65_0.png)

图 5.3 StatefulWidget 示例

(`MaterialApp` 类) 被用于实现材料设计。`HelloBooksApp` 类继承自 `StatelessWidget`。Flutter 应用是一个无状态组件，因为它是不可变的。它可以包含可变和不可变的组件作为其子组件。`HelloBooksApp` 组件实现了父类 `StatelessWidget` 的 `build()` 方法。`build()` 方法负责将组件组合到用户界面中。在 `build()` 方法中，返回了 `MaterialApp` 组件。`Text` (`Text` 类) 组件用于显示“Hello Books”文本。让我们在下面的代码中创建一个 `MaterialApp` 并显示“Hello Books”文本：

```dart
class HelloBooksApp extends StatelessWidget {
  // 此组件是应用的根
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      // 没有 SafeArea 的 Text Widget
      home: Text('Hello Books'),
    );
  }
}
```

## 入口点

我们准备好启动 `HelloBooksApp`。`debugShowCheckedModeBanner` 标志被设置为 `false`。

```dart
void main() {
```
