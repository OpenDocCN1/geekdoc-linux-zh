# 第43章 内联函数

在编译阶段，将会编译器把函数体展开并嵌入到每一个调用的函数，就是内联函数。

> 指令清单43.1 一个简单的例子

```
#include <stdio.h>

int celsius_to_fahrenheit (int celsius)
{
    return celsius * 9 / 5 + 32;
}

int main(int argc, char *argv[])
{
    int celsius= atol(argv[1]);
    printf("%d\n", celsius_to_fahrenheit(celsius));
}
```

此处的汇编层面的具体指令与源代码几乎对应。然而，如果在GC编译环境下，我们采用-3参数优化的话，我们会看到如下所示的代码。

> 指令清单43.2 GCC 4.8.1优化

```
_main:
    push   ebp
    mov    ebp, esp
    and    esp, -16
    sub    esp, 16
    call   main
    mov    eax, DWORD PTR [ebp+12]
```