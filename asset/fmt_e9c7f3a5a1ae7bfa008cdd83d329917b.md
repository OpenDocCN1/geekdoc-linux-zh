
`Beep(0FFFF)`; // 一个简单的 beep。如果没有设备，将使用 `speaker` 生成。

## 题目2

对应章节：`3.7` 节

```c
#include <unistd.h>

int main()
{
    sleep(2);
}
```

## 第5章

### 题目1

对应章节：`5.5` 节
如果启用 `MSVC` 的优化功能，程序显示的数字分别是 `EBP` 的值、`RA` 和 `argc`。在命令行中执行 `main()` 函数分配 8 字节空间，所以会有。

### 题目2

对应章节：`5.5` 节
这些都是 UNIX 时间程序，源代码如下：

```c
#include <stdio.h>
#include <time.h>
int main(int argc, char* argv[])
{
    time_t vTime = time((time_t*)0);
    printf("%d\n", vTime);
}
```

## 第7章

### 题目1

对应章节：`7.4` 节
Linux 下将所有字符串放置到 `.rodata` 段，它是只读的（“只读数据”）：

```
$ objdump -s 1
```

```
Contents of section .rodata:
400600 0100200 526573756c74 2573a00 Result: %s..
400610 4865c6c 6fc,207f2c64 210a00 Hello, world!..
```

## 第13章

### 题目1

对应章节：`13.5` 节
提示：`printf()` 只会被调用一次。

## 第14章

### 题目3

对应章节：`14.4` 节

```c
#include <stdio.h>
int main()
{
    for(int i = 100; i > 0; --i)
    printf("%d\n", i);
}
```

### 题目4

对应章节：`14.4` 节

```c
#include <stdio.h>
int main() {
    int i;
    for(i=1; i<100; i++)
    printf("%d\n", i);
}
```

## 第15章

### 题目1

对应章节：`15.2` 节
这是一个统计字符串中空格的程序，源代码如下：

```c
int f(const char* aStr)
{
    const char* veos = aStr;
    int vCount = 0;
    for(;veos;veos)
    {
        if (*veos == ' ') ++vCount;
    }
    return vCount;
}
```

## 第16章

### 题目1

对应章节：`16.3` 节

```c
int f(int a)
{
    return a;
}
```

## 第17章

### 题目2

对应章节：`17.10` 节
计算 5 个双精度浮数的平均值，源代码如下：

```c
double f(double a1, double a2, double a3, double a4, double a5)
{
    return a1*a2*a3*a4*a5 / 5.0;
}
```

## 第18章

### 题目1

对应章节：`18.9` 节
两个 `100x200` 矩阵的双精度加法运算，源代码如下：

```c
#define M 100
#define N 200
void s(double *a, double *b, double *c)
{
    for (int i=0; i<N;i++)
        for (int j=0; j<M;j++)
            *(c+i*M+j)=(a+i*M+j) + *(b+i*M+j);
}
```

### 题目2

对应章节：`18.9` 节
两个矩阵（一个是 `100x200`，另一个是 `100x300`）的乘法运算，生成一个 `100x300` 的矩阵。源代码如下：

```c
#define M 100
#define N 200
#define P 300
void m(double *a, double *b, double *c)
{
    for (int i=0; i<M;i++)
        for (int j=0; j<P;j++)
        {
            *(c+i*M+j)=0;
            for (int k=0; k<N;k++) *(c+i*M+j)+=(a+i*M+j) * *(b+i*M+j);
        }
}
```

### 题目3

对应章节：`18.9.3` 节

```c
double f(double array[50][120], int x, int y)
{
    return array[x][y];
}
```

### 题目4

对应章节：`18.9.4` 节

```c
double f(double array[50][120], int x, int y)
{
    return array[x][y];
}
```

## 对应章节: `21.7.1`节

这个程序将显示文件所有者的 `uid` ID。其源代码如下所示

```c
#include <sys/types.h>
#include <sys/stat.h>
#include <time.h>
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[])
{
    struct stat sb;
    if (argc == 2)
    {
        fprintf(stderr, "Usage: %s pathname\n", argv[0]);
        return 0;
    }
    if (stat(argv[1], &sb) == -1)
    {
        // error
        return 0;
    }
    printf("%ld\n", (long) sb.st_uid);
}
```

### 题目2

对应章节: `21.7.2`节

提示: 研究的侧重点应当放在 `Jcc`、`MOVSx` 和 `MOVZX` 指令。

```c
#include <stdio.h>
struct some_struct
{
    int a;
    unsigned int b;
    float f;
    double d;
    char c;
    unsigned char uc;
};
```

```c
void f(struct some_struct *s)
{
    if (s->a > 1000)
    {
        if (s->b > 10)
        {
            printf("%f\n", s->f * 444 + s->d * 123);
            printf("%c, %d\n", s->uc);
        }
        else
        {
            printf("error #2\n");
        }
    }
    else
    {
        printf("error #1\n");
    }
}
```

## 第41章

### 题目1

对应章节：`41.6`节

```c
int f(int a)
{
    return a/661;
}
```

## 第50章

### 题目1

对应章节：`50.5.1`节

源代码：

```c
#include <stdio.h>
int is_prime(int number)
{
    int i;
    for (i=2; i<number; i++)
    {
        if (number % i == 0 && i != number)
            return 0;
    }
    return 1;
}
int main()
{
    printf("%d\n", is_prime(137));
}
```

## G. 2 初级练习题

### G.2.1 练习题 1.1

这是一个返回2个个数中最大值的函数。

### G.2.2 练习题 1.4

程序源代码如下:

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char buf[128];
    printf("enter password\n");
    if (scanf("%s", buf)!=1)
        printf("no password supplied\n");
    if (strcmp(buf, "metallica")==0)
```
