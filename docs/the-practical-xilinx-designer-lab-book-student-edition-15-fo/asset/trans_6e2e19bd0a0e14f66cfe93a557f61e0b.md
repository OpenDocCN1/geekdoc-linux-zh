

Figure 4.6 将偶校验生成器符号连接到 I/O 引脚。

Figure 4.7 选择用于仿真的引脚。

the parity generator for all possible input combinations. The waveforms should resemble those of Figure 4.3.

在编译设计之前，将以下约束放置在 EVPAR_40.UCF 约束文件中：

```
NET B0    LOC=P44;
NET B1    LOC=P45;
NET B2    LOC=P46;
NET B3    LOC=P47;
NET B4    LOC=P48;
NET B5    LOC=P49;
# NET B6  LOC=P32;
# NET B7  LOC=P34;
NET ODD   LOC=P25;# LED segment SO
```

B6 和 B7 输入的约束被注释掉了，因此它们没有效果（我只是把它们留在那里，以免忘记这些输入仍在使用）。另请注意，所有输入和输出名称都已转换为大写，因为原理图中的 I/O 端子始终具有大写名称。

使用上面显示的用户约束文件编译偶校验生成器后，我们可以打开 Place&Route 报告文件并找到以下信息：

| Device utilization summary: |
| IO | 7/112 | 6% used |
|  | 7/61 | 11% bonded |
| LOGIC | 1/196 | 0% used |
| SPECIAL | 2/1167 | 0% used |
| IOB | 7/112 | 6% used |
| CLB | 1/196 | 0% used |
| MODE0 | 1/1 | 100% used |
| MODE2 | 1/1 | 100% used |

最后两行表明我们成功尝试将 M0 和 M2 专用引脚用作输入。

偶校验生成器的配置位流可以像这样下载到 XS40 板中：

```
C:\XCPROJ\EVPAR_40> XSLOAD EVPAR_40.BIT
```

现在你可以对校验生成器进行实际测试。例如，命令

C:\XCPROJ\EVPAR_40> XSPORT 00101100

将点亮 7 段 LED 的 S0 段，因为输入模式包含奇数个 1 位。另一方面，命令

C:\XCPROJ\EVPAR_40> XSPORT 10110001

将熄灭 S0 段，因为输入模式包含偶数个 1 位。

## 用于 X595 板的 8 位加法器

加法是经常使用的操作，因此定义一个可以在其他设计中使用的加法器模块是有意义的。我们可以使用上一章中的 1 位加法器模块来构建更大的加法器。由 1 位加法器模块构建 8 位加法器所需的连接如图 4.8 所示。唯一剩下的问题是程序性的：我们如何使用 Foundation Series 原理图编辑器制作 1 位加法器模块并将它们连接在一起？

![](img/5124daf79d2807d81e49f49c22f1f8c1_130_0.png)

Figure 4.8
使用 8 个 1 位加法器模块构建 8 位加法器模块。

让我们开始为 XC95108 CPLD 创建 ADD8_95 原理图模式项目。然后，使用 Document → Add 菜单项添加 C:\XCPROJ\ADD1_95\ADD1.SCH 原理图文件（见图 3.13）到当前项目。双击原理图名称以打开它。1 位加法器原理图显示后，按如下方式编辑它：

- 1. 双击 INPUT0 端子。当 I/O Terminal 窗口出现时，将端子的名称更改为 A。按照相同的方法将 INPUT1 更改为 B，将 CARRY_INPUT 更改为 CIN，并将 CARRY_OUTPUT

更改为 COUT 更短的名称在我们使用这些模块构建更大的加法器时显示起来会更容易。

- 2. 用一根将输入连接到输出的导线绕过每个 IBUF 和 OBUF 缓冲器。

- 3. 删除 IBUF 和 OBUF 缓冲器。由于我们将把 1 位加法器封装成一个模块，因此模块的 I/O 不一定需要连接到 CPLD 的引脚。请注意，如果你没有将缓冲器的输入连接到其输出，I/O 端子将随缓冲器一起消失。这就是之前步骤的原因。

完成所有这些步骤后，你的原理图应如下图 4.9 所示。接下来，我们必须创建一个符号来表示 1 位加法器，以便在其他原理图中使用它。为此，选择 Hierarchy → Create Macro Symbol from Current Sheet 菜单项。将出现如图 4.10 所示的 Create Symbol 窗口。在 Symbol Name 字段中输入你想要引用的 1 位加法器模块的名称（我选择了 MY_ADD1，但你可能想要更有创意）。你还可以输入一句话到 Comment 字段以引用此模块的功能。然后单击 OK。然后你会收到 MY_ADD1 已添加到符号列表中的通知，并被问及是否要修改 MY_ADD1 的符号。只需单击 No。

![](img/5124daf79d2807d81e49f49c22f1f8c1_131_0.png)

Figure 4.9 ADD1.SCH 修改为封装成模块（与图 3.13 对比）。

