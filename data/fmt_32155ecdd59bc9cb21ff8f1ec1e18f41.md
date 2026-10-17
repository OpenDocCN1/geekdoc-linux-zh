
# 数据建模

## ANDROID
截图 13.5 来自 Android 模拟器。

## iOS
截图 13.6 来自 iPhone。

## DESKTOP (macOS)
截图 13.7 来自 macOS。

## WEB (Chrome)
截图 13.8 来自 Chrome 浏览器。

## SOURCE
代码源代码来自 Flutter。

## 结论
恭喜！你使用 Flutter 制作了自己的书籍列表应用。在本章中，你学习了如何通过 API 获取书籍信息。最后，你学习了如何将 API 响应转换为 JSON 格式。

## 参考文献
- Dart Dev. (2020). `LinkedHashMap<K, V>`. 来自自 Dart: https://api.dart.dev/stable/2.8/collection/LinkedHashMap.html
- Dart Team. (2020). `convert`. 来自自 Dart: https://api.dart.dev/stable/2.7/dart-convert.html
- Dart Team. (2020). `HttpResponse`. 来自自 Dart: https://api.dart.dev/stable/2.7/dart-io/HttpResponse.html
- Dart Team. (2020). `Map<K, V>`. 来自自 Dart: https://api.dart.dev/stable/2.8/dart-core/Map.html
- Flutter Team. (2020). `BuildContext`. 来自自 Flutter: https://api.flutter.dev/widgets/BuildContext.html
- Flutter Team. (2020). `ListView`. 来自自 Flutter: https://api.flutter.dev/widgets/ListView.html
- Google, (2020). `Card`. 来自自 Flutter: https://api.flutter.dev/flutter/material/Card.html
- Google, (2020). `Cards`. 来自自 material.io: https://material.io/components/cards
- Google, (2020). `Column`. 来自自 Flutter: https://api.flutter.dev/flutter/widgets/Column.html
- Google, (2020). `Flexible`. 来自自 Flutter: https://api.flutter.dev/flutter/widgets/Flexible.html
- Google, (2020). `ListView`. 来自自 Flutter: https://api.flutter.dev/flutter/widgets/ListView.html
- Google, (2020). `Row`. 来自自 Flutter: https://api.flutter.dev/flutter/widgets/Row.html
- Google, (2020). `Text`. 来自自 Flutter: https://api.flutter.dev/flutter/widgets/Text.html

# 14 导航与路由

在上一章（第 12 章：集成 REST API），我们学习了如何向 Books API 发送 RESTful HTTP 请求并获取书籍列表数据。在上一章（第 13 章：数据建模）中，我们使用数据模型类在 `ListView` 组件中渲染了书籍。使用了一个自定义组件 – `BookTile` 来渲染每个项目。`BookTile` 组件只显示了关于书籍的三个信息点：标题（作者）和封面图像。`ListView` 组件为从 API 返回的每个项目显示了一个 `BookWidget`。接下来，我们想要显示有关书籍的更多详细信息，例如出版日期、描述等。每本书书都有自己的详细信息页面。在本章中，我们将开始通过渲染书籍的描述来创建这个简单的页面 – `BookDetailsPage`。稍后，我们将学习如何为 `BookListing` 屏幕中的选定项目构建从 `BookListing` 屏幕到 `BookDetailsPage` 屏幕的导航。图 14.1 显示了我们在上一章（第 13 章：数据建模）中创建的 `BooksApp` 首页。

在本章中，我们将学习三种类型的导航和路由，以实现从 `BookListing` 首页到 `BookDetailsPage` 屏幕的导航。`BookDetailsPage` 仅如图 14.2 所示显示书籍详情。

在下一章（第 15 章：第二个页面：书籍详情）中，我们将继续构建 `BookDetailsPage` 界面。

## 简单的 BookDetailsPage 屏幕

在本节中，你将学习构建一个基础二级组件 `BookDetailsPage`，它被用占位符来理解 Flutter 中的导航和路由概念。这个简单页面的结构如图 14.3 所示。

`BookDetailsPage` 是一个 `StatelessWidget`，有两个子组件：`AppBar` 和 `Center`。`AppBar` 显示书籍的标题，`Center` 组件被赋值给 `Scaffold` 组件的 `body` 属性。`Center` 组件有一个 `Child` 组件来显示书籍的详细描述。

```dart
import 'package:flutter/material.dart';

import 'book.dart';

class BookDetailsPage extends StatelessWidget {
  final BookModel book;

  const BookDetailsPage({Key key, this.book}) : super(key: key);

  @override
```

![](img/ffb84d2e382861a17088a545dbd2b0c6_246_0.png)

**图 14.1** `BookListing` – `BooksApp` 的首页。使用 `BookTile` 组件列出书籍

```dart
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text(book.volumeInfo.title),
    ),
    body: Center(
      child: Text(book.volumeInfo.description),
    )
  );
}
```

![](img/ffb84d2e382861a17088a545dbd2b0c6_247_0.png)

通过这本实战书籍，对 Python 核心语言进行全面、深入的介绍。基于作者 Mark Lutz 的流行课程，这个更新的版本将帮助你快速使用 Python 编写高效、高质量的代码。这是一个入门的理想方式——无论你是编程新手，还是精通其他语言的专业开发人员。这本易于理解、自学的教程包含了测验、练习和有用的插图，带你从 Python 2.7 和 3.3（3.X 和 2.X 系列的最新发布版本）以及今天所有常用的发布版本开始。你还将学习最近在 Python 中变得常见的高级语言特性。探索 Python 的内置对象类型如列表、数字和字典；使用 Python 语句创建和处理对象，并学习 Python 的通用语法；使用函数避免代码冗余并封装代码以复用；将语句、函数和其他工具组合成更大的模块；深入研究 Python 的面向对象编程。

# 236

# 实战 Flutter

```dart
book: booksListing[0],
  },
},
{
```

