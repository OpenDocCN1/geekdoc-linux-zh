

# 第94章 8086的寻址方式

在 MS-DOS 和 Win16（参见本书第73节和第35.5节）平台的 16 位应用程序中，我们可以看到程序指针指向两个 16 位内存构成。这是什么情况？这并不是 MS-DOS 和 8086 的另一个怪异特性。

虽然 8086/8088 属于 16 位 CPU，但它有 20 位的 RAM 地址空间（内存总线有 20 个引脚），即它可以寻址的存储空间为 1MB。这 1MB 的外部内存空间又被划分为最大 640KB 的 ROM、显存、EMS 卡等等。

16 位的 8086/8088 CPU 实际上是由 8080 CPU 而来的。8080 CPU 的地址空间只有 16 位，因此能控制的内存只有 64KB。8086 的设计理念认为 64KB 空间不够用，而且 8086 还要兼容旧平台的程序，因此将 1MB 的内存划分成若干段使用。这就是早期的虚拟内存技术。8086 的寄存器只有两个 16 位寄存器，为了进行更大范围（20 位）的寻址，它得借助新出的段寄存器。从此 CPU 有了 CS、DS、ES 和 SS 寄存器。20 位的内存指针通过短寄存器和地址寄存器（DS:BX）来实现：

```
real_address = (segment_register << 4) + address_register
```

举例来说，通过 PC 兼容的主机，但显卡（EGA、VGA）的显示只有 64KB。要写显存，就要在某个段寄存器（例如 DS）写入 `0xA000`。如此一来，程序就可以通过 `DS:0` 到 `DS:FFFF` 访问整个显存。虽然地址总线是 20 位，超过了 16 位寄存器的表达范围，但 PC 可以借助段寄存器毫无障碍地访问 `0xA000` 到 `0FFFF`。

程序还能直接访问固定的内存地址（例如 `0x1234`），但操作系统加载程序到的起始地址并不是固定的。段寄存器的出现解决了这种问题——它可由段寄存器进行相对寻址，程序不需要关心自己加载到了什么 RAM 地址。

事实上，MS-DOS 系统下的指针由段地址和段内偏移构成，由两个 16 位数值表示。20 位指针总线足以满足这种寻址方式的需求。这意味着程序员就需要重新计算内存地址了：他们要不停地考虑空间和效率的平衡，仔细规划数据分配情况。

另外，8086 的寻址方式决定了每个内存块不能大于 64KB。

8086 平台仍然继承了段寄存器（segment registers），只是工作方式完全不同。

在支持更大 RAM 的 80386 CPU 时代，市面上流行的仍然是 MS-DOS。有一批叫 DOS Extenders 的粉丝在 Windows 系统以后继续坚守 DOS 阵地。他们甚至开发出了类似 OS 一样的系统。这种系统不仅实现了 CPU 保护模式的切换功能，而且大幅地改进了内存 API，可以继续支持 MS-DOS 的应用程序。著名的有：DOS/4GW（游戏 DOOM 就是面向它编译的）、Phar Lap 和 PMODE。

在 Win32 之前，16 位的 Windows 3.x 仍然沿用了这种寻址方式。

# 第95章 基本块重排

## 95.1 PGO 的优化方式

PGO 是 Profile-guided optimization 的缩写，中文译为“配置引导优化”。经过 PGO 方式优化后，程序中的某些基本块（basic block）指的是程序里执行的语句顺序。基本块由第一个语句构成入口，由最后一句语句构成出口。在执行程序时，不可从入口以外进入该基本块（被跳入），也不可从出口以外的地址跳出该基本块（可能被调整到执行文件的任意位置）。

很明显，函数中的程序代码存在执行频率的差异。例如，循环语句类代码的执行频率必然很高，而错误报告、异常处理之类代码的执行频率较低。

在未使用 PGO 时，编译器首先会生成一个包含运行细节的特殊程序。随后，研发人员通过运行手段收集程序的各项统计信息。最后，编译器根据这些统计信息对可执行文件进行调整和优化，把执行率较小的基本块移动到其他地方。

在 PGO 优化后的程序，频繁执行的函数代码会被调整得更为紧凑。PGO 优化了条件跳转的性能，提高了 CPU 分支预测的准确率。这些特性有助于提升程序性能。

Oracle是由 Intel C++ 编译器生成的程序。本文收录了 Oracle 中 `generic.dll` (Win32) 的代码。

```
指令清单95.1 orgeneric.dll (Win32)
```

public _skgfsync
proc near

; address 0x6030D86A

db                 66h
pop                ebp
push               esp
mov                ebp, esp
mov                edx, [ebp+0Ch]
test               edx, edx
jnz                short loc_6030D884
mov                eax, [edx+30h]
test               eax, 400h
jnz                __VInfreq__skgfsync ; write to log
continue:
mov                eax, [ebp+8]
mov                edx, [ebp+10h]
mov                dword ptr [eax], 0
lea                eax, [edx+0F]
and                eax, 0FFFF
mov                ecx, [eax]
cmp                ecx, 4572963
jnz                error ; exit with
mov                esp, ebp
pop                ebp
ret
_skgfsync

; address 0x60B95F0
__VInfreq__skgfsync:
mov                eax, [edx]
test               eax, eax
jz                continue
mov                ecx, [ebp+10h]
push               ecx
mov                ecx, [ebp+8]
push               edx
push               ecx
push               offset ;skgfsync(se=0x,ctx=0x,ov=0x)
push               ecx
call               dword ptr [edx+4]
dword ptr [eax] ; write to log
add                esp, 14h
jmp                continue

error: mov edx, [ebp+8]
mov dword ptr [edx], 69AA ; function called with invalid/IO structure
mov eax, [eax]
mov dword ptr [edx+4], eax ; 4004
mov esp, ebp
pop ebp
ret

