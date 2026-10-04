# 第21章 结构体

在C/C++的数据结构里结构体（structure）是由一系列数据结构简单堆积而成的的数据类型。结构体中的各项数据元素，可以是相同类型的数据，也可以是不同类型的数据。[1]

# 21.1 MSVC: systemtime

本节以Win32描述系统时间的SYSTEMTIME结构体为例。

函数对它的定义如下[2]

指令清单21.1 WinBase.h

```
typedef struct _SYSTEMTIME {
WORD wYear;
WORD wMonth;
WORD wDayOfWeek;
WORD wDay;
WORD wHour;
WORD wMinute;
WORD wSecond;
WORD wMilliseconds;
} SYSTEMTIME;
```

根据上述声明，获取系统时间的程序大致如下：

```
#include <windows.h>
#include <stdio.h>
void main() {
  SYSTEMTIME t;
  GetSystemTime(&t);

  printf("%04d-%02d-%02d %02d:%02d:%02d\n", t);
```