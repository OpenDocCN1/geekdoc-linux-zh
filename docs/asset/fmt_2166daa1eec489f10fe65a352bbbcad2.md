
```assembly
TITLE Scrolling the Console Window (Scroll.asm)
INCLUDE Irvine32.inc
.data
message BYTE : "To this line of text was written To the screen buffer",0dh,0ah
messageSize = ($-message)
outHandle DWORD 0 ; 标准输出句柄
bytesWritten DWORD ? ; 写入字节数
lineNum DWORD 0
windowRect SMALL_RECT <0,0,60,11> ; 左,上,右,下
.code
main PROC
INVOKE GetStdHandle, STD_OUTPUT_HANDLE
mov outHandle, eax
.REPEAT
mov eax,lineNum
call WriteDec ; 显示每个行号
INVOKE WriteConsole,
outHandle, ; 控制台输出句柄
ADDR message, ; 字符串指针
messageSize, ; 字符串长度
ADDR bytesWritten, ; 返回写入的字节数
0 ; 不使用
inc lineNum ; 下一个行号
UNTIL lineNum > 50
; 相对于屏幕缓冲区调整并重新定位控制台窗口。
INVOKE SetConsoleWindowInfo,
outHandle,
TRUE,
ADDR windowRect ; 窗口矩形
call ReadChar ; 等待按键
call Clrscr ; 清除屏幕缓冲区
call ReadChar ; 等待第二个按键
```
```assembly
INVOKE ExitProcess,0
main ENDP
END main
```

最好直接从 MS-Windows 资源管理器运行此程序，而不是在集成编辑器环境中。编辑器可能会影响控制台窗口的行为和外观。注意，你必须在最后按一次键：第一次清除屏幕缓冲区，第二次结束程序。（这是为了测试目的而添加的。）

## 11.1.6.4 SetConsoleBufferSize 函数

`SetConsoleBufferSize` 函数允许你将屏幕缓冲区设置为 X 列 Y 行。以下是其原型：

```assembly
SetConsoleBufferSize PROTO,
outHandle:DWORD,      ; 屏幕缓冲区句柄
dwSize:COORD           ; 新的屏幕缓冲区尺寸
```

## 11.1.7 控制光标

Win32 API 提供了设置光标大小、可见性和屏幕位置的函数。与这些函数相关的重要数据结构是 `CONSOLE_CURSOR_INFO`，它包含有关控制台光标大小和可见性的信息：

```assembly
CONSOLE_CURSOR_INFO STRUCT
dwSize ?
bVisible BOOL =
CONSOLE_CURSOR_INFO END
```

`dwSize` 是光标填充字符单元的百分比（1 到 100）。如果 `bVisible` 等于 `TRUE`，则光标可见。

### 11.1.7.1 GetConsoleCursorInfo 函数

`GetConsoleCursorInfo` 函数返回控制台光标的大小和可见性。传入指向 `CONSOLE_CURSOR_INFO` 结构的指针：

```assembly
GetConsoleCursorInfo PROTO,
outHandle:DWORD,      ; 输出句柄
pCursorInfo:PTR CONSOLE_CURSOR_INFO ; 光标信息
```

默认情况下，光标大小为 25，表示字符单元被光标填充了 25%。

### 11.1.7.2 SetConsoleCursorInfo 函数

`SetConsoleCursorInfo` 函数设置光标的大小和可见性。传入指向 `CONSOLE_CURSOR_INFO` 结构的指针：

```assembly
SetConsoleCursorInfo PROTO,
outHandle:DWORD,      ; 输出句柄
pCursorInfo:PTR CONSOLE_CURSOR_ ; 光标信息
```

### 11.1.7.3 GetConsolePosition 函数

`GetConsolePosition` 函数返回光标的 X Y 坐标。传入指向 `COORD` 结构的指针：

```assembly
GetConsolePosition PROTO,
outHandle:DWORD,      ; 输出句柄
pCursorPos:PTR COORD ; 光标位置
```

### 11.1.7.4 SetConsolePosition 函数

`SetConsolePosition` 函数设置光标的 X Y 坐标。传入 `COORD` 结构的指针：

```assembly
SetConsolePosition PROTO,
outHandle:DWORD,      ; 输出句柄
pCursorPos:PTR COORD
```

## 11.1.8 控制颜色

有两种方法可以控制控制台文本的颜色。你可以通过调用 `SetAttribute` 更改当前文本颜色，也可以通过调用 `WriteOutputAttribute` 设置特定单元的属性。

### 11.1.8.1 SetAttribute 函数

`SetAttribute` 函数设置后续输出的前景颜色。以下是其原型：

```assembly
SetAttribute PROTO,
outHandle:DWORD,      ; 输出句柄
wAttributes:WORD     ; 属性
```

### 11.1.8.2 WriteOutputAttribute 函数

`WriteOutputAttribute` 函数将属性数组复制到连续单元。以下是其原型：

