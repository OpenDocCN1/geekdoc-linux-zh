
## 描述

字节字符串函数处理不以 NULL 结尾的字符串。请参见每个函数的单独页面。

# 另请参见

`bcmp(3)`, `bcopy(3)`, `bzero(3)`, `memccpy(3)`, `memchr(3)`, `memcmp(3)`, `memcpy(3)`, `memfrob(3)`, `memmem(3)`, `memmove(3)`, `memset(3)`

> 1993年6月8日

# atan2

`atan2`—两个变量的反正切函数

## 概要

```c
#include <math.h>

double atan2(double y, double x);
```

## 描述

`atan2()` 函数计算两个变量 `x` 和 `y` 的反正切角。它与计算 `y/x` 的反正切角相似，不同在于使用两个参数的正弦值来确定结果所在的象限。

## 返回值

`atan2()` 函数以弧度为单位返回结果，该值在 `-PI` 和 `PI` 之间（包含）。

## 符合标准

SVID 3, POSIX, BSD 4.3, ISO 9899

## 另请参见

`acos(3)`, `asin(3)`, `atan(3)`, `cos(3)`, `sin(3)`, `tan(3)`

1993年6月8日

# atanh

`atanh`—反双曲正切函数

## 概要

```c
#include <math.h>

double atanh(double);
```

## 描述

`atanh()` 函数计算 `x` 的反双曲正切。如果 `x` 的绝对值大于 1.0，`acosh()` 返回非数字（NaN），并设置 `errno`。

## 错误

- `EDOM`: `x` 超出范围。

## 符合标准

SVID 3, POSIX, BSD 4.3, ISO 9899

## 另请参见

`asinh(3)`, `acosh(3)`, `cos(3)`, `sinh(3)`, `tanh(3)`

1993年6月13日

# atexit

`atexit`—注册一个在程序正常结束时调用的函数

## 概要

```c
#include <stdlib.h>

int atexit(void (*function));
```

## 描述

`atexit()` 函数注册给定的函数，使其在程序正常结束时（无论是通过 `exit(2)` 还是从程序的 `main` 函数返回）被调用。函数按照注册的反顺序进行调用；不传递任何参数。

## 返回值

如果 `exit(i)` 函数执行成功，返回值 0；否则返回值 -1，并设置全局变量 `errno` 以指示错误。

## 错误

- `ENOMEM`: 内存不足以添加该函数。

## 符合标准

SVID 3, BSD 4.3, ISO 9899

## 另请参见

`exit(3)`, `onexit(3)`

> GNU, 1993年3月29日

# atof

`atof`—将字符串转换为双精度浮点数

## 概要

```c
#include <stdlib.h>

double atof(const char *nptr);
```

## 描述

`atof(nptr)` 函数将 `nptr` 指向的字符串初始部分转换为 double。其行为与 `strtod(nptr, char **NULL)` 相同；但 `atof()` 不检测错误。

## 返回值

转换后的值。

## 符合标准

SVID 3, POSIX, BSD 4.3, ISO 9899

## 另请参见

`atoi(3)`, `atoi(3)`, `strtod(3)`, `strtol(3)`, `strt(3)`

> GNU, 1993年3月29日

# atoi

`atoi`—将字符串转换为整数

## 概要

```c
#include <stdlib.h>

int atoi(const char *nptr);
```

## 描述

`atoi()` 函数将 `nptr` 指向的字符串初始部分转换为 int。其行为与 `strtol(nptr, char **NULL, 10)` 相同；但 `atoi()` 不检测错误。

## 返回值

转换后的值。

## 符合标准

SVID 3, POSIX, 4.3, BSD, ISO 9899

## 另请参见

`atol(3)`, `atoi(3)`, `strtod(3)`, `strtol(3)`, `strtol(3)`

> GNU, 1999年3月29日

# atol

`atol`—将字符串转换为长整数

## 概要

```c
#include <stdlib.h>

long atol(const char *nptr);
```

## 描述

`atoi()` 函数将 `nptr` 指向的字符串初始部分转换为 long。其行为与 `strtol(nptr, char **NULL)` 相同；但 `atoi()` 不检测错误。

## 返回值

转换后的值。

## 符合标准

SVID 3, POSIX, 4.3, BSD

## 另请参见

`atol(3)`, `atoi(3)`, `strtod(3)`, `strtol(3)`

> GNU, 1999年

# bcmp

`bcmp`—比较字符串

## 概要

```c
#include <string.h>

int bcmp(const void *s1, const void *s2, int n);
```

## 描述

`bcmp()` 函数比较 `s1` 和 `s2` 的前 `n` 个字节。如果字符串相等，`bcmp()` 返回 0；否则返回非零值。

## 返回值

如果字符串相等，`bcmp()` 返回 0。

## 符合标准

4.3, 该函数已废用——请使用 `memcmp`。

## 另请参见

`memcmp(3)`, `strcmp(3)`, `strncmp(3)`

# bcopy

`bcopy`—拷贝字符串

## 概要

```c
#include <string.h>

void bcopy(const void *src, void *dest, int n);
```

## 描述

`bcopy()` 函数将 `src` 的前 `n` 个字节拷贝到 `dest`。如果 `n` 为 0，则不拷贝。

## 返回值

`bcopy()` 不返回值。

## 符合标准

4.3, 该函数已废用——请使用 `memcpy`。

## 另请参见

`memcpy(3)`, `str#`

## 第三部分：库函数

```c
unsigned long int ntohl(unsigned long int netlong);
unsigned short int ntohs(unsigned short int netshort);
```

## 描述

`htonl()` 函数将长整型 `hostlong` 从主机字节序转换为网络字节序。
`htons()` 函数将短整型 `hostshort` 从主机字节序转换为网络字节序。
`ntohl()` 函数将长整型 `netlong` 从网络字节序转换为主机字节序。
`ntohs()` 函数将短整型 `netshort` 从网络字节序转换为主机字节序。
在 i386 上，主机字节序是低有效字节在前，而互联网使用的网络字节序是高有效字节在前。

## 遵循

BSD 4.3

## 另请

`gethostbyname(3)`, `getservent(3)`

> BSD, 1993年4月15日

## bzero

`bzero`—向字节字符串写入 os 字节

## 概要

```c
#include <string.h>

void bzero(void *s, int n);
```

## 描述

`bzero()` 函数将字节字符串 `s` 的前 `n` 个字节置为 0。

## 返回值

`bzero()` 函数没有返回值。

## 遵循

4.3BSD。此函数已废弃——在新程序中使用 `memset`。

## 另请

`memset(3)`, `swab(3)`

> GNU, 1993年4月9日

## catgets

`catgets`—从消息目录中获取消息

## 概要

```c
#include <features.h>
#include <nl_types.h>
```
