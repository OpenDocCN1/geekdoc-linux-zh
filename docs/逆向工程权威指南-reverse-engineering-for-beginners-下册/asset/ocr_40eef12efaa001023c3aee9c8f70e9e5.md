# # 第8章 参数获取

调用方 (caller) 函数通过栈帧向被调用方 (callee) 函数传递参数。本章介绍被调用方获取参数的具体方式。

指令清单8.1 范例

```
#include <stdio.h>
int f (int a, int b, int c)
{
    return a*b+c;
}
int main()
{
    printf("%d\n", f(1, 2, 3));
    return 0;
}
```

# ## 8.1 x86

# ### 8.1.1 MSVC

使用MSVC 2010编译上述程序，可得到汇编指令如下。

指令清单8.2 MSVC 2010 Express

| TEXT SEGMENT | |
|---|---|
| a$ = 8 | ; size = 4 |
| b$ = 12 | ; size = 4 |
| c$ = 16 | ; size = 4 |
| _f PROC | ebp |
| push ebp |
| mov ebp, esp |
| mov eax, _ DWORD PTR _a$[ebp] |