
`mov eax,yellow + (blue * 16)`

`call SetTextColor`

如果你想了解颜色，请参见第 5.3.2 。`Irvine16` 库不支持 `SetTextColor`。

### WaitMsg
`WaitMsg` 过程显示消息 "Press [Enter] to continue..." 并等待用户按下 Enter 键。当你想要在数据滚动之前暂停屏幕显示时，此过程非常有用。它没有输入参数。示例调用为：

```
call WaitMsg
```

### WriteBin
`WriteBin` 过程以二进制格式将整数写入标准输出。当你调用 `WriteBin` 时，将整数传递到 `EAX`。二进制位每 4 位一组进行显示，以便阅读。例如：

```
mov eax,1234AFh
call WriteBin
; 显示: "0001 0010 0011 0100"
```

### WriteChar
`WriteChar` 过程将单个字符写入标准输出。在调用过程之前，将字符（或其 ASCII 码）放入 `AL`：

```
mov al,'A'
call WriteChar
; 显示: "A"
```

### WriteDec
`WriteDec` 过程以十进制格式将 32 位无符号整数写入标准输出，并带有前导零。在调用它之前，将整数放入 `EAX`：

```
mov eax,295
call WriteDec
; 显示: "295"
```

### WriteHex
`WriteHex` 过程以十六进制格式将 32 位无符号整数写入标准输出。必要时会插入前导零。在调用它之前，将整数放入 `EAX`：

```
mov eax,7FFF
call WriteHex
; 显示: "0000FFFF"
```

### WriteInt
`WriteInt` 过程将 32 位符号整数以十进制格式写入标准输出，并带有符号位。在调用它之前，将整数放入 `EAX`：

```
mov eax,21653
call WriteInt
; 显示: "+21653"
```

### WriteString
`WriteString` 过程将空终止字符串写入标准输出。调用它时，将字符串的偏移量放入 `EDX`。例如：

```
.data
prompt BYTE "Enter your name: "
.code
mov edx,OFFSET prompt
call WriteString
```

## 5.3 库

### 5.3.2.1 Irvine32.inc 头文件

以下是 `Irvine32.inc` 头文件的部分列表。它包含了每个库过程原型，以及颜色常量、结构和符号定义。此文件会随时间变化，请确保从书籍网站获取最新版本：

```
; Irvine32.lib 的包含文件
INCLUDE SmallWin.inc
.NLIST
---------------------------------------
;过程原型
---------------------------------------
Clrscr PROTO
Crlf PROTO
Delay PROTO
DumpMem PROTO
DumpRegs PROTO
GetCommand PROTO
GetMilliseconds PROTO
Getotxy PROTO
Randomize PROTO
RandomRange PROTO
Random32 PROTO
ReadInt PROTO
ReadChar PROTO
ReadHex PROTO
ReadString PROTO
SetTextColor PROTO
WaitMsg PROTO
WriteBin PROTO
WriteChar PROTO
WriteDec PROTO
WriteHex PROTO
WriteString PROTO
; 标准 4 位颜色定义
;
| black = 0000b |
| blue = 0001b |
| green = 0010b |
| cyan = 0011b |
| red = 0100b |
| magenta = 0101b |
| brown = 0110b |
| lightGray = 0111b |
| gray = 1000b |
| lightBlue = 1001b |
| lightGreen = 1010b |
| lightCyan = 1011b |
| lightRed = 1100b |
| lightMagenta = 1101b |
| yellow = 1110b |
| white = 1111b |
.LIST
```

此文件顶部的 `.NLIST` 指令防止在汇编器创建的源列表中显示这些行。在文件末尾，`.LIST` 指令再次启用源行显示。

# 3 本书的链接库 149

```
INCLUDE Irvine32.inc
CR = 0Dh                    ; 回车
LF = 0Ah                    ; 换行符
```

```
.data
str1 BYTE "Generating 20 random integers between "
      BYTE "0 and 990",CR,LF,0"
str2 BYTE "Enter a 32-bit signed integer: ",0"
str3 BYTE "Enter your name: ",0"
str4 BYTE "The following key was pressed: ",0"
str5 BYTE "Displaying the registers:",CR,LF,0
str6 BYTE "Hello, ",0
```

```
buffer      BYTE 50 dup(0)
dwordVal DWORD ?
.code
main PROC
      ; 将文本颜色设为：白色背景上的黑色文字：
      mov eax,black+ (white * 16)
      call SetTextColor
      call Clrscr                 ; 清除屏幕
      call Randomize              ; 重置随机数序列
      ; 在 0 到 990 之间生成 20 个随机整数。
      ; 包含 500 毫秒的延迟。
      mov edx,OFFSET str1          ; 显示消息
      call WriteString
      mov ecx,20                   ; 循环计数器
      mov dh,2                    ; 屏幕行 2
      mov dl1,0                    ; 屏幕列 0
```

