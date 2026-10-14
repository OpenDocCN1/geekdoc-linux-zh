

## Listing 6.12 使用 XC9500 内置 D 触发器带异步清零的 VHDL 代码。

```
001- -- Built-in D Flip-Flops
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY bidff IS
007- PORT
008- (
009-   c: IN STD_LOGIC;       -- clock
010-   d: IN STD_LOGIC;       -- data
011-   aclr: IN STD_LOGIC;    -- active-low asynchronous clear
012-   q: OUT STD_LOGIC        -- stored data bit value
013- );
014- END bidff;
015-
016- ARCHITECTURE bidff_arch OF bidff IS
017-   COMPONENT FDPC PORT       -- interface to the built-in DFF
018-   (
019-     C: IN STD_LOGIC;
020-     CLR: IN STD_LOGIC;
021-     PRE: IN STD_LOGIC;
022-     D: IN STD_LOGIC;
023-     Q: OUT STD_LOGIC
024-   );
025-   END COMPONENT;
026-   SIGNAL aclr: STD_LOGIC;
027-   SIGNAL cb: STD_LOGIC;
028-   SIGNAL pre: STD_LOGIC;
029- BEGIN
030-   aclr <= NOT(aclr);       -- invert sense of clear
031-   cb <= NOT(c);            -- invert clock to falling edge
032-   pre <= '0';              -- disable preset
033-   u0: FDPC PORT MAP (C=>cb, D=>d, CLR=>aclr, PRE=>pre,
034-                      Q=>q);
035- END bidff_arch;
```

## Listing 6.13 XC9500 CPLD 内置 D 触发器带异步清零的 XNF。

```
001- LCNAT, 5
002- SYM, Q, DFF, SCHNM=FDPC, LIBVER=2.0.0
003- PIN, D, I, D
004- PIN, C, I, C
005- PIN, PRE, I, PRE
006- PIN, CLR, I, CLR
007- PIN, Q, O, Q
008- END
009- EOF
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_207_0.png)

## Figure 6.12 内置 D 触发器的仿真波形。

将 BIDFF 设计编译并下载到 XS40 或 XS95 板上后，以下命令序列应给出所示结果：

| Command | ACLRB | D | C | LED SO (SQ) |
|---|---|---|---|---|
| XSPORT 101 | 1 | 0 | 1 | ??? |
| XSPORT 110 | 1 | 1 | 0 | Bright (1) |
| XSPORT 010 | 0 | 1 | 0 | Dark (0) |
| XSPORT 011 | 0 | 1 | 1 | Dark (0) |
| XSPORT 010 | 0 | 1 | 0 | Dark (0) |

## A Toggle Flip-Flop Counter

作为我们最后的示例，Listing 6.14 显示了一个由触发器构成的 3 位计数器。我们从第 7 行开始声明 3 个 DFF T0、T1 和 T2。这些 D 触发器通过加载其内容的反相值（第 11 行）被转换为触发器。然后计数器的最低有效位由第 12 行输入时钟 C 的正向边沿驱动。在第 13 行，计数器的下一位由 T0，即 LSB 的输出驱动。以同样的方式，计数器的最高有效位 T2 由第 14 行的 T1 驱动。最后，在第 15 行，我们为每个 TFF 提供一个有效高的异步清零，以便在需要时随时清除计数器。

## Listing 6.14 由触发器构成的 3 位计数器的 ABEL 代码。

```
001- MODULE TGLCNT
002- TITLE '3-bit toggle flip-flop counter'
003-
004- DECLARATIONS
005- C PIN; "clock input
006- ACLR PIN; "clear input
007- T2..T0 PIN ISTYPE 'REG'; "DFFs for counter
008-
009- EQUATIONS
010- [T2..T0] := ![T2..T0]; "make DFFs into TFFs
011- T0.CLK = C; "LS bit clocked by input clock
012- T1.CLK = T0; "remaining bits clocked by output
013- T2.CLK = T1; "of the preceding bit
014- [T2..T0].ACLR = ACLR; "connect the asynchronous clear
015-
016- END TGLCNT
```

3 位计数器的等效 VHDL 代码如 Listing 6.15 所示。触发器被实现为 3 个不同的进程。在主时钟输入的上升沿，bit0 进程（第 27–35 行）通过加载其反相值（第 32 和 33 行）来切换 t0 TFF 输出。t0 输出是用于计数器下一位时钟的信号，由 bit1 进程（第 37–45 行）描述。而该位的 t1 输出则是用于计数器最高有效位时钟的信号，由 bit2 进程（第 47–55 行）描述。每个进程在异步清零输入为高电平时将覆盖切换操作并清除其位。

Listing 6.15 中的 VHDL 代码还具有特殊修改，以便它能在 XS40 板上运行。当针对 XC4000 FPGA 时，Foundation Series 综合软件会尝试使用特殊的时钟缓冲器来驱动时钟信号到触发器。这些缓冲器最大限度地减小了时钟信号到达各触发器的时间

