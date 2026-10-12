
## Qt5 开发教程

![](img/80af6fd0c5ad221222cba94201825f7f_47_0.png)

### 为什么它是共享的？

Android SDK 独立于其集成开发环境。在 Android Studio 中找到的 Android SDK 工具显示了包含 SDK 的文件夹，这也会影响其他开发工具。作为有经验的 Android 开发者，您可能会发现可以使用 Android SDK 替代以获得无限制的额外功能。

在屏幕左上角的栏的项目符号中，选择 `Android Android > Build` 以打开 Android 应用程序的构建配置。在下一步中，点击 `Build Android APK` 子栏目中的 `Details` 以打开参数设置。Android SDK 允许您决定在编译过程中应该使用哪个版本的 SDK。Qt 部署将回到 APK 中的 Qt 库——在主场景中部署您的应用程序之前，请务必检查许可。

例如，如果您对 Android 子栏目感兴趣，将点击 `Create template`。在下一步，将弹出一个向导。

当加载了正确的样式表时，控制相当合理，但 Qt 的类加载器则并非如此。

### Android 基于 Java，它访问原生 API 可能需要如图 4 所示的两种语言之间的连接

接下来，点击应用程序输出中的 `Stop` 按钮终止应用程序执行，并在智能手机上重启程序。由于框架的问题，应用程序将以图 4 所示的原生触摸屏界面启动。

幸运的是，这并不困难。打开 `main.cpp` 并如下所示入口点：

```cpp
int main(int argc, char *argv[]) {
    qputenv("QT_ANDROID_NATIVE_STYLE","");
    return QApplication(argc, argv);
}
```

该代码使用了 `putenv` 函数，允许您将变量写入 Qt 的执行状态：我们使用 `QT_ANDROID_NATIVE_STYLE`，在所有实例中都必须使用原生样式运行时。例如，变量应该在实例化 `QApplication` 之前设置，因为 Qt 会在初始化后检查其状态的变化。

> 创建 Android 模板向导
>
> 选择 Android 的源目录。
>
> Android 源目录中的文件被复制到用于构建 Android 目录，默认文件将被覆盖。
>
> https://doc.qt.io/androidManifest.html
>
> - 将文件复制到 Android 目录

## manifest 在哪里？

Android 开发者知道 manifest 是 Android 应用程序最重要的部分之一：它可用于定义应用程序与操作系统之间的交互。默认情况下，创建的 Qt 应用程序不带 manifest 文件。相反，Qt Creator 会在编译过程中使用来自 Eclipse 环境的 PRO 文件的信息创建一个“默认”文件：如果您对它满意，点击 XML 源码树以返回类似于 Android Studio 的代码编辑体验。

解决此问题需要我们使用一个之前从没用过的 Qt Creator 功能——点击

空白的区域意味着您能够配置程序符号：其中一个是一个打开以选择程序符号的对话框。权限可以通过切换按钮处理。请记住，Qt 会分析添加到 PRO 文件中的模块，并尝试确定需要哪些隐式权限——这些权限通常不会显示在其中。

接下来我们要求您选择 Android 软件包源目录。

## 图 5

完成后，是时候查看实际界面了。Digia 使用一组专门用于与 Android 交互的方法扩展了原始的“简单”Java 界面——我们将运行 `runAndroidThread`：

![](img/80af6fd0c5ad221222cba94201825f7f_48_0.png)

```cpp
void mainWindow::showToast(const QString &message, int duration) {
    QtAndroid::runOnAndroidThread(message, duration);
}
```

大而言，它按照您的预期工作工作：一个 `Runnable` 被设置为 Android UI 线程，并在其中执行。

由于 C++ 和 Java 使用完全不同的结构，Java 字符串是从传入的字符串新创建的：

```cpp
QObject* javaString = QtAndroidObject::fromString(message);
```

需要实际调用 `makeToast`。这个调用很有趣，因为第三个参数——它描述了方法的“签名”，并影响了用于其他参数的解析逻辑：

```cpp
QObject* object = QtAndroidObject::callStaticMethod("Toast", "makeToast", 
    QVariant("android.content.Context;java.lang.CharSequence"), QVariant("android.widget/Toast"), QVariant()));
invokeMethod(object, "show");
```

最后，调用生成的 Toast 对象的显示方法：

```cpp
toast.callMethod("show");
```

完成后，您必须从不同的位置显示 `showToast`——结果看起来如图 5 所示。

![](img/80af6fd0c5ad221222cba94201825f7f_48_1.png)

- Android 模板

## 图 1

| 系统 | 负载图表 | 内存分配器 | 应用 | 进程 | 端口 | 表格查看器 | 追踪概述 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 表格名称 | 表格 ID | 对象 | | 大小 (kb) | 所有者 ID | 所有者名称 | |
| lud | | | 6 | 2 | <0130.0> | | mnesia_monitor |

表信息：

| 记录名称 | 数量 | 年 | 月份 |
| :--- | :--- | :--- | :--- |
| lud | lud | 2017 | 6 |
| lud | lud | 2017 | 7 |
| lud | lud | 2017 | 8 |
| lud | lud | 2017 | 9 |
| lud | lud | 2017 | 10 |

### 标识与所有者

- 名称: `lud`
- ID: `lud`
- 命名表: `lud`
- 所有者: `<0130.0>`
- 所有者名称: `mnesia_monitor`
- 节点: `nonode@nhost`
- TV Mnesia: `lud@nonode@nhost`

### 设置

- 源: `mnesia`

在这里它只是一个单节点。此外，Mnesia 可以将数据存储在内存中，也可以在磁盘上，而 ETS 只能使用内存。如果你想回滚事务——ETS 不提供此功能。此外，Mnesia 提供了更好的查询语法，如果你有大量数据或想要创建高效的查询，可以使用它。

因此，为了在 Mnesia 数据库和表上启动记录，以便能够使用正确的参数启动 `mnesia:create_schema()` 函数：`mnesia:create_schema(node())`。`node()` 函数是该函数的参数，它返回当前节点的标识符。这意味着 Mnesia 实例目前使用单个节点。

结果是，Mnesia 和 ETS 在表面上有所不同，它提供了更多功能。因此，根结底，Mnesia 比 ETS 更强大，这意味着当你需要强大时，请选择 Mnesia。

> Mnesia 默认不运行；因为你不希望 Erlang 自动运行不必要的进程。

## 有用的函数

本节将介绍在处理 Mnesia 数据库时能让工作更轻松的函数：

- `mnesia:create_schema()` 此函数用于创建新架构。
- `mnesia:build_table()` 此函数允许在运行的 Mnesia 数据库上构建新表。
- `mnesia:write()` 此函数用于向 Mnesia 数据库的表插入新记录。
- `mnesia:transaction()` 此函数用于在写入记录时执行命令。
- `mnesia:table_info()` 此函数返回作为参数传递给它的表信息。请注意，`mnesia:table_info()` 需要第二个参数来指定你想要获取的信息类型——例如，使用 `'all'` 作为第二个参数将返回所有内容！

那时，Mnesia 将创建一个目录来存放其文件，该目录将命名为 `Mnesia.nonode@nhost` 并包含以下内容：

```
total 12
--- 1 mnesia msouk May 12 07:53 STATE_log
rw- 1 mnesia msouk June 22 07:53 SCHEMA.DAT
```