```
L1: call Gotoxy
      mov eax,991                 ; 表示范围上限 +1
      call RandomRange            ; EAX = 随机整数
      call WriteDec               ; 以无符号十进制显示
      mov eax,500
      call Delay                   ; 暂停 500 毫秒
      inc dh                       ; 下一个屏幕行
      add dl1,2                    ; 向右移动 2 列
Loop L1
```

```
call Crlf           ; 换行
call WaitMsg             ; "按下 [Enter]..."
call Crlscr             ; 清除屏幕
; 输入一个有符号十进制整数并以
; 各种格式重新显示：
mov  edx,OFFSET str2      ; "Enter a 32-bit..."
call WriteString
call ReadInt             ; 输入整数
mov  dwordVal,eax         ; 保存到变量
call Crlf               ; 换行
call WriteInt             ; 以有符号十进制显示
call Crlf
call WriteHex             ; 以十六进制显示
call Crlf
call WriteBin             ; 以二进制显示
call Crlf
; 显示 CPU 寄存器：
call Crlf
mov  edx,OFFSET str5      ; "Displaying the registers:"
call WriteString
call DumpRegs             ; 显示寄存器和标志位
call Crlf
; 显示内存导出：
mov  esi,OFFSET dwordVal  ; 起始偏移
mov  ecx,LENGTHOF dwordVal ; dwordVal 中的单元数
mov  ebx,TYPE dwordVal    ; 双字大小
call DumpMem             ; 显示内存
call Crlf               ; 换行
call WaitMsg             ; "按下 [Enter]..."
; 询问用户输入他们的名字：
call Crlscr             ; 清除屏幕
mov  edx,OFFSET str3      ; "Enter your name: "
call WriteString
mov  edx,OFFSET buffer   ; 指向缓冲区
mov  ecx,SIZEOF buffer - 1  ; 最大字符数
```

## 5.3 本书的链接库

```
call ReadString ; 输入名字
mov edx,OFFSET str6 ; "Hello,"
call WriteString
mov edx,OFFSET buffer ; 显示名字
call WriteString
call Crlf
exit
main ENDP
END main
```

示例输出。这里是程序输出的一个示例。整数是随机的，你的输出屏幕将显示不同的数字：

![](img/ea8a6a99b0e33c5c1bf5dd603b329094_180_0.png)

在你按下回车键后，程序显示以下内容：

```
C:\WINDOWS\System32\cmd.exe
Enter a 32-bit signed integer: 12345
+12345
00003039
0000 0000 0000 0011 0000 0000 1001
Displaying the registers:
EAX=00003039 EBX=7FFD0000 ECX=000404CC
ESI=00000000 EDI=00000000 EBP=0012FFF0 ESP=0012FFC4
EIP=000401B6 EFL=00000286 CF=0 SF=1 ZF=0 OF=0
Dump of offset 00040122
00003039
Press [Enter] to continue...
```

当你输入名字时，程序会重新显示它。（最后的“Press any key” 不是由程序生成的）。

```
C:\WINDOWS\System32\cmd.exe
Enter your name: Kip Irvine
Hello, Kip Irvine
Press any key to continue .
```

## 5.3.4 节复习

- 链接库中的哪个过程在选定范围内生成随机整数？
- 链接库中的哪个过程显示“Press [Enter] to continue...”并等待回车键？
- 哪些语句会导致程序暂停 500 毫秒？
- 链接库中的哪个过程将无符号整数以十进制格式写入标准输出？
- 链接库中的哪个过程将光标标置于特定的控制台窗口？
- 使用 `Irvine32.inc` 文件时需要哪个指示符？
- `ReadString` 包含哪些类型的语句？
- `DumpMem` 需要哪些输入参数？
- `DumpRegs` 过程显示了哪些处理器状态标志位？
- 挑战：编写语句，提示用户输入一个字符串到字节数组中。

## 5.4 栈操作

如果你像下面的插图那样将十个盘子叠在一起，你就是创建了一个栈。如果这些盘子非常重，那么制定一条规则“不能从中间取出盘子”是有意义的。新的盘子只能添加到顶部，而永远不能添加到底部中间：

| 10 |
| 9 |
| 8 |
| 7 |
| 6 |
| 5 |
| 4 |
| 3 |
| 2 |

栈也被称为 LIFO 结构（后进先出），因为最后放入的元素最先被取出。

## 5.4.2 PUSH 和 POP 指令

### 5.4.2.1 PUSH 指令

