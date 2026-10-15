
```
001- -- LED Blanking (LEDBLANK.VHD)
002-
003- LIBRARY IEEE,xse;
004- USE IEEE.std_logic_1164.ALL;
005- USE xse.led.ALL;
006-
007- ENTITY ledblank IS
008- PORT
009- (
010- d: IN STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit hex value
011- blank: IN STD_LOGIC; -- active-high blanking input
012- s: OUT STD_LOGIC_VECTOR (6 DOWNTO 0) -- drivers for LED
013- );
014- END ledblank;
015-
016- ARCHITECTURE ledblank_arch OF ledblank IS
017- SIGNAL tmp: STD_LOGIC_VECTOR (6 DOWNTO 0);
018- BEGIN
019- u0: leddcd PORT MAP(d=>d,s=>tmp);
020- s<=tmp WHEN blank='1' ELSE "ZZZZZZZ";
021- END ledblank_arch;
```

`LEDBLANK.VHD` 和 `XSE.VHD` 文件放置在 `XCPROJ-V` 目录中的 `BLANK_95` 和 `BLANK_40` HDL 模式项目中。将 `LEDBLANK.VHD` 文件添加到项目中，并在项目中创建一个新库并将 `XSE.VHD` 添加到其中。然后如果目标是 `XS40` 板，请将以下约束放入 `BLANK_40.UCF` 文件中：

```
NET D<0> LOC=P44;
NET D<1> LOC=P45;
NET D<2> LOC=P46;
NET D<3> LOC=P47;
NET BLANK LOC=P48;
NET S<0> LOC=P25;
NET S<1> LOC=P26;
NET S<2> LOC=P24;
NET S<3> LOC=P20;
NET S<4> LOC=P23;
NET S<5> LOC=P18;
NET S<6> LOC=P19;
```

#### Listing 5.3 来自 `XSE.VHDL` 库 VHDL 源代码的 `led` 包和 `LED` 解码器模块描述。 (续。)

```
042-  "0101111" WHEN "1011",
043-  "1100101" WHEN "1100",
044-  "0011111" WHEN "1101",
045-  "1101101" WHEN "1110",
046-  "1101100" WHEN "1111",
047-  "0000000" WHEN OTHERS;
048- END ledcd_arch;
```

或者如果要使用 `XS95` 板，请将这些约束放入 `BLANK_95.UCF` 文件中：

```
NET D<0>        LOC=P46;
NET D<1>        LOC=P47;
NET D<2>        LOC=P48;
NET D<3>        LOC=P50;
NET BLANK       LOC=P51;
NET S<0>        LOC=P21;
NET S<1>        LOC=P23;
NET S<2>        LOC=P19;
NET S<3>        LOC=P17;
NET S<4>        LOC=P18;
NET S<5>        LOC=P14;
NET S<6>        LOC=P15;
```

设计编译完成后，可以将其下载到 `XS40` 板：

```
C:\XCPROJ_V\BLANK_40> XSLOAD BLANK_40.BIT
```

或者编译设计，创建 `SVF` 文件，并下载到 `XS95` 板：

```
C:\XCPROJ-V\BLANK_95> XSLOAD BLANK_95.SVF
```

下载完成后，以下 `XSPORT` 参数与电路输入之间的映射生效：

| XSPORT Bit | LED Decoder Input |

|---|---|

| $b_0$ | D<0> |

| $b_1$ | D<1> |

| $b_2$ | D<2> |

| $b_3$ | D<3> |

| $b_4$ | BLANK |

| $b_5$–$b_7$ | *** Not Used *** |

以下命令将测试消隐电路：

```text
C:\XCPROJ-V\BLANK_40> XSPORT 00110
C:\XCPROJ-V\BLANK_40> XSPORT 10110
```

第一个命令应在七段 `LED` 上显示数字 6。第二个命令将禁用所有驱动器并熄灭 `LED` 段。

### Measuring Gate Delay

图 5.12 显示了一个简单的电路 `DELAY`，用于演示门延迟。当 `INP` 转换到逻辑 0 值时，输出应在 1 个门延迟后变为逻辑 0。然后当 `INP` 回升到逻辑 1 时，`OUT1` 将在 1 个门延迟后变高。这会在第二个与门的两个输入上放置逻辑 1，因此 `OUT2` 将在 `OUT1` 之后 1 个门延迟变高。并且 `OUT3` 将在另一个门延迟后变为逻辑 1，其后 `OUT4` 再延迟 1 个门延迟。

![](img/5124daf79d2807d81e49f49c22f1f8c1_172_0.png)

**Figure 5.12** A simple circuit for demonstrating propagation delay.

请注意附着在每个输入和输出端子上的小方框。这些是探针，它们监视所附着的网络或端子，并将逻辑值发送到模拟器中的波形查看器窗口。它们是按如下方式添加的：

- 1. 在 **Schematic Capture** 窗口中选择 **Mode → Test Points** 菜单项。

- 2. 单击要在模拟器的 **Waveform Viewer** 窗口中显示的每个网络或端子。

一旦探针被添加到原理图中，信号将在我们启动模拟器后立即出现在波形查看器窗口中。

`DELAY` 电路的功能仿真并不很有趣 - 输出 `OUT4..OUT1` 与 `INP` 输入完全同步移动！为了看到门延迟的影响，请单击逻辑模拟器窗口工具栏中仿真模式的下拉菜单并选择 `Unit` 而不是 `Functional`。这将模拟器置于单位延迟模式，其中门的输出在输入变化后 1 个时间单位发生变化。

但一个门延迟有多长？这由模拟器算法使用的仿真精度决定。仿真精度是两个非同时信号转换之间最小的时间增量。您可以通过在逻辑模拟器窗口中选择 `Options → Preferences...` 菜单项来设置精度。在出现的首选项窗口中（图 5.13），在 `Simulation` 选项卡的 `Simulation Precision` 框中输入所需的精度。我在这个示例中选择了 1 纳秒。我还将 `B0` 激励器的周期设置为 10 纳秒，并将激励器的 `B2` 位连接到 `INP` 输入。这意味着 `DELAY` 电路的输入每二十纳秒变化一次，这为输出在输入再次变化之前稳定提供了充足的时间。

![](img/5124daf79d2807d81e49f49c22f1f8c1_173_0.png)

Figure 5.13 Setting the simulation precision.

一旦仿真精度和输入激励器设置好，我们就可以仿真设计并查看单位门延迟的效果。结果如图 5.14 所示。正如预期的那样，在上升转换时输出各自偏移 1 个门延迟，而在负向转换时它们同时下降。但请注意 `OUT1` 在信号转换后变化 3 ns（即 3 个门延迟）

position on the `INP` input. The 2 additional gate delays arise from the delays incurred by going through the input and output buffers.

![](img/5124daf79d2807d81e49f49c22f1f8c1_174_0.png)

#### Figure 5.14 Simulated waveforms for the DELAY circuit with unit gate delays.

The actual circuit delays in the `DELAY` circuit cannot be tested from your PC keyboard or observed using the `LED` digit. Instead, you have to drive the input with the oscillator on the `XS40` or `XS95` Boards and observe the outputs with a dual-trace oscilloscope. Use the following pin assignments for the `XS40` Board:
