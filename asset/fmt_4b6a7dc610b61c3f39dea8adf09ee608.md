
`DISKIO` 结构包含起始扇区号、要读或写的扇区数量以及扇区缓冲区段/偏移地址：

```
DISKIO STRUCT
startSector DWORD 0 ;起始扇区号
numS WORD 1 ; 扇区数量
bufferOff WORD buffer ; 缓冲区偏移
bufferSeg WORD @DATA ; 缓冲区段
DISKIO ENDS
```

以下是用于存储扇区数据的缓冲区示例，以及一个 `DISKIO` 结构变量：

```asm
.data
buffer BYTE 512 DUP(?)
diskStruct DISKIO
```

调用函数 `7305h` 时，传递给 `SI` 的参数决定了你是想读取还是写入扇区。读取时，清零第 0 位；写入时，设置第 0 位。此外，在使用以下方案写入扇区时，会配置第 13、14 和 15 位：

| 字节 13-15 | 扇区类型 |
|---|---|
| 000 | 其他/未知 |
| 001 | FAT 数据 |
| 010 | 目录数据 |
| 011 | 普通文件数据 |

剩余位（1 到 12 位）必须始终清零。

示例 1：以下语句从 C 盘器读取一个或多个扇区：

```asm
mov ax,7305h ; 绝对读/写
mov cx,0FFFh ; 始终为此值
mov dl,3 ; C 盘
mov bx,OFFSET diskStruct ; DISKIO 结构
mov si,0 ; 读取扇区
int 21h
```

示例 2：以下语句从 A 盘器写入一个或多个扇区：

```asm
mov ax,7305h ; 绝对读/写
mov cx,0FFFh ; 始终为此值
mov dl,1 ; A 盘
mov bx,OFFSET diskStruct ; DISKIO 结构
mov si,6001h ; 写入普通扇区
int 21h
```

## 14.4 读取和写入磁盘扇区 (7305h)

### 14.4.1 扇区显示程序

让我们通过编写一个读取并以 ASCII 格式显示单个磁盘扇区的程序，充分利用我们学到的扇区知识。伪代码列在此处：

```
显示标题
请求起始扇区号和驱动器号
循环直到 (按键 <> ESC)
读取一个扇区
如果是 MS-DOS 错误则退出
显示一个扇区
等待按键
扇区号加1
结束循环
```

程序列表：此处是 `Sector16.asm` 程序的完整列表。它可以在 Windows 95、98.0 和 Me 下运行，但在 Windows NT、2000 或 XP 下无法运行，因为这些系统对磁盘访问的安全性更严格：

```asm
TITLE Sector Display Program                (Sector16.asm)
; 演示 INT 21h 函数 7305h (ABSDReadWrite)
; 此实模式模式程序读取并显示磁盘扇区。

INCLUDE Irvine16.inc
Setcursor PROTO, row:BYTE, col:BYTE
EOLN EQ = 0dh,0ah
ESC_ROW = 1bh
DATA_ROW = 5
DATA_COL = 0
SECTOR_SIZE = 512
READ_MODE = 0                      ; 用于函数 7305h

DISKIO STRUCT
startSector WORD ?                ;起始扇区号
numS WORD 1                       ; 扇区数量
bufferOff WORD buffer              ; 缓冲区偏移
bufferSeg WORD @DATA             ; 缓冲区段
DISKIO ENDS
```

第 14 章 磁盘基础

```asm
.data
driveNumber BYTE ?
diskStruct DISIO <>
buffer BYTE SECTOR_SIZE DUP(0),0    ; 一个扇区

curr_row BYTE ?
curr_col BYTE ?
; 字符串资源
strLine BYTE EOLN, 79 DUP (0C4h),EOLN,0
strHeading BYTE "Sector Display Program (Sector16.exe)"
             BYTE EOLN,EOL,0
```

```asm
strAskSector BYTE "输入起始扇区号: "
strDrive BYTE "输入驱动器号 (1=A, 2=B, 3=C, 4=D, 5=E, 6=F): "
strCannotRead BYTE EOLN, **** 无法读取扇区。
BYTE "按任意键...", EOLN, 0

strReadingSector BYTE "按 Esc 退出，或按任意键继续..."
BYTE EOLN, EOLN, "正在读取扇区: "
```

```asm
.code
main PROC
mov ax,@data
mov ds,ax
call Clrscr
mov dx,OFFSET strHeading      ; 显示欢迎语
call Writestring               ; 请求用户...
call AskForSectorNumber

L1: call Clrscr
call ReadSector                ; 读取一个扇区
jc L2                           ; 如果错误则退出
call DisplaySector
call ReadChar
cmp al,ESC_KEY
je L3                           ; 是：退出
inc struct.startSector ; 下一个扇区
jmp L1                          ; 重复循环

L2: mov dx,OFFSET strCannotRead  ; 错误消息
call Writestring
call ReadChar

L3: call Clrscr
exit
main ENDP
```

```asm
AskForSectorNumber PROC
; 提示用户输入起始扇区号
; 和驱动器号。初始化 DISKIO 结构中的
; startSector 字段，以及
; driveNumber 变量。

push
mov dx,OFFSET strSector
call Writestring
call ReadInt
mov struct.startSector,ax
call Crlf
mov dx,OFFSET strDrive
call WriteString
mov driveNumber,al
call Crlf
pop
ret
AskForSectorNumber ENDP
```

```asm
ReadSector PROC
; 将扇区读入缓冲区。
; 接收：CF=0 表示成功，
; 否则 CF=1。

push
mov ax,7305h           ; 绝对读/写
mov cx,-1                ; 始终为此值
mov dl,driveNumber      ; 驱动器号
mov bx,OFFSET diskStruct  ; DISKIO 结构
mov si,0                ; 读取扇区
int 21h                  ; 写入
pop
ret
ReadSector END
```

```asm
DisplaySector PROC
; 以 ASCII 格式显示扇区。
; 接收：无。
; 要求：缓冲区必须包含数据。
push
...
pop
ret
DisplaySector ENDP
```

注：由于原文提供的文本在代码块和标题处存在重复和乱序，已按照高级文档工程师的逻辑确保内容的连贯性并去除了冗余部分。
