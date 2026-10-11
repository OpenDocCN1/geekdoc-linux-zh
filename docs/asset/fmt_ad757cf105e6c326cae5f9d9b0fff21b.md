
# 无条件跳转

其中 `label` 是程序文本段中的一个标签。汇编器将生成一个相对于 `rip` 的相对跳转指令（rip relative jump instruction），这意味着控制流将转移到相对于当前指令指针（instruction pointer）当前值的位置。最简单的相对跳转使用一个 8 位符号立即数，并编码为 2 字节。这允许向前或向后跳转约 127 字节。下一种相对跳转使用 32 位符号立即数，总共需要 5 字节。幸运的是，汇编器会找出可以使用哪种类型并选择较短的形式。程序员只需指定标签。

跳转语句的效果是 CPU 将控制权转移到加载地址处的指令。除非与条件跳转配合使用，否则这通常并不令人兴奋。然而，跳转指令可以跳转到包含在寄存器或内存位置中的地址。条件移动可能可以使用无条件跳转到包含在寄存器中的地址。还有一种有趣的可能性——实现一个 `switch` 语句。假设你有一个变量 `i`，已知它包含 0 到 2 之间的值。那么你可以构造一个地址数组，并使用跳转指令根据 `i` 的值跳转到代码段。这里有一个示例：

```
segment .data

switch:

  dq main.case0

  dq main.case1

  dq main.case2

i:

  dq 2

segment .text

global main

main:

  mov rax, [i] ; 将 i 移到 switch (i)

case0:

  mov rbx, 0 ; 如果 i == 0，跳转到这里

  jmp .end

case1:

  mov rbx, 1 ; 如果 i == 1，跳转到这里

  jmp .end
```

无条件跳转指令（`jmp`）是 `goto` 语句的汇编版本。然而，使用 `jmp` 显然不可耻。它在汇编语言中是必要的，而在高级语言中 `goto` 是可以避免的。

`jmp` 指令的基本形式是：

```
jmp
label
```

其中 `label` 是程序文本段中的一个标签。汇编器将生成一个相对于 `rip` 的相对跳转指令，这意味着控制流将转移到相对于当前指令指针（instruction pointer）当前值的位置。最简单的相对跳转使用一个 8 位符号立即数，并编码为 2 字节。这允许向前或向后跳转约 127 字节。下一种相对跳转使用 32 位符号立即数，总共需要 5 字节。幸运的是，汇编器会找出可以使用哪种类型并选择较短的形式。程序员只需指定标签。

## 8.2 条件跳转 (8.2 Conditional jump)

条件跳转（conditional jump）允许根据标志位（flags）来执行跳转。如果这两个动作非常简单，那么条件移动是高效的。如果每个动作都是几条很长的指令，那么我们需要条件跳转语句来跳转到一种替代方案，同时允许 CPU 通过不跳转来处理第二种替代方案。在完成第二种替代方案后，我们通常需要跳过第一种方案的代码。我们需要条件和无条件分支语句。

条件跳转（conditional jump）是汇编语言中的 `if` 语句。常用的条件跳转包括 `jz`（跳转零）、`jnz`（跳转非零）、`je`（相等）、`jne`（跳转不相等）、`jg`（跳转大于）、`jge`（跳转大于等于）、`jl`（跳转小于）、`jle`（跳转小于等于）、`jc`（跳转进位）、`jnc`（跳转无进位）、`ja`（跳转以及）、`jae`（跳转以及等于）。

以下是常用的条件跳转指令：

| 指令 | 含义 |
| :--- | :--- |
| `jz` | 跳转为零 |
| `jnz` | 跳转非零 |
| `je` | 跳转相等 |
| `jne` | 跳转不相等 |
| `jg` | 跳转大于 |
| `jge` | 跳转大于等于 |
| `jl` | 跳转小于 |
| `jle` | 跳转小于等于 |
| `jc` | 跳转进位 |
| `jnc` | 跳转无进位 |
| `ja` | 跳转以及 |
| `jae` | 跳转以及等于 |

条件跳转通常与 `cmp`（比较）或 `test` 指令配合使用。`cmp` 会将两个操作数相减并设置标志位，而 `test` 对两个操作数进行位与运算并设置标志位。

例如：

```
cmp eax, ebx

jz label ; 如果 eax 等于 ebx，则跳转到 label
```

```
; jmp endif
} else {
; else:
; max = a;
mov [max], rax
}
endif;
```

# If/else-if/else 语句

就像在 C/C++ 中一样，你可以在 else 子句中使用 if 语句，在汇编代码条件语句的 else 子句中继续进行测试。以下是 C 语言中的简短 if/else-if/else 语句：

```
if (a < b) {
result = 1;
} else if (a > c) {
result = 2;
} else {
result = 3;
}
```

这段代码可能是 2 个条件语句的良好候选，但简单就是美。以下是该代码对应的汇编代码：

```
if (a < b) {
mov rex, [a]
mov rbx, [b]
cmp rex, rbx
jnl else_if
result = 1;
jmp endif
} else if (a > c) {
mov rcx, [c]
cmp rex, rcx
jng result = 2;
mov qword [result], 2
jmp endif
} else {
result = 3;
mov qword [result], 3
}
```
