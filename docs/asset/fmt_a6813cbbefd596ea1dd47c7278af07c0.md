
```asm
; 显示彩色窗口并在内部写入文本。
INCLUDE Irvine16.inc
.data
message BYTE "Message in Window", 0

code
main PROC
mov ax,@data
mov ds,ax

; 滚动窗口。
mov ax,0600h ; 滚动窗口
mov bh,(blue SHL 4) OR yellow ; 属性
mov cx,050AAh ; 左上角
mov dx,0A30h ; 右下角
int 10h

; 将光标置于窗口内。
mov ah,2 ; 设置光标位置
mov dx,0714h ; 第 7 行，第 20 列
mov bh,0 ; video页 0
int 10h

; 在窗口中写入一些文本。
mov dx,OFFSET message
call WriteString

; 等待按键。
mov ah,10h
int 16h
exit
main ENDP
END
```

### 15.3.3.7 窗口向下滚动 (07h)

向下滚动功能与 `06h` 相同，只是窗口内的文本是向下移动。它使用相同的输入。

### 15.3.3.8 读取字符和属性 (08h)

`INT 10h` 功能 `8` 返回光标处的字符及其属性，如下所示。该功能用于从屏幕读取文本（屏幕抓取/screen scraping），可以将文本转换为语音以供视障用户使用。

| 描述 | 读取字符和属性 |

| --- | --- |

| 接收 | `AH = 8`  
`BH = 页` |

| 返回 | `AL = 字符的 ASCII 码`  
`AH = 字符的属性` |

| 示例调用 | `mov ah,8`  
`mov bh,0 ; video页`  
`int 10h`  
`mov char,al ; 保存字符`  
`mov attrib,ah ; 保存属性` |

### 15.3.3.9 输出字符和属性 (09h)

`INT 10h` 功能 `9` 在光标位置写入彩色字符。如下所示，此功能可以显示任何 0 到 31 的 ASCII 字符。

| 描述 | 输出字符和属性 |

| --- | --- |

| 接收 | `AH = 9`  
`AL = 字符的 ASCII 码`  
`BH = 视频页`  
`BL = 属性` |

| 返回 | 无 |

| 示例调用 | `mov ah, 9`  
`mov al, 'A' ; ASCII 字符`  
`mov bh,0 ; 页`  
`mov bl,fh ; 属性（白底蓝字）`  
`mov cx,1 ; 重复次数`  
`int 10h` |

| 注意 | 写入字符后不移动光标。`CX` 中的重复计数指定字符重复次数。字符不应超出范围。写入字符后，如果要在同一行写入更多字符，必须调用 `INT 10h` 功能 `2` 来移动光标。 |

### 15.3.3.10 输出字符 (0Ah)

`INT 10h` 功能 `0Ah` 在不改变当前屏幕属性的情况下的光标位置写入字符。所示，它与功能 `9` 的区别在于没有指定属性。

| 描述 | 输出字符 |

| --- | --- |

| 接收 | `AH = 0Ah`  
`AL = 字符`  
`BH = 视频页`  
`CX = 重复次数` |

| 返回 | 无 |

| 示例调用 | `mov ah, 0Ah ; ASCII 字符`  
`mov al, 'A' ; 页 0`  
`mov bh, 0`  
`mov cx, 1 ; 重复次数`  
`int 10h` |

| 注意 | 不移动光标。 |

### 15.3.3.11 闪烁和强度模式

`INT 10h` 有许多实用的子功能，包括 `03h`，允许通过颜色属性的最高位控制颜色强度或闪烁。详情如下：

| `INT 10h` 功能 `10h, 子功能 03h` | |

|------|

| 描述 | 闪烁/强度位 |

| 接收 | `AH = 10h`  
`AL = 3`  
`BL = 闪烁模式 (0 = 开启强度，1 = 开启闪烁)` |

| 返回 | 无 |

| 示例调用 | `mov ah, 10h`  
`mov al, 3`  
`mov bl, 1 ; 开启闪烁`  
`int 10h` |

| 注意 | 在 MS-Windows 下，视频显示必须在全屏窗口中运行。 |

### 15.3.3.12 获取视频模式信息 (0Fh)

