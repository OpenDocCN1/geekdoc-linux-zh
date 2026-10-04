在GCC生成的相应代码中，RTTI表的构造稍微有些不同。

# 51.2 ostream输出流

我们来看一个经典的例子“hello world!”，这里我们试图采用输出流的方式重新实现它。

```
#include <iostream>

int main()
{
    std::cout << "Hello, world!\n";
}
```

几乎所有的教科书都写明，运算符“<<”的作用是“重载”其他类型的数据，主要用于对象之间的运算。我们来看看符“<<”的输出流用法。

> 指令清单51.18 精简版的MSVC 2012的程序代码

```
$SG37112 DB Hello, world!, 0aH, 00H

_main PROC
    push OFFSET $SG37112
    push OFFSET ?cout@$std@$3V?$basic_ostream@DU?
    $char_traits@D$std@@@1@A, std::cout
    call ??$76U?$char_traits@D$std@@@0@YAAAV?$basic_ostream@DU? \
        \ $char_traits@D$std@@@0@0@AAV10@PBDZ
    std::operator<<std::char_traits<char> >
    add     esp, 8
    xor     eax, eax
    ret     0
_main END
```

我们把源程序稍微修改一下：

```
#include <iostream>

int main()
{
    std::cout << "Hello, " << "world!\n";
}
```

教科书这种运算符会从左到右依次进行。实际上确实如此:

> 指令清单51.19 MSVC 2012下的程序实现