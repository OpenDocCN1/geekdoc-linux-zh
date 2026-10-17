
# 视频模块说明

## 基础操作

```
mov AH, BYTE [BX+DI] ; 从表中加载数字到 AH
mov [SI], AH ; 将数字存入字符串
ret ; 完成！
```

## WordStr

`WordStr` -- 将 `AX` 中的字(word) 转换为 `DS:SI` 处的字符串

最后更新 99/9/19

1 处入口点：

`WordStr:`

调用者必须传递：

- `AX` : 要转换的字
- `DS` : 目标字符串的段
- `SI` : 目标字符串的偏移

```
WordStr:
    mov CX, AX ; 将转换值保存到 CX
    mov AH, AL ; 交换高低位以处理高位
    call Byte2Str ; 将 AL 转换为字符串到 SI
    add SI, 2 ; 将 SI 移动 2 个字符
    mov AX, CX ; 将转换值加载到 AX
    call Byte2Str ; 将 AL 转换为字符串到 SI
    ; 我们完成了！
```

## VidCheck

`VidCheck` -- 识别视频信息

最后更新 99/9/19

1 处入口点：

`VidCheck:`

; 程序开始这里：

```
call VidCheck ; 初始化所有视频信息
mov VidSegment, BufSize ; 清屏

; 接下来我们确定当前的字体大小：
mov AX, Segment ; 将段复制到 AX
cmp AX, MCGA ; 查看是否为 MCGA
jne TryOld ; 如果不是，则是 MCGA
mov FontSize, 16 ; MCGA 支持 16 像素字体
jmp GetName

TryOld:
    cmp AX, MDA ; 代码是 MDA 吗
    jne TryGA ; 如果不是，则是 CGA
    mov FontSize, 8 ; MDA 使用 8 像素字体
    jmp GetName

TryGA:
    cmp AX, CGA ; 代码是 CGA 吗
    jne TryVGA ; 如果不是，则是 VGA
    mov FontSize, 14 ; CGA 使用 14 像素字体
    jmp GetName

TryVGA:
    mov AL, 11H ; 选择视频 11H
    mov BH, 0 ; 获取当前字体信息
    int 10H ; 调用视频服务
    mov FontSize, CL ; 字体像素返回 CL

GetName:
    mov AL, [DispType] ; 将适配器代码加载到 AL
    xor AX, AH ; 确保 AH 没有杂质
    mov DI, AX ; 将 AX（带代码）复制到 DI
    mov CL, 5 ; 我们必须将代码移动 5 位以乘以 32
    sh DI, CL ; 将代码乘以 32 作为表格索引
    mov BX, DeviceInfo ; 将原始表地址加载到 BX
    mov [BoardName], BX ; 将视频表指针保存到 BoardName
    add [BoardName], DI ; 添加偏移量以指向正确的元素
```

## 汇编语言分步详解

```
mov [VisibleY], AL    ; 将其存储在 VisibleY 变量中
mov AH, [VisibleX]    ; 将屏幕列数加载到 AH
xchg AH, AL           ; 交换 AH & AL 以实现 0 基索引
dec AL                ; 列数减 1 以实现 0 基索引
dec AH                ; 行数减 1 以实现 0 基索引
mov [LRXY], AX        ; 将 0 基的 X,Y 字存储到 LRXY 变量中
```

最后，我们在以下位置计算刷新缓冲区的大小：

```
mul [VisibleX], [VisibleY]      ; 我们将屏幕行数乘以屏幕列数
mul BYTE [VisibleAttr]          ; 乘以 2（用于属性字节）以获得缓冲区大小
shl AX, 1                       ; 将行数 * 列数乘以 2
mov [VidBufSize], AX            ; 将刷新缓冲区大小存储在 VidBufSize 中
```

```
ret                     ; 返回到调用者
```

## DispID

`DispID` - 标识已安装的显示适配器

- 最后更新于 99/9/18
- 1 个入口点：`DispID:`
- 调用者不传递任何参数
- 程序在 `AX` 中返回一个代码值。
- 代码如下：
    - `0`: 适配器未知；建议中止
    - `1`: `MDA`（单色显示适配器）
    - `2`: `CGA`（彩色图形适配器）