`INT 10h` 功能 `0Fh` 返回视频模式信息，包括编号、列数和活动视频页，如下所示。

| `INT 10h` 功能 `0Fh` |

|------|

| 描述 | 获取当前视频模式信息 |

| 接收 | `AH = 0Fh` |

| 返回 | `AL = 当前显示模式`  
`AH = 列数（字符或像素）`  
`BH = 视频视频页` |

| `INT10h` 功能 `0Fh` | |

| --- | --- |

| 示例调用 | `mov ah, 0Fh` |

| | `int 10h` |

| | `mov vmode,al ; 保存模式` |

| | `mov columns, ah ; 保存列` |

| | `mov page, bh ; 保存页` |

| 注意 | 在文本和图形模式下均有效。 |

### 15.3.3.13 电报字模式写入字符串 (13h)

表所示的 `INT 10h` 功能 `13h` 在指定的行和列位置向屏幕写入字符串。字符串可以可选包含字符和属性值。（可以参考书籍网站上的 `Color2.asm` 程序作为工作示例。）

| `INT 10h` 功能 `13h` | |

| --- | --- |

| 描述 | 电报字模式写入字符串 |

| 接收 | `AH = 13h`  
`AL = 写入模式（见注释）`  
`BH = 视频页`  
`BL = 属性（如果 AL = 00h 或 01h）`  
`CX = 字符串长度（字符计数）`  
`DH, DL = 屏幕行、列`  
`ES:BP = 字符串的段:偏移量` |

| 返回 | 无 |

| 示例调用 | `.data`  
`colorString BYTE 'A',1F,'B',1Ch,'C',1Bh,'D',1Ch`  
`row BYTE 10`  
`column BYTE 20`  
`.code`  
`mov ax,SEG colorString ; 设置 ES 段`  
`mov es,ax`  
`mov ah,13h ; 写入字符串`  
`mov al,2 ; 写入模式`  
`mov bh,0 ; 视频页`  
`mov cx, (SIZEOF colorString) / 2 ; 字符串长度`  
`mov dh,row ; 行`  
`mov dl,column ; 列`  
`mov bp,OFFSET colorString ; 偏移量`  
`int 10h` |

# INT 10h 功能 13h

| 注意事项 | 写入模式值： |

|---|---|

| | `00h = 字符串仅包含字符代码；写入后光标不更新，属性存储在 BL 中。` |

| | `01h = 字符串仅包含字符代码；写入后光标更新，属性存储在 BL 中。` |

| | `02h = 字符串包含交替的字符代码和属性字节；写入后光标位置更新。` |

| | `03h = 字符串包含交替的字符代码和属性字节；写入后光标位置更新。` |

## 15.3.3.14 示例：显示彩色字符串

以下程序（`ColorSasm`）在控制台上显示一个字符串，每个字符使用不同的颜色。如果你想看到字符，必须在全屏模式下运行。默认情况下启用了闪烁，但你可以移除对 `EnableBlinking` 的调用，并在深灰色背景上查看相同的字符串。

```asm
TITLE Color String Example (ColorStr.asm)
INCLUDE Irvine6.inc
.data
ATTRIB_HI = 10000000b
string BYTE = "ABCDEFGHIJKMNOP"
color BYTE (black SHL 4) OR blue

.code
main PROC
mov ax, @data
mov ds, ax
    call ClrScr
call EnableBlinking ; 这是可选的
mov cx, SIZEOF string
mov si, OFFSET string
L1:push cx ; 保存循环计数器
mov ah, 9 ; 写入字符/属性
mov al, [si] ; 要字符的字符
mov bh, 0 ; 视频页 0
mov bl, color ; 属性
or bl, ATTRIB_HI ; 设置闪烁/强度位
mov cx, 1 ; 显示一次
int 10h ; 移动光标到
mov cx, 1 ; 下一屏幕列
call AdvanceCursor ; 下一个颜色
inc color
```

```asm
inc si              ; 下一个字符
pop cx              ; 恢复循环计数器
Loop L1
call Crlf
exit
main ENDP
```

