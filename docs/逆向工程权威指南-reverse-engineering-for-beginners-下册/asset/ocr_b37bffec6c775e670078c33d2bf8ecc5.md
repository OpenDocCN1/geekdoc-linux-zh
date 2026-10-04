# 第35章 温度转换

入门级的书籍一般都会介绍“华氏温度转换为摄氏温度”的例。

从华氏度转换成摄氏度的计算公式为

```
$C = \frac{5 \cdot (F - 32)}{9}$
```

笔者对程序添加了简单的错处理：

+   ① 输入的温度必须正确。
② 核查最终结果，确保不会出现绝对零度（-273℃）以下的摄氏温度值。这是中物理学课上介绍的一个常识。

说明：用函数exit()立即退出程序，且不会向调用函数返回任何值。

# 35.1 整数值

```
#include <stdio.h>
#include <stdlib.h>

int main() {
    int celsius, fahr;
    printf("Enter temperature in Fahrenheit:\n\n");
    if (scanf("%d", &fahr)!=1)
```