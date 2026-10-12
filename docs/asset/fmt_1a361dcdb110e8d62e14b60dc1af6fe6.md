
切换到你首选的通道后，你需要运行命令 `flutter upgrade` 来引入更新。

## 为 ANDROID 平台设置

### ANDROID STUDIO

下一步是安装 Android Studio（安装 Android Studio）以及最新的 Android SDK、Android SDK 命令行工具、Android 构建工具（tools）。

### ANDROID 模拟器

在 Android Studio 中使用 Android Virtual Device (AVD) 管理器创建模拟器（Android Studio > Tools > AVD Manager）。点击“Create Virtual Device”按钮创建虚拟设备。为你的模拟器选择硬件、系统镜像 (x64) 和 AVD 标识。点击“Finish”将在 AVD 管理器中创建一个 AVD。通过运行命令 `flutter devices` 在终端中查看它进行验证。

你也可以通过下面的 `flutter devices` 命令查看设备列表：

```
$ flutter devices
1 connected devices:
```

Android SDK built for x86 (mobile) • emulator-5554 • android-x86 • Android 10 (API 29) (emulator)

### 测试你的设置

使用 `flutter create testapp` 创建一个测试项目，并如所示运行：

```
flutter create testapp

cd testapp

flutter run -d android
```

![](img/ffb84d2e382861a17088a545dbd2b0c6_42_0.png)

图 3.1 在 Android 模拟器中运行的 TestApp

参考图 3.1 查看在 Android 模拟器中运行的默认应用。

### Android 设备

在 Android 设备上运行 Flutter 应用需要运行 Android 4.1 (API level 16) 或更高版本的设备。你需要使用 USB 线将设备连接到计算机。启用 USB调试（在设备上配置开发者选项）。使用 `flutter devices` 命令测试连接。它应该会在控制台上列出该设备或其他设备（如果有）。

### 设置环境

请参考 Flutter 文档（Android 设置）获取详细的 Android 设置说明。

## 为 iOS 平台设置

### Xcode

从 Mac App Store (Xcode) 或网页 (Xcode) 安装最新稳定版的 Xcode。按照提示进行安装。安装 Xcode 的同时也会安装命令行工具。请参考 Flutter 文档（安装 Xcode）获取关于安装和设置 Xcode 的详细说明。

### iOS 模拟器

在 Mac 上，使用命令 `open -a simulator` 打开模拟器。在编写本文时，默认模拟器是 iPhone SE (第二代) (iPhone SE (2nd generation))。参考文档（设置 iOS）获取设置 iOS 模拟器的说明。你也可以通过如下 `flutter devices` 命令查看设备列表：

- flutter devices
  connected devices:
- Android SDK built for x86 (mobile) • emulator-5554
- android-x86 • Android 10 (API 29) • (emulator)
- iPhone SE (2nd generation) (mobile) • FCF81DB2

测试你的设置

使用 `flutter create testapp` 创建一个测试项目，并如所示运行：

```
flutter create testapp
cd testapp
flutter run -d android
```

参考图 3.1 查看在 Android 模拟器中运行的默认应用。

### Android 设备

在 Android 设备上运行 Flutter 应用需要运行 Android 4.1 (API level 16) 或更高版本的设备。你需要使用 USB 线将设备连接到计算机以访问。启用 USB 调试（在设备上配置开发者选项）。使用 `flutter devices` 命令测试连接。它应该会在控制台上列出该设备或其他设备（如果有）。

### 设置环境

请参考 Flutter 文档（Android 设置）获取详细的 Android 设置说明。

## 为 iOS 平台设置

### Xcode

从 Mac App Store (Xcode) 或网页 (Xcode) 安装最新稳定版的 Xcode。按照提示进行安装。安装 Xcode 的同时也会安装命令行工具。请参考 Flutter 文档（安装 Xcode）获取关于安装和设置 Xcode 的详细说明。

### iOS 模拟器

在 Mac 上，使用命令 `open -a simulator` 打开模拟器。在编写本文时，默认模拟器是 iPhone SE (第二代) (iPhone SE (2nd generation))。参考文档（设置 iOS）获取设置 iOS 模拟器的说明。你也可以通过如下 `flutter devices` 命令查看设备列表：

- flutter devices

  connected devices:

- Android SDK built for x86 (mobile) • emulator-5554

- android-x86 • Android 10 (API 29) • (emulator)

- iPhone SE (2nd generation) (mobile) • FCF81DB2

测试你的设置

使用 `flutter create testapp` 创建一个测试项目，并如所示运行：

```
flutter create testapp

cd testapp

flutter run -d android
```

![](img/ffb84d2e382861a17088a545dbd2b0c6_44_0.png)

图 3.2 在 iOS 中运行的 TestApp

参考图 3.1 查看在 Android 模拟器中运行的默认应用。

### Android 设备

在 Android 设备上运行 Flutter 应用需要运行 Android 4.1 (API level 16) 或更高版本的设备。你需要使用 USB 线将设备连接到计算机以访问。启用 USB 调试（在设备上配置开发者选项）。使用 `flutter devices` 命令测试连接。它应该会在控制台上列出该设备或其他设备（如果有）。

## 为 WEB 设置

在编写本文时，Flutter 对网页的支持仍处于早期阶段。目前网页支持在 beta 通道中可用。使用 `flutter channel beta` 切换到 beta 通道。不要忘记运行 `flutter upgrade` 命令并启用 Web 支持。

```
flutter channel beta

flutter upgrade
```

# 实战 Flutter

![](img/ffb84d2e382861a17088a545dbd2b0c6_46_0.png)

图 3.4 在 chrome 中运行的 TestApp

```
$ flutter channel dev

$ flutter upgrade

//针对 macOS

$ flutter config --enable-macos-desktop

//针对 Linux

$ flutter config --enable-linux-desktop
```

你只会在 Linux 机器上看到 Linux 设备。
现在你的环境已经开启了桌面端支持，在 Android Studio 顶部工具栏的设备选择列表中，除了 'Chrome (web)' 和 'Web Server (web)' 外，你应该还能看到 'macOS (Desktop)'。

请参考图 3.5 查看 Android Studio 的“Run”（运行）工具栏显示的 macOS(desktop) 和 chrome 设备。

你也可以通过下面的 `flutter devices` 命令查看设备列表：

![](img/ffb84d2e382861a17088a545dbd2b0c6_46_1.png)

图 3.5 Android Studio 运行工具栏在设备列表中显示 macOS 桌面和 web 设备

# 环境配置

```
$ flutter devices

3 个连接设备:

+   - macOS (desktop) - macos - darwin-x64 - Mac OS X

- 10.15.0.1973

- Web Server (web) - web-server - web-javascript - Flutter Tools
```
