
`A` 和 `B` 总线上显示的两个值的总和。这并不是 exhaustive 测试，但它确实让我们对 8 位加法器工作正常抱有希望。（如果你的结果与所示不符，你可能需要更改总线的方向。单击总线名称然后选择 Signal → Bus → Direction。由总线位表示的十六进制值将通过反转总线线的位顺序重新计算。对每个出现问题的总线执行此操作。）

加法器似乎工作正常。在为 XS95 板编译 3 位加法器之前，将以下约束放在 `ADD8_95.UCF` 文件中（注意每个构成总线的各个输入的索引周围添加了 `<...>`）：

```
NET CIN      LOC=P46;
NET A<0>      LOC=P47;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_139_0.png)

#### 图 4.18 8 位加法器仿真的波形。

```
NET A<1>      LOC=P48;
NET A<2>      LOC=P50;
NET B<0>      LOC=P51;
NET B<1>      LOC=P52;
NET B<2>      LOC=P81;
NET SUM<0>    LOC=P21; # LED segment S0
NET SUM<1>    LOC=P23; # LED segment S1
NET SUM<2>    LOC=P19; # LED segment S2
#### the following constraints assign unused ADDB terminals to out-of-the-way pins
NET COUT      LOC=P7;
NET A<3>      LOC=P75;
NET A<4>      LOC=P79;
NET A<5>      LOC=P82;
NET A<6>      LOC=P84;
NET A<7>      LOC=P1;
NET B<3>      LOC=P61;
NET B<4>      LOC=P55;
NET B<5>      LOC=P57;
NET B<6>      LOC=P58;
NET B<7>      LOC=P83;
NET SUM<3>    LOC=P2;
NET SUM<4>    LOC=P53;
NET SUM<5>    LOC=P56;
NET SUM<6>    LOC=P54;
NET SUM<7>    LOC=P6;
```

PC 的并行端口仅限于驱动 8 位加法器输入中的 8 个。我将一位分配给进位输入，`A` 和 `B` 总线各分配 3 位。剩余的 `A` 和 `B` 输入位被分配到 XS95 板上不会干扰的引脚上。（你可以手动将这些引脚接地，但不是必须的，因为它们只影响 `SUM` 输出的上位。）此外，LED 数码管段仅由 `SUM` 总线的低 3 位输出驱动。其余 `SUM` 位和进位输出被分配到其他不碍事的引脚。

在生成 bitstream 文件后，使用 Tools → Device Programming → JTAG Programmer 菜单项将其转换为存储在 `ADD8_95` 项目顶层目录中的 SVF。`ADD8_95.SVF` 文件构建完成后，将其下载到 XS95 板。然后你可以测试设计。`XSPORT` 命令的位分配如下：

| `XSPORT` 位 | 加法器输入 |
|---|---|
| `b0` | `CIN` |
| `b1` | `A0` |
| `b2` | `A1` |
| `b3` | `A2` |
| `b4` | `B0` |
| `b5` | `B1` |
| `b6` | `B2` |
| `b7` | ***未使用*** |

LED 段与和位分配如下：

| LED 段 | 和位 |
|---|---|
| `S0` | `SUM0` |
| `S1` | `SUM1` |
| `S2` | `SUM2` |
| `S3–S6` | ***未使用*** |

例如，要在没有进位输入（0）的情况下将 2（010）和 3（011）相加，你将发出命令：

```
C:\XCPROJ\ADD8_95\> XSPORT 0100110
```

然后你应期望结果为 5（101）。因此，7 段 LED 的左下段和底部段应亮起。

至此，你已使用 1 位加法器模块构建了 8 位加法器。你可以取出 8 位加法器，移除 `XSPT` 和 `OBUF`，并将其保存为 `MY_ADD8` 8 位加法器模块。`MY_ADD8` 模块可在设计中需要 8 位加法器的任何地方使用。比重新编码要省每次需要时添加一个。最终，你将建立一套在设计中经常使用的模块集合。这些模块在作用上类似于“零件柜”。事实上，原理图编辑器中 `SC` 符号窗口显示的零件列表就是如此。

### 面向 XS40 板的 8 位加法器

你可以以与为 XS95 板所做的方式相同的方式为 XS40 板构建一个 8 位加法器模块：创建 `MY_ADD1` 1 位加法器模块，然后复制它并添加连接以构建 8 位加法器。

但需要做一个修改。正如我们在偶校验生成器设计中所看到的，PC 并行端口的 8 个输出中有 2 个驱动 XS40 板上 XC4000XL FPGA 的专用输入。这意味着我们必须在原理图中使用特殊符号，因为将约束写入以将网络或终端分配给专用引脚是非法的。

8 位加法器由并行端口的 7 个输出驱动：一个用于进位输入，三个用于两个被加数的低位。这意味着我们至少需要使用一个专用引脚。在本例中，我将使用 `M0` 引脚。图 4.19 显示了对 8 位加法器布线进行以下修改后得到的电路：

1. 已移除 `BIB2` 到 `BIB` 总线的连接。
2. 一个新的输入缓冲器已连接到 `MY_ADD1` 1 位加法器模块的 `H3` 实例的 `B` 输入。
3. 新 `IBUF` 模块的输入由 `MD0` 符号驱动，该符号对应于来自专用 `M0` 引脚的输入。

这些修改的结果是，8 位加法器 `B` 输入的第三位现在由 `M0` 引脚上的值驱动，而不是来自 `B2` 总线位。因此，`B2` 位被分配到以下 `ADDB_40.UCF` 用户约束文件中的一个偏僻引脚：

```
NET CIN          LOC=P44;
NET A<0>          LOC=P45;
NET A<1>          LOC=P46;
NET A<2>          LOC=P47;
NET B<0>          LOC=P48;
NET B<1>          LOC=P49;
NET B<2>          LOC=P6;     # assign to some out-of-the-way pin
NET SUM<0>        LOC=P25;    # LED segment S0
NET SUM<1>        LOC=P26;    # LED segment S1
NET SUM<2>        LOC=P24;    # LED segment S2
#### the following constraints assign unused ADDB terminals to out-of-the-way pins
NET COUT          LOC=P7;
```

#### 图 4.19 XS40 为基础的 8 位加法器布线更改。

```
NET A<3> LOC=P78;
NET A<4> LOC=P79;
NET A<5> LOC=P82;
NET A<6> LOC=P84;
NET A<7> LOC=P3;
NET B<3> LOC=P5;
NET B<4> LOC=P60;
NET B<5> LOC=P56;
NET B<6> LOC=P58;
NET B<7> LOC=P59;
NET SUM<3> LOC=P83;
NET SUM<4> LOC=P4;
NET SUM<5> LOC=P50;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_142_0.png)

```
NET SUM<6>    LOC=P57;
NET SUM<7>    LOC=P51;
```

编译完 XC405XL FPGA 的设计后，加法器的配置位流可以像这样下载到 XS40 板中：

```
C:\XCPROJ\ADD8_40> XSLOAD ADD8_40.BIT
```

现在你可以用加法器进行实际测试。例如，要在进位输入设为 1 的情况下将 3 (011) 加 3 (011)，你将发出命令：

```
C:\XCPROJ\ADD8_95> XSPORT 0110111
```

然后你期望得到 7 (111) 的结果。因此，7 段 LED 的左下、右下和底部段应亮起。

### VHDL 中的 8 位加法器

在本节中，我们将使用 VHDL 和 Foundation 系列软件的 HDL 设计流程模式为 XS95 板和 XS40 板构建一个 8 位加法器。我们还将看到如何在 VHDL 中创建自己的零件库。

首先在 `XCPROJ-V` 目录中创建一个名为 `ADD8_95` 的 HDL 模式项目。然后打开一个 HDL 编辑器窗口并创建一个名为 `XSE.VHD` 的 VHDL 文件，该文件将保存供其他设计使用的组件库。目前，`XSE.VHD` 仅包含一个组件，即单一位全加法器（清单 4.5）。
