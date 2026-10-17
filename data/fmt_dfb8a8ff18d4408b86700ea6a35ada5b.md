
```assembly
INCLUDE Irvine32.inc

.data
endl EQU <0dh,0ah> ; 行结束序列
message BYTE " - - - - Console1.asm - -"
BYTE endl, endl
BYTE "This program is a simple demonstration of console ",endl
BYTE "mode output, using the GetStdHandle and WriteConsole ",endl
BYTE "functions.",endl
BYTE " - - - -"
BYTE endl, endl, endl
messageSize = $(-message)

consoleHandle DWORD 0 ;指向标准输出设备的句柄
bytesWritten DWORD ? ; 写入的字节数

.code
main PROC
; 获取控制台输出句柄：
INVOKE GetStdHandle, STD_OUTPUT_HANDLE
mov consoleHandle,eax

; 向控制台写入字符串：
INVOKE WriteConsole,
consoleHandle, ; 控制台输出句柄
ADDR message, ; 字符串指针
messageSize, ; 字符串长度
ADDR bytesWritten, ; 返回写入的字节数
0 ; 未使用
INVOKE ExitProcess,0
main ENDP
END main.
```

程序产生以下输出：

```
Console1.asm
-----------------------------------------------------------------
This program is a simple demonstration of console
mode output, using the GetStdHandle and WriteConsole
functions.
----------------------------------------------------------------
```

### 11.1.4.4 WriteConsoleOutputCharacter 函数

`WriteConsoleOutputCharacter` 函数将字符数组复制到屏幕缓冲区连续单元格中，从指定位置开始。以下是其原型：

```assembly
WriteConsoleOutputCharacter PROTO,
handlesScreenBuf: DWORD, ; 控制台输出句柄
pBuffer:PTR BYTE, ; 缓冲区指针
bufsize:DWORD, ; 缓冲区大小
xyPos:COORD, ; 起单元格坐标
pCount:PTR DWORD ; 输出计数
```

如果文本行尾，会自动换行。缓冲区中的属性值不会改变。如果函数无法写入字符，它将返回零。制表符、回车和换行符等 ASCII 控制代码会被忽略。

## 11.1.5 文件的读取与写入

### 11.1 Win32 控制台编程

`NULL`,

`CREATE_ALWAYS`,

`FILE_ATTRIBUTE_NORMAL`,

`0` 覆盖现有文件

- 仅当文件不存在时才创建新文件：

  `INVOKE CreateFile`,

  `ADDR filename`,

  `GENERIC_WRITE`,

  `DO_NOT_SHARE`,

  `NULL`,

  `CREATE_NEW`,

  `FILE_ATTRIBUTE_NORMAL`,

  `0` 不删除现有文件

名为 `DO_NOT_SHARE` 和 `NULL` 的常量定义在本章程序使用的包含头文件中。请参阅书籍网站上所有包含头文件和链接库的最新文档。

### 11.1.5.2 CloseHandle 函数

`CloseHandle` 函数关闭已打开的句柄。其原型如下：

```
CloseHandle PROTO, handle:DWORD
```

### 11.1.5.3 ReadFile 函数

`ReadFile` 从输入文件中读取文本。`ReadFile` 可以可选地以异步模式运行，这意味着程序不需要等待操作完成。以下是其原型：

```
ReadFile PROTO,
handle:DWORD,
pBuffer:PTR BYTE,
BufferSize:DWORD,
pBytesRead:PTR DWORD,
pOverlapped:PTR DWORD,
; 从输入文件读取缓冲区
; 文件句柄
; 缓冲区指针
; 要读取的字节数
; 实际读取的字节数
; 指向异步信息的指针
```

`handle` 参数是 `CreateFile` 返回的已打开句柄。`pBuffer` 参数指向用于接收数据的缓冲区。`BufferSize` 参数指定了从文件中读取的最大字节数。`pBytesRead` 参数指向一个整数变量，用于在函数返回时指示实际读取的字节数；值为 0 表示文件末尾。`pOverlapped` 参数是可选的；它指向一个结构，指定函数如何异步地读取文件。对于同步操作（默认），请将空指针 `0` 作为 `pOverlapped` 值传递。

### 11.1.5.4 WriteFile 函数

