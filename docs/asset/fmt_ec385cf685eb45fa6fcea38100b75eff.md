
```assembly
mov %rcx, -0x20(%rbp)  # RCX -> RBP-0x20
addl $1, (%rax)         # 1 + RAX -> RAX
push %rsi               # RSP - 8 -> RSP
                                RSI -> RSP
inc (%rcx)              # 1 + RCX -> RCX
```

© 2023 Software Diagnostics

存储与加载类似。

### x64 流指令 (x64 Flow Instructions)

![](img/c36cc1b69ac7baa75db5d13135bb9d30_186_0.png)

`Goto`（无条件跳转）通过 `JMP` 指令实现。函数调用通过 `CALL` 指令实现。对于条件分支，请参考官方官方文档。

### x64 函数参数 (x64 Function Parameters)

![](img/c36cc1b69ac7baa75db5d13135bb9d30_187_0.png)

在 x64 Linux 平台上，从左到右的前六个 C 和 C++ 函数参数移动到 CPU 寄存器，其余参数通过栈位置传递。

### x64 结构体函数参数 (x64 Struct Function Parameters)

![](img/c36cc1b69ac7baa75db5d13135bb9d30_0.png)

当调用对象结构体非静态成员函数时，第一个参数是隐式的，并在 x64 Linux 平台上通过 **`RDI`** 传递。它是一个对象地址，用于帮助方法区分相同结构类型的对象并引用正确的字段内存。其余参数按常法传递。

### A64 CPU 寄存器

![](img/c36cc1b69ac7baa75db5d13135bb9d30_189_0.png)

从 `X0` 到 `X30` 共有 31 个通用寄存器，其中一些被分配给特定任务，例如过程内调用（`X16`、`XIP7` 和 `X17`）、栈帧寻址（帧指针，`FP`, `X29`）以及返回地址，即所谓的链接寄存器（Link Register，`LR`, `X30`）。当您调用一个函数时，调用者的返回地址会被保存在 `LR` 中，而不会像 Intel/AMD x64 那样。被调用者的返回指令使用 `LR` 中的地址赋给 `PC` 并恢复执行。但如果被调用者又调用了其他函数，则需要手动将当前的 `LR` 保存到某个地方（通常在栈上）。当然，还有栈指针 **`SP`**。为了获取零值，还有一个所谓的零寄存器 `XZR`**。所有的 `X` 寄存器都是 64 位的，32 位低位通过 `W` 前缀进行访问。接下来，我们简要回顾与我们练习相关的某些方面。

### A64 指令与寄存器

![](img/c36cc1b69ac7baa75db5d13135bb9d30_190_0.png)

- 令码 `DST, SRC, SRC2`

- 示例：

```assembly
mov  x0, #16          // X0 <- 16 (0x10)
mov  x29, sp         // X29 <- SP
add  x1, x2, #16     // X1 <- X2+16 (0x10)
mul  x1, x2, x3      // X1 <- X2*X3
blr x8              // X8 已经包含了
                     // 函数地址 (&func)
                     // LR <- PC+4; PC &func
                     // SP <- SP-48 (-0x30)
sub  sp, sp, #48     // 为局部变量留出空间
```

这张幻灯片展示了几个涉及寄存器操作的 CPU 指令示例，例如移动值和进行算术运算。如果您习惯 Windows 上的 WinDbg，那么操作数的方向与 Intel x64 的反汇编格式相同。它等同于赋值。`BLR` 是对地址在寄存器中的函数的调用。`BL` 代表 Branch and Link（跳转并链接）。

### A64 内存与栈寻址

![](img/c36cc1b69ac7baa75db5d13135bb9d30_191_0.png)

在查看内存操作之前，让我们先看内存寻址的图形化表示。线程栈只是其他内存区域之一，因此除了 **`SP`** 和 **`X29 (FP)`** 外，可以使用任何其他寄存器。请注意，栈向低地址方向增长，因此要访问之前推入的值，您需要使用相对于 **`SP`** 的正偏移量。

### A64 内存加载指令

![](img/c36cc1b69ac7baa75db5d13135bb9d30_192_0.png)

- 令码 `DST, DST_, [SRC], Offset`

- 令码 `DST, DST_, [SRC], Offset` // 后递增

- 示例：

