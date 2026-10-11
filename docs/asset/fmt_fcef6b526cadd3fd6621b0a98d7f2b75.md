
- 19.17 编写一个程序，从用户处输入整数并判断其是否为素数。如果不是素数，显示其唯一的质因数。记住，素数的因数只有 1 和素数本身。每个非素数都有唯一的质因数分解。例如，考虑数字 54。54 的质因数是 2、3 和 3。当这些值相乘时，结果是 54。对于数字 54，

- 19.18 使用数组作为 List 来显示元素。

- 19.19 使用数组作为 List 来显示元素。

- 19.20 使用数组作为 List 来显示元素。

# Applet 简介

## 目标

在本章中你将学习：

- 区分 applet 和应用程序。
- 通过 JDK 观察一些有趣的 Java 特性。
- 编写简单的 applet。
- 编写超文本标记语言（HTML）文档将 applet 加载到 applet 容器中。
- 生命周期内自动调用的五个方法。

## 20.1 引言

### 20.1 JDK 提供的示例 Applet

### 20.2 简单 Applet：绘图

#### 20.3.1 在 appletviewer 中执行 applet

#### 20.3.2 在网络浏览器中执行 applet

#### 20.4 Applet 生命周期

#### 20.5 使用方法初始化实例变量

#### 20.6 沙盒安全模型

#### 20.7 互联网和网络资源

#### 20.8 结语

总结 | 术语 | 自测练习题 | 自测练习题答案 | 练习题

# 第 20 章 Java Applet 简介

更新指定的位置以反映您选择的安装目录和磁盘驱动器，或不同版本的 JDK。

如果您使用的 Java 开发工具未带 Java 演示（demos），可以从 Sun Microsystems 网站 `java.sun.com/javase/6/` 下载（带演示的 JDK）。

## 井井棋（TicTacToe）Applet

TicTacToe 演示 applet 允许您与电脑进行井井棋游戏。要执行此 applet，请打开命令窗口并切换到 JDK 的 demo 目录。

demo 目录包含多个子目录。您可以通过在 Windows 上执行 `dir` 命令或在 UNIX/Linux/Max OS X 上执行 `ls` 命令来列出它们。我们讨论了 `applets` 和 `j` 目录中的示例程序。`jfc` (Java Foundation Classes) 目录包含了演示 Java 图形和 GUI 特性的 applet 和应用程序。

切换到 `applets` 目录并列出其内容以查看演示 applet 的目录名称。图 20.1 提供了每个示例 applet 的简要描述。如果您的浏览器支持 Java，您可以在浏览器中打开站点 `java.sun.com/javase/6/docs/technotes/samples/demos.html` 并点击“Applets Page”链接来测试这些 applet。我们将通过命令窗口中的 `appletviewer` 命令来演示这些 applet。

| 名称 | 描述 |
| :--- | :--- |
| Animator | 执行四种不同的动画。 |
| ArcTest | 演示绘制弧。您可以与 applet 交互以更改显示的弧属性。 |
| BarChart | 绘制简单的条形图。 |
| Blink | 显示不同颜色的色的文本。 |
| CardTest | 演示多个 GUI 组件和布局。 |
| Clock | 绘制带有旋转指针、当前日期和时间的钟。时钟每秒更新一次。 |
| DitherTest | 演示一种名为抖动（dithering）的图形技术，允许颜色从一种逐渐变为另一种。 |
| DrawTest | 允许用户通过拖动鼠标绘制不同颜色的线条和点。 |
| Fractal | 绘制分形。分形的显示通常需要复杂的计算。 |
| GraphicsTest | 绘制形状以说明图形能力。 |
| **图 20.1** | applets 目录中的示例。（第 1/2） |

## 20.2 JDK 提供的示例 Applet

94

