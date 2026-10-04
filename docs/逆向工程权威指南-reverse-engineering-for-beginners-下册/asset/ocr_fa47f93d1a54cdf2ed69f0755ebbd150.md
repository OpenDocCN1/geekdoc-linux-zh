# G. 3 中级练习题

# G. 3.1 练习题2.1

这个函数可以根据牛尔顿法计算平方根，其算法源自Harold Abelson, Gerald Jay Sussman, and Julie Sussman:《Structure and Interpretation of Computer Programs》(1996)。

程序源代码如下：

```
// algorithm taken from SICP
#include <math.h>
double average(double a, double b)
{
    return (a + b) / 2.0;
}
double improve(double guess, double x)
{
    return average(guess, x/guess);
}
int good_enough(double guess, double x)
{
    double d = abs(guess*guess - x);
    return (d < 0.001);
}
double square_root(double guess, double x)
{
    while (good_enough(guess, x)==0)
        guess = improve(guess, x);
    return guess;
}
double my_sqrt(double x)
{
    return square_root(1, x);
}
int main()
{
```