当输入值为1时，目标偏移量的方法是:9乘以4、加上Lrtx4的偏移量。当输入值为22时，目标偏移量为:0乘以4、结果为0。在转移表Lrtx4之后就是L7的标签的指令了，这部分将负责打印字符22。请注意，转移表位于单独的.rodata段。编译器没有把它配到.text代码段里。

上述转移表有一个偏移0xF7。这个偏移量指向了打印默认字符串（L2标签）的相关指令。

# 13.4 Fall—through

Switch()语言还有一种常见的使用方法—fall through.

```
1 #define R 1
2 #define W 2
3 #define RW 3
4
5 void f(int type)
6 {
7     int read=0, write=0;
8     switch (type)
9     {
10
11        case RW:
12            read=1;
13
14        case W:
15            write=1;
16            break;
17
18        case R:
19            read=1;
20            break;
21
22        default:
23            break;
24    };
25    printf("read=%d,write=%d\n", read, write);
26 }
```

如果type为1（参见第一行可知，是读取权限R为真的情况），则read的值会被设置为1;如果type为2(W)，则write被设置为1;如果type为3(RW)，则read和write的值都被设置为1。

无论type的值是RW还是W，程序都会执行第14行的指令。type为RW的描述语句里没有break指令，从而利用switch语句的fall through的效应。

# 13.4.1 MSVC x86 指令列表13.13 MSVC 2012