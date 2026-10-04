# # 第10章 指针

指针通常用于帮助函数处理返回值（请参阅第7章的例）。当函数需要返回多个值时，它通常都是通过指针传递返回值的。

# ## 10.1 全局变量

```
#include <stdio.h>

void fl (int x, int y, int *sum, int *product)
{
    *sum=x+y;
    *product=x*y;
}

int sum, product;
void main()
{
    fl(123, 456, &sum, &product);
    printf("sum=%d, product=%d\n", sum, product);
}
```

经MSVC 2010（启用优化选项/0b）编译上述程序，可得到如下所示的指令：

```
指令清单10.1 Optimizing MSVC 2010 (/0b)
COMM      _product:DWORD
COMM      sum:DWORD
$SG2803 DB  'sum=%d, product=%d', 0aH, 00H
x$ = 8          ; size = 4
y$ = 12         ; size = 4
sum$ = 16      ; size = 4
_product$ = 20  ; size = 4

_f1      PROC
```