| 名称 | 描述 |
| :--- | :--- |
| GridLayout | 绘制由线条连接的许多节点（用矩形表示）的图。拖动节点调整屏幕上的其他节点并演示复杂的交互。 |
| ImageMap | 演示带有热点的图像。将鼠标指针悬停在图像的某些区域会高亮该区域并在 applet 容器的左下角显示消息。点击图像处听 applet 说“hi”。 |
| JumpingBox | 让矩形在屏幕上随机移动。尝试用鼠标点击它！ |
| MoleculeViewer | 提供多个化学分子的三维视图。拖动鼠标从不同角度查看。 |
| NervousText | 绘制在 applet 中跳动的文本。 |
| SimpleGraph | 绘制复杂的曲线。 |
| SortDemo | 比较三种排序技术。排序（第 16 章中描述）对信息进行排序——如字母排序。当您从窗口执行此示例时，会出现三个 appletviewer 窗口。当您在浏览器中执行此示例时，三个演示并排出现。点击每个演示开始排序。注意排序以不同的速度运行。 |
| StyleSheet | 演示简单的行和列表格。 |
| TicTacToe | 允许用户与电脑玩井井棋。 |
| WireFrame | 绘制作为线框的三维形状。拖动鼠标从不同角度查看形状。 |
| **图 20.1** | applets 目录中的示例。（第 2/2。） |

切换到 `TicTacToe` 子目录，您将找到用于执行 applet 的 `example1.html` HTML 文件。在命令窗口中，使用命令

```
appletviewer example1.html
```

并按回车。这执行了 appletviewer applet 容器，它加载了作为命令行参数的 `example1.html` HTML 文件。appletviewer 确定加载文档并执行 applet。图 20.2 显示了使用此 applet 玩井井棋的截图。

您是 X 玩家。与 applet 交互：将鼠标指向想要放置 X 的方格并点击鼠标按钮。applet 会播放声音；如果方格已被占用，则这是一个无效移动，applet 会播放不同的声音指示您无法执行该移动。在您移动后，applet 通过做出自己的移动做出响应。

# 第 20 章 Java Applet 简介

![](img/1df0d1e8ac007b95647eb8ea3839af_987_0.png)

图 20.2 | TicTacToe applet 示例执行。

再次玩，点击 appletviewer 的 Applet 菜单并选择“Reload”项（图 20.3）。要关闭 appletviewer，点击 appletviewer 的 Applet 菜单并选择“Quit”项。

![](img/1df0d1e8ac007b95647eb8ea3839af_987_1.png)

图 20.3 | Applet 菜单。

再次玩，点击 appletviewer 的 Applet 菜单并选择“Reload”项（图 20.3）。要关闭 appletviewer，点击 appletviewer 的 Applet 菜单并选择“Quit”项。

切换到 `TicTacToe` 子目录，您将找到用于执行 applet 的 `example1.html` HTML 文件。在命令窗口中，使用命令

```
appletviewer example1.html
```

并按回车。这执行了 appletviewer applet 容器，它加载了作为命令行参数的 `example1.html` HTML 文件。appletviewer 确定加载文档并执行 applet。图 20.2 显示了使用此 applet 玩井井棋的多个截图。

DrawTest 允许用户通过拖动鼠标绘制不同颜色的线条和点。

## 20.2 JDK 提供的示例 Applet

![](img/1df0d1e8ac007b95647eb8ea3839af_988_0.png)

图 20.4 | DrawTest applet 示例执行。

DrawTest 允许用户通过拖动鼠标绘制不同颜色的线条和点。

您是 X 玩家。与 applet 交互：将鼠标指向想要放置 X 的方格并点击鼠标按钮。applet 会播放声音；如果方格已被占用，则这是一个无效移动，applet 会播放不同的声音指示您无法执行该移动。在您移动后，applet 通过做出自己的移动做出响应。

SortDemo 比较三种排序技术。排序（第 16 章中描述）对信息进行排序——如字母排序。当您从窗口执行此示例时，会出现三个 appletviewer 窗口。当您在浏览器中执行此示例时，三个演示并排出现。点击每个演示开始排序。注意排序以不同的速度运行。

## 20.3 简单 Java Applet：绘制字符串

每个 Java applet 都是一个图形用户界面，您可以在其上使用 11 章引入的技术放置 GUI 组件，或使用第 12 章演示的技巧进行绘制。在本章中，我们将演示如何在 applet 上进行绘制。

### 20.3 简单的 Java Applet: 绘制字符串