```asm
push ax
push bx
mov ax, 1003h      ; 切换闪烁/强度
mov bl,1            ; 启用闪烁
int 10h
pop bx
pop ax
ret
EnableBlinking ENDP
```

`AdvanceCursor` 过程可以用于任何使用 `INT 10h` 写入控制台的程序。

```asm
;
AdvanceCursor PROC
; 将光标向右移动 n 列。
; 接收：CX = 列数
; 返回：无
```

```asm
pusha
L1:
push cx              ; 保存循环计数器
mov ah,3h           ; 获取光标位置
mov bh,0             ; 存入 DH, DL
int 10h             ; 改变了 CX 寄存器!
inc dl              ; 增加列
mov ah,2h           ; 设置光标位置
int 10h
pop cx              ; 恢复循环计数器
loop L1              ; 下一列
```

554

第 15 章 • BIOS 级编程

```asm
popa
ret
AdvanceCursor ENDP
END main
```

## 15.3.4 库过程示例

让我们来看 Irvine 16 库中的两个实用、简单的过程：`Gotoxy` 和 `Clrscr`。

### 15.3.4.1 Gotoxy 过程

`Gotoxy` 过程在视频页 0 上设置光标位置：

```asm
;
Gotoxy PROC
;
; 设置视频页 0 上的光标位置。
; 接收：DH,DL = 行，列
; 返回：无
;
pusha
mov ah, 2          ; 设置光标位置
mov bh, 0          ; 视频页 0
int 10h
popa
ret
Gotoxy ENDP
```

### 15.3.4.2 Clrscr 过程

`Clrscr` 过程清除屏幕并将光标位于视频页 0 的第 0 行第 0 列：

```asm
;
Clrscr PROC
;
; 清除屏幕（视频页 0）并将光标定位
; 在第 0 行第 0 列。
; 接收：无
; 返回：无
pusha
mov ax, 0600h      ; 向上滚动窗口
mov cx, 0          ; 左上角 (0,0)
mov dx, 184F       ; 右下角 (24,79)
mov bh, 7          ; 普通属性
int 10h           ; 调用 BIOS
mov ah, 2          ; 将光标定位在 0,0
mov bh, 0          ; 视频页 0
mov dx, 0          ; 第 0 行第 0 列
```

35

## 15.4 使用 INT 10h 绘制图形

```asm
int 10h
popa
ret
Clscr ENDP
```

## 15.3.5 节复习

1. 本节开头提到的访问视频显示器的三个级别是什么？

2. 哪种访问级别产生的输出最快？

3. 如何在全屏模式下运行程序？

4. 当计算机在 MS-DOS 中启动时，默认视频模式是什么？

5. 视频显示器的每个位置对于单个字符存储了什么信息？

6 在视频显示器上产生任何颜色需要哪些电子束？

7. 显示视频属性字节中前景颜色和背景颜色的映射。

8. 哪一个 `INT 10h` 函数滚动窗口？

9. 哪一个 `INT 10h` 写入字符和属性？

10. 哪一个 `INT 10h` 设置光标？

11. 哪一个 `INT 10h` 获取视频模式？

12. 哪一个 `INT 10h` 参数是必要的？

13. 哪一个 `INT 10h` 是允许的？

14. 哪一个 `INT 10h` 滚动窗口？

15. 哪一个 `INT 10h` 写入当前位置？

16. 哪一个 `INT 10h` 切换闪烁？

17. 哪一个 `INT 10h` 应该赋值？

18. 挑战：如果你面对空白屏幕，你为什么在盯着看？

## 15.4 使用 INT 10h 绘制图形

通过写入视频内存来绘制点是相当容易的，10h 显示了颜色数。

15-6 视频模式

| 模式 | 分辨率（列 X 行） | 颜色数 |

|---|---|

| 6 | 640 X 200 | 2 |

| 0D | 320 X 200 | 16 |

| 0E | 320 X 200 | 16 |

| 0F | 640 X 350 | 2 |

| 11h | 640 X 350 | 16 |

| 12h | 640 X 480 | 2 |

| 13h | 640 X 480 | 16 |

| 14h | 800 X 600 | 2 |

| 6A | 800 X 600 | 16 |