```assembly
WriteOutputAttribute PROTO,
outHandle:DWORD,      ; 输出句柄
pAttribute:PTR WORD,  ; 属性
Length:DWORD,         ; 长度
xyCoord:COORD,        ; 起始单元
pCount:PTR DWORD      ; 单元数
```

### 11.1.8.3 示例 WriteColors

为了演示颜色和属性的使用，`WriteColors` 程序创建了一个字符数组和一个属性数组（每个字符对应一个属性）。它调用 `WriteOutputAttribute` 将属性写入屏幕缓冲区，并调用 `WriteCharacter` 将字符写入同一个缓冲区：

```assembly
TITLE Writing Color (WriteColors.asm)
INCLUDE Irvine32.inc
.data
outHandle DWORD ?
cellsWritten DWORD ?
yPos COORD <10,2>

; 字符代码数组：
buffer BYTE 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15
BYTE 16,17,18,19,20

BufSize = ($ - buffer)
; 属性数组：
attributes WORD 0FH,0Eh,0DH,0CH,0Bh,0Ah,9,8,7,6
5,4,3,2,1,0Eh,0Bh

.code
main PROC 控制台标准输出句柄：
; Get StdHandle,
INVOKE GetStdHandle,STD_OUTPUT_HANDLE
mov outHandle, eax
; 设置相邻单元的颜色：
INVOKE WriteOutputAttribute,
outHandle, ADDR attributes,
BufSize, yPos,
ADDR cellsWritten

; 写入字符代码 1 到 20：
INVOKE WriteCharacter,
outHandle, ADDR buffer, BufSize,
yPos,
ADDR cellsWritten

INVOKE ExitProcess,0          ; 结束程序
main ENDP
END main
```

这是程序输出的快照，显示字符代码 1–20 显示为图形字符。每个字符颜色都不同，尽管颜色在打印页面上并不显示：

## 11.1 Win32 控制台编程

### 11.1.9 时间和日期函数

Win32 API 提供了相当多的时间和日期函数。对于初学者来说，你可以获取和设置当前的日期和时间。在本节中，我们只展示了此类函数的一小部分，但你可能也想查看表 11-6 中列出的 Win32 函数。

表 11-6 Win32 日期时间函数.a

| 函数 | 描述 |
| --- | --- |
| CompareFile | 比较两个 64 位的文件时间。 |
| DosTimeToToFile | 将 MS-DOS 日期时间值转换为 64 位文件时间。 |
| FileTimeToDosDate | 转换为 MS-DOS 日期时间值。 |
| FileTimeToLocalFile | 将 UTC（通用协调时间）文件时间转换为本地时间。 |
| FileTimeToSystemTime | 将 64 位文件时间转换为系统格式。 |
| GetFileTime | 获取文件创建、最后访问和最后修改的日期和时间。 |
| GetLocalTime | 获取当前的本地日期和时间。 |
| GetSystemTime | 获取 UTC 格式的当前系统日期和时间。 |
| GetSystemTimeAdjustment | Determine系统是否对其时钟应用周期性时间调整。 |
| GetSystemTimeAsFileTime | 获取 UTC 格式的当前系统日期和时间。 |
| GetTickCount | 获取系统启动以来经过的毫秒数。 |
| GetTimeZoneInformation | 获取当前的时区参数。 |
| LocalTimeToToFile | 将本地文件时间转换为基于 UTC的时间。 |
| SetFileTime | 设置文件创建、最后访问和最后修改的日期和时间。 |
| SetLocalTime | 设置当前的本地日期和时间。 |
| SetSystemTime | 设置当前的系统日期和时间。 |
| SetSystemTimeAdjustment | 启用或禁用对系统时钟的周期性时间调整。 |
| SetTimeZoneInformation | 设置当前的时区参数。 |

表 11-6 Win32 日期时间函数.a（续）

| 函数 | 描述 |
| --- | --- |
| SystemTimeToToFile | 将系统时间转换为文件时间。 |
| SystemTimeToSpecificLocal | 将 UTC 时间转换为指定时区的对应本地时间。 |

a 来源：Microsoft MSDN Windows SDK 文档。

`SYSTEMTIME` 结构体。`SYSTEMTIME` 结构体用于与日期时间相关的 Windows API 函数：

- `SYSTEMTIME STRUCT`
- `wYear WORD ?` : 年份（4 位）
- `wMonth WORD ?` : 月份（1-12）
- `wDayOfWeek WORD ?` : 星期（0-6）
- `wDay WORD ?` : 日期（1-31）
- `wHour WORD ?` : 小时（0-23）
- `wMinute WORD ?` : 分钟（0-59）
- `wSecond WORD ?` : 秒（0-59）
- `wMilliseconds WORD ?` : 毫秒（0-999）
- `SYSTEMTIME ENDS`

