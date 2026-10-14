

## 图 6.7 由触发器构建计数器。

![](img/5124daf79d2807d81e49f49c22f1f8c1_189_0.png)

## 实验

### 一个 S-R 触发器

我们将从构建一个简单的 S-R 触发器开始。列表 6.1 显示了该触发器的 ABEL 代码。第 11 行和第 12 行描述了一对交叉耦合 NAND 门的连接。列表 6.2 以 VHDL 展示了相同的 S-R 触发器，交叉耦合 NAND 门位于第 18 行和第 19 行。

（注意我将使用以 B 结尾的名称来表示在逻辑 0 时有效的信号。因此 /S 在 ABEL 或 VHDL 文件中出现时被命名为 SB。这只是我个人的约定，你不必这样做。）

### 列表 6.1 简单 SR 触发器的 ABEL 代码。

```
001- MODULE SRFF1
002- TITLE 'simple SR flip-flop'
003-
004- DECLARATIONS
005- SBPIN;             "/S input
006- RBPIN;             "/R input
007- Q PIN ISTYPE 'COM';  "Q output
008- QBPIN ISTYPE 'COM';  "/Q output
009-
010- EQUATIONS
011- Q = !(SB & QB);
012- QB = !(RB & Q);
013- END SRFF1
```

在对该设计的网表进行综合后，我们可以执行仿真以检查其操作。对于此示例，我们将使用 Stimulator Selection 窗口将 SB 和 RB 输入连接到键盘的键。只需在 Waveform Viewer 窗口中突出显示 SB 输入的名称，然后在 Stimulator Selection 窗口中单击鼠标上的 Q 键盘符号。这将把输入绑定到该键盘键。重复此操作将 RB 输入绑定到 W 键。然后关闭 Stimulator Selection 窗口。

现在我们可以通过按下 Q 和 W 键来切换 SB 或 RB 输入的值。单击 Logic Simulator 窗口工具栏上的按钮会使用当前输入执行一次仿真步。然后我们按下键盘上的 Q 和 W 键来更改输入并进行另一次仿真步。SRFF 的仿真操作如图 6.8 所示。

### 列表 6.2 简单 SR 触发器的 VHDL 代码。

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

请注意，仿真开始时 Q 和 QB 输出处于未知状态。NAND 门之间的反馈阻碍了仿真器尝试确定触发器的初始状态。一旦 SB 输入被拉低到 0，Q NAND 门的输出必须稳定在逻辑 1。随着 RB 和 Q 现在都为逻辑 1，QB 输出变为逻辑 0。因此触发器的状态不再未知。

当 SB 输入返回到 1 时，Q 输出保持为 1。因此，SRFF 存储了由 SB 输入加载的逻辑 1。然后当 RB 输入变低时，QB 输出被设置为逻辑 1 而 Q 输出变低。当 RB 输入返回到逻辑 1 时这种情况仍然持续，因此现在 SRFF 存储的是逻辑 0。看起来 SR 触发器工作正常，至少在仿真中是这样。

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

在编译并下载 SRFF1 设计后，当你使用给定的命令序列在 XS40 或 XS95 板上操作设计时，应该会看到以下结果：

| 命令 | RB | SB | LED S0 (Q) | LED S1 (Q_) |
|---|---|---|---|---|
| XSPORT 10 | 1 | 0 | 亮 (1) | 暗 (0) |
| XSPORT 11 | 1 | 1 | 亮 (1) | 暗 (0) |
| XSPORT 01 | 0 | 1 | 暗 (0) | 亮 (1) |
| XSPORT 11 | 1 | 1 | 暗 (0) | 亮 (1) |

这些结果与仿真中发现的结果相匹配。

列表 6.1 中的 ABEL 代码在 FPLD 中使用 2 个宏单元或 LUT，因为我们同时生成 Q 输出及其补码。如果只需要 Q 输出，列表 6.3 中的 ABEL 代码就足够了，它仅使用 1 个宏单元或 LUT。列表 6.3 用

