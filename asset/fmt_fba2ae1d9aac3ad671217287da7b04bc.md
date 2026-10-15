
```
NET c        LOC=P44;    # B0 argument of XSPORT
NET nickel    LOC=P45;    # B1 argument of XSPORT
NET dime      LOC=P46;    # B2 argument of XSPORT
NET coin_ret  LOC=P47;    # B3 argument of XSPORT
NET swill     LOC=P48;    # B4 argument of XSPORT
NET krunk     LOC=P49;    # B5 argument of XSPORT
NET cents0    LOC=P25;    # S0 LED segment
NET cents5    LOC=P26;    # S1 LED segment
NET cents10   LOC=P24;    # S2 LED segment
NET cents15   LOC=P20;    # S3 LED segment
NET cents20   LOC=P23;    # S4 LED segment
NET cents25   LOC=P18;    # S5 LED segment
```

或者对 XS95 开发板使用以下约束：

```
NET c        LOC=P46;    # B0 argument of XSPORT
NET nickel    LOC=P47;    # B1 argument of XSPORT
NET dime      LOC=P48;    # B2 argument of XSPORT
NET coin_ret  LOC=P50;    # B3 argument of XSPORT
NET swill     LOC=P51;    # B4 argument of XSPORT
NET krunk     LOC=P52;    # B5 argument of XSPORT
NET cents0    LOC=P21;  # S0 LED segment
NET cents5    LOC=P23;  # S1 LED segment
NET cents10   LOC=P19;  # S2 LED segment
NET cents15   LOC=P17;  # S3 LED segment
NET cents20   LOC=P18;  # S4 LED segment
NET cents25   LOC=P14;  # S5 LED segment
```

BIT 或 SVF 文件也可以分别下载到 XS40 或 XS95 开发板，并通过 PC 并口进行测试。存储当前状态的 DFF 输出连接到 LED 数码管的段。这样可以在每次操作后直观地显示饮料机的状态。你可以通过以下命令序列的组合来逐步测试状态机的各种工作流程。每个序列都会激活一个特定输入，然后向饮料分配控制器发送一个时钟上升沿。

| 顾客输入 | XSPORT 命令序列 |
|---|---|
| 复位 | `XSPORT 111110`<br>`XSPORT 111111`<br>`XSPORT 111110` |
| 投入 5 美分 | `XSPORT 000010`<br>`XSPORT 000011`<br>`XSPORT 000000` |
| 投入 10 美分 | `XSPORT 000100`<br>`XSPORT 000101`<br>`XSPORT 000000` |
| 退币 | `XSPORT 001000`<br>`XSPORT 001001`<br>`XSPORT 000000` |
| 取 Swill | `XSPORT 010000`<br>`XSPORT 010001`<br>`XSPORT 000000` |
| 取 Krunk | `XSPORT 100000`<br>`XSPORT 100001`<br>`XSPORT 000000` |

### 重新审视饮料分配控制器

如果你仔细观察，就会注意到图 7.13 中仿真波形有一个问题：导致退出一枚 10 美分硬币的 `RET_DIME` 输出在 36-40 ns 期间有效。这是因为在 36 ns 时时钟上升沿输入了一枚 10 美分硬币，机器立即从 15 美分状态转移到 25 美分状态，而 `DIME` 输入在 40 ns 之前仍然有效。状态机看到 `DIME` 输入上仍然存在逻辑 1，便认为顾客正在投入一枚新的 10 美分硬币。由于状态机现在处于 25 美分状态，不再需要更多钱就能获得饮料，因此状态机理所当然地退出一枚 10 美分硬币。最终结果就是顾客只需 15 美分就能得到一罐 Swill 或 Krunk。

上述问题可以通过在状态机中增加一个名为“Armed”的新状态并修改 25 美分状态下的动作来解决，如表 7.7 所示。

**表 7.7** 修订后的饮料分配逻辑真值表。