`wDayOfWeek` 字段从星期日=0 开始，星期一=1，以此类推。`wMilliseconds` 的值不是精确的，因为计算机的内部时钟随着时间的推移而修改。

#### 11.1.9.1 GetLocalTime 和 SetLocalTime

`GetLocalTime` 函数根据系统时钟返回日期和当前时间。时间已根据本地区域进行了调整。调用时，传递指向 `SYSTEMTIME` 结构体的指针：

```
GetLocalTime PROTO,
pSystemTime:PTR SYSTEMTIME
```

`SetLocalTime` 函数设置系统的本地日期和时间。调用它时，传递指向 `SYSTEMTIME` 结构体的指针：

```
SetLocalTime PROTO,
pSystemTime:PTR SYSTEMTIME
```

如果函数执行成功，它返回一个非零整数；如果失败，则返回零。

以下是 `GetLocalTime` 的示例调用：

```
.data
sysTime SYSTEMTIME <>
.code
INVOKE GetLocalTime, ADDR sysTime
```

#### 11.1.9.2 GetTickCount 函数

`GetTickCount` 函数返回系统启动以来经过的毫秒数：

```
GetTickCount PROTO             ; 返回值在 EAX 中
```

由于返回值是一个双字（doubleword），如果系统连续运行 49.7 天，时间将回绕零。你可以使用此函数在循环中监控已过的时间，并在达到特定时间限制时跳出循环。例如，下面的程序每 100 毫秒在屏幕上显示一个点，并检查经过的时间直到达到 5000 毫秒。此代码可以用于各种程序：

```
TITLE Calculate Elapsed Time      (TimingLoop.asm)
```

```
; 此程序使用 GetTickCount 来计算
; 程序启动以来经过的
; 毫秒数
```

```
INCLUDE Irvine32.inc
TIME_LIMIT = 5000
.data
startTime DWORD ?
dot BYTE ",0"
.code
main PROC
INVOKE GetTickCount      ; 获取毫秒
mov startTime,eax
L1:mov edx,OFFSET dot ; 显示一个点
call Print
INVOKE Sleep,100      ; 睡眠 100 ms
INVOKE GetTickCount
sub eax,startTime
cmp eax,TIME_LIMIT
jb L1
exit
main ENDP
```

`Sleep` 函数挂起当前线程指定的毫秒数：

```
Sleep PROTO,
Milliseconds:DWORD
```

#### 11.1.9.5 创建秒表

我们可以使用 `GetTickCount` 函数作为工具创建两个协作形成秒表的过程。一个名为 `TimerStart` 的过程记录当前时间。另一个过程（命名为 `GetDateTime`）接收一个双字指针，并将当前日期时间存储在 `FILETIME` 结构体中。建议步骤如下：

1. 调用 `GetLocalTime` 填充 `SYSTEMTIME` 结构体。
2. 调用 `SystemTimeToToFile` 将 `SYSTEMTIME` 转换为 `FILETIME`。
3. 将结果 `FILETIME` 拷贝到两个双字（64 位整数）。

```
FILETIME STRUCT
loDateTime ?
hiDateTime ?
FILETIME ENDS
```

```
GetDateTime PROC,
pStartTime:PTR QWORD
LOCAL sysTime:SYSTEMTIME, flTime:FILETIME
; 获取日期时间并存储在变量中。
; 接收一个指向变量的指针，该变量将持有
; 当前时间。
; 返回：无
------------------------------------------------------
```

INVOKE GetLocalTime,
ADDR sysTime
INVOKE SystemTimeToToFile,
ADDR sysTime,
ADDR flTime
mov esi,pStartTime
mov eax,flTime.loDateTime
mov DWORD PTR [esi],eax
mov eax,flTime.hiDateTime
mov DWORD PTR [esi+4],eax
ret
GetDateTime ENDP
```

`TimerStart` 记录当前时间。
`TimerStop` 返回自上次调用 Timer 以来经过的毫秒数。下面的 `Timer.asm` 程序调用这两个过程，并通过调用 `Sleep` 函数创建一个有意延迟：

```
TITLE Calculate Elapsed Time (Timer.asm)
```

```
; 使用 Win32 GetTickCount 函数
; 展示一个简单的秒表
```

```
INCLUDE Irvine32.inc
```

```
TimerStart PROTO,
pSavedTime: PTR DWORD
```

```
TimerStop PROTO,
pSavedTime: PTR DWORD
```

```
.data
msg BYTE " milliseconds have elapsed",0dh,0ah,0
timer1 DWORD ? ?
```

```
.code
main PROC
INVOKE TimerStart,           ; 开始计时
    ADDR timer1
INVOKE Sleep, 5000          ; 睡眠 5 秒
INVOKE TimerStop,           ; EAX = 经过的毫秒
    ADDR timer1
call WriteDec                ; 显示经过的时间
mov edx,OFFSET msg
call WriteString
exit
main ENDP
```

```
------------------------------------------------------
TimerStart PROC USES esi,
```
