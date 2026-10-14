
```abel
"when the signal, write, is high. When write goes low, it will output the saved value at pins D7..D0

inputs
write        pin;
myclock      pin;

"Bi-directional signal also has a register associated with it.
D7..D0        pin istype 'reg';

"Define my sets
Data = [D7..D0];

Equations
Data.oe = !write;    "3-State the data lines
                     "when writing to register

Data.clk = myclock;

WHEN (write==1) THEN Data := Data.pin;
"When we are writing to the part, read the
"data pins and save in data register.
ELSE
Data := Data;
"Else, drive the data pins with the value
"saved in the register so we can read it back.
end;
```

## 锁存器

锁存器可以通过两种方式实现。在第一个示例中，`latch_output` 利用触发器的异步置位和复位来实现一个锁存器。

```abel
module ltest1

input,le        pin;
latch_output    pin istype 'reg';

equations

latch_output.ap = input & le;
latch_output.ar = !input & le;
latch_output.clk = 0; "Clock must be
"grounded

latch_output.d = 0; "D-input must be
"grounded

test_vectors ([input, le] -> [latch_output])
[0,0] -> [0];
[1,0] -> [0];
[0,1] -> [0];
[1,1] -> [1];
[1,0] -> [1];
[0,1] -> [0];

end;
```

锁存器也可以通过使用反馈路径和提供一个冗余乘积项来消除毛刺，以组合方式实现。这需要以下代码：

```abel
MODULE comlatch;

le      pin;
input   pin;
latch_out pin istype 'com,retain';

// The ABEL compiler will retain redundant
// logic for the latch_out output
// because they have the RETAIN attribute.
// However, the MINIMIZE OFF property
// statement is required to instruct the
// Xilinx fitter to also retain the
// redundant logic.

xeqid property 'minimize off latch_out';
" The fitter will retain redundant logic
" for these nodes

EQUATIONS;

    latch_out = input & le
    " latch is transparent high
# latch_out & !le
    " latch data on falling edge of le
# latch_out & input;
    " Redundant product term

TEST_VECTORS
([le, input] -> [latch_out])
[1, 0 ] -> [ 0 ]; " transparent
[1, 1 ] -> [ 1 ]; " transparent
[0, 1 ] -> [ 1 ]; " latch a 1
[0, 0 ] -> [ 1 ]; " change input
[1, 0 ] -> [ 0 ]; " transparent
[0, 0 ] -> [ 0 ]; " latch a 0
[0, 1 ] -> [ 0 ]; " change data

END; " All modules must have an END statement
```

## 计数器

计数器在各种应用中非常有用，例如存储器接口、生成延迟状态或简单的状态机。本示例演示了如何构建一个带有计数使能的可加载加/减计数器。

```abel
module counter

"32-bit Up/Down counter with parallel load and enable

"Outputs
Q31..00    pin istype 'reg';

"Inputs
D31..00    pin;          " Load Cmd
Load       pin;          " Count Cmd
Count_Enable pin;        " Up/Down Cmd
UpDown     pin;          " Clock
myclk      pin;

Counter = [Q31..00];
Input   = [D31..00];

Equations
@carry 4;
Counter.clk = myclk;
WHEN (!Load & Count_Enable & UpDown)
THEN Counter := Counter + 1
else
WHEN (!Load & Count_Enable & !UpDown)
THEN Counter := Counter - 1
else
WHEN (Load)
THEN Counter := Input;
else
```

## 多路选择器

多路选择器可用于控制设计中的数据流。以下示例演示了如何实现一个 16 位 4 选 1 寄存器型多路选择器：

```abel
module mux2
A15..A0    pin; " Inputs
B15..B0    pin; " Inputs
C15..C0    pin; " Inputs
D15..D0    pin; " Inputs
Q15..Q0    pin istype 'reg'; " output

Sel1..Sel0 pin;
clk        pin;

Output = [Q20..Q0];
DataA = [A20..A0];
DataB = [B20..B0];
DataC = [C20..C0];
DataD = [D20..D0];
Select = [Sel1..Sel0];

Equations

Output.clk = clk;

WHEN Select == 0 THEN Output := DataA
else WHEN Select == 1 THEN Output := DataB
else WHEN Select == 2 THEN Output := DataC
else Output := DataD;

end
```

## 结论

ABEL 使得复杂的行为级设计可以轻松地实现和仿真。此外，通过 ABEL 属性语句可以方便地访问器件的特殊特性和功能。ABEL 是一种简单而强大的软件工具，为设计者提供了一种高效的语言，用于开发 Xilinx FPGA 和 CPLD 设计。