| 当前状态 | 5 美分 | 10 美分 | 退币 | Swill | Krunk | 无输入 |
|---|---|---|---|---|---|---|
| 0 美分 | →5 美分 | →10 美分 | →0 美分 | →0 美分 | →0 美分 | →0 美分 |
| 5 美分 | →10 美分 | →15 美分 | →0 美分，ret_nick = 1 | →5 美分 | →5 美分 | →5 美分 |
| 10 美分 | →15 美分 | →20 美分 | →0 美分，ret_dime = 1 | →10 美分 | →10 美分 | →10 美分 |
| 15 美分 | →20 美分 | →25 美分 | →0 美分，ret_dime = 1 | →15 美分 | →15 美分 | →15 美分 |
| 20 美分 | →25 美分 | →25 美分，ret_nick = 1 | →10 美分，ret_dime = 1 | →20 美分 | →20 美分 | →20 美分 |
| 25 美分 | →25 美分 | →25 美分 | →25 美分 | →25 美分 | →25 美分 | →Armed |
| Armed | →Armed，ret_nick = 1 | →Armed，ret_dime = 1 | →15 美分，ret_dime = 1 | →0 美分，disp_swill = 1 | →0 美分，disp_krunk = 1 | →Armed |

在修订后的状态转移表中，只要任一输入处于逻辑 1 电平，状态机就保持在 25 美分状态。同时，在 25 美分状态下，不会为退币或饮料分配机制产生任何输出信号。只有当所有输入都处于逻辑 0 电平（即“无输入”）时，才会从 25 美分状态转移到 Armed 状态。在 Armed 状态下，状态机将再次响应输入，用于选择所需饮料以及接收和退还钱币。

现在你可能会想：“哦不！我得重新检查整个真值表，插入这个新状态，并修正所有转移和输出！”这种想法会让任何人都不愿意动手修改。正因如此，ABEL 提供了像 VHDL 中那样的语言结构，使描述状态机变得容易（至少比我们之前所做的要容易）。清单 7.5 展示了我们修订后的饮料分配控制器的 ABEL 代码。现在我们可以看看它与之前的 ABEL 设计有何不同。

首先，我们在第 21 行添加了一个新的状态触发器，名为 `ARMED`。当控制器处于 Armed 状态时，该触发器会为开启状态。在第 26–32 行我们定义了一组状态名称，并为每个状态分配特定的位模式。请注意，这只是我们之前使用的独热编码，只是增加了 `ARMED` 触发器。（触发器的名称在第 25 行的注释中列出，这样你就可以看到每个状态对应的活动触发器。）第 36–41 行将触发器的时钟、预置和复位输入连接起来，就像之前的设计一样。`ARMED` 触发器已添加到这些语句中。

第 43 行的 `STATE_DIAGRAM` 关键字开始描述我们饮料分配器控制器的行为。该关键字后面跟着一个方括号括起来的列表，其中列出了存储此状态机的状态的触发器状态。为了正确运行，这些触发器名称的顺序必须与你在第 26–32 行的状态分配中对触发器的排序相匹配。

状态机描述的其余部分由 7 组语句组成——控制器中每个状态对应一组。每组都以一个以冒号结尾的状态标签开始，该标签指示以下语句适用的状态。例如，在第 46 行，`ST_CENTSO` 标签表示第 47、48 和 49 行的语句将描述状态机在处于 0¢ 状态时应如何动作。

第 47–49 行是一个简单的 `IF-THEN-ELSE` 结构。其基本语法如下：

```
IF <boolean expression A == TRUE> THEN <next state B>
ELSE IF <boolean expression C == TRUE> THEN <next state D>
......
ELSE <next state Z>;
```

`IF-THEN-ELSE` 语句生成一个逻辑电路，用于评估涉及状态机输入的一组布尔表达式。第一个求值为逻辑 1（TRUE）的表达式将导致状态机进入对应 `THEN` 关键字后列出的下一个状态。如果没有任何表达式为 TRUE，则状态机将转换到最终 `ELSE` 子句中列出的下一个状态。（请注意一定要用分号终止 `IF-THEN-ELSE` 语句。）
