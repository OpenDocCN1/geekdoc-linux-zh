在采用这种算法时，我们可采用通用类型（union）的数据表示单精度浮点数（float）。这个方法可以利用C/C++的数据结构，按照一种与与读取方式不同的数据类型存储浮点数据的各个组成部分。本例中，我们创建一个union变量，然后把把它当作float或uint32_t型数据进行读取。换句话来说，这就是一种hack，而且比较深的hack。

# 第20章的例子介绍整型PRNG的有关程序。因而本节不再重复其数据格式。

```
#include <stdio.h>
#include <stdint.h>
#include <time.h>

// integer PRNG definitions, data and routines:

//constants from the Numerical Recipes book
const uint32_t RNG_a=1664525;
const uint32_t RNG_c=1013904223;
uint32_t RNG_state; // global variable

void my_srand(uint32_t i)
{
    RNG_state=i;
}
uint32_t my_rand()
{
    RNG_state=RNG*RNG_a+RNG_c;
    return RNG_state;
}

// FPU PRNG definitions and routines:
union uint32_t_float
{
    uint32_t i;
    float f;
}

float float_rand()
{
    union uint32_t_float tmp;
    tmp.i=my_rand() & 0x007ffff | 0x3F800000;
    return tmp.f-1;
```