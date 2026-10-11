
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

## 特定语言的用法选项 7

下面的示例使用了 `CBLAS`：

### 示例 7-3 使用 CBLAS 接口代替直接从 C 调用 BLAS

### 对 Boost uBLAS 矩阵矩阵乘法的支持

如果你熟悉 `uBLAS`，可以在 C++ 中使用 Intel MKL 替换 Boost `uBLAS` 函数来执行 `uBLAS` 矩阵矩阵乘法。`uBLAS` 属于 Boost C++ 开源库，为密集、压缩和稀疏矩阵提供 BLAS 功能。

# 7 Intel® Math Kernel Library 用户指南

该库使用表达式模板技术将表达式作为函数参数传递，这允许单次通过评估向量和矩阵表达式，而无需临时矩阵。`uBLAS` 提供了两种模式：

- `Debug`（安全）模式，默认模式。

  执行类型和一致性检查。

- `Release`（快速）模式。

  通过 `NDEBUG` 预处理器符号启用。

Boost `uBLAS` 的文档可以在 `www.boost.org/` 获取。

Intel MKL 提供了重载的 `prod()` 函数，用于用 Intel MKL `gem` 调用替换 `uBLAS` 稠密矩阵乘法。尽管这会破坏 `uBLAS` 稠密矩阵乘法与 Intel MKL `gem` 调用的结合，但对于较大的矩阵尺寸，其优势可能是巨大的。要使用 Intel MKL，请执行以下操作：

- 在代码中添加相应的头文件。

- 链接库。

- 按照文档描述使用函数。

# 特定语言的用法

在构建和运行示例时，将从 Java 源码生成特定包装器和示例类的文档。要浏览文档，请打开 `docs` 目录下的索引文件（由构建脚本创建）：

```
<mkl directory>/examples/java/docs/index.html
```

针对 `CBLAS`、`VML`、`VSL RNG` 和 `FFT` 的 Java 包装器建立了与底层原生函数对应的接口，因此您可以参考 Intel MKL 参考手册来了解它们的功能和参数。类似于 `ESSL` 的函数的接口在在生成的 `com.intel.mkl.ESSL` 类的文档中描述。

每个包装器都包含 Java 接口部分和 C 语言中的 JNI 存根（stub）。您可以在以下目录中找到源码：

```
<mkl directory>/examples/java/wrappers
```

`CBLAS` 和 `VML` 包装器的 Java 和 C 部分都演示了直观的方法，您可以使用该方法来涵盖额外的 `CBLAS` 函数。

`FFT` 包装器更为复杂，因为它需要支持 FFT 描述对象的生命周期。为了计算单个傅里叶变换，应用程序需要使用相同的 FFT 描述符副本多次调用 FFT 软件。包装器提供了处理类来持有原生描述符，而虚拟机则运行字节码。

`VSL RNG` 包装器与 `FFT` 的类似。包装器提供了处理类来持有流状态的原生描述符。

卷积和相关性函数的包装器缓解了 `VSL` 接口的相同困难，该接口假设“任务描述符”具有类似的生命周期。包装器对这些函数使用了类似于 `ESSL` 的接口，这对于 i 维数据的情况更为简单。JNI 存根理想情况下将 MKL 函数封装在 C 语言中类似于 `ESSL` 的包装器中，并将描述符的生命周期“打包”到单个原生方法的调用中。

该包装器符合 JNI 规范 1.1 和 5.0 版本，并适用于几乎所有现代 Java 实现。

示例和包装器的 Java 部分在《Java 语言规范（第一版）》中有所描述，并结合“内部类”功能进行了扩展（这指的是 20 世纪 90 年代后期）。此级别的语言版本受所有版本的 Sun Java 开发工具包 (`JDK*`) 开发工具包以及从 1.1.5 版本开始的兼容实现（或所有现代版本的 Java）的支持。

C 语言的级别为“标准 C”（即 `C89`），并对 Intel MKL 接口和 JNI 头文件所需的整数和浮点数据类型有额外假设。也就是说，原生 `float` 和 `double` 数据类型必须分别与 JNI `float` 和 `double` 数据类型相同，且原生 `int` 必须是 4 字节长度。

# 7 Intel® Math Kernel Library 用户指南

## 运行示例

Java 示例支持 Intel MKL 支持的所有 C 和 C++ 编译器。用于运行示例的 `makefile` 还需要 `make` 实用程序，该程序通常由 Linux* 操作系统发行版提供。

运行 Java 示例需要 `JDK*` 开发工具包来编译和运行 Java 代码。计算机上必须安装 Java 实现，或者通过网络可用。您可以从供应商网站下载 JDK。

示例应适用于所有版本的 JDK。然而，它们仅在以下 Java 实现上进行了测试：

- 来自 Sun Microsystems, Inc. (`http://sun.com`) 的 `J2SE* SDK 1.4.2`, `JDK 5.0` 和 `6.0`

- 来自 BEA Systems, Inc. (`http://bea.com`) 的 `JRockit* JDK 1.4.2` 和 `5.0`

![](img/78e923baedeba397a89d376927830122_87_0.png)

> 注意。Sun Microsystems Corporation 的实现仅支持使用 IA-32 和 Intel® 64 架构的处理器。来自 BEA Systems 的 `JRockit* JDK` 也支持 Intel® Itanium® 2 处理器。

请注意，计算机上预装的 Java 运行时环境 (`JRE*`) 系统是不的。您需要支持以下工具set的 `JDK*` 开发工具包：

- `java`

- `javac`

- `javah`

- `javadoc`

为了让示例 `makefile` 使用这些工具，请设置 `JAVA_HOME` 环境变量并将 JDK 二进制目录添加到系统 PATH 中，例如，使用 `bash` shell：

```
export JAVA_HOME=/home/<user name>/jdk1.5_09
```

```
export PATH=$JAVA_HOME/bin:${PATH}
```

如果分配了 `JDK_HOME` 环境变量，您可能还需要清除它：

```
unset JDK_HOME
```

要启动示例，请使用 Intel MKL Java 示例目录下的 `makefile`：

```
make [so32|soem64|so64|lib32|libem64] [function...] [compiler=...]
```

如果您输入 `make` 命令而省略目标 (`so32`)，`makefile` 将打印帮助信息，解释目标和参数。

要查看示例列表，请查看 Java 示例目录下的 `examples.lst` 文件。

## 已知局限性

局限性分为：

- 功能

- 性能

- 已知 bug

**功能。** 如果通过包装器（如 Intel MKL Java 示例提供的包装器）从 Java 环境调用，某些 MKL 函数可能无法工作。只有在 Intel MKL Java 示例章节列出的特定 `CBLAS`、`FFT`、`VML`、`VSL RNG` 以及卷积/相关性函数在 Java 环境下经过测试。因此，您可以使用 Java 包装器处理这些 `CBLAS`、`FFT`、`VML`、`VSL RNG` 和卷积/相关性函数。
