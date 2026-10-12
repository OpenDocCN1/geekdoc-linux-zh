
使用`Python`，您如下所示导入`ScriptForge`服务：

```
from scriptforge import \

    CreateScriptService
```

对于给定的文档，它将出现在图1的新文档中，以及一个以文件命名的独立文件夹中，只有在文档完成后才会。

关于`LibreOffice`的最后提示：默认情况下，`LibreOffice`宏拒绝运行您尝试的任何宏（或者在示例文档中找到）。您可以通过`工具 | 选项 | LibreOffice | 安全 | 宏安全`来调整安全级别和信任源。

要安装`APSO`，只需访问最新版本并添加到`LibreOffice`，按照说明操作。一旦安装了`APSO`，您将在`LibreOffice`菜单中看到`ScriptForge`：一个宏组织器，通过`Alt+Shift+F1`检测到`Python`。

## 宏与脚本

除了宏之外，`LibreOffice`的第三方使用“脚本”一词来运行`LibreOffice`代码以实现任务。您可能好奇两者之间的真实区别，或者难以找到一个简单的示例。从个人经验来看，对于所有实际用途，这两个概念没有区别，至少对于终端用户和初学者。

## ScriptForge 解决方案

从经验来看，`LibreOffice`宏和脚本非常有帮助。除了第三方教程，您还可以找到大量的官方文档，以及最常用的用户文档集[4]。这还展示了可能需要的脚本以及相应的`API`。

`Script`库提供了处理字符串、元素数组（例如表格中的单元格或文本文档中的列表）的`ScriptForge`服务示例，通过使用这些函数，您可以对数据进行排序、创建`CSV`表格或数据库，并使用正则表达式替换文本。

`ScriptForge`在三个部分中具有这些功能，如图5所示，您可以与图4进行比较：除了核心库和关联库（所有这些将由`ScriptForge`开发），以及由第三方提供的扩展。

## LibreOffice 中的 Python

在`LibreOffice` “原生”支持的四种语言中，我更倾向于使用`Python`，因为即使在`LibreOffice`之外我也经常使用它。由于`Python`的`LibreOffice`自动化，似乎在其他方面，核心库持有所有以下级别的代码：

- 运行宏……
- 编辑宏……
- 开发工具
- 扩展管理器……
- 自定义……
- 数字签名
- 引擎
- `XML`过滤器设置……

图3：`LibreOffice`的`APSO`扩展允许在运行`LibreOffice`时与`Python`代码交互。

当您的`LibreOffice`代码变得难以调试且耗费时间时，`ScriptForge`旨在让编写宏和脚本变得更容易。通过`ScriptForge`，您可以快速

`LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM`

第266期 2022年10月 39

## 使用 ScriptForge 的 LibreOffice 宏

## 入门

在篇文章中，我将重点介绍如何开始使用`ScriptForge`，通过展示如何将其加载并运行作为用户特定的宏，以及作为通用的（文档特定的）不带宏的基于`ScriptForge`的代码运行，因为后者的设置是最复杂的场景。

![](img/6816acb85ab93ecedbe75e6e9cb5d00d_39_0.png)

非常强大的编程环境：`LibreCalc`的数字处理和图表能力通过`Python`无穷尽的库和功能得以增强。当然，获取一个单元格进行编辑并不直接，但它展示了使用`ScriptForge`读写电子表格是多么简单（第5-7行）。与其在第6行使用解释器，你可以像第8行所示使用`Python`，将从网络获取的值赋值给变量，你也可以根据需要调用它。

数据结构、文件管理以及本地化处理问题。相关的库被分为三组，分别处理`LibreOffice`文件（文档）、用户对话框、电子表格和数据库。数据库可以访问`LibreOffice`内部或外部文件，通过`SQL`查询读取和写入记录。

你可以使用`ScriptForge`库编写这些宏。一旦你熟悉了这些宏，就可以使用它们在文档（例如工作表）和`Python`数据结构之间往回数据，以进行更复杂的处理。

考虑下面示例所示的基于`ScriptForge`的代码，这是一个从当前文档内容中读取标题并将其作为参数插入的宏。

## 运行 ScriptForge

现在我将展示`LibreOffice`如何识别并运行列表1中的代码，包括作为用户特定脚本和已启用的脚本。对于用户特定脚本，你应该打开你偏好的编辑器，复制代码

## 列表 1：示例 ScriptForge

```
01 from script import createScriptService
02 doc = createScriptService("Calc")
03 # get the current document
04 def increment_cell(args=None):
05 value = doc.getValue("A1")
06 value += 1
07 doc.SetValue("A1", value)
08 g_exportedScripts = (increment_cell, )
09 from scriptforge import createScriptService
10 bas = createScriptService("Basic")
11 bas.MsgBox("Hello!")
```
