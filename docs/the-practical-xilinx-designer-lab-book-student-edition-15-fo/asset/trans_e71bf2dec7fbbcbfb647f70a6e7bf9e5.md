

每次需要时添加一个。最终，你将建立一套在设计中经常使用的模块集合。这些模块在作用上类似于“零件柜”。事实上，原理图编辑器中 SC 符号窗口显示的零件列表就是如此。

## 面向 XS40 板的 8 位加法器

你可以以与为 XS95 板所做的方式相同的方式为 XS40 板构建一个 8 位加法器模块：创建 MY_ADD1 1 位加法器模块，然后复制它并添加连接以构建 8 位加法器。

但需要做一个修改。正如我们在偶校验生成器设计中所看到的，PC 并行端口的 8 个输出中有 2 个驱动 XS40 板上 XC4000XL FPGA 的专用输入。这意味着我们必须在原理图中使用特殊符号，因为将约束写入以将网络或终端分配给专用引脚是非法的。

8 位加法器由并行端口的 7 个输出驱动：一个用于进位输入，三个用于两个被加数的低位。这意味着我们至少需要使用一个专用引脚。在本例中，我将使用 M0 引脚。图 4.19 显示了对 8 位加法器布线进行以下修改后得到的电路：

- 1. 已移除 BIB2 到 BIB 总线的连接。
- 2. 一个新的输入缓冲器已连接到 MY_ADD1 1 位加法器模块的 H3 实例的 B 输入。
- 3. 新 IBUF 模块的输入由 MD0 符号驱动，该符号对应于来自专用 M0 引脚的输入。

这些修改的结果是，8 位加法器 B 输入的第三位现在由 M0 引脚上的值驱动，而不是来自 B2 总线位。因此，B2 位被分配到以下 ADDB_40.UCF 用户约束文件中的一个偏僻引脚：

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
# the following constraints assign unused ADDB terminals to out-of-the-way pins
NET COUT          LOC=P7;
```

### 图 4.19 XS40 为基础的 8 位加法器布线更改。

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

## VHDL 中的 8 位加法器

在本节中，我们将使用 VHDL 和 Foundation 系列软件的 HDL 设计流程模式为 XS95 板和 XS40 板构建一个 8 位加法器。我们还将看到如何在 VHDL 中创建自己的零件库。

首先在 XCPROJ-V 目录中创建一个名为 ADD8_95 的 HDL 模式项目。然后打开一个 HDL 编辑器窗口并创建一个名为 XSE.VHD 的 VHDL 文件，该文件将保存供其他设计使用的组件库。目前，XSE.VHD 仅包含一个组件，即单一位全加法器（清单 4.5）。

XSE.VHD 文件的底部部分（第 21 行至第 42 行）只是我们在第 3 章中完成的 fulladd 设计的 ENTITY 和 ARCHITECTURE 部分。此文件中唯一的新的特性是第 8 行至第 19 行的 PACKAGE 声明部分。PACKAGE 关键字之后是我们选择的包名（adder），随后是一个 COMPONENT 语句，声明了 fulladd 模块的接口。此 COMPONENT 语句的形式与我们在 EVPAR.VHD 文件中所有模块都在同一文件中声明时所使用的形式完全相同。如果我们想将多个模块放入 adder 包中，那么我们在 PACKAGE 部分中将有多个 COMPONENT 语句。