```
mov AH, 1AH           ; 选择 PS/2 识别适配器服务
xor AL, AL            ; 选择获取组合代码子服务 (AL=0)
int 10H               ; 调用视频中断
cmp AL, 1AH           ; 如果 AL 返回 1AH，则说明我们有一个 PS/2 适配器
jne TryGA             ; 如果不是，跳转到下方测试是否存在 EGA
mov AL, BL            ; 将组合代码放入 AL
ret                   ; 然后返回！

TryGA:
    mov AH, 12H       ; 选择 EGA 备用功能
    mov BX, 10H       ; 选择配置信息子服务
    int 10H           ; 调用 VIDEO 中断
    cmp BX, 10H       ; 如果 BX 保持不变，则表示不存在 EGA
    je OldBorders     ; 转到旧版本查看是 MDA 还是 CGA
    cmp BH, 0         ; 如果 BH = 0，则为 EGA/彩色组合
    je EGAColor       ; 否则是 EGA/单色
    mov AL, 5         ; 为 EGA 单色存储代码 5
    ret               ; 然后返回！

EGAColor:
    mov AL, 4         ; 为 EGA 彩色存储代码 4
```

## 位、标志位、分支与表格

`ret` ; 然后返回！

`OldBorders:`

```
int 11H ; 调用设备配置中断
and AL, 30H ; 掩盖除第 4 和第 5 位以外的所有位
cmp AL, 30H ; 如果第 4 和第 5 位均为 1，则为 MDA
jne CGA ; 否则为 CGA
mov AL, 1 ; 为 MDA 存储代码 1
ret ; 然后返回！

CGA:
mov AL, 2 ; 为 CGA 存储代码 2
ret ; 然后返回！
```

## 数据段定义

`[SECTION .data]`

; 显示信息变量

; 下面的变量块均与视频系统相关，并由 `VidCheck` 过程初始化：

- `DispType` DB 0 ; 显示适配器类型代码
- `VidSegment` DW 0B00H ; 安装的显示缓冲器的段
- `VidOrigin` DW 0 ; 指向刷新缓冲器的远指针偏移量
- `VisibleX` DB 80 ; 屏幕上的列数
- `VisibleY` DB 25 ; 屏幕上的行数
- `VidBufSize` DW 4000 ; 默认为 25 X 80 X 2（字符与属性）
- `FontSize` DB 8 ; 8、14 或 16；默认为 8
- `BoardName` DW 0 ; 指向安装卡板名称字符串的近指针
- `LRXY` DW 14FH ; 80 x 25 屏幕左下角的 X,Y 坐标

; 显示信息查找表

; 这是一个包含所有合法显示适配器信息的查找表。每个元素的第一个字段是一个 26 字符字符串，包含对适配器的简要描述。下一个字段是视频刷新缓冲区的段。最后三个字段分别是当适配器加载 8 像素、14 像素和 16 像素字体时的屏幕行数。注意并非所有适配器都支持所有字体，但为所有适配器类型都提供了三种字体的屏幕行数。非法组合将不会被访问。

```
VidInfoTbl DW 'No adapter identified' ; 代码 0
DW 0B00H
DB 25, 25

DW 'Monochrome Display Adapter ' ; 代码 1
DW 0B00H
DB 25, 25

DW 'Color Graphics Adapter' ; 代码 2
DW 0800H
DB 25, 25

DW 'Code 3: Undefined' ; 代码 3
DW 0800H
DB 25, 25

DW 'EGA with color monitor' ; 代码 4
DW 0800H
DB 43, 25

DW 'EGA with mono monitor' ; 代码 5
DW 0800H
DB 43, 25

DW 'Code 6: Undefined' ; 代码 6
DW 0800H
DB 25, 25

DW 'VGA with mono monitor' ; 代码 7
DW 0800H
DB 50, 27

DW 'VGA with color monitor' ; 代码 8
DW 0800H
DB 50, 27

DW 'Code 9: Undefined' ; 代码 9
DW 0800H
DB 25, 25

DW 'MCGA with digital color' ; 代码 0AH
DW 0800H
DB 25, 25

DW 'MCGA with monochrome' ; 代码 0BH
DW 0800H
DB 25, 25

DW 'MCGA with analog color' ; 代码 0CH
DW 0800H
DB 25, 25
```