```assembly
ldr x0, [sp] // x0 ← 地址 SP+0 处的值
ldr x0, [x29, -8] // x0 ← 地址 X29-0x8 处的值
ldr x29, x30, [sp, #16] // x29 ← 地址 SP+32 (0x20) 处的值
ldr x29, x30, [sp] // x30 ← 地址 SP+0 (0x28) (注：此处原文可能有误，保持翻译)
ld x29, x30, [sp] // x29 ← 地址 SP+0 (此处为ld)
```

常量编码在指令中，但如果我们需要任意值，则必须从内存中获取。方括号表示相对于某些寄存器中存储地址的内存访问。还有一个在加载后调整寄存器值的选项，即所谓的后递增，它可以为负。

### A64 内存存储指令

- 令码 `SRC, SRC2, [DST, Offset]`

- 令码 `SRC, SRC2, [DST, Offset]!` // 前递增

- 示例：

```assembly
str x0, [sp, #16]               // x0 -> 地址 SP+16 (0x10) 处的值
str x0, [x29, #-8]             // x0 -> 地址 SP+32 处的值
stp x29, x30, [sp, #32]          // x29 -> 地址 SP+40 (0x28) 处的值
stp x29, x30, [sp, #-16]!        // SP -> SP-16 (-0x10)
                                     // x29 -> 设置地址 SP 处的值
                                     // x30 -> 设置地址 SP+8 处的值
```

操作数的顺序与其他指令相反。在存储之前，有可能对目标寄存器进行前递增。

### A64 流指令

令码 `DST, SRC`

示例：

```assembly
adrp x0, 0x42000      // x0 ← 0x42000
b 0x10493fc         
```

由于原文中存在一些乱序或重复的描述，以下是基于上下文的逻辑翻译：

由于指令大小为 4 字节，`ADRP` 指令用于计算页面地址。`B` 指令用于无条件跳转。

### A64 捕获变量

![](img/c36cc1b69ac7baa75db5d13135bb9d30_195_0.png)

在 ARM64 平台上，栈操作是通过寄存器传递的。

### A64 结构体参数

![](img/c36cc1b69ac7baa75db5d13135bb9d30_196_0.png)

当调用成员函数时，第一个参数通过寄存器传递。

### Clang 伪代码示例及对应的 x64 反汇编

```cpp
// Clang
struct Lambda0 {
  int b;
  Lambda0(int _b) : b(_b) {}
  auto operator()(int x) { return b-x; }
} negate5;
```

```cpp
// Clang
struct Lambda1 {
  int& rb;
  Lambda1(int& _rb) : rb(_rb) {}
  auto operator()(int x) { return rb-x; }
} negate6;
```

```assembly
movl $0x,-0x4(rbp),%eax
mov -0x18(rbp),%eax
lea -0x18(rbp),%rdi
mov $0xa,%esi
callq $<0::operator()(int) const>
```

```assembly
movl $0x,-0x4(rbp),%rcx
lea -0x28(rbp),%rcx
mov -0x28(rbp),%rdi
mov $0xa,%esi
callq *$1::operator()(int) const>
```

### A64 示例

```cpp
{
  int b = 0;
  auto negate1 = [&](int x) { return b - x; };
  auto negate2 = [&](int x) { return b - x; };
  auto negate4 = [&](int x) { return b - x; };
  auto negate5 = [&](int x) { return b - x; }; negate5(10);
  auto negate6 = [&](int x) { return b - x; }; negate6(10);
}
```

```cpp
// GCC
struct lambda<int> {
  int b;
  lambda<int>(int b) : b(b) {}
  auto operator()(int x) { return b-x; }
} negate5;
```

```assembly
  str wzr, [sp, #36]
  ldr w0, [sp, #32]
  str [sp, #32]
  add x0, sp, #0x20
  mov w1, #0xa
  str [sp, #0x24]
  mov x1, sp, #0xa0
  bl <<lambda<int>::operator()(int) const
```

针对相同 lambda 的 GCC 伪代码及对应的 ARM64 反汇编：

```cpp
// GCC
struct lambda<int> {
  int b;
  lambda<int>(int _b) : b(_b) {}
  auto operator()(int x) { return b-x; }
} negate5;
```

```assembly
  str wzr, [sp, #36]
  ldr w0, [sp, #32]
  str [sp, #32]
  add x0, sp, #0x20
  mov w1, #0xa
  bl <<lambda<int>::operator()(int) const
```

```cpp
// GCC
struct lambda<int> {
  int rb;
  lambda<int>(int _rb) : rb(_rb) {}
  auto operator()(int x) { return rb-x; }
} negate5;
```

```assembly
  ldr w0, [sp, #36]
  ldr w0, [sp, #24]
  add x0, sp, #0x20
  str x0, [sp, #48]
  mov w1, #0xa
  str x0, [sp, #0x30]
  bl <<lambda<int>::operator()(int) const
```

### 作为参数的 Lambda

```cpp
auto negate = [](int x) { return -x; };

int apply(int arg, int (*pf)(int)) {
    return pf(arg);
}

int apply2(int arg, decltype(negate) f) {
    return f(arg);
}

void foo() {
    // Clang: apply(100, $<0::operator()(int) const&&$0)
    apply(100, negate);
}
```

```assembly
apply: // Clang
push %rbp
mov %rbp, %rsp
sub %rsp, $16
mov %edi, -10(%rbp)
mov -8(%rbp),%rsi
mov %rdi
callq *%rsi

apply2: // Clang
push %rbp
mov %rbp, %rsp
sub %rsp, $16
mov %edi, 4(%rbp)
mov 8(%rbp),%rsi
mov %x12(%rbp),%rdi
lea -x8(%rbp),%rdi
callq $<0::operator()(int) const
```

`Lambda` 可以作为函数参数传递。我们可以使用 `decltype` 来指定它们的类型。如果期望的是普通的函数指针，则内部会有一个特殊的调用者函数处理调用。如果期望的是 lambda 类型参数，则会调用 lambda 函数对象的 `operator()`。

```cpp
auto negate = [](int x) { return -x; };

int apply(int arg, int (*pf)(int)) {
    return pf(arg);
}

int apply2(int arg, decltype(negate) f) {
    return f(arg);
}

void foo() {
    // Clang: apply(100, $<0::operator()(int) const&&$0)
    apply(100, negate);
}
```

### 对应的 Clang x64 汇编

```assembly
apply: // Clang
push %rbp
mov %rbp, %rsp
sub %rsp, $16
mov %edi, -10(%rbp)
mov -8(%rbp),%rsi
mov %rdi
callq *%rsi

apply2: // Clang
push %rbp
mov %rbp, %rsp
sub %rsp, $16
mov %edi, 4(%rbp)
mov 8(%rbp),%rsi
mov %x12(%rbp),%rdi
lea -x8(%rbp),%rdi
callq $<0::operator()(int) const
```

### A64 Lambda 参数示例

```cpp
auto negate = [](int x) { return -x; };

int apply(int arg, int (*pf)(int)) {
    return pf(arg);
}

int apply2(int arg, decltype(negate) f) {
    return f(arg);
}

void foo() {
    // Clang: apply(100, $<0::operator()(int) const&&$0)
    apply(100, negate);
}
```

```assembly
  str wzr, [sp, #36]
  ldr w0, [sp, #32]
  str [sp, #32]
  add x0, sp, #0x20
  mov w1, #0xa
  str [sp, #0x24]
  mov x1, sp, #0xa0
  bl <<lambda<int>::operator()(int) const
```

### Lambda 参数优化

如果你通过引用传递 lambda，则不会产生函数对象的拷贝。代码示例及对应的汇编语言：

```cpp
auto negate = [](int x) { return -x; };
int apply3(int arg, const decltype(negate)& crf) {
    return crf(arg);
}
void bar() {
    apply3(103, negate);
}
```

在 x64 Clang 反汇编中，我们看到通过 `RSI` 传递的函数对象地址，它随后作为 `operator()` 的隐式参数：

```assembly
apply3: // Clang
push %rbp
mov %rbp, %rsp
sub %rsp, $0x0
mov %edi,-4(%rbp)
mov %rsi,-0x10(rbp)
mov -0x10(rbp),%rdi
mov -4(%rbp),%esi
callq $<0::operator()(int) const>
add $0x10,%rsp
pop %rbp
retq
```

### A64 优化示例

```cpp
auto negate = [](int x) { return -x; };
int apply3(int arg, const decltype(negate)& crf) {
    return crf(arg);
}
void bar() {
    apply3(102, negate);
}
```

在 Clang x64 汇编语言中，我们看到了捕获上下文的函数对象构造函数：
