
当被调用函数 `callee`（本例中 `scanf` 函数）使用 `EAX` 寄存器值向调用函数 `caller`（本例中 `jne` 指令）传递返回值。

之后，`CMP EAX, 1` 指令对返回值进行比对，检查其值是否为 1。

`JNE` 是跳转指令，全称是“Jump if Not Equal”。在两个值不同时跳转。

就是，如果 `EAX` 寄存器的值不是 1，则程序将跳转到 `JNE` 所指向的地址（本例中会接到 `$LN1@main`），在将控制权交给这个地址之后，CPU 将执行其后的打印指令，显示“What you entered? Huh?”。另一种情况是 `scanf` 函数成功读取指定数据类型的数据，其返回值为 1，此时不会发生跳转，而是继续执行 `JNE` 以前的指令，显示“You entered %d... ”和变量 `x` 的值。

`scanf` 函数成功赋值变量值的情况下，程序一路执行到 `JMP`（无条件跳转）指令。该指令跳转到第二个调用指令 `printf` 函数的指令，从“`XOR EAX, EAX`”指令开始，并完成返回 0 的操作。

可见，“一般地说”是指判断语句中出现的“`CMP/Jcc`”指令。此处 `cc` 是英文“condition code”的缩写。比较两个指令会设置处理器的标志位 [44]。`Jcc` 指令会检查标志位，判断是否进行跳转。

但是这种说法容易产生误导，实际 `CMP` 指令进行的操作是减法运算。确切地说，不仅是 `CMP` 指令，所有的“数学/算术计算”指令都会设置标志位。

是的，如果将 1 与 1 比较，1-1=0，`ZF` 标志位为“零”标识，最终运算结果是 0，将被计算指令设置为 1。两个不同的数值进行 `CMP` 比较时，`ZF` 标志位的值绝不会是 1。`JNE` 指令会根据 `ZF` 标志位的判断决定是否需要跳转，实际上两者都是（Jump if Not Zero）的同义。`JNE` 和 `JNZ` 的 `opcode` 相同。如同即使使用减法运算操作 `SUB` 来替换 `CMP`，`Jcc` 指令也可以进行正常的跳转。但在未使用 `SUB` 指令时，我们还需要使用一个寄存器保存运算结果，而 `CMP` 则不需要使用寄存器保存运算结果。

### 7.3.2 MSVC: x86

现在介绍推荐的好习惯。对于初学者来说，使用 MSVC 编译器的 `MD` 值很重要。这个选项要选择“不要链接（Link）函数而是从 MSVC* DLL 导入这些标准函数”。总之，使用 `/MD` 选项的好处是一目了然的，我们需要知道它在哪里、调用了哪些标准函数。

在使用 `IDA` 分析程序的时候，要充分利用它的标记功能。比如分析这段程序的时候，我们可能会发现错误的时候执行 `JNE` 跳转。这时就可以用鼠标点击跳转的 `JNE` 指令，按下“n”键，将对应的标签（label）改名为“error”，然后对出错的标签重命名为“exit”。这种改进可以大幅增强代码的可读性。

```text
.text:00401000

.text:00401000 var_4 = dword ptr -4

.text:00401000 argc = dword ptr 8

.text:00401000 argv = dword ptr 8

.text:00401000 envp = dword ptr 10h

.text:00401000

.text:00401000

                   push             ebp
.text:00401001      mov             ebp, esp
.text:00401003      push             ecx
.text:00401004      push             offset Format ; "Enter X: \n"
.text:00401009      call             ds:printf
.text:0040100F      add              esp, 4
.text:00401012      lea             eax, [ebp+var_4]
.text:00401015      push             ecax
.text:00401016      push             offset aD ; "%d"
.text:0040101B      call             ds:scanf
.text:00401021      add              esp, 8
.text:00401024      cmp             eax, 1
.text:00401027      jnz              short error
.text:00401029      mov             ecx, [ebp+var_4]
.text:0040102C      push             ecx
.text:0040102D      push             offset aE ; "You entered...\n"
.text:00401032      call             ds:printf
.text:00401038      add              esp, 8
.text:0040103B      jmp              short exit
```

如此一来，这段代码就容易理解了。虽然重命名标签的功能强大，但是每一个指令无疑都是。此外 `IDA` 还有一些高级用法。整理代码：标记某段代码后，键盘上的“-号”，整段代码将被隐藏，只留下地址和标签。在例子中我隐藏了这两段代码，并对整段代码进行了命名。

```text
.text:00401000 segmenttext
.text:00401012 get X
.text:00401024      cmp             eax, 1
.text:00401027      jnz              short error
.text:00401029      mov             ecx, [ebp+var_4]
.text:0040102C      push             ecx
.text:0040102D      push             offset aE ; "You entered...\n"
.text:00401032      call             ds:printf
.text:00401038      add              esp, 8
.text:0040103B      jmp              short exit
```

如需显示之前的代码，可以直接使用数字上的“+”号。按下空格键，`IDA` 将进入图解模式。其效果如图7 所示。

```c
int __cdecl main()
var_4 = dword ptr -4
argc = dword ptr 8
argv = dword ptr 8
envp = dword ptr 1Ch
push ebp
mov ebp, esp
push ecx
push offset Format ; "Enter X:\n"
call ds:printf
add esp, 4
lea eax, [ebp+var_4]
push eax
push offset a0 ; "%d"
call ds:scanf
add esp, 8
cmp eax, 1
jnz short exit
```
