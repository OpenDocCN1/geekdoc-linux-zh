
```python
10
11 def doB(registers,args):
12     (_addr,_)=args
13     registers[PC] = addr
14     return registers
15
16 def doZ(registers,args):
17     (r1,addr1,addr2)=args
18     if registers[r1]:
19         registers[PC] = addr1
20     else:
21         registers[PC] = addr2
22     return registers
23
```

`executeInstruction` 函数通过指令上的条件简单调用相应的处理函数：

> Listing 1.3 executeInstruction (instr,args,registers,systemState):

```python
1 def executeInstruction(instr,args,registers,systemState):
2     if instr=LDR:
3         (registers,systemState)=doLDR(registers,systemState,args)
4     elif instr=STR:
5         (registers,systemState)=doSTR(registers,systemState,args)
6     elif:
7         ...
8     else:
9         ...
10    return (registers,systemState)
```

### Listing 1.3 简单处理器

通过这些定义，我们可以构建一个简单的处理器：

> Listing 1.3 processorAction

```python
1 def processorAction(registers,systemState):
2     # 获取指令
3     ir = fetchInstruction(registers,systemState)
4     # 解码指令
5     (opcode,args) = decodeInstruction(ir)
6     # 执行指令
7     (registers,systemState) = executeInstruction(opcode,args,registers,systemState)
8     return registers,systemState
```

`executeInstruction` 函数通过指令上的条件简单调用相应的处理函数：

> Listing 1.3 executeInstruction (instr,args,registers,systemState):

```python
1 def executeInstruction(instr,args,registers,systemState):
2     if instr=LDR:
3         (registers,systemState)=doLDR(registers,systemState,args)
4     elif instr=STR:
5         (registers,systemState)=doSTR(registers,systemState,args)
6     elif instr=B:
7         registers = doB(registers,args)
8     elif instr=CBZ:
9         registers = doZ(registers,args)
10    else:
11        ...
12    return (registers,systemState)
```

# 1.4 高级处理器模型

骨干模型缺少了一些关键特征；在此，我们引入它们。

## 1.4.1 栈支持

栈是一块按后进先出（LIFO）方式访问的连续内存。数据通过“推送”操作添加到栈顶，通过“弹出”操作从顶部取出。大多数架构都包含一个留给栈指针的寄存器。在 Arm 中：

> Listing 1.4.1 示例栈指令

```assembly
1 [PUSH,R1],
2 [POP,R2]
3 ]
```

`PUSH` 和 `POP` 指令的编码方式与 `LDR` 和 `STR` 操作类似。在我们的模型中，我们扩展 `executeInstruction` 以支持栈：

## 1.4.2 子程序调用

设置栈的主要原因之一是为了处理器能够处理子程序调用，特别是调用其他子程序或自调用自己（递归调用）。这是因为每当我们调用子程序时，子程序中的代码都会覆盖寄存器文件，因此我们需要在调用子程序之前保存寄存器。

为了支持这种机制，大多数处理器都有改变控制流的指令：第一条指令调用指令将程序计数器更改到要调用的子程序的位置。第二条指令返回指令返回子程序调用后的位置。这些指令使用栈或专用寄存器来保存程序计数器。

在 Arm 32 位指令集中，调用和返回指令通常使用 `BL` 和 `BX` 实现；Arm 约定返回地址存储在链接寄存器 `LR` 中，我们在模型中也使用相同的约定。我们扩展 `executeInstruction` 以支持子程序的调用和返回：

### Listing 1.4.3 调用/返回实现

```python
def doCall(registers,args):
2 pctr=registers[PC]
3 (_,saddr,)=args
4 registers[LR]=pctr
5 registers[PC]=saddr
```

# 第 1 章 | 以内存为中心的模型

```python
return registers
def doReturn(registers,args):
  lreg = registers[LR]
  registers[PC]=lreg
return registers
```

## 1.4.3 中断处理

现在让我们扩展处理器模型以存储中断。当处理器接收到中断请求时，它必须采取某些特定操作。这些操作只是特殊的微型程序，被称为中断处理程序或中断服务例程序（ISR）。处理器使用主内存中一段称为中断向量表（IVT）的区域将中断请求与处理程序关联起来。

处理器是如何处理中断的？在每一个时钟周期内（即在我们的模型中每次调用 `processorAction`），如果发生了中断，处理器就必须运行相应的 ISR。在我们的模型中，这意味着处理器需要检查 `irqs`，从 `ivt` 中获取相应的 ISR（在我们的模型中它是 `systemArray` 的一个切片），并执行它。事实上，ISR 是一个普通的子程序，但代码中没有对应的 `CALL` 指令。在执行 ISR 之前，处理器会将一些寄存器值存储在栈上，例如，Arm Cortex-M3 会存储 R0-R3, R12, PC 和 LR []。根据 Arm 架构过程调用标准 [6]，被调用的子程序负责存储 R4-R1。在我们的简单模型中，我们只存储 PC，将其扩展以支持 AAPCS 是一项微不足道的练习。

```python
def checkIrqs(registers,ivt,irqs):
  idx=0
  for irq in irqs:
    if irq:
      # 将程序计数器保存到链接寄存器
      registers[LR]=registers[PC]
      # 将程序计数器设置为 ISR 起地址
      registers[PC]=ivt[idx]
      # 清除中断请求
      irqs[idx]=False
      break
    idx+=1
  return (registers, irqs)
```

## 1.4.4 直接内存访问

现代基于处理器的系统的另一个组件是支持直接内存访问（DMA）。这是一种机制允许外设设备直接将数据传输到主内存，而不经过处理器。在系统中，DMA 控制器单元通常是一个外设设备（例如 PrimeCell DMA 控制器），我们将我们的 DMA 模型也实现为一个外设设备。

DMA 传输的原理是 CPU 通过向 DMA 单元寄存器写入数据启动传输，然后在传输过程中运行指令，最后在传输完成后接收 DMA 控制器的中断。

通常，DMA 传输是传输大块数据，否则这将长时间占用处理器的。在我们的简单模型中，DMA 控制器有四个寄存器：

- 源地址寄存器 `DSR`
- 目的地址寄存器 `DDR`
- 计数器 `DCO`
- 控制寄存器 `DCR`

这个外设与模型中的其他设备不同，它可以操作整个系统状态。在某种程度上，我们可以 DMA 控制器视为一种特殊的处理器，只执行内存传输操作。模型实现如下：

![](img/17ca5177da1b1e15b2169f9c7932e5b6_39_0.png)
