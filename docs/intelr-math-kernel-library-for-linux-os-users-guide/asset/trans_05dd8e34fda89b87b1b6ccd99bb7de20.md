

# 在 C/C++ 代码中调用返回复值的 BLAS 函数

在处理从 C 调用返回复值的 BLAS 函数时，你必须格外小心。这个问题是因为 BLAS 由 Fortran 函数组成，而它们返回的复值在 C 和 Fortran 中的处理方式完全不同。然而，除了普通的函数调用外，Fortran 还允许像调用子程序（subroutines）一样调用函数，这为从 C 程序调用函数时提供了一种正确返回复值的机制。当 Fortran 函数被用作子程序调用时，返回值是调用序列中的第一个参数。C 程序员可以使用此特性。

下面的示例展示了这是如何运作的。

普通的 Fortran 函数调用：
`result = cdotc( n, x, l, y, 1 )`

作为子程序调用函数：
`call cdotc( result, n, x, l, y, 1, )`

从 C 调用函数（注意参数被暴露了）：
`cdotc(&result, &n, &one, y, &one )`

![](img/78e923baedeba397a89d376927830122_79_0.png)

> 注意。Intel MKL 在 Fortran 风格（不区分大小写）的 BLAS 中同时具有大写和小写入口，带有或不带有结尾下划线。因此，所有这些名称都是等效且接受的：cdotc, cdotc_, cdotc_

上面的示例展示了从 C 和 C++ 应用调用返回复值的级 1 BLAS 函数的方法之一。更简单的方法是使用 CBLAS 接口。例如，你可以使用 CBLAS 接口调用相同的函数：

```c
cblas_cdotu( n, x, l, y, l, &result )
```

![](img/78e923baedeba397a89d376927830122_79_1.png)

> 注意。在这种情况下，复值作为参数列表的最后一个。

以下示例展示了在 C 和 C++ 中使用 Fortran 风格的 BLAS 接口，以及 CBLAS（C 语言）接口。

下面的示例说明了从 C 程序调用复数 BLAS  1 函数 zdotc()。该函数计算两个双精度向量的点积。

在例示例中，复数点积通过结构体 c 返回。

# 示例 7-1 从 C 调用复数 BLAS 1 函数

```cpp
#include "mkl.h"

#define N 5
void main()
{
    MKL_int n = N, inc = 1, incb = 1, i;
    MKL_Complex16 a[N], b[N], c;
    for( i = 0; i < n; i++){
        a[i].re = (double)i; a[i].im = (double)i * 2.0;
        b[i].re = (double)(n - i); b[i].im = (double)i * 2.0;
    }

    zdotc(&c, &n, a, &inca, b, &incb);
    printf("The complex dot product is: %6.2f, %6.2f\n", c.re, c.im);
}
```

```cpp
#include <complex>
#include <iostream>
#define MKL_Complex16 std::complex<double>
#include "mkl.h"

#define N 5

int main()
{
    int n, incr = 1, incb = i;
    std::complex<double> a[N], b[N], c;
    n = N;
    for(i = 0; i < n; i++) {
        a[i] = std::complex<double>(i,i*2.0);
        b[i] = std::complex<double>(n-i,i*2.0);
    }
    zdotc(&c, &n, a, &incr, b, &incb);
    std::cout << "The complex dot product is: " << c << std::endl;
    return 0;
}
```

# 特定语言的用法选项 7

下面的示例使用了 CBLAS：

# 示例 7-3 使用 CBLAS 接口代替直接从 C 调用 BLAS

# 对 Boost uBLAS 矩阵矩阵乘法的支持

如果你熟悉 uBLAS，可以在 C++ 中使用 Intel MKL 替换 Boost uBLAS 函数来执行 uBLAS 矩阵矩阵乘法。uBLAS 属于 Boost C++ 开源库，为密集、压缩和稀疏矩阵提供 BLAS 功能。

# 7 Intel® Math Kernel Library 用户指南

该库使用表达式模板技术将表达式作为函数参数传递，这允许单次通过评估向量和矩阵表达式，而无需临时矩阵。uBLAS 提供了两种模式：

- Debug（安全）模式，默认模式。
  执行类型和一致性检查。

- Release（快速）模式。
  通过 NDEBUG 预处理器符号启用。

Boost uBLAS 的文档可以在 www.boost.org/ 获取。

Intel MKL 提供了重载的 `prod()` 函数，用于用 Intel MKL gem 调用替换 uBLAS 稠密矩阵乘法。尽管这会破坏 uBLAS 稠密矩阵乘法与 Intel MKL gem 调用的结合，但对于较大的矩阵尺寸，其优势可能是巨大的。要使用 Intel MKL，请执行以下操作：

- 在代码中添加相应的头文件。
- 链接库。
- 按照文档描述使用函数。

