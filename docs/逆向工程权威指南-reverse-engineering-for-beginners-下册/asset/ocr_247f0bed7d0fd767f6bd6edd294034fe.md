```
call    _putchar
cmp     esi, edi ; meet struct end
jnz     short loc_8048408 ; j=0\lea     esp, [ebp-0Ch]
pop     ebx
pop     esi
pop     edi
pop     ebp
retn
```

# 21.4 结构的字段封装

结构的字段封装方法构成了这种数据类型的一个重要特性。[6]

我们以后下面的例子来加以。

```
#include <stdio.h>
struct s {
    char a;
    int b;
    char c;
    int d;
}
void f(struct s s) {
    printf("a=%d; b=%d; c=%d; d=%d\n", s.a, s.b, s.c, s.d);
}
int main() {
    struct s tmp;
    tmp.a=1;
    tmp.b=2;
    tmp.c=3;
    tmp.d=4;
    f(tmp);
}
```

其中有2个单字节型char字段和2个4字节的int型变量。

# 21.4.1 x86

使用MSVC 2012 (开启选项/GS- /Ob0) 编译，可以得到如下的代码：

指令清单21.16 MSVC 2012/GS-/060

```
1 _tmp$ = -16
2 _main    PROC
```