`Digits` DB '0123456789ABCDEF' ; 用于数字/字符串转换的查找表。

这两个变量是宏使用的屏幕清空“原子”。高位字节是显示属性，而低位字节是用于填充刷新缓冲区以清空屏幕的字符。

```
HToneAtom DW 07BH
ClearAtom
```

## 字符串处理基础

你应该像考虑分段（segments）那样来考虑字符串：通过定义它们的寄存器值来考虑。

与你在该类语言中思考字符串的方式相比，这稍微有点“反向”的：当你设置一对寄存器指向一个字符串时（如果你在实模式或保护模式平坦模型下工作，则使用单个寄存器），你就拥有了一个字符串。而一旦你指向一个字符串，字符串的长度就由你放在 `CX` 寄存器中的值定义。

这是关键所在：汇编中的字符串完全由你放在寄存器中的值定义。CPU 的硅片中固化了一组关于字符串和寄存器的假设。当你执行其中一条字符串指令时（正如我稍后描述的那样），CPU 会利用这些假设来确定它要读取或写入到内存的哪一个区域。

### 源字符串与目标字符串

在汇编工作中，字符串有两种。**源字符串**是从其读取的字符串。**目标字符串**向其写入的字符串。两者之间的区别仅仅是寄存器的问题；源字符串和目标字符串可以重叠。事实上，同一块内存可以同时既是源字符串又是目标字符串。

以下是 CPU 在执行字符串指令时对字符串做出的假设：

- 源字符串由 `DS:SI` 指向。
- 目标字符串由 `ES:DI` 指向。
- 两种字符串的长度都是你放在 `CX` 中的值。
- 来自源字符串或发往目标字符串的数据必须通过 `AX` 寄存器。

注意，段寄存器的使用主要适用于实模式下的分段模型。在实模式平坦模型中，正如你现在应该知道的，所有的段寄存器都包含相同的值，因此在很多情况下它们基本上被排除在考虑之外，字符串操作也包含在内。（保护模式平坦模型也是如此，你将在后面的章节中学习到。）CPU 可以同时识别源字符串和目标字符串，因为 `DS:SI` 和 `ES:DI` 可以持有相互独立的值。然而，由于只有一个 `CX` 寄存器，当它们被同时使用时（例如将源字符串复制到目标字符串），源字符串和目标字符串的长度必须相同。

### 汇编语言步骤详解

记住源字符串和目标字符串区别的一种方法是看它们的偏移量寄存器。`SI` 代表“源索引（source index）”，而 `DI` 代表“目标索引（destination index）”。

## REP STOSW，软件机枪扫

在脑海中巩固所有字符串背景信息的最好方法是看到字符串指令的工作。在这一节中，我展示了一个实用的视频显示工具，它使用了最简单的字符串指令 `STOSW`。（意为按字存储字符串 Store String by Word。） 讨论涉及一种被称为“前缀”（prefix）的东西，我还没有详细介绍。请先等一下，稍后我们会讨论前缀。

### 对视频显示缓冲区进行机枪扫

我们之前讨论的 `Clr` 过程依赖 BIOS 来处理实际的清屏工作。BIOS 是很大一个黑箱，我们并不要求知道它是如何工作的。BIOS 的问题在于它只知道如何将屏幕清为空白。某些程序（例如 Borland/Turbo Pascal 的最新版本）通过将屏幕清空为 PC 的半调字符（字符代码 176 到 178）来赋予自己一种时尚、有立体感的外观。BIOS 做不到这一点。如果你想要半调效果，就必须自己动手。这不涉及比将单个字符串字（两个字节）复制到你的视频刷新缓冲区中的每个位置更复杂的操作。

此类操作应该始终在紧凑的循环中完成。显而易见的方法是将其放入循环中。

```
Clear:
    mov [DI], AX ; 将 AX 拷贝到 ES:DI
    inc DI       ; DI 递增
    dec CX       ; CX 减 1
    jnz Clear    ; 如果 CX 不为 0 则再次循环
```

# 串联它们

```
rep stosw
GotoXY 0,0 ; Move hardware cursor to UL corner of screen
%endmacro
```

不要被“远指针（far pointer）”的概念吓到。这是你以后会反复听到的术语，而现在是介绍它的很好时机。简单来说，指针就是一个地址。**近指针（near pointer）**仅仅是一个偏移地址，它与某个段寄存器中的某个值配合使用，而该值推测是不改变的。在真实的平坦模型（flat model）程序中，指向所有对象的指针定义上都是近指针。

远指针是一个由段值（segment value）和偏移值（offset value）组成的指针，两者都可以随时被更改，并协同工作。视频刷新缓冲区通常不是你数据段的一部分，所以如果你要处理它，可能需要使用远指针来访问它，就像我们在这里做的那样。每当你需要引用存在真实平坦模型程序 64K 边界之外的内容（例如系统的文本视频缓冲区）时，你都会使用远指针。

注意，`Clear` 宏的大部分是准备工作。`LES` 指令将 `ES` 和 `DI` 都加载为目标字符串的地址。屏幕原子字符加上属性值被加载到 `AX` 中。

`CX` 的处理值得稍微解释一下。`BufLength` 中的值是视频刷新缓冲区以字节为单位的大小。但请记住，假设 `CX` 包含 `AX` 写入内存的次数。`AX` 是一个字（word），而一个字是 2 字节长。因此，每当 `STOSW` 触发时，就会写入 2 字节的视频刷新缓冲区。因此，为了告诉 `CX` 要射击多少次，我们必须将刷新缓冲区的大小（以字节为单位）除以 2，以便以字为单位表示刷新缓冲区的大小。

正如我在第 10 章中解释的，将寄存器中的值除以 2 是很容易的。你只需要将寄存器的值右移一位即可。这就是 `SHR CX,1` 指令的作用：将 `CX` 除以 2。

# STOSW 和方向标志 DF

注意 `Clear` 宏中的 `CLD` 指令。为了避免混淆，我在此之前没有提到它。大多数时候，当你使用 `STOSW` 时，你会希望它在内存中“向上”运行；即从较低的内存地址到较高的内存地址。在 `Clear` 中，你将视频刷新缓冲区的起始地址放入 `ES` 和 `DI`，然后将字符/属性对射入连续增加的内存地址。每当 `STOSW` 向内存中射入一个字时，`DI` 就会增加 2，以指向内存中下一个更高的字。

这是逻辑上的操作方法，但并不一定要这样做。`STOSW` 可以很容易地从高地址开始并在内存中向下移动。在每次存储内存时，`DI` 可以改而递减 2。

`STOSW` 向哪个方向射击——向上连续递高的地址，还是向下连续递低的地址——是由 Flags 寄存器中的一个标志控制的。这就是方向标志 `DF`（Direction flag）。`DF` 这一生的唯一工作就是控制某些指令（如 `STOSW`）的方向，使其可以在内存中沿两个方向之一移动。这些指令大部分（如 `STOSW`）都是字符串指令。

`DF` 的含义是：当 `DF` 被设置时（即 `DF` 的值为 1 时），`STOSW` 及其它的字符串指令“向下”工作，从高地址到低地址。当 `DF` 被清除（即它的值为 0 时），`STOSW` 及其兄弟姐妹们“向上”工作，从低地址到高地址。这种转向仅仅是 `DI` 调整的方向：当 `DF` 被设置时，`DI` 递减；当 `DF` 被清除时，`DI` 递增。

CPU 重置时，方向标志默认为 0（向上）。它通常通过两种方式之一更改：使用 `CLD` 指令或使用 `STD` 指令。`CLD` 清除 `DF`，而 `STD` 设置 `DF`。（在调试时你应该记住，`POPF` 指令也可以更改 `DF`，因为它从栈中弹出一组新的标志并存入 Flags 寄存器。）在字符串指令之前放置合适的 `CLD` 或 `STD` 始终是一个好主意，以确保你的机器以正确的方向射击！

人们有时会很困惑，认为 `DF` 也控制字符串指令是增加还是递减 `CX`。才不是的！字符串指令中没有任何一个操作会增加 `CX`！你向 `CX` 中放置一个计数值，它就会倒计时向下递减，仅此而已。`DF` 对此无话可说。

`Clear` 宏是该书光盘随附 `MYLIB.MAC` 宏库的一部分。当你构建新的宏工具时，你可能也会将它们存放在 `MYLIB.MAC` 中。

# 半自动武器：没有 REP 的 STOSW
