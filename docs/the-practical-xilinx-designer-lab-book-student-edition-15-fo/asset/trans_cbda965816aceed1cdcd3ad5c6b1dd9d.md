

## 列表 6.6 时钟 SRFF 的行为 VHDL 代码。

``` 
001- -- Clocked S-R Flip-Flop
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY csrff IS
007- PORT (
008- c: IN STD_LOGIC; -- clock
009- sb: IN STD_LOGIC; -- active-low set input
010- rb: IN STD_LOGIC; -- active-low reset input
011- q: BUFFER STD_LOGIC; -- stored data bit value
012- qb: OUT STD_LOGIC -- inverted output
013- );
014- END csrff;
015-
016- ARCHITECTURE csrff_arch OF csrff IS
017- BEGIN
018- PROCESS (c,sb,rb,q)
019- BEGIN
020- IF c='1' THEN -- change state only when clock is high
021- IF (sb='0') THEN
022- q <= '1';
023- ELSIF (rb='0') THEN
024- q <= '0';
025- END IF;
026- END IF;
027- END PROCESS;
028- qb <= q; -- generate the inverted output
029- END csrff_arch;
030-
```

或对 XS95 板使用以下约束：

+   NET c LOC=P46; # B0 argument of XSPORT
+   NET sb LOC=P47; # B1 argument of XSPORT
+   NET rb LOC=P48; # B2 argument of XSPORT
+   NET q LOC=P21; # S0 LED segment
+   NET qb LOC=P23; # S1 LED segment

![](img/5124daf79d2807d81e49f49c22f1f8c1_197_0.png)

## 图 6.9 时钟 SR 触发器的模拟波形。

编译并下载 CSRFF 设计后，当你使用给定的命令序列在 XS40 或 XS95 板上操作该设计时，应该会看到以下结果：

| Command | RB | SB | C | LED S0 (Q) | LED S1 (QB) |
|---|---|---|---|---|---|
| XSPORT 101 | 1 | 0 | 1 | Bright (1) | Dark (0) |
| XSPORT 111 | 1 | 1 | 1 | Bright (1) | Dark (0) |
| XSPORT 011 | 0 | 1 | 1 | Dark (0) | Bright (1) |
| XSPORT 111 | 1 | 1 | 1 | Dark (0) | Bright (1) |
| XSPORT 100 | 1 | 0 | 0 | Dark (0) | Bright (1) |
| XSPORT 110 | 1 | 1 | 0 | Dark (0) | Bright (1) |
| XSPORT 010 | 0 | 1 | 0 | Dark (0) | Bright (1) |
| XSPORT 110 | 1 | 1 | 0 | Dark (0) | Bright (1) |

这些结果显示时钟输入按预期通过并阻断 SB 和 RB 输入。

## 边沿触发 D 触发器

现在我们可以使用时钟 SRFF 来构建一个边沿触发的 D 触发器。ABEL 代码如列表 6.7 所示。第 13 行和第 14 行描述了主时钟 DFF，第 15 行和第 16 行描述了随后的从 DFF。从时钟是主时钟的反相拷贝。

## 列表 6.7 边沿触发主从 D 触发器的 ABEL 代码。

``` 
001- MODULE MSDFF
002- TITLE 'edge-triggered D flip-flop'
003-
004- DECLARATIONS
005- C       PIN;                 "clock input
006- D       PIN;                 "D input
007- MQ      PIN ISTYPE 'COM';    "master Q output
008- MQB     PIN ISTYPE 'COM';    "master /Q output
009- SQ      PIN ISTYPE 'COM';    "slave Q output
010- SQB     PIN ISTYPE 'COM';    "slave /Q output
011-
012- EQUATIONS
013- MQ  = !( !( !(!D & C) & MQB) );  "master clocked DFF
014- MQB = !( !( !D & C) & MQ );
015- SQ  = !( !( !(!MQ & !C) & SQB) );  "slave clocked DFF
016- SQB = !( !( !MQ & !C) & SQ );    "with inverted clock
017-
018- END MSDFF
```

列表 6.8 是边沿触发 D 触发器的行为 VHDL 描述。进程现在对数据 d 和时钟 c 输入的变化敏感（第 18 行）。我们需要一种方法来描述时钟输入上的下降沿，以便触发 sq 输出的变化。这是通过 VHDL 属性 'event' 完成的，该属性可以附加到信号上，并在信号值与进程上次执行时不同时求值为 TRUE 条件。在第 20 行，IF 语句中的条件为真，如果 c 信号在进程上次执行期间为高但现在为低。然后第 21 行将执行并将 d 输入上的值传输到 sq 输出。现在如果 d 输入值发生变化但 c 不变（即 c 仍为低），进程将再次执行。但第 21 行不会执行，因为 c'event 为 FALSE（即 c 的值没有变化）。因此，列表 6.8 描述的触发器是边沿触发而不是电平敏感的。

ABEL 版本边沿触发 DFF 的模拟波形如图 6.10 所示。模拟开始时，主触发器和从触发器都处于未知状态。一旦时钟上升到高电平，主触发器就接受 D 输入上存在的逻辑 0。从触发器仍然处于未知状态，因为其时钟输入为低（C 输入的反相），这阻止了主触发器的输出进入。一旦时钟下降到逻辑 0，从触发器输出被设置为逻辑零。请注意，主触发器和从触发器如何以一种“桶形传送带”的方式传递 D 输入。