`PUSH` 指令首先递减 `ESP`，然后将 16 位或 32 位的源操作数复制到栈中。16 位操作数会导致 `ESP` 递减 2。32 位操作数会导致 `ESP` 递减 4。共有三种指令格式：

```assembly
PUSH r/m16
PUSH r/m32
PUSH imm32
```

> 如果你的程序调用了 `Irvine32` 库的过程，你应该始终推送 32 位的值；否则，该库使用的 Win32 控制台函数将无法正常工作。如果你的程序调用了 `Irvine16` 库的过程（在实地址模式下），你可以推送 16 位和 32 位的值。

在保护模式下，立即数始终是 32 位。在实地址模式下，除非使用了 `.386` 处理器指令，否则立即数默认为 16 位。（此处已使用 `.386` 指令。）

### 5.4.2.2 POP 指令

`POP` 指令首先将 `ESP` 指向的栈元素的内容复制到 16 位或 32 位的操作数中，并增加 `ESP`。如果操作数是 16 位，`ESP` 增加 2；如果操作数是 32 位，`ESP` 增加 4：

```assembly
POP r/m16
POP r/m32
```

### 5.4.2.3 PUSHFD 和 POPFD 指令

`PUSHFD` 指令将 32 位的 `EFLAGS` 寄存器推入栈，而 `POPFD` 将栈内容弹出到 `EFLAGS`：

```assembly
pushfd
popfd
```

实地址模式使用 `PUSHFD` 指令将 16 位的 `FLAGS` 寄存器推入栈，使用 `POPFD` 将栈弹出到 `FLAGS`。

有时对标志位进行备份是有用的，以便以后将它们恢复到原来的值。实现这一点的方法是将代码块封装在 `PUSHFD` 和 `POPFD` 之间：

```assembly
pushfd
; 保存标志
;
; 这里是任何语句序列...
;
popfd
; 恢复标志
```

## 5.4 栈操作

在使用此类类型的 push 和 pop 时，你必须非常小心程序的执行路径不要跳过 `POPFD`。当程序随着时间的推移被修改（并希望改进）时，记住所有 push 和 pop 的位置可能会很困难。一种容易出错的类似方法是将标志位保存在变量中：

```assembly
.data
saveFlags DWORD ?
.code
push ; 将标志推入栈
pop saveFlags ; 复制到变量
```

以下语句从同一个变量中恢复标志位：

```assembly
push saveFlags ; 推入保存的标志值
popfd ; 复制到标志寄存器
```

### 5.4.2.4 PUSH, PUSHA, POPAD, 和 POPA

`PUSH` 指令按照以下顺序将所有 32 位通用寄存器推入栈中：`EAX`, `ECX`, `EDX`, `EBX`, `ESP`（原始值），`EBP`, `EDI`, `EDI`。`POPAD` 指令按相反顺序从栈中弹出寄存器。同样，随 80286 处理器引入的 `PUSHA` 指令按出的顺序将 16 位通用寄存器（`AX`, `CX`, `DX`, `BX`, `SP` 值, `BP`, `SI`, `DI`）推入栈中。`POPA` 指令按相反顺序弹出寄存器。

如果你编写了一个修改 32 位寄存器的过程，请在过程开始处使用 `PUSH` 在结束处使用 `POPAD` 来保存和恢复寄存器。以下代码段是一个示例：

```assembly
MySub PROC
pushad ; 保存通用寄存器
mov eax,
mov edx,
mov ecx,
popad ; 恢复通用寄存器
ret
MySub ENDP
```

### 5.4.2.5 示例：反转字符串

`RevString` 程序循环遍历字符串并将每个字符推入栈中。它从栈中弹出字母（按相反顺序），并将它们存回同一个字符串变量中。由于栈是 LIFO（后进先出）结构，字符串将以反向顺序显示：

## TITLE 反转字符串 (RevStr.asm)

```assembly
INCLUDE Irvine32.inc
.data
aName BYTE "Abraham Lincoln",0
nameSize = ($ - aName) - 1
.code
main PROC
    ; 将名称推入栈中。
    mov ecx,nameSize
    mov esi,0
L1:movzx eax,aName[esi]   ; 获取字符
    push eax                    ; 推入栈
    inc esi
    Loop L1
    ; 从栈中反向弹出名称，
    ; 存储在 aName 数组中。
    mov ecx,nameSize
    mov esi,0
L2:pop eax                  ; 获取字符
    mov aName[esi],al           ; 存储在字符串
    inc esi
    Loop L2
    ; 显示名称。
    mov edx,OFFSET aName
    call WriteString
    call Crlf
    exit
main ENDP
END
```

## 5.4.3 章节练习

1. 在保护模式下，哪两个寄存器……
2. 栈与类型（type）有何不同？
3. 为什么栈被称为 LIFO？
