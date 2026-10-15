
程序函数的其他指令，`PUSH`和`POP`工作方式与`STMFD`/`LDMFD`相同。

虽然表面上看不出来，但实际上它们也会调整`SP`指针/`ADR`指令

与前文的作用。而`MOVS`指令负责返回值（`R0`寄存器）零。

### 3.4.3 ARM模式、开启优化选项的Code

如果不启用优化选项，`Xcode 6.3`将会产生大量的冗余代码，所以开始启用优化选项，让其生成最优的代码。通过指定生成编译`-O3`，使用`Xcode`编译`world`。这将得到如下所示的汇编代码。

### 3.13 开启优化选项 Xcode 6.3 (LLVM) (ARM模式)

```
.text:000028C4 helloworld
.text:000028C4 80 40 2D E9 STMFD SP!,{R7, LR}
.text:000028C8 86 06 01 E3 MOV R0, #0x186
.text:000028C8 07 70 A0 E1 MOV R7, SP
.text:000028D0 00 00 A3 MOV R0, R7
.text:000028D4 00 00 8F E0 ADD R0, PC, R0
.text:000028D8 C3 05 00 EB BL _puts
.text:000028DC 00 00 A3 MOV R0, #0
_text:00002E0 80 80 E8 LDMDF SP!, {R7, PC}
_cstring:00003F62 48 65 31 6C 6C+aHelloWorld_0 DCB"Hello\nWorld!", 0
```

我们就不重复介绍`STMFD`/`LDMFD`指令了。

第一个`MOV`指令字符串“Hello World!”的偏移量，`0x1686`赋值到`R0`寄存器。

“`MOV R0, #0`”将写入`R0`寄存器的高16位。在`ARM`模式里，常规的`MOV`指令可以操作字符串的低16位，而单条`ARM`指令最多32位字。当然，寄存器之间的数据传递没有这种限制。所以对寄存器的高位（第16位到第31位）进行赋值操作的`MOV`指令应运行而。然而此处的`MOV`指令可有不可，因为在执行一条指令“`MOV R0, 0x1686`”时，`R0`寄存器的高16位就会被清零。这或许就是编译器智能化的缺陷。

“`ADD R0, PC`”将`PC`和`R0`进行加法，计算出字符串的绝对地址。之前介绍了“位置无关”，我们知道程序运行之后的起始地址并不固定。程序对这个地址进行执行了必要的修正。

然后，通过`BL`指令调用`puts()`函数，而没有前文那样调用`printf()`函数。这种差异来自于`GCC`编译器[20]，编译器将第一个`printf()`函数替换为`puts()`函数（两个函数的参数完全相同）。

所谓“几乎”就意味着它们在差异实质上，如果`printf()`函数支持“`%`”开头的控制，而`puts()`函数则不支持这类字符串字符控制。如果参数中有这类类控制符，那么两个函数的输出结果还会相同。

为什么`GCC`编译器会做这种替换？大概是因为这种情况下`puts()`的效率更高。由于`puts()`函数不处理控制符（`%`），只是把每个字符输出到`stdout`设备，所以`puts()`函数的运行速度更快[21]。

后面的“`MOV R0, #0`”将`R0`寄存器清零。

## 3.4.4 Thumb-2下、开启优化选项的Xcode (LLVM)

默认情况下，`Xcode 4.6.3`会启用优化模式，并以`Thumb-2`模式编译源程序。

（此处省略重复的分析内容）

`17 jalr $25`

`18 addiu $4,$4,lo($LC0); branch delay slot`

`19 restore the RA:`

`20 lw $31,28($sp)`

`21 ; copy 0 from zero to v0:`

`22 move $2,$0`

`23 ; return by jumping to the RA:`

`24 j $31`

`25 ; function epilogue:`

`26 addiu $sp,$sp,32`

