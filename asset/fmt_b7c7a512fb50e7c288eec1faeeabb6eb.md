
```
DISKIO STRUCT
startSector DWORD 0 ;起始扇区号
numS WORD 1 ; 扇区数量
bufferOff WORD buffer ; 缓冲区偏移
bufferSeg WORD @DATA ; 缓冲区段
DISKIO ENDS
```

以下是用于存储扇区数据的缓冲区示例，以及一个 `DISKIO` 结构变量：

```
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

```
mov ax,7305h ; 绝对读/写
mov cx,0FFFh ; 始终为此值
mov dl,3 ; C 盘
mov bx,OFFSET diskStruct ; DISKIO 结构
mov si,0 ; 读取扇区
int 21h
```

示例 2：以下语句从 A 盘器写入一个或多个扇区：

```
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

```
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

第 14 章 磁盘基础

```
strAskSector BYTE "输入起始扇区号: "
strDrive BYTE "输入驱动器号 (1=A, 2=B, 3=C, 4=D, 5=E, 6=F): "
strCannotRead BYTE EOLN, **** 无法读取扇区。
BYTE "按任意键...", EOLN, 0

strReadingSector BYTE "按 Esc 退出，或按任意键继续..."
BYTE EOLN, EOLN, "正在读取扇区: "
```

```
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

```
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

14.4 读取和写入磁盘扇区 (7305h)
```

```
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

```
DisplaySector PROC
; 以 ASCII 格式显示扇区。
; 接收：无。
; 要求：缓冲区必须包含数据。
 dx,, str str      ; 显示欢迎欢迎
call Writ
;; 请求用户...
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

## 表 14-6 选 INT 21h 磁盘服务（续）

| 功能号 | 功能名称 |
|---|---|
| 4Eh | 查找第一个匹配的文件 |
| 4Fh | 查找下一个匹配的文件 |
| 56h | 重命名文件 |
| 57h | 获取/设置文件日期和时间 |
| 59h | 获取扩展错误信息 |

让我们详细查看几个常用的函数。MS-DOS 中断及其描述的更详尽列表可以在附录 C 中找到。

## 14.5.1 获取磁盘空闲空间 (7303h)

`INT 21h` 功能 `7303h` 可用于查找磁盘卷的大小以及可用空闲空间的大小。信息以名为 `ExtGetDskFspecStruct` 的标准结构返回，如下所示：

```
ExtGetDskFspecStruct STRUC
Size WORD ?
nLevel WORD ?
ectorsPerCluster DWORD ?
BytesSector DWORD ?
AvailableClusters DWORD ?
TotalClusters DWORD ?
AvailablePhysectors DWORD ?
AvailableAllocationUnits DWORD ?
TotalAllocationUnits DWORD ?
Rsvd DWORD 2 DUP (?)
nGetDskfspecStruct ENDS
```

（该结构的副本位于 `Irvine_16.inc` 文件中。）以下列表包含每个字段的要描述：

- **Size**: 一个返回值，表示 `ExtGetDskFspecStruct` 结构的大小，单位为字节。当执行 `INT 21h` 功能 `7303h` (Get_ExtFreespace) 时，会将结构的大小放在此成员中。
- **Level**: 输入和返回的级别值。此字段必须初始化为零。
- **SectorsPerCluster**: 每个簇内的扇区数量。
- **BytesPerSector**: 每个扇区内的字节数。
- **AvailableClusters**: 可用簇的数量。
- **TotalClusters**: 卷上的簇总数。

## 14.5 系统级文件函数

- **AvailablePhysSectors**: 卷上可用的物理扇区数量，不考虑压缩调整。
- **TotalPhysSectors**: 卷上的物理扇区总数，不考虑压缩调整。
- **AvailableAllocationUnits**: 卷上可用的分配单元数量，不考虑压缩调整。
- **TotalAllocationUnits**: 卷上的分配单元总数，不考虑压缩调整。
- **Rsvd**: 预留成员。

调用 `INT 21h` 功能 `7303h` 的函数时，需要以下输入参数：

- `AX` 必须等于 `7303h`。
- `ES`：必须指向一个 `GetDskFreeSpcStruct` 变量。
- `CX`：必须包含 `GetDskFreeSpcStruct` 变量的大小。
- `DS`：必须指向一个包含驱动器名称的空终止字符串。你可以使用 MS-DOS 类型的驱动器规范，例如 ("C:")，或者可以使用通用命名约定卷规范，例如 ("\\ServerShare")。

如果函数执行成功，它将携带进位标志（Carry flag）和结构中的标志。否则，它将携带进位标志。调用函数后，以下类型的计算可能有用：

- 要找出卷以 KB 为单位有多大，请使用以下公式：`(TotalClusters * SectorsPerCluster * BytesPerSector) / 1024`。
- 要找出卷中存在多少 KB 为单位的空闲空间，公式应为：`(AvailableClusters * SectorsPerCluster * BytesPerSector) / 1024`。

### 14.5.1.1 磁盘空闲空间程序

程序使用 `INT 21h` 功能 `7303h` 获取 FAT 类型驱动器的空闲空间信息。它显示卷的大小和空闲空间：

```
TITLE Disk Free Space (DiskSpc.asm)
```

```
; 此程序在 Windows 95, 98 和 Me 下可产生有意义的输出
;但在 Windows NT, 2000 或 XP 下可能不产生输出。
INCLUDE Irvine16.inc
.data
buffer GetDskFreeSpcStruct <
driveName BYTE "C:\",0
str1 BYTE "Volume size (KB): ",0
str2 BYTE "Free space (KB): ",0
str3 BYTE "Function call failed.",0dh,ah,0
```

```
.code
main PROC
mov ax,@data
mov ds,ax
mov es,ax ; ES 必须指向数据段
mov buffer.Level,0 ; 必须为零
mov di,OFFSET buffer ; ES:DI 指向 buffer
mov cx,SIZE buffer ; buffer 大小
mov dx,OFFSET DriverManager ; 指向驱动器名称的指针
mov ax,7303h ; 获取磁盘空空间
int 21h
jc error ; 如果 CF=1 则失败
mov dx,OFFSET strl ; 卷大小
call WriteString
call CalVolumeSize
call WriteDec
call Crlf
mov dx,OFFSET str2 ; 空闲空间
call WriteString
call CalVolumeFree
call WriteDec
call Crlf
jmp quit
error:
mov dx,OFFSET str3 ; 函数调用失败
call WriteString
quit:
exit
main ENDP
```

```
CalcVolumeSize PROC
; 计算并返回卷的大小，单位为 KB。
; 接收：buffer 变量，一个 ExtGetDkFreeSpcStruct
; 返回：EAX = 卷的大小
; 备注：(SectorsPerCluster * 512 * TotalClusters) / 1024
mov eax,buffer.SectorsPerCluster
shl eax,9 ; 乘以 512
mul buffer.TotalClusters
div 1024 ; 除以 1024
retCalcVolumeSize ENDP
```

```
CalcVolumeFree PROC
; 计算并返回卷的空闲空间，单位为 KB。
; 接收：buffer 变量，一个 ExtGetDkFreeSpcStruct
; 返回：EAX = 空闲空间
; 备注：(SectorsPerCluster * 512 * AvailableClusters) / 1024
; ---------------------------------------
mov eax,buffer.SectorsPerCluster
shl eax,9 ; 乘以 512
mul buffer.AvailableClusters
div 1024 ; 除以 1024
ret
CalcVolume ENDP
END main
```

## 14.5.2 创建目录 (39h)

`INT 21h` 功能 `39h` 创建新目录。它接收一个指向空终止字符串的指针。以下示例显示如何创建一个目录：

```
.data
pathname BYTE "\ASM",0
.code
mov ah,39h ; 创建目录
mov dx,OFFSET pathname
int 21h
```

如果失败，进位标志将被设置。可能的错误代码为 3（未找到路径）和 5（已存在）。

## 14.5.3 删除目录 (3Ah)

`INT 21h` 功能 `3Ah` 删除子目录。它接收驱动器和路径的指针。如果驱动器为空，则假设为默认驱动器。以下代码从 C 盘删除 `\ASM`：

```
.data
pathname BYTE 'C:\ASM',0
.code
mov ah,3Ah ; 删除子目录
mov dx,OFFSET pathname
int 21h
```

如果函数失败，进位标志将被设置。可能的错误代码为 5（拒绝访问：目录包含文件）。

## 14.5.4 设置当前目录 (3Bh)

`INT 21h` 功能 `3Bh` 设置当前目录。它接收一个指向目标驱动和路径的空终止字符串。例如，以下语句将当前目录设置为 `C:\ASM\PROGS`：

```
.data
pathname BYTE "C:\ASM\PROGS", 0
.code
mov ah,3Bh ; 设置当前目录
mov dx,OFFSET pathname
int 21h
```

## 14.5.5 获取当前目录 (47h)

`INT 21h` 返回一个包含当前目录的字符串。它接收驱动器号 `DL`（0=默认，1=A，2=B 等）以及一个指向 64 字节缓冲区的 `DS:SI`。在此缓冲区中，MS-DOS 放置从根目录开始的完整空终止字符串（省略驱动器字母和前斜杠）。如果函数返回时进位标志被设置，`AX` 中可能的错误代码为 `0Fh`（无效驱动器规范）。

在以下示例中，MS-DOS 返回默认驱动器的当前目录路径。假设当前目录是 `C:\ASM\PROGS`，MS-DOS 返回的字符串为 `C:\ASM\PROGS`：

```
.data
pathname BYTE 64 dup(0)      ; MS-DOS 存储在此
```
