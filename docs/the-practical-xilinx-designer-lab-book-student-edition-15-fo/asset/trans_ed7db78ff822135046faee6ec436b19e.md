

（不幸的是，XC9500 系列 CPLD 不提供将宏单元用作逻辑或存储器的选项。因此，本节内容与使用 XS95 板的用户无关。抱歉。）

清单 8.5 显示了一些使用由两个 16x2 内置 RAM 构成的 RAM16X4 RAM 模块的 VHDL 代码。该模块的 COMPONENT 声明在第 20-28 行，是通过查看 Xilinx\Synth\xilinx\macros\Xc4000e\v6_xnf 目录下的 RAM16X4.V6X 文件确定的。RAM 模块具有 4 位输入和输出总线、4 位地址总线，以及一个高电平有效的写使能输入。

RAM 模块在第 52-58 行被实例化。由于我们只构建一个 4x4 存储器，因此只需要两个地址位。因此，在第 54 行，模块的下两个地址输入连接到地址总线。由于不需要，上两个地址位连接到在第 49 行保持逻辑 0 的 gnd 信号。

由于我们针对的是 XS40 板，因此需要从 XC4005XL FPGA 的模式引脚获取部分输入。这在第 43-46 行完成。从模式引脚输入的信号与 2 位输入总线连接起来形成 4 位 inb 总线。inb 总线在第 55 行连接到 RAM 模块。RAM 模块的剩余输出和写使能端口连接到 mem3 设计中的对应信号（第 56 行和第 57 行）。

图 8.21 显示了 MEM3 设计的仿真波形。对存储器进行了四次写入，通过施加地址和数据值，然后在 WE 输入上放置一个正脉冲。在 0-110 ns 的间隔内，十六进制值 0xC、0x3、0x5 和 0xA 分别写入存储器位置 0、1、2 和 3。然后在 120 ns 到 160 ns 之间将这些值读回这些位置。从每个位置读出的值与写入其中的数据相匹配，因此存储器似乎工作正常。

MEM3 设计的用户约束文件如下：

```
NET we              LOC=P44;    # B0 argument of XSPORT
# NET NE oe          LOC=P45;    # OE is not used with the internal memories
NET a<0>             LOC=P46;    # B2 argument of XSPORT
NET a<1>             LOC=P47;    # B3 argument of XSPORT
NET inpc<0>          LOC=P48;    # B4 argument of XSPORT
NET inpc<1>          LOC=P49;    # B5 argument of XSPORT
# NET inpc<2>         LOC=P32;    # B6 argument of XSPORT
# NET inpc<3>         LOC=P34;    # B7 argument of XSPORT
NET s<0>             LOC=P25;    # S0 LED segment
NET s<1>             LOC=P26;    # S1 LED segment
NET s<2>             LOC=P24;    # S2 LED segment
NET s<3>             LOC=P20;    # S3 LED segment
NET s<4>             LOC=P23;    # S4 LED segment
```

## 清单 8.5 使用内置 FPGA 存储器构建的 4 位宽异步存储器的 VHDL 版本。（续。）

```
042- u0: md0 PORT MAP (MD0=>MD0in); -- connect the mode inputs to
043- u0: md2 PORT MAP (MD2=>MD2in); -- the bus feeding the RAM module
044- u2: IBuf PORT MAP (I=>MD0in, O=>MD0out);
045- u3: IBuf PORT MAP (I=>MD2in, O=>MD2out);
046- inb <= MD2out & MD0out & inp(1 DOWNTO 0); -- concatenate bits into bus
047-
048- gnd <= '0'; -- connect signal to logic 0;
049-
050- -- connect the RAM16X4 component I/O to the I/O of this module
051- u4: ram16x4 PORT MAP
052-       (
053-         A0=>a(0), A1=>a(1), A2=>gnd, A3=>gnd,       -- connect address bus
054-         D0=>inb(0), D1=>inb(1), D2=>inb(2), D3=>inb(3), -- connect input bus
055-         Q0=>o(0), Q1=>o(1), Q2=>o(2), Q3=>o(3),    -- connect output bus
056-         WE=>we                                          -- connect write-enable
057-       );
058-
059- u5: ledcdcd PORT MAP (d=>o, s=>s); -- show output hex digit on LED
060- END mem3_arch;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_307_0.png)

**图 8.21** 使用 XC4005XL FPGA 的内置异步存储器的 VHDL 设计的仿真。

```
NET s<5>    LOC=P18;  # S5 LED segment
NET s<6>    LOC=P19;  # S6 LED segment
```

使用此存储器可以执行的操作与我们使用 D 触发器构建的异步存储器非常相似（只是写使能被反转）：

| 操作 | XSPORT 命令序列 |
|---|---|
| 写入位置 1 (01) 的值 7 (0111) | XSPORT 01110110<br>XSPORT 01110111<br>XSPORT 01110110 |
| 写入位置 3 (11) 的值 10 (1010) | XSPORT 10101110<br>XSPORT 10101111<br>XSPORT 10101110 |
| 读取位置 0 (00) | XSPORT 0010 |
| 读取位置 2 (10) | XSPORT 1010 |

除了异步 RAM 之外，XC4000 系列还提供同步 RAM 和双端口 RAM。图 8.22 给出了在原理图中使用的内部 16×2 双端口同步 RAM 的示例。RAM 是通过从原理图编辑器的 SC Symbols 窗口中选择 RAM16x2D 符号实例化的。它配备了一个正常的地址总线（A3..A0），该总线控制使用 INP0..INP0 输入总线和 SP01..SP00 输出总线分别写入或读取哪个存储器位置。此外，还提供了一个只读的第二端口，可让你通过 DPRA3..DPRA0 输入地址，并通过输出总线 DPO1..DPO0 读取存储器位置的内容。（PC 并行端口没有足够的引脚来驱动所有这些地址位，因此在原理图中每个地址的上两个位都连接到地。）

MEM4 设计的约束文件如下。注意，存储器的每个 2 位输出端口都连接到一对唯一的 LED 段，以便我们可以观察两个独立端口输出的值。

```
NET CLK     LOC=P44;  # B0 argument of XSPORT
NET WE      LOC=P45;  # B1 argument of XSPORT
NET INP0    LOC=P46;  # B2 argument of XSPORT
NET INP1    LOC=P47;  # B3 argument of XSPORT
NET A0      LOC=P48;  # B4 argument of XSPORT
NET A1      LOC=P49;  # B5 argument of XSPORT
# NET DPRA0  LOC=P32;  # B6 argument of XSPORT
# NET DPRA1  LOC=P34;  # B7 argument of XSPORT
NET S1      LOC=P26;  # S1 LED segment (for SP00)
NET S2      LOC=P24;  # S2 LED segment (for SP01)
```