主函数启动的指令初始化了全局指针寄存器`GP`寄存器的值，并且把它加到64KB段的中央。同时，程序将`RA`寄存器的值存储到本地数据中。同样使用`puts()`函数加载了`printf()`函数。而`puts()`的地址，则通过`LUI(Load Word)`指令加载了`$25`寄存器。此后，字符串的高16位和低16位分别通过`LUI(Load Upper Immediate)`和`ADDIU(Add Immediate Unsigned Word)`指令加载到`$4`寄存器。`LUI`的`Upper-`指令说明将数据存储到寄存器的高16位。与此对应，`ADDIU`把将地址的低16位进行运算。但是会先于`JALR`之后[22]。`$4`其实是`AO`寄存器，在调用函数时跳转到第一个参数[23]

`JALR(Jump and Link Register)`指令跳转到`$25`寄存器的地址，即`puts()`的启动地址，并且把一条`LW`指令的地址存储在`RA`寄存器中。拷贝，`MIPS`调用函数的方法与`ARM`架构相似。注意的是，由于存在延迟终止，存储在`RA`寄存器的值并不是已经运行的，“一条”指令的地址，而是后面那（延迟终止后的）指令的地址。在执行这条`JALR`指令的时候，写入`RA`寄存器的值是`PC+8`，而不是那条`LW`指令的地址。

第19行的`LW(Load Word)`指令，用于把地中的`RA`值恢复。请注意，这条指令并不被调用函数的函数尾声。

第22行的`MOVE`指令把`$0($ZERO)`的值复制给`$2($VO)`。`MIPS`有一个寄存器，它的值是常量0。很明显，因为`MIPS`的开发者为了计算机中使用最多的常量，所以他们创建了一种`$0`寄存器提供数值0的机制。这个例子是为了另外另一个值值得注意的现象，在`MIPS`系统中，没有在寄存器之间复制数值的（硬件），`move, MOV, STORE`，通过加法指令`ADD DST, SRC,$SRC`变相来实现，即`DST=SRC+0`，这两种操作等效。由此可见，`MIPS`开发者希望可能复用`opcode`，从精简`opcode`的总数。然而并不代表每次运行`MOVE`指令时`CPU`都会进行实际的加法运算。`CPU`能够这类伪仿进行优化处理，在运行它们的时候并不会用到`ALU (Arithmetic logic unit)`。

第24行的`J`指令跳转到`RA`所指向的地址，完成被调用函数返回调用者函数的操作。还是由于分支预测延迟效应，其后的`ADDIU`指令会先由`J`指令运行，构成函数尾部。

我们再来看`IDA`生成的指令清单，熟悉一下寄存器的伪名名称。

## 代码清单.39 Optimizing GCC4.4.5(IDA)

```
1 .text:00000000 main:
2 .text:00000000
3 .text:00000000 var_10      = -0x10
4 .text:00000000 var_4       = -4
5 .text:00000000
6 ; function prologue:
7 ; set the GP:
8 .text:00000000
9 >> 16)lui               $gp, (__gnu_local_gp
10 .text:00000004      addiu    $sp, -0x20
11 .text:00000008      la       $gp, (__gnu_local_gp
12 ; save the RA to local stack:
13 .text:0000000C      sw       $ra,0x20+var_4
14 ; save the GP to local stack:
15 ; for some reason, this instruction is missing in GCC
assembly output:
16 .text:00000010      sw       $gp,0x20+var_10
17 ; load the address of puts() function from
18 $t9:
19 .text:00000014      lw       $t9,0x16(puts)($gp)
20 ; form the address of the text string in a0:
21 .text:00000018      lui      $a0,($LC0>>16)
22 "Hello, world!"
23 ; jump to puts(), saving the return address link register:
24 .text:0000001C      jalr     $t9
25 .text:00000020      la       $a0,($LC0&xFFFF)
26 "Hello, world!"
27 ; restore the RA:
28 .text:00000024      sw       $ra,0x20+var_4
29 ; copy 0 from zero to v0:
30 .text:00000026      move $v0,$zero
31 ; return by jumping to the RA:
32 .text:0000002c      jr $ra
33 ; function epilogue addiu $sp,0x20
34 .text:0000030
```
