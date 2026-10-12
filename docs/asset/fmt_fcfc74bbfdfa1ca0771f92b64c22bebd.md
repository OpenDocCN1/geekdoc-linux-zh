
beta

stable

## 创建 Flutter 项目

创建 Flutter 项目有两种方法：使用 Terminal 中的命令行工具或使用 IDE。你也可以先用命令行创建项目，之后从 IDE 中打开。

### 使用命令行 (TERMINAL)

运行以下命令为‘Hello Books’应用创建一个 `hello_books` 项目。

```
$ flutter create hello_books
```

默认情况下，包结构为 `com.example.hello_books`。在创建项目时，可以使用下面的命令指定自己的包名。

```
flutter create --org com.pragmatic_flutter hello_books
```

上述命令会将 Android 的包名和 iOS 的束标识符设置为 `com.pragmatic_flutter.hello_books`。

你可以通过点击启动屏幕上的“Open an existing Studio Project”（打开现有的 Studio 项目）选项在 Android Studio 中打开此项目，如图 4.2 所示。

### 使用 IDE (ANDROID STUDIO)

“新建 Flutter 项目”屏幕

在启动屏幕上选择此选项以启动新项目，如图 4.3 所示。

#### Flutter 项目结构

![](img/ffb84d2e382861a17088a545db2b0c6_53_0.png)

图 4.2 Android Studio 启动屏幕显示“Open an existing Android Studio Project”选项

![](img/ffb84d2e382861a17088a545db2b0c6_53_1.png)

图 4.3 “新建 Flutter 项目”屏幕

#### 实战 Flutter

![](img/ffb84d2e382861a17088a545db2b0c6_54_0.png)

图 4.4 “New Flutter Project”屏幕

##### “New Flutter Project”屏幕

此屏幕提供了创建 Flutter 项目、Flutter 模块、包或插件的选项。由于我们正在创建一个 Flutter 应用，因此像图 4.4 所示选择‘Flutter Application’选项。

##### “New Flutter Application”屏幕

在图 4.5 所示的屏幕上为新的 Flutter 应用配置选项。

![](img/ffb84d2e382861a17088a545db2b0c6_54_1.png)

图 4.5 “New Flutter Application”屏幕（配置项目）

![](img/ffb84d2e382861a17088a545dbd2b0c6_55_0.png)

图 4.6 `New Flutter Application` （设置包名）

接下来，提供包名以组织源代码。你还需要如图 4.6 所示，选择对“android artifacts”（Android 制品）的支持以及 Android 和 iOS 平台的 Kotlin 和 Swift 语言支持。

##### 跨平台 Flutter 项目结构

Flutter 项目在 `lib` 文件夹中包含共享代码。每个平台都有自己的文件夹来存放平台特定的代码。Flutter App 可以部署到各个平台对应的 `android`、`iOS`、`web`、`linux` 和 `macOS` 文件夹。项目结构的可视化如图 4.7。

让我们查看重要项目目录和文件的详情：

- `lib/`: 此文件夹包含 Dart 文件。这是所有平台（如 iOS、Web、桌面和嵌入式设备）的共享代码。书中仅关注 Android、iOS、Web 和桌面 (macOS)。
- `android/`: 此文件夹包含 Android 代码，包括 `AndroidManifest.xml`。
- `ios/`: 此文件夹包含 Swift 语言编写的 iOS 应用原生代码。
- `web/`: 此文件夹包括 `index.html` 以及可以部署到公共托管网站的资源。
- `linux/`: 此文件夹包含与 Linux 平台相关的代码。该文件夹通过启用对桌面(Linux)的支持生成，但只能在 Linux 机器上编译。
- `macos/`: 此文件夹包含用于 macOS 平台的原生代码。
- `test/`: 此文件夹包含所有单元测试类。
- `pubspec.yaml`: 这是 Flutter 应用的依赖管理和配置文件。

![](img/ffb84d2e382861a17088a545dbd2b0c6_56_0.png)

图 4.7 Android Studio 中的 Flutter 项目结构

##### 运行默认应用：ANDROID, iOS, WEB 和 DESKTOP

在本节中，我们将在所有四个平台（Android、iOS、web 和桌面 (macOS)）上运行‘hello_books’ Flutter 应用。让我们使用一个简单的命令 `flutter run -d all` 一起在四个平台上运行‘hello_books’ 项目。

###### ANDROID 平台

在 Android 模拟器上运行的 Hello Books 应用如图 4.8 所示。

###### iOS 平台

在 iOS 模拟器上运行的 Hello Books 应用如图 4.9 所示。

###### WEB 平台

在 Chrome 浏览器中运行的 HelloBooks 应用如图 4.10 所示。

![](img/ffb84d2e382861a17088a545dbd2b0c6_57_0.png)

**图 4.8** 在 Android 模拟器上运行的 Hello Books

###### DESKTOP (macOS) 平台

在 macOS 平台上运行的 Hello Books 应用如图 4.11 所示。

##### 线源代码

`hello_books` 项目源代码可以在 GitHub 上找到（第 04 章：[Flutter 项目结构 (hello_books)](hello_books)）。

##### 运行代码示例

Flutter 文档对开发者友好且易于遵循。它带有一个示例代码段库。它提供了通过示例代码 ID 创建 Flutter 应用并将其作为独立的 Flutter 应用运行的支持。

![](img/ffb84d2e382861a17088a545dbd2b0c6_58_0.png)

图 4.9 在 iOS 模拟器上运行的 Hello Books

###### 列出示例代码 ID

以下命令将示例代码标识符/ID 导出到‘samples.json’ 文件中。

```
flutter create --list-samples=samples.json
```

###### ‘samples.json’文件的内容

下面是该文件的一小段。这段特定的示例代码演示了‘BottomAppBar’组件的使用以及其中的停靠式‘FloatingActionButton’。你将在接下来的章节中学习这些组件和构建界面。本节的目的是让你学会自己探索 Flutter 的官方示例代码。

![](img/ffb84d2e382861a17088a545dbd2b0c6_59_0.png)

图 4.10 在 Web 平台运行的 Hello Books

![](img/ffb84d2e382861a17088a545dbd2b0c6_59_1.png)

图 4.11 在 macOS 平台运行的 Hello Books

```
{
  "sourcePath": "lib/src/material/scaffold.dart",
  "sourceLine": 1009,
  "id": "material.Scaffold.3",
  "channel": "master",
  "serial": "3",
  "package": "flutter",
  "library": "material",
  "element": "Scaffold",
  "file": "material.Scaffold.3.dart",
  "description": "此示例显示了一个带有 AppBar、BottomAppBar 和 FloatingActionButton 的 Scaffold。body 是一个放置在 Center 中的 Text，以便通过 FloatingActionButtonLocation.centered 将文本在停靠的 BottomAppBar 内部进行居中对齐。FloatingActionButton 会增加计数器值。"
}
```

###### 从示例代码创建应用

一旦你获得了示例代码的 id，请在以下命令中替换它。你还需要提供示例应用的名称。

```bash
flutter create --sample=<id> <app_name>
```

使用以下命令：

```bash
flutter create --sample=<id>
```
