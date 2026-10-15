
![](img/72fce958343eeb5d6d0322213ea85399_282_0.png)

- 6 使用 `sin` 设置 `_xscale`。
- 7 使用 `sin` 设置 `_rotation`。
- 8 进入测试环境。
- 9 测试你的电影。

注意：关于如何测试你的电影的说明，请参阅第 38 页。
电影剪辑将缩放并旋转。

## 使用调试器

修正错误——通常称为调试——是编写程序的正常部分。Flash 提供了许多工具来帮助调试。使用调试器显示加载的电影、片段、属性和实例。调试器允许你在电影运行时查看并调整属性和变量。然后你可以返回脚本并进行必要的更改。

## 调试操作

## 额外

调试器使用一个特殊版本的 Flash Player —— 调试播放器（Debug Player）——它会在你安装 Flash 5 时自动安装。要激活 Flash 调试器，点击 `Control ⌤ Debug` 模式。

你可以将 Flash 调试播放器作为独立播放器使用。如果你在发布设置对话框的选项卡中选择允许调试（Debugging Permitted），你可以在播放电影时使用调试器。只需点击 Flash 调试播放器菜单中的 `Control ⌤ Debugger` 即可。在使用 Flash 调试播放器配合调试器时，必须打开 Flash。你可能希望为你的电影设置密码，因为任何使用 Flash 调试播放器的人都能查看你的属性和变量设置。发布设置对话框的 Flash 选项卡提供了一个选项，允许你为调试器设置密码。

要向监视列表（Watch list）添加变量，选择该变量，点击调试器面板右上角的 `□` 添加“监视”（Add Watch）。要从监视列表中移除变量，选择该变量，点击 `□` 然后点击“移除监视”（Remove Watch）。

你可以从 Macromedia 网站下载最新版本的 Flash 调试器。随附的 CD-ROM 中包含该网站的链接。

![](img/72fce958343eeb5d6d0322213ea85399_284_0.png)

Olive 和翡绿 Pojo

Olive 和 Emerald

- 3 点击一个关卡或实例以选择它。
- 4 点击“属性”（Properties）选项卡以查看属性。
- 5 双击一个值并输入内容来更改属性。
- 6 点击“变量”（Variables）选项卡查看你的变量。
- 7 双击一个值来更改变量。
- 你可以使用调试器对你的电影进行故障排除。

## 使用输出窗口

输出窗口是测试环境的一部分。输出窗口显示帮助你排查电影故障的信息。如果你的电影中有语法错误，当你进入测试环境时，错误消息会自动显示。错误有助于定位脚本中的问题。

你可以使用 `trace` 动作来评估表达式。当你调试电影并需要知道表达式的返回值时，这非常有用。`trace` 动作的结果会显示在输出窗口中。`trace` 动作的语法为：

```
trace(expression);
```

使用参数 `expression` 来指定你想评估的表达式。例如，以下脚本每当用户点击按钮时都会增加 `x` 的值，并将结果发送到输出窗口：

```
(on release)

trace(++x);
```

输出窗口菜单提供了若干选项，允许将输出窗口的内容复制到剪贴板、清空输出窗口、将输出窗口的内容保存为文件或打印输出窗口的内容。选择“保存”（Save）允许你将输出内容保存为 TXT 或 OG 文件。

“选项”（Options）还允许你选择接收到的错误深度：从无（None）、错误（Errors）、警告（Warnings）和详细（Verbose）中选择。选择“无”将关闭错误显示。

你可以使用 `trace` 动作向任何使用测试环境的人显示消息。例如，`trace("hello")` 在输出窗口中显示 "hello"。

![](img/72fce958343eeb5d6d0322213ea85399_285_0.png)

## 使用 trace 动作

- 1. 选择要添加 ActionScript 的帧、按钮或电影。
- 2. 使用 `trace` 动作评估表达式。
- 3. 移动到测试环境。

注意：此示例使用了 `trace.fa` 文件，你可以在随书附的 CD-ROM 中找到它。

## 额外

这里显示的脚本使用 `trace` 动作来显示数组的变化。

```
Script:

on (release)

name = ["George", "John", "James"];

trace(name);

name[1] = "Chris";

trace(name);

name.push("Gene", "Charles", "Sue");

trace(name);
```

第一次 Trace 的结果：
George,John,James

第二次 Trace 的结果：
George,Chris,James

第三次 Trace 的结果：
George,Chris,James, Gene,Charles, Sue

![](img/72fce958343eeb5d6d0322213ea85399_286_0.png)

- 6 点击按钮测试你的电影。
- 每当你点击一次时，输出窗口都会显示 trace 的结果。

## 选项菜单

- 1 点击“选项”（Options）打开选项菜单。
- 2. 选择一个选项。

- 你可以使用选项将输出窗口的内容复制到剪贴板、清空输出窗口、将输出窗口的内容保存为文件或打印输出窗口的内容。

## FLASH ACTIONCRIPT

## 使用列表对象

在测试环境中，你可以使用菜单选择 `Debug`（调试）-> `List Objects`（列表对象），在输出窗口中显示当前帧的关卡、对象类型和目标路径。对象类型包括电影剪辑（movie clip）、文本（text）和按钮（button）。当你想要查找目标路径或文本字段的赋值时，列表对象菜单非常有用。

当你使用 `Debug -> List Objects` 时，输出窗口不会随调试器自动更新。你每次想要获取信息时必须选择该菜单。

## 额外

以下是选择 `Debug -> List Objects` 菜单的输出示例。

```
Example:

Level #0: Frame=1

Edit Text: Variable=level0.titleV

Text:

Movie Clip: Frame=1

Target=level0.Olive

Shape:

Movie Clip: Frame=1

Target=level0.Emerald

Shape:

Button:

Shape:

Edit Text: Variable=StartMoviex
```
