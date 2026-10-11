
rax 76                  rsi 0x7fffffffeb38 r8 0x400cfa

rbx 76                  rdi 0x1               r9 0x0

rcx 0xffffffffffffbp 0x7fffffeea50 r10 0x1

rdx 0x7fffffeb48 rsp 0x7fffffeea50 r11 0x246

rip 0x400c36            eflags ZF

```
移位位数 76（6 位）将得到 `set` 的字。因为 $2^6 = 64$，这在 `rbx` 中留下了 1。

## Registers

```
rax 76                  rsi 0x7ffffeb38 r8 0x40cfa

rbx 1                   rdi 0x1               r9 0x0

rcx 0xffffffffff 0x7ffffea50 r10 0x1

rdx 0x7ffffeb48 rsp 0x7ffffea50 r11 0x24
```

在 `rax` 中得到了该位的另一个副本。

## Registers

```
rax 76                  rsi 0x7ffffeb38 r8 0x40cfa

rbx 1                   rdi 0x1               r9 0x0

rcx 12                  rbp 0x7ffffea50 r10 0x1

rdx 1                   rsp 0x7ffffea50 r11 0x246
```

这 6 位将是该字。

第 76 位将是包含该位的内存字。

## Registers

```
rax 76                  rsi 0x7ffffeb38 r8 0x40cfa

rbx 1                   rdi 0x1               r9 0x0

rcx 12                  rbp 0x7ffffea50 r10 0x1

rdx 1                   rsp 0x7ffffea50 r11 0x246
```

接下来使用 `xor` 清零 `rdx`。

## Registers

```
rax 76                  rsi 0x7ffffeb38 r8 0x40cfa

rbx 1                   rdi 0x1               r9 0x0

rcx 12                  rbp 0x7ffffea50 r10 0x1

rdx 0                   rsp 0x7ffffea50 r11 0x246
```

第 18 行测试我们要从数组测试的位。你会注意到进位标志（CF）被设置了。

## Registers

```
rax 76                  rsi 0x7ffffeb38 r8 0x40cfa

rbx 1                   rdi 0x1               r9 0x0

rcx 12                  rbp 0x7ffffea50 r10 0x1

rdx 0                   rsp 0x7ffffea50 r11 0x246
```

第 19 行使用 `setcc` 指令设置 `dl` 为1，因为它在集合中。

## Registers

```
rax 76                  rsi 0x7ffffeb38 r8 0x40cfa

rbx 1                   rdi 0x1               r9 0x0

rcx 12                  rbp 0x7ffffea50 r10 0x1

rdx 1                   rsp 0x7ffffea50 r11 0x246
```

第 20 行设置集合中的位。

```
mov rex, [sample] : 将 qword 移入 rex

shl rex, 12 : 清除高位

shr rex, 35 : 对齐位域

mov [field], rex : 保存字段
```

现在，假设我们希望将 `sample` 的第 51-23 位填充为 `field` 中的位。简单的方法是将值进行旋转以对齐字段，向右移，然后将字段左移回第 23-51 位。以下是代码：

```
mov rex, [sample] : 将 qword 移入 rex

ror rex, 23 : 将第 23 位对齐到 0

shr rex, 29 : 清除 29 位

shl rex, 29 : 再次对齐位

or rex, [field] : 假设 field 是 29 位

rol rex, 23 : 重新对齐位域

mov [sample], rex : 将字段存储在内存中
```

## 练习 (Exercises)

- 1. 编写一个汇编程序，计算内存中一个字节中所有 1 位（1 bits）的数量。使用重复代码而不是循环。
- 2. 编写一个汇编程序，使用 `xor` 交换内存中的两个四字节字（quad-words）。使用以下算法：

```
a = a ^ b

b = a ^ b

b = a ^ b
```
- 3. 编写一个汇编程序，使用内存中的 3 个四字节字来表示 3 组：A、B 和 C。每个组都允许在四字节字对应的位中存储从 0-63 的集合值。执行以下步骤：

```
insert 0 into A

insert 1 into A

insert 7 into A

insert 13 into A

insert 1 into B

insert 3 into B

insert 12 into B

store A union B into C

store A intersect B into C

store A - B into C

remove 7 from C
```
- 4. 编写一个汇编程序，将存储在内存中的四字节字移动到寄存器中，然后计算该字 8 个字节的异或。使用 `or` 或 `rol` 指来操作寄存器的位，以保留原始值。
- 5. 编写一个汇编程序，解析内存中的一个双精度浮（double）。这是一个 64 位的浮点值。将符号位存储在一个内存位置。将减去偏置值（bias）后的指数存储在第二个内存位置。将带有前导隐式 1 位的小数部分字段存储在第三个内存位置。
- 6. 编写一个汇编程序，使用整数算术和位操作执行两个浮点数的乘积。从内存中的两个浮点数开始，并将乘积存储在内存中。

# 第 8 章 (Chapter 8)

## 分支与循环 (Branching and looping)

到为止，我们的代码未使用任何分支语句。使用条件移动指令（conditional move instructions）为代码增加了一些灵活性，同时保留了 CPU 的流水线内容。我们已经看到，重复指令来处理四字节字的每个字节或每个字节的每一位可能是很麻烦的。在下一节我们将处理数组。通过重复指令来处理包含 100 万个元素的数组是愚蠢的。这可能是可能的，但处理变动大小的数组将非常痛苦。我们需要循环。

在许多程序中，您需要测试一个条件并根据结果执行 2 个动作之一。如果这两个动作非常简单，那么条件移动是高效的。如果每个动作都是几条很长的指令，那么我们需要条件跳转语句（conditional jump statement）来跳转到一种替代方案，同时允许 CPU 通过不跳转来处理另一种替代方案。在完成第二种替代方案后，我们通常需要跳过第一种方案的代码。我们需要条件和无条件分支语句。

## 8.1 无条件跳转 (8.1 Unconditional jump)

无条件跳转指令（`jmp`）是 `goto` 语句的汇编版本。然而，使用 `jmp` 显然不可耻。它在汇编语言中是必要的，而在高级语言中 `goto` 是可以避免的。

`jmp` 指令的基本形式是：

```
jmp

label
```
