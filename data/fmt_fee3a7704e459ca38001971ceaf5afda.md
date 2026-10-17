
在对该设计的网表进行综合后，我们可以执行仿真以检查其操作。对于此示例，我们将使用 Stimulator Selection 窗口将`SB`和`RB`输入连接到键盘的键。只需在 Waveform Viewer 窗口中突出显示`SB`输入的名称，然后在 Stimulator Selection 窗口中单击鼠标上的 Q 键盘符号。这将把输入绑定到该键盘键。重复此操作将`RB`输入绑定到 W 键。然后关闭 Stimulator Selection 窗口。

现在我们可以通过按下 Q 和 W 键来切换`SB`或`RB`输入的值。单击 Logic Simulator 窗口工具栏上的按钮会使用当前输入执行一次仿真步。然后我们按下键盘上的 Q 和 W 键来更改输入并进行另一次仿真步。SRFF 的仿真操作如图 6.8 所示。

#### 列表 6.2 简单 SR 触发器的 VHDL 代码

``` 
001- -- S-R Flip-Flop
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY srff1 IS
007- PORT
008- (
009-   sb: IN STD_LOGIC;    -- active-low set input
010-   rb: IN STD_LOGIC;    -- active-low reset input
011-   q: BUFFER STD_LOGIC; -- data output
012-   qb: BUFFER STD_LOGIC -- inverted data output
013- );
014- END srff1;
015-
016- ARCHITECTURE srff1_arch OF srff1 IS
017- BEGIN
018-   q  <= (NOT sb AND qb);  -- cross-coupled NAND gates
019-   qb <= (NOT rb AND q);
020- END srff1_arch;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_191_0.png)

**图 6.8** 简单 SR 触发器的仿真波形。

请注意，仿真开始时`Q`和`QB`输出处于未知状态。NAND 门之间的反馈阻碍了仿真器尝试确定触发器的初始状态。一旦`SB`输入被拉低到 0，`Q` NAND 门的输出必须稳定在逻辑 1。随着`RB`和`Q`现在都为逻辑 1，`QB`输出变为逻辑 0。因此触发器的状态不再未知。

当`SB`输入返回到 1 时，`Q`输出保持为 1。因此，SRFF 存储了由`SB`输入加载的逻辑 1。然后当`RB`输入变低时，`QB`输出被设置为逻辑 1 而`Q`输出变低。当`RB`输入返回到逻辑 1 时这种情况仍然持续，因此现在 SRFF 存储的是逻辑 0。看起来 SR 触发器工作正常，至少在仿真中是这样。

现在我们可以将 SRFF 下载到 XS40 或 XS95 板上进行实际测试。为 XS40 板创建用户约束文件，将输入和输出分配如下：

``` 
NET sb    LOC=P44;  # B0 argument of XSPORT
NET rb    LOC=P45;  # B1 argument of XSPORT
NET q     LOC=P25;  # S0 LED segment
NET qb    LOC=P26;  # S1 LED segment
```

或对 XS95 板使用以下约束：

``` 
NET sb    LOC=P46;  # B0 argument of XSPORT
NET rb    LOC=P47;  # B1 argument of XSPORT
NET q     LOC=P21;  # S0 LED segment
NET qb    LOC=P23;  # S1 LED segment
```

在编译并下载`SRFF1`设计后，当你使用给定的命令序列在 XS40 或 XS95 板上操作设计时，应该会看到以下结果：

| 命令 | `RB` | `SB` | LED S0 (`Q`) | LED S1 (`Q_`) |
|---|---|---|---|---|
| `XSPORT 10` | 1 | 0 | 亮 (1) | 暗 (0) |
| `XSPORT 11` | 1 | 1 | 亮 (1) | 暗 (0) |
| `XSPORT 01` | 0 | 1 | 暗 (0) | 亮 (1) |
| `XSPORT 11` | 1 | 1 | 暗 (0) | 亮 (1) |

这些结果与仿真中发现的结果相匹配。

列表 6.1 中的 ABEL 代码在 FPLD 中使用 2 个宏单元或 LUT，因为我们同时生成`Q`输出及其补码。如果只需要`Q`输出，列表 6.3 中的 ABEL 代码就足够了，它仅使用 1 个宏单元或 LUT。列表 6.3 用第 12 行的方程式。这个 SRFF 与清单 6.3 所描述的 SRFF 完全相同。

#### 清单 6.3 单个宏单元或 LUT SR 触发器的 ABEL 代码

``` 
001- MODULE SRFF2
002- TITLE 'simple SR flip-flop'
003-
004- DECLARATIONS
005- SB PIN;                 "S input
006- RB PIN;                 "R input
007- Q PIN ISTYPE 'COM';     "Q output
008-
009- EQUATIONS
010- Q = !(SB & !(RB & Q));
011-
012- END SRFF2
```

没有`QB`输出的 SRFF 的 VHDL 代码如清单 6.4 所示。该 SRFF 仅消耗 1 个 LUT 或 CLB，但它是以行为风格而非布尔方程的形式描述的。行为逻辑描述通常有一个或多个进程，由 `PROCESS...END PROCESS` 语句包围。`PROCESS` 关键字后跟一个带括号的敏感信号列表。若列表中任何信号的值发生变化，则执行进程块中的语句。

清单 6.4 中从第 17 行开始的进程，如果`sb`或`qb`输入或`q`输出发生变化，就会启动。通常，敏感信号列表包含所有在条件表达式中作为操作数出现，或在进程块语句的 `<=` 赋值运算符右侧出现的信号。

第 19 至 25 行的 `IF...ELSIF...ELSE` 条件语句描述了 SR 触发器的实际操作。第 20 行在`sb`输入为低时将`q`输出置 1。但如果`sb`不为 0 而`rb`为 0，则第 22 行将`q`复位为 0。最后，第 24 行说明，若`sb`和`rb`均不为低，则`q`的值不会改变。这正是我们在 SR 触发器中所需要的操作。

注意，我们甚至不需要第 23 和第 24 行的语句，删除它们不会影响触发器的操作。考虑`sb=0`且`rb=1`的情况。执行第 20 行后，`q`输出为 1，然后进程结束。接着，如果`sb`变为高电平，这一变化将再次启动进程。但此时`sb`和`rb`都不为低，因此第 20 行或第 22 行的赋值语句都不会执行。由于没有显式语句设置其值，`q`输出将保持其之前的值 1。当输出因为进程中没有执行任何赋值语句而保留其最后的值时，该输出就具有一个隐含锁存器。带有隐含锁存器的 SR 触发器与清单 6.4 中在第 23 和第 24 行带有显式锁存器的触发器工作原理相同。

清单 6.4 中的另一个新特性是，在接口描述的第 11 行，`q`输出被声明为 `BUFFER` 而不是 `OUT`。VHDL 要求 `OUT` 信号的值只能从模块输出，而不能在模块的 `ARCHITECTURE` 部分内部读取。因此，如果`q`被声明为 `OUT`，那么像第 24 行那样将其用在赋值运算符右侧就是非法的。VHDL 提供了 `BUFFER` 和 `INOUT` 关键字，用来声明既可以作为输出、又能将其值反馈回模块的信号。

#### 清单 6.4 单个宏单元或 LUT SR 触发器的行为级 VHDL 代码
