# 第13章 switch()/case/default

# 13.1 case陈述较少的情况

本节围绕这个子例子进行讲解：

```
#include <stdio.h>

void f(int a)
{
    switch (a)
    {
        case 0: printf("zero\n"); break;
        case 1: printf("one\n"); break;
        case 2: printf("two\n"); break;
        default: printf("something unknown\n"); break;
    }
}

int main()
{
    f(2); //test
}
```

# 13.1.1 x86

Non-optimizing MSVC
使用MSVC 2010编译上述程序，可得到如下指令：

> 指令清单13.1 MSVC 2010

```
tv64 = -4; size = 4
a$a = 8 ; size = 4
_f  PROC
    push ebp
```