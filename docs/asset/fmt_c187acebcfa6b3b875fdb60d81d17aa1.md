
```
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

除了异步 RAM 之外，XC4000 系列还提供同步 RAM 和双端口 RAM。图 8.22 给出了在原理图中使用的内部 16×2 双端口同步 RAM 的示例。RAM 是通过从原理图编辑器的 SC Symbols 窗口中选择 `RAM16x2D` 符号实例化的。它配备了一个正常的地址总线（`A3..A0`），该总线控制使用 `INP0..INP0` 输入总线和 `SP01..SP00` 输出总线分别写入或读取哪个存储器位置。此外，还提供了一个只读的第二端口，可让你通过 `DPRA3..DPRA0` 输入地址，并通过输出总线 `DPO1..DPO0` 读取存储器位置的内容。（PC 并行端口没有足够的引脚来驱动所有这些地址位，因此在原理图中每个地址的上两个位都连接到地。）

`MEM4` 设计的约束文件如下。注意，存储器的每个 2 位输出端口都连接到一对唯一的 LED 段，以便我们可以观察两个独立端口输出的值。

```
NET CLK     LOC=P44;  # B0 argument of XSPORT

NET WE      LOC=P45;  # B1 argument of XSPORT

NET INP0    LOC=P46;  # B2 argument of XSPORT

NET INP1    LOC=P47;  # B3 argument of XSPORT

NET A0      LOC=P48;  # B4 argument of XSPORT

NET A1      LOC=P49;  # B5 argument of XSPORT

#### NET DPRA0  LOC=P32;  # B6 argument of XSPORT

#### NET DPRA1  LOC=P34;  # B7 argument of XSPORT

NET S1      LOC=P26;  # S1 LED segment (for SP00)

NET S2      LOC=P24;  # S2 LED segment (for SP01)
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_309_0.png)

图 8.22 使用 XC4005XL FPGA 的内置同步双端口存储器。

```
NET S4    LOC=P23;    # S4 LED segment (for DP00)

NET S5    LOC=P18;    # S5 LED segment (for DP01)
```