`WriteFile` 函数使用输出句柄向文件写入数据。句柄可以是屏幕缓冲区句柄，也可以分配给文本文件。该函数从文件内部位置指针指示的位置开始向文件写入数据。写操作完成后，文件的位置指针将根据实际写入的字节数进行调整。以下是函数原型：

```
WriteFile PROTO;
fileHandle:DWORD,          ; 输出句柄
buffer:PTR BYTE,         ; 缓冲区指针
bufSize:DWORD,            ; 缓冲区大小
bytesWritten:PTR DWORD,   ; 写入的字节数
pOveroverlapped:PTR DWORD,  ; 指向异步信息的指针
```

### 11.1.5 示例写入程序

以下程序（`WriteFile.asm`）创建一个新文件并向文件中写入一些文本。它使用了 `CREATE_ALWAYS` 选项，因此任何现有文件将被擦擦：

```
TITLE Using WriteFile                          (WriteFile.asm)
```

```
INCLUDE Irvine32.inc
```

```
.data
buffer BYTE "This text is written to an output file.",0dh,0ah
bufSize = = ($-buffer)
errMsg BYTE "Cannot create file.",0dh,0ah,0
filename    BYTE "output.txt",0
fileHandle  DWORD ?                 ; 输出文件的句柄
bytesWritten DWORD ?               ; 写入的字节数
```

```
.code
main PROC
INVOKE CreateFile,
  ADDR filename, GENERIC_WRITE, DO_NOT_SHARE, NULL,
  CREATE_ATTRIBUTES, FILE_ATTRIBUTE_NORMAL, 0
mov fileHandle, eax          ; 保存文件句柄
  IF eax == INVALID_HANDLE_VALUE
  mov edx, OFFSET errMsg      ; 显示错误消息
  call WriteString
  jmp QuitNow
ENDP
```

```
INVOKE WriteFile,          ; 将文本写入文件
  fileHandle,               ; 文件句柄
  ADDR buffer,               ; 缓冲区指针
  bufSize,                  ; 要写入的字节数
  ADDR bytesWritten,        ; 写入的字节数
  0                         ; 重叠执行标志
```

```
INVOKE CloseHandle, fileHandle
```

QuitNow:

INVOKE ExitProcess,0 ; 结束程序

main ENDP

END main

### 11.1.5.6 移动文件指针

`SetFilePointer` 函数指定已打开文件的位置指针。该函数可用于向文件追加数据，或执行随机访问记录处理：

```
SetFilePointer PROTO,
handle:DWORD, ; 文件句柄
DistanceLo:SDWORD, ; 移动指针的字节数
DistanceHi:PTR SDWORD, ; 指向要移动字节数的指针，高位
moveMethod:DWORD ; 起点
```

`moveMethod` 参数指定了移动文件指针的起点。共有三个可能的值：`FILE_BEGIN`、`FILE_CURRENT` 和 `FILE_END`。距离本身是一个 64 位有符号整数值，分为两个部分：

- `nDistanceLo` - 低 32 位

- `pDistanceHi` - 指向包含高 32 位的变量指针。

如果 `DistanceHi` 为空，则仅使用 `nDistanceLo` 中的值来移动文件指针。以下是一个准备在文件末尾追加数据的示例调用：

```
INVOKE SetFilePointer,
handle, ; 文件句柄
0, ; 距离低位
0, ; 距离高位
FILE_END ; 移动方法
```

在示例磁盘上，`AppendFile.asm` 程序向现有文件追加数据。`ReadFile.asm` 程序打开由 `WriteFile.asm` 创建的文件，读取数据，关闭文件并显示缓冲区：

```
TITLE ReadFile (ReadFile)
INCLUDE Irvine32.inc
.data
buffer 500 DUP(?)
bufSize = = 500
errMsg BYTE "Cannot open file.",0dh,0ah,0
filename    BYTE "output.txt",0
fileHandle  DWORD ?                 ; 文件句柄
byteCount DWORD ?               ; 字节数

.code
main PROC
INVOKE CreateFile,
  ADDR filename, GENERIC_READ, DO_NOT_SHARE, NULL,
  OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL, 0
mov fileHandle, eax          ; 保存文件句柄
  IF eax == INVALID_HANDLE_VALUE
  mov edx, OFFSET errMsg      ; 显示错误消息
  call WriteString
  jmp QuitNow

INVOKE ReadFile,
  fileHandle,               ; 文件句柄
  ADDR buffer,               ; 缓冲区指针
  bufSize,                  ; 要读取的字节数
  ADDR byteCount,           ; 实际读取的字节数
  0                         ; 重叠执行标志

mov esi, byteCount          ; 字节数
mov buffer[esi],0           ; 插入终止符
call WriteString              ; 显示缓冲区
INVOKE CloseHandle, fileHandle

QuitNow:
INVOKE ExitProcess,0 ; 结束程序
main ENDP
END main
```