[580

第 15 章 • BIOS 级编程

视频模式坐标从左上角的 x=0, y=0 到右下角的 x=XMax-1, y=YMax-1。

## 15.4.1 INT 10h 相关函数

### 15.4.1.1 写入像素 (0Ch)

`0Ch` 函数所示，在适配器处于图形模式时在屏幕上绘制像素。它的执行速度较慢，特别是当绘制大量像素时。

| `INT 10h 0Ch` |

|---|---|

| 说明 | 写入像素 |

| 接收 | `AH = 0Ch`  
`AL = 像素值`  
`BH = 视频页`  
`CX = x坐标`  
`DX = y坐标` |

| 返回 | 无 |

| 示例调用 | `mov ah,0Ch`  
`mov al,pixelValue`  
`mov bh,videoPage`  
`mov cx,x_coord`  
`mov dx,y_coord`  
`int 10h` |

| 注意事项 | 视频显示必须处于图形模式。双色模式下为 (0–1)，十六色模式下为 (0–15)。如果设置了第 7 位，则新像素将与当前像素内容进行异或（允许擦除像素）。 |

### 15.4.1.2 读取像素 (0Dh)

`0Dh` 所示，在给定的行列位置从屏幕读取像素，并将像素值返回到 `AL` 中。

| `INT 10h` 函数 `0Dh` |

|---|---|

| 说明 | 读取像素 |

| 接收 | `AH = 0Dh`  
`BH = 视频页`  
`CX = x坐标`  
`DX = y坐标` |

| 返回 | `AL = 像素值` |

| 示例调用 | `mov ah,0Dh`  
`mov bh,0 ; 视频页 0`  
`mov cx,x_coord`  
`mov dx,y_coord`  
`int 10h`  
`mov pixelValue,al` |

| 注意事项 | 视频显示必须处于图形模式。双色模式下像素值为 0 或 1，十六色模式下为 (0–15)。 |

## 15.4.2 DrawLine 程序

`DrawLine` 程序使用 `INT 10h` 切换到图形模式并绘制一条直线水平线。你可以通过修改当前选择 Mode 11h 的程序语句来尝试不同的图形模式：

```asm
mov ah,0               ; 设置视频模式
mov al,Mode_11      ; 为不同模式进行修改
int 10h             ; 调用 BIOS 例程
```

558

第 15 章 • BIOS 级编程

在 MS-Windows 中，此程序应全全模式下运行。² 以下是程序列表：

# 标题 DrawLine 程序 (Pixel1.asm)

```asm
; 此程序使用 INT 10h
; 调用来绘制一条直线。
INCLUDE Irvine16.inc

; 视频模式常数
Mode_0E = 6        ; 640 X 200, 2 色
Mode_0D = 0Dh      ; 320 X 200, 16 色
Mode_0E = 0Eh      ; 640 X 200, 16 色
Mode_0F = 0F       ; 640 X 350, 2 色
Mode_10 = 10h     ; 640 X 350, 16 色

Mode_11 = 11h     ; 640 X 480, 2 色
Mode_12 = 12h     ; 640 X 480, 16 色
Mode_13 = 13h     ; 320 X 200, 256 色
Mode_6A = 6Ah      ; 800 X 600, 16 色

.data
saveMode BYTE ?   ; 保存当前视频模式
currentX WORD 100 ; 列数 (X 坐标)
currentY WORD 100 ; 行数 (Y 坐标)
color BYTE        ; 默认颜色

; 在 2 色模式下，白色 = 1
; 在 16 色模式下，蓝色 = 1

.code
main PROC
mov ax,@data
mov ds,ax

; 保存视频模式
mov ah, 0Fh
int 10h
mov saveMode,al

; 切换到图形模式
mov ah, 0          ; 设置视频模式
mov al,Mode_11
int 10h

; 绘制直线
LineLength = 100
```

² 在显存（video RAM）较小的电脑上，在 MS-Windows 下运行 `Pixel1.asm` 和 `Pixel2.asm` 可能会遇到困难。如果此问题，请切换到模式 1Bh 或启动到纯 MS-DOS 模式。

## 15.4 使用 INT 10h 绘制图形
