

## Listing 5.5 4位超前进位加法器的 VHDL 代码 (LKADD.VHD)。

```vhdl
-- Look-ahead Adder

LIBRARY IEEE;
USE IEEE.std_logic_1164.ALL;

-- Look-ahead Adder interface description
ENTITY lkadd IS
    PORT
    (
        a: IN STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit addend
        b: IN STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit addend
        cin: IN STD_LOGIC; -- input carry
        sum: OUT STD_LOGIC_VECTOR (3 DOWNTO 0); -- 4-bit sum
        cout: OUT STD_LOGIC -- carry output
    );
END lkadd;

-- Look-ahead Adder architecture description
ARCHITECTURE lkadd_arch OF lkadd IS
    -- signal vectors for transferring the carry-propagate,
    -- carry-generate, and carry signals between the adder stages
    SIGNAL g: STD_LOGIC_VECTOR (3 DOWNTO 0); -- carry-generate
    SIGNAL p: STD_LOGIC_VECTOR (3 DOWNTO 0); -- carry-propagate
    SIGNAL c: STD_LOGIC_VECTOR (3 DOWNTO 0); -- carry
BEGIN
    PROCESS (a,b,cin,g,p,c)
    BEGIN
        -- use a FOR loop to iteratively connect the logic operations
        -- for the carry-generate, carry-propagate, and sum signals
        FOR i IN 0 TO 3
        LOOP
            g(i) <= a(i) AND b(i);
            p(i) <= a(i) XOR b(i);
            sum(i) <= p(i) XOR c(i);
        END LOOP;
        -- compute the carry bits for each stage of the adder
        c(0) <= cin;
        c(1) <= g(0) OR (p(0) AND c(0));
        c(2) <= g(1) OR (p(1) AND g(0)) OR
                (p(1) AND p(0) AND c(0));
        c(3) <= g(2) OR (p(2) AND g(1)) OR
                (p(2) AND p(1) AND g(0)) OR
                (p(2) AND p(1) AND p(0) AND c(0));
        cout <= g(3) OR (p(3) AND g(2)) OR
                (p(3) AND p(2) AND g(1)) OR
                (p(3) AND p(2) AND p(1) AND g(0)) OR
                (p(3) AND p(2) AND p(1) AND p(0) AND c(0));
    END PROCESS;
END lkadd_arch;
```

## 项目

1. 编译上一章中的 8 位行波进位加法器。创建一个简单的输入模式，使加法器在将时钟波形作为 $c_{in}$ 输入到加法器时表现出最坏情况延迟。仿真加法器并观察延迟。将加法器下载到你的 XS40 或 XS95 板上，并用示波器测量延迟。

2. 使用 4 位超前进位模块设计一个 8 位超前进位加法器。对该加法器施加相同的输入模式。仿真加法器并观察最坏情况延迟。将加法器下载到你的 XS40 或 XS95 板上，并用示波器测量延迟。将该加法器的最坏情况延迟和大小与行波进位加法器进行比较（使用报告文件）。更快的设计在你的 FPGA 中是否占用更多空间？

## 触发器

### 目标

- 展示触发器的工作原理。
- 展示不同类型的触发器。
- 展示计数器是如何由触发器构成的。

### 讨论

到目前为止，我们实验的组合电路仅根据当前输入产生输出。当输入发生变化时，输出会立即发生变化（当然经过一定的门延迟）。组合电路没有记住过去发生的事情的方法；它们是当下的产物。

本章将向你介绍时序电路。时序电路能够记住它们所经历的事情，并利用它来改变未来的行为。计数器就是时序电路的一个例子，因为它记住当前值并可以对其加一以得到下一个值。计数器的当前值被称为其状态。当前状态决定了计数器的下一个状态。例如，如果计数器当前存储数字五，那么下一次计数器被命令递增时，它将存储值六。从五到六的状态变化称为状态转换。

状态的概念很容易理解，但我们目前还不足以构建计数器。我们必须从更简单的东西开始。最简单的时序电路是 S-R 触发器 (SRFF)。SRFF 可以记住单个位是 1 还是 0。这个单比特存储器可以用作所有其他时序电路的基础。

SRFF 的操作如图 6.1a 所示。SRFF 由两个 2 输入 NAND 门构成，每个门的输出都反馈到另一个门的其中一个输入。NAND 门的剩余输入标记为 /S 和 /R，而输出标记为 Q 和 /Q。在图 6.1a 中，/S 和 /R 均保持在 +5 V，而 Q = 1 且 /Q = 0。请注意，当 /S = 1 且 /Q = 0 时，Q 输出应为 1，因为其 NAND 门的一个输入为低电平。另请注意，当

