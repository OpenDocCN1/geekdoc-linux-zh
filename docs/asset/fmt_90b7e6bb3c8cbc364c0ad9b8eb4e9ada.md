
此示例（Chapter01: Quick Reference to Dart2 (Collections））的源代码可以在 GitHub 上找到。

## 函数

让我们创建一个函数，检查传递的参数是否为 'Flutter' 并返回布尔值。如果精确匹配 'Flutter' 则返回 true，否则返回 false。此类函数被称为“命名函数”，因为函数名描述了它们的意图。

```dart
bool isFlutter(String str) {
  return str == 'Flutter';
}
// 使用命名函数
dynamic result = isFlutter("Flutter");
print(result);

// 输出
true
```

## 带有可选参数的函数

创建一个函数 'concat(...)'，当第二个字符串可用时将两个字符串拼接。在这种情况下，第二个字符串可以使用方括号 '[]' 作为可选参数传递。

```dart
String concat(String str1, [String str2]) {
  return str2 != null ? "$str1 $str2" : str1;
}

// 使用方法
result = concat("Priyanka", "Tyagi");
print(result);

// 输出
Priyanka Tyagi
```

## 命名参数

提供可选参数另一种方法是使用命名参数。它们可以使用大括号 '{}' 传递。

```dart
// 命名参数：在大括号中带有可选参数的函数
String concat2(String str1, {String str2}) {
  return str2 != null ? "$str1 $str2" : str1;
}
```

## Dart 基础

```dart
// 使用带有大括号{}的可选参数的函数
result = concat2("Priyanka", str2: "Tyagi");
print(result);
// 输出
Priyanka
Tyagi
```

## 将函数作为参数传递

Dart 2 语言允许将函数作为参数传递给另一个函数。让我们创建一个函数 `int subtract(int a, int b)` 来计算两个数之间的差。

# Dart 基础

Google. (2020, 11 13). [List<E> 类]。获取自官方 Dart 语言文档：

https://api.dart.dev/stable/2.10.3/dart-core/List-class.html

Google. (2020, 11 13). [Map<K, V> 类]。获取自官方 Dart 语言文档：

https://api.dart.dev/stable/2.10.3/dart-core/Map-class.html

Google. (2020, 11 13). [Object 类]。获取自官方 Dart 语言文档：

https://api.dart.dev/stable/2.10.3/dart-core/Object-class.html

Google. (2020, 11 13). [RuntimeType 属性]。获取自官方 Dart 语言文档：

https://api.dart.dev/stable/2.10.2/dart-core/Object/RuntimeType.html

Google. (2020, 11 13). [Set<E> 类]。获取自官方 Dart 语言文档：

https://api.dart.dev/stable/2.10.3/dart-core/Set-class.html

Google. (2020, 11 13). [展开运算符]。获取自官方 Dart 语言文档：

https://dart.dev/guides/language/language-tour#spread-operator

Moore, K. (2018, 08 07). [宣布 Dart 2 稳定版和 Dart Web平台]。获取自 Medium：https://medium.com/dartlang/dart-2-stable-and-the-dart-web-platform-3775d8ea7?

Tyagi, P. (2020, 11 13). [第 01 章：Dart2 快速参考（类）]。获取自 Pragmatic Flutter GitHub 仓库：https://github.com/ptygocodecamp/pragmatic_flutter/blob/master/lib/chapter01/classes.dart

Tyagi, P. (2020, 11 13). [第 01 章：Dart2 快速参考（集合）]。获取自 Pragmatic Flutter GitHub 仓库：https://github.com/ptygocodecamp/pragmatic_flutter/blob/master/lib/chapter01/collections.dart

Tyagi, P. (2020, 11 13). [第 01 章：Dart2 快速参考（函数）]。获取自 Pragmatic Flutter GitHub 仓库：https://github.com/ptygocodecamp/pragmatic_flutter/blob/master/lib/chapter01/functions.dart

Tyagi, P. (2020, 11 13). [第 01 章：Dart2 快速参考（变量与数据类型）]。获取自 Pragmatic Flutter GitHub 仓库：https://github.com/ptygocodecamp/pragmatic_flutter/blob/master/lib/chapter01/variables.dart

![](img/ffb84d2e382861a17088a545dbd2b0c6_30_0.png)

# 2 Flutter 简介

Flutter 是一种用于开发跨平台应用程序的开源软件开发包 (SDK)(Flutter)，并且免费使用。它是 Google 的 SDK，用于通过单一代码库为移动端、Web 和桌面构建美观、快速且原生编译的应用程序。Flutter 应用使用 Dart 语言 (Dart) 编写。Dart 针对构建自定义用户界面 (UI) 和快速的跨平台应用程序进行了优化。Dart 代码会被编译为运行在目标平台的原生机器代码。例如，Web 端 Dart 代码会被编译为 JavaScript。Flutter 是一个完整的框架，提供了 UI 渲染、组件、状态管理解决方案、导航、测试以及硬件应用程序编程接口 (APIs)，用于与传感器、蓝牙等设备级功能进行交互。

## 跨平台解决方案

“跨平台解决方案”一词代表在不同平台之间复用代码，或者说“编写一次，随处运行”。具有百分之百代码复用的完美跨平台解决方案是每个移动开发者梦寐以求的圣杯。让我们讨论一些用于最大化 Web、Android、iPhone 操作系统 (iOS) 和桌面等多个部署目标的可共享代码的解决方案。

## 原生 SDK

在应用开发领域，原生 SDK（软件开发包）主要指 Apple iOS SDK（开发 iOS 应用）和 Google 的 Android SDK（开发 Android 应用），分别用于在 iOS 和 Android 平台上构建移动应用。iOS 应用使用 Objective-C (Objective-C) 或 Swift (Swift) 编程语言开发。Android 应用使用 Java (Java) 或 Kotlin（一种让开发者更快乐的现代编程语言）开发。你的应用代码原生运行在平台平台上。原生代码被编译为运行在特定平台（如 iOS 或 Android）。

在这种架构中，如图 2.1 所示，应用“App-X”直接与平台通信并访问平台服务。平台端创建在屏幕画布上渲染的组件。事件会回传给组件。在这种情况下，你需要为每个平台编写两个独立的“App-X”实现版本。不同的实现也意味着两个应用都是用完全不同的语言编写的。

Android 和 iOS 平台支持旧版（iOS 使用 Objective-C，Android 使用 Java）和现代（iOS 使用 Swift，Android 使用 Kotlin）编程语言

# 16

# Pragmatic Flutter

| 画布 | | 平台 |

| :--- | :--- | :--- |

| | | 平台服务 |

| | OEM | 传感器 |

| | | 位置 |

![](img/ffb84d2e382861a17088a545dbd2b0c6_30_0.png)

**图 2.1** 原生平台

## 为什么选择 Flutter

现在你已经熟悉 Flutter 提供的功能（Flutter 的革命性），让我们来看看一些让 Flutter 领先竞争对手的优势。

## 开发者生产力

“热重载”(Hot Reload) 帮助开发者移动得。此功能允许开发者在编写代码时即可在界面上看到更改。

# Flutter 简介
