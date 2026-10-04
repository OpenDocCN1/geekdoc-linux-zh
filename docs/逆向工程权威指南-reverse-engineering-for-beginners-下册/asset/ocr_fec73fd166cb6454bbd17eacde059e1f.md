如果将1与1比较，1-1=0，ZF标志位为“零”标识，最终运算结果是
0将被计算指令设置为1。两个不同的数值进行CMP比较时，ZF标志位的值
绝不会是1。JNE指令会根据ZF标志位的判断决定是否需要跳转，实际上
两者都是（Jump if Not Zero）的同义。JNE和JNZ的opcode相同。如同
即使使用减法运算操作SUB来替换CMP指令，Jcc指令也可以进行正常的
跳转。但未在使用SUB指令时，我们还需要使用一个寄存器保存运算结果，而
CMP则不需要使用寄存器保存运算结果。

# 7.3.2 MSVC: x86

现在来介绍推荐的好习惯。对于初学者来说，使用MSVC编译器的MD/MD
值很重要。这个选项要选择“不要链接（Link）函数
而是从MSVR* DLL导入这些标准函数。总之，使用/MD选项的
好处是一目了然的，我们需要知道它在哪里、调用了哪些标准函数。

在使用IDA分析程序的时候，要充分利用它的标记功能。比如，分析
这段程序的时候，我们可能会发现错误的时候执行JNE跳转。这时就可以用
鼠标点击跳转的JNE指令，按下“n”键，将对应的标签（label）改名为
“error”，然后对出错的标签重命名为“exit”。这种改进可以大幅
增强代码的可读性。

```
.text:00401000
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
.text:00401015      push             eax
.text:00401016      push             offset aD ; "%d"
.text:0040101B      call             ds:scanf
.text:00401021      add              esp, 8
.text:00401024      cmp             eax, 1
.text:00401027      jnz              short error
.text:00401029      mov             ecx, [ebp+var_4]
.text:0040102C      push             ecx
.text:0040102D      push             offset aYou ; "You entered d...\n"
.text:00401032      call             ds:printf
.text:00401038      add              esp, 8
.text:0040103B      jmp              short exit
```

* 非