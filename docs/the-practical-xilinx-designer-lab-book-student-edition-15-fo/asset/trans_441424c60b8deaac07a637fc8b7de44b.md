
要添加电路的输出，请单击 New（新建），在 Name（名称）字段中输入 Hwy3，然后选择 Output（输出）单选按钮。接着单击 Advanced（高级）按钮，打开 Advanced Port Settings（高级端口设置）窗口。单击 Combinatorial（组合）单选按钮，再单击 OK（确定）按钮。现在所有输入和输出都已定义，单击 Finish（完成）按钮即可。

此时，将出现一个 HDL 编辑器窗口（图 2.13），其中包含 Trip-Genie 逻辑的框架。你应该会在文件顶部看到模块名称和标题。接下来是输入引脚以及我们之前添加的一个组合输出引脚的声明。再往文件下方，是专门用于逻辑方程的部分。我们只需输入上一章中为 Hwy3 输出推导出的布尔方程。该方程输入在第 17 行和第 18 行，如下所示：

```
Hwy3 = (Hootersville & !Mayberry # (Hootersville & Mayberry) & (SilerCity & !MtPilot);
```

我们使用 ABEL 运算符来表示以下布尔运算：

| 布尔运算 | ABEL 运算符 |
|---|---|
| 与（AND） | & |
| 或（OR） | # |
| 非（NOT） | ! |

现在我们需要检查一下，以确保没有犯下简单的错误。选择 Synthesis → Check Syntax 菜单项。此时会弹出一个小窗口，提示正在检查 ABEL 代码中是否存在错误。几秒钟后，该窗口会被另一个显示 Check Successful（检查成功）的窗口取代。单击此窗口中的 OK（确定）按钮。

（当你第一次开始使用 ABEL 设计自己的电路时，很可能会遇到语法错误。每个错误都会在 HDL 编辑器窗口中高亮显示，错误信息会出现在窗口底部。通过选择 Tools → Language Assistant 菜单项，可以获得无错误的 ABEL 代码示例。此时会出现一个 Language Assistant-ABEL 窗口，左侧列出主题。单击 + 符号可逐级展开到特定主题。单击某个主题后，该主题的 ABEL 代码示例就会出现在窗口右侧。你可以将示例剪切并粘贴到自己的代码中，然后针对自己的特定设计进行编辑。）

一旦确认没有语法错误，我们就可以从 ABEL 代码生成网表。网表是将 ABEL 代码提炼为一组逻辑门以及它们之间连接的结果。首先，单击 Synthesis → Options... 菜单项。在出现的 ABEL6 窗口中，单击 Chip（芯片）单选按钮，然后点击 OK（确定）。这将指示综合器创建一个网表

![](img/5124daf79d2807d81e49f49c22f1f8c1_49_0.png)

## 图 2.13 已填入 Trip-Genie ABEL 代码框架的 HDL 编辑器窗口。

用于独立设计。（Macro（宏）单选按钮用于 ABEL 代码所描述的电路被用作更大设计的一部分时。）然后点击 Synthesis → Synthesize 菜单项，开始编译过程。此时会出现一个小弹出窗口，提示 ABEL 代码正在被综合。不到一分钟，该窗口就会被另一个显示 Synthesis Successful（综合成功）的窗口取代。单击此窗口中的 OK（确定）按钮。现在，Trip-Genie 的 Hwy3 输出的网表已经生成。

设计输入现已完成，请在 HDL 编辑器窗口中选择 File → Save。然后选择 File → Exit。

返回 Project Manager 窗口后，我们必须将 TRIP-GENI.ABL 文件纳入项目。选择 Document → Add... 菜单项，并在对话框窗口中列出类型为 ABEL (*.ABL)¹ 的项。选中 TRIPGENI.ABL 并单击 Open（打开）。然后你应该会在组成 TRIPGENI 项目的文件列表中找到 TRIPGENI.ABL（图 2.14）。

1. 如果你想避免重新输入所有内容，可以从随书附带的 CD-ROM 中获取本书的所有设计示例。

![](img/5124daf79d2807d81e49f49c22f1f8c1_50_0.png)

## 图 2.14 将 TRIPGENI.ABL 文件添加到 TRIPG_95 项目后的 Project Manager 窗口。

## 使用原理图编辑器输入设计

在本节中，我将向你展示如何使用原理图编辑器输入 Trip-Genie 的 Hwy3 输出设计。（如果你已经使用 ABEL 文件描述了设计，可以跳过本节。这个基于原理图的设计针对的是 XC4000XL FPGA，因此你会在 TRIPG_40 项目中找到它。）在 Project Manager 窗口中，选择 Tools → Design Entry → Schematic Editor...（或单击 Project Manager 窗口的 Flow（流程）选项卡中的按钮），此时会出现一个原理图编辑器窗口。然后使用 File → Save As... 菜单项将原理图命名为 TRIPGENI.SCH。

我们需要做的第一件事是为 Hwy3 电路添加门电路。选择 Mode → Symbols 菜单项（或单击该按钮），屏幕会出现 SC Symbols 窗口，其中列出我们可以使用的所有组件类型。我们
