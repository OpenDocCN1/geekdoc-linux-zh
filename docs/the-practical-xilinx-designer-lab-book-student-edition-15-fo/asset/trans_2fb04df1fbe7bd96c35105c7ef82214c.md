

![](img/5124daf79d2807d81e49f49c22f1f8c1_381_0.png)

### Figure 10.5 Details of DWARF's arithmetic circuitry.

当 LD_ACC 为逻辑 1 且 CLOCK 输入上有上升沿时，从 H2 多路复用器获取数据。

零标志和进位标志也在 CLOCK 上升沿时更新，分别当 LD_Z 或 LD_CRY 为逻辑 1 时。零标志始终被加载为来自 D 总线 8 位值与寄存器组进行按位 AND 后的所有位结果的 NOR，图 10.6 显示了 ZEROTEST 模块的细节。

进位标志（图 10.7）如果 ALU_CRY 输入为高，则被加载为 8 位加法器的进位输出（ADD8 模块的 CO）。这允许在多字节算术运算中传播进位位。但如果 ALU_CRY=0，则进位标志被加载为 SET_CRY 输入上的值，从而允许将进位标志强制为 1 或 0。

RESET 输入上的逻辑 1 会将累加器和状态标志清零。

进位和零标志通过 CARRY 和 ZERO 输出离开 ALU 模块。累加器值出现在 [ACC7..ACC0] 输出上。设置 DRV_D_ACC=1 可让累加器驱动 D 总线（图 10.3）。这为将累加器存储到外部存储器、寄存器组，或将累加器作为操作数反馈回 ALU 提供了路径。

![](img/5124daf79d2807d81e49f49c22f1f8c1_382_0.png)

### Figure 10.6 Detailed circuitry for DWARF's ZEROTEST module.

![](img/5124daf79d2807d81e49f49c22f1f8c1_382_1.png)

### Figure 10.7 Detailed circuitry for DWARF's carry flag.

DWARF 的存储器地址生成电路如图 10.8 所示。程序计数器（左上）显示 PC（参考标识符为 PC0）只是一个来自标准元件库的 8 位可加载计数器（CB8CLE）。

LD_PC 输入上的逻辑 1 会在 CLOCK 的下一个上升沿将 PC 从 D 总线加载新值。此操作用于程序内的跳转。另一方面，INC_PC 输入上的逻辑 1 会使 PC 增加其值。此操作在指令的正常顺序执行期间是必需的。

程序计数器中的值可以通过置高 DRV_D_PC 信号驱动到 D 总线上。这使内部三态缓冲器（BUFES）的驱动器启用，以便 PC 值可以通过。此操作在 PC 值被存储到外部 RAM 的堆栈时是必需的。

通过置高 RESET 或 CLR_PC 信号可清除 PC。此操作在 DWARF 首次启动时是必需的，以便程序执行可以从 PROGRAM 区域的地址 0 开始。程序计数器也在 ISR 开始时被清除。

接下来看堆栈指针（图 10.8，左下）显示 SP（参考标识符为 SP0）只是一个来自原理图编辑器标准元件库的 8 位可加载上下计数器（CC8CLED）。

![](img/5124daf79d2807d81e49f49c22f1f8c1_383_0.png)

### Figure 10.8 DWARF's program counter, stack pointer, address selector, and RAM control circuitry.

CHG_SP 输入上的逻辑 1 会导致堆栈指针在 CLOCK 信号的上升沿改变其值。如果在 INC_SP 输入上施加逻辑 1，则该变化为递增。否则，SP 中的值将被递减。递增（递减）操作在值被压入（弹出）堆栈时是必需的。

通过置高 RESET 信号可清除 SP。此操作在 DWARF 启动时是必需的，以便堆栈从 STACK 区域的地址 0 开始向上增长。由于不需要随机寻址堆栈的内容，因此计数器的 DI[7:0] 输入保持未连接，且加载信号（L）连接到逻辑零。

寄存器组的 B 输出、SP 和 PC 是地址多路复用器模块（图 10.8，右下，ADDR_MUX）的 A、B 和 C 输入。地址多路复用器选择其输入之一作为 RAM 地址的低 8 位的来源，并设置高 7 位以使 DATA、STACK 和 PROGRAM 存储器区域分离。ADDR_MUX 在 SEL0 和 SEL1 输入设置下输出以下值：

| SEL1 | SEL0 | [ADDR14..ADDR8] | [ADDR7..ADDR0] | Region |
|---|---|---|---|---|
| 0 | 0 | 1111111 | [REG7..REG0] | DATA |
| 0 | 1 | 1111110 | [SP7..SP0] | STACK |
| 1 | 0 | 0000001 | [PC7..PC0] | unused |
| 1 | 1 | 0000000 | [PC7..PC0] | PROGRAM |

当 SEL0=SEL1=0 时访问外部 RAM 的 DATA 区域。寄存器组的 B 输出提供地址的低 8 位，而高 7 位被设置为 0x7F。因此，DATA 区域位于 RAM 的顶部，介于十六进制地址 0x7F00 和 0x7FFF 之间。以类似的方式，STACK 区域（SEL0=1，SEL1=0）占据地址范围 0x7E00–0x7EFF，堆栈指针提供低八位地址。PROGRAM 区域（SEL0 = SEL1 = 1）占据 RAM 的最低 256 字节（0x0000–0x00FF），PC 自然地作为该区域地址低 8 位的来源。

地址多路复用器的详细电路如图 10.9 所示。它主要由两个 8 位多路复用器组成，它们串联工作以在 SEL0 和 SEL1 输入的控制下将三个字节宽的 A、B 或 C 输入之一引导到 [07..00] 输出。SEL0 和 SEL1 还连接到一组反相器，为存储器地址的高 7 位生成每个存储器区域的正确位模式。

用于驱动外部 RAM 控制输入的杂项电路显示在图 10.8 的右上部分。RAM 通过将片选（CS_）连接到逻辑零（GND）永久使能。输出使能

