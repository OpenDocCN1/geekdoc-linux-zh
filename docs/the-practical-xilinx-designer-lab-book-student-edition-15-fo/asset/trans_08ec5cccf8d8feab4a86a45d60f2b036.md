

首先，我们在第 21 行添加了一个新的状态触发器，名为 ARMED。当控制器处于 Armed 状态时，该触发器会为开启状态。在第 26–32 行我们定义了一组状态名称，并为每个状态分配特定的位模式。请注意，这只是我们之前使用的独热编码，只是增加了 ARMED 触发器。（触发器的名称在第 25 行的注释中列出，这样你就可以看到每个状态对应的活动触发器。）第 36–41 行将触发器的时钟、预置和复位输入连接起来，就像之前的设计一样。ARMED 触发器已添加到这些语句中。

第 43 行的 STATE_DIAGRAM 关键字开始描述我们饮料分配器控制器的行为。该关键字后面跟着一个方括号括起来的列表，其中列出了存储此状态机的状态的触发器状态。为了正确运行，这些触发器名称的顺序必须与你在第 26–32 行的状态分配中对触发器的排序相匹配。

状态机描述的其余部分由 7 组语句组成——控制器中每个状态对应一组。每组都以一个以冒号结尾的状态标签开始，该标签指示以下语句适用的状态。例如，在第 46 行，ST_CENTSO 标签表示第 47、48 和 49 行的语句将描述状态机在处于 0¢ 状态时应如何动作。

第 47–49 行是一个简单的 IF-THEN-ELSE 结构。其基本语法如下：

```
IF <boolean expression A == TRUE> THEN <next state B>
ELSE IF <boolean expression C == TRUE> THEN <next state D>
......
ELSE <next state Z>;
```

IF-THEN-ELSE 语句生成一个逻辑电路，用于评估涉及状态机输入的一组布尔表达式。第一个求值为逻辑 1（TRUE）的表达式将导致状态机进入对应 THEN 关键字后列出的下一个状态。如果没有任何表达式为 TRUE，则状态机将转换到最终 ELSE 子句中列出的下一个状态。（请注意一定要用分号终止 IF-THEN-ELSE 语句。）

为了更具体地说明，请查看第 46–49 行。假设状态机处于 0¢ 状态，第 47 行表示如果插入一枚镍币，控制器将移动到 5¢ 状态。如果没有插入镍币但插入了硬币，则控制器移动到 10¢ 状态。最后，如果既没有插入镍币也没有插入硬币，控制器将保持在 0¢ 状态。这种行为几乎与我们修订后的状态转换表第一行中描述的内容相匹配。（我们稍后会讨论细微的差异。）

IF-THEN-ELSE 语句是描述状态机状态转换的一种非常易读的方式，但我们如何描述控制分配器和退币机构的输出动作呢？这可以通过 WITH 关键字实现，它允许我们将布尔表达式分配给特定输出。WITH 用于 IF-THEN-ELSE 语句中下一个状态标签之后。修订后的语法如下：

```
IF <boolean expression A == TRUE> THEN <next state B>
    WITH <output E = boolean expression F>
ELSE IF <boolean expression C == TRUE> THEN <next state D>
    WITH <output G = boolean expression H>
...
ELSE <next state Z> WITH <output W = boolean expression X>;
```

基本上，IF-THEN-WITH-ELSE 语句不仅生成下一个状态逻辑，而且还会导致布尔表达式的值在特定条件适用时立即出现在指定的输出上。如前所述，电路评估涉及状态机输入的一组布尔表达式。第一个求值为逻辑 1（TRUE）的表达式将导致 WITH 关键字后列出的布尔方程的值立即出现在相关输出上。如果没有任何表达式为 TRUE，则最终 ELSE 子句中的 WITH 子句将被激活。

以第 83–89 行为例说明 WITH 关键字的用法。假设控制器处于 Armed 状态，第 84 行指出插入一枚镍币将导致控制器激活退币并退回一枚镍币（RET_NICK=1）。第 85 行和第 86 行要求如果插入硬币或按下退币按钮，则分别退回一枚硬币。第 87 行和第 88 行在激活 Swill 或 Krunk 按钮时分别激活 Swill 或 Krunk 罐分配的输出。如果之前没有任何输入为 TRUE，则不会激活任何输出（第 89 行）。

使用 WITH 子句和大括号括起来的布尔方程组，可以同时控制多个输出。例如，如果在 Armed 状态下按下退币输入，控制器可以同时退回一枚硬币和一枚镍币（前提是退币机构能够处理）。修改后的 IF-THEN-WITH-ELSE 语句如下所示：

```
STATE ST_ARMED:
IF NICKEL THEN ST_ARMED WITH RET_NICK=1
ELSE IF DIME THEN ST_ARMED WITH RET_DIME=1
ELSE IF COIN_RET THEN ST_CENTS10 WITH {RET_DIME=1; RET_NICK=1;}
ELSE IF SWILL THEN ST_CENTSO WITH DISP_SWILL=1
ELSE IF KRUNK THEN ST_CENTSO WITH DISP_KRUNK=1
ELSE ST_ARMED;
```
