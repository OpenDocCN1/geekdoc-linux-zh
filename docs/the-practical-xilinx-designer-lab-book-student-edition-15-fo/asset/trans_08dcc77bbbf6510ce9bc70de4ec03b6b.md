

有了你对 ABEL 状态机语法的全新认识，你应该能够解释清单 7.5 的每一行，并将其与原始状态转换表联系起来。事实上，你用来综合网络表的 ABEL 编译器也是这样做的。编译器解析 STATE_DIAGRAM 语句并构建自己的状态转换表。然后编译器可以像你在前面各节中所做的那样，推导出用于生成下一状态和输出的电路。因此软件工具并没有做任何神奇的事情。

我们也可以重新制作饮品分配器状态机的 VHDL 版本，如清单 7.6 所示。与 3 状态计数器 VHDL 示例（清单 7.2）一样，此代码使用了两个进程：一个用于根据当前状态和输入的值计算输出和下一状态（第 59–113 行），另一个进程仅在时钟输入上更新当前状态为新的下一状态值（第 119–127 行）。因此，我们在第 37 行和第 38 行分别声明了两个数组来保存当前状态和下一状态。

新的 armed 输出在第 25 行的接口描述中添加，并且当前状态和下一状态数组以及状态定义在第 37 至 46 行扩展以处理这个额外位。此设计的输出状态连接到第 49 至 55 行的当前状态数组元素。

第一个进程首先将状态机的所有组合输出赋值为低逻辑电平（第 61–64 行）。这确保了如果以下条件语句未对其进行设置，这些输出仍会被设为某个值。如果我们不执行此初始化步骤，则这些输出将变成隐含锁存器。下一状态数组也在第 65 行初始化为复位状态（使用 0c）。这将导致状态机在进入非法状态时重新启动。

随后在第 67–112 行有一个大的 IF...THEN...ELSE 语句，它使用当前状态和输入来计算下一状态和输出。作为 VHDL 代码如何工作的示例，考虑当前状态为 20c 的情况。此时 cents20 触发器应为开启，因此 curr_drink_state 数组应为 0010000。这与 st_cents20 常量匹配，因此第 90 行的语句被执行。这激活了第 91–95 行的嵌套 IF...THEN...ELSE 语句。如果插入一枚十美分硬币，则执行会落到第 92 行。第 92 行的语句将 ret_nick 输出赋值为逻辑 1。因此一枚镍币将被退还给顾客。同时，next_drink_state 数组被加载为 st_cents25。st_cents25 常量为 0100000，因此 next_drink_state(5) 元素被置位，其他元素被清除。

继续该示例，第二个进程在时钟输入上出现上升沿时将 next_drink_state 数组传输到 curr_drink_state 数组。这会将 curr_drink_state 加载为 st_cents25，即 0100000。这会置位 curr_drink_state(5) 元素并复位其他所有元素。curr_drink_state(5) 元素在第

### Listing 7.5 ABEL code for the revised drink dispenser controller.

```
001- MODULE DRINK2;
002- TITLE 'drink dispenser controller (2nd version)'
003-
004- DECLARATIONS
005- C PIN;                      *clock input
006- NICKEL PIN;                 *nickel inserted input
007- DIME PIN;                   *dime inserted input
008- COIN_RET PIN;               *coin-return input
009- SWILL PIN;                  *Swill selection
010- KRUNK PIN;                  *Krunk selection
011- RET_NICK PIN ISTYPE 'COM';  *return nickel output
012- RET_DIME PIN ISTYPE 'COM';  *return dime output
013- DISP_SWILL PIN ISTYPE 'COM'; *dispense swill output
014- DISP_KRUNK PIN ISTYPE 'COM'; *dispense krunk output
015- CENTS0 PIN ISTYPE 'REG';    *DFF for 0-cents state
016- CENTS5 PIN ISTYPE 'REG';    *DFF for 5-cents state
017- CENTS10 PIN ISTYPE 'REG';   *DFF for 10-cents state
018- CENTS15 PIN ISTYPE 'REG';   *DFF for 15-cents state
019- CENTS20 PIN ISTYPE 'REG';   *DFF for 20-cents state
020- CENTS25 PIN ISTYPE 'REG';   *DFF for 25-cents state
021- ARMED PIN ISTYPE 'REG';     *DFF for armed state
022- RESET = NICKEL & DIME & COIN_RET & SWILL & KRUNK; *reset trigger
023-
024- *now make some state assignments
025-
026- ARMED CENTS25 CENTS20 CENTS15 CENTS10 CENTS5 CENTS0
027- ST_CENTS0 = [0, 0, 0, 0, 0, 0, 1];
028- ST_CENTS5 = [0, 0, 0, 0, 0, 1, 0];
029- ST_CENTS10 = [0, 0, 0, 0, 1, 0, 0];
030- ST_CENTS15 = [0, 0, 0, 1, 0, 0, 0];
031- ST_CENTS20 = [0, 0, 1, 0, 0, 0, 0];
032- ST_CENTS25 = [0, 1, 0, 0, 0, 0, 0];
033- ST_ARMED = [1, 0, 0, 0, 0, 0, 0];
034-
035- EQUATIONS
036-
037- *clock controller state DFFs
038- [CENTS0,CENTS5,CENTS10,CENTS15,CENTS20,CENTS25,ARMED].CLK = C;
039- *next two statements asynchronously reset controller
040- *to the cents0 state (0000001)
041- CENTS0.ASET = RESET;
042- [CENTS5,CENTS10,CENTS15,CENTS20,CENTS25,ARMED].ACLR = RESET;
```