### 11.1.6 控制台操作

Win32 API 对控制窗口提供了有限的控制，以及存储数据的屏幕缓冲区。图 11-1 显示缓冲区可以比显示的行数大。控制窗口作为一个“视口”，只显示缓冲区的一部分。

有几个函数可以影响控制窗口及其位置。`SetConsoleWindow` 设置控制窗口相对于缓冲区的大小和位置。`GetConsoleScreenBuffer` 返回控制窗口的坐标。`SetCursorPosition` 将光标设置为缓冲区内的任何位置：如果该区域不可见，则控制窗口将移动。

### 11.1.6.1 SetConsoleTitle

`SetConsoleTitle` 函数允许你更改控制窗口的标题。示例如下：

```
.data
titleStr BYTE "Console title", 0
.code
INVOKE SetConsoleTitle, ADDR titleStr
```

### 11.1.6.2 GetConsoleScreenBufferInfo

`GetConsoleBufferInfo` 函数返回控制窗口当前状态。它有两个参数：控制屏幕的句柄和一个指向由函数填充的结构的指针：

```
GetConsoleBufferInfo PROTO,
noutHandle:DWORD,      ; 屏幕缓冲区句柄
pBufferInfo:PTR SCREEN_BUFFER_INFO
```

以下是 `CONSOLE_SCREEN_BUFFER_INFO` 结构：

```
CONSOLE_SCREEN_BUFFER_INFO STRUCT
dSize           COORD <
dCursorPos      COORD <
```

```assembly
wAttributes      WORD ?
srWindow         SMALL_RECT <
maxWindow       COORD <
CONSOLE_SCREEN_BUFFER_INFO ENDS
```

`dwSize` 返回屏幕缓冲区的尺寸，单位为字符列和行。`dwCursorPos` 返回光标的位置。这两个字段都是 `COORD` 结构体。`Attributes` 返回由 `WriteConsole` 等函数写入控制台的字符的前景和背景颜色。`srWindow` 返回控制台窗口相对于屏幕区的坐标。`maxWindow` 根据当前屏幕缓冲区大小、字体和视频显示大小返回控制台窗口的最大尺寸。以下是该函数的示例调用：

```assembly
.data
consoleInfo CONSOLE_SCREEN_BUFFER_INFO <
.code
INVOKE GetConsolescreenBufferInfo, outHandle,
ADDR consoleInfo
```

以下是结构体数据的示例，由 Microsoft Visual Studio 调试器显示：

| Name | Value |

|---|---|

| consoleInfo | {..} |

| dwSize | 120 |

| X | |

| Y | 50 |

| dwCursorPos | {..} |

| X | 20 |

| Y | 5 |

| wAttributes | 7 |

| srWindow | {..} |

| Left | 0 |

| Top | 0 |

| Right | 79 |

| Bottom | 24 |

| maxWindow | {..} |

| X | 100 |

| Y | 46 |

### 11.1.6.3 SetConsoleWindowInfo 函数

`SetConsoleWindowInfo` 函数设置控制台窗口相对于其屏幕区的尺寸和位置。以下是其函数原型：

```assembly
SetConsoleWindowInfo PROTO,      ; 设置控制台窗口的位置
stdHandle:DWORD,                ; 屏幕缓冲区句柄
bAbsolute:DWORD,                 ; 坐标类型
ConsoleRect:PTR SMALL_RECT,    ; 指向窗口矩形的指针
```

`hAbsolute` 参数指示 `pConsoleRect` 指向的结构体中的坐标如何使用。如果 `hAbsolute` 为 `true`，坐标指定控制台窗口新的左上角和右下角。如果 `hAbsolute` 为 `false`，则坐标将加到当前窗口坐标上。

下面的 `Scroll` 程序向屏幕缓冲区写入五十行文本。然后它调整控制台窗口的大小并重新定位，从而有效地使文本向后滚动。它使用了 `SetConsoleWindowInfo` 函数：
