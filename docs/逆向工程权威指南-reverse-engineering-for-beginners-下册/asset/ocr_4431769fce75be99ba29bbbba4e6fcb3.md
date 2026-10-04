# 第39章 循环：几个迭代

多数循环语句只有有一个迭代器。但是在汇编层面，一个迭代器可能对应多个数据实体。

下面所示的是一个简单的例子。

```
#include <stdio.h>

void f(int *al, int *a2, size_t cnt)
{
    size_t i;

    // copy from one array to another in some weird scheme
    for (i=0; i<cnt; i++)
        al[i*3]=a2[i*7];
}
```

我们可以看到，每次迭代都有两次乘法运算，是很耗费时间的操作。不能优化一下呢？答案是肯定的。如果仔细看程序代码，就会发现这个程序的矩阵的参数是跳跃的，我们可以比较容易地不用乘法就把它计算出来。

# 39.1 三个迭代器

指令序列39.1 采用MSVC 2013 x64优化的代码

```
f               PROC
    ; RDX=al
    ; RCX=a2
    ; R8=cnt

    test    r8, r8      ; cnt==0? exit then
```