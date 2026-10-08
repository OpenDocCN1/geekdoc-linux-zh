

# 表 3-1 高级目录结构（续）

| 目录 | 注释 |
|---|---|
| <mkl directory>/tools/plugins/com.intel.mkl.help | 包含带有 WebHelp 格式的 Intel MKL 参考手册的 Eclipse 插件。注释请参见 mkl_documentation.com。 |
| <Intel Compiler directory>/documentation/en_US/mkl | 包含在 Intel® C++ Professional Edition 或 Intel® Fortran Compiler Professional Edition 中的 Intel MKL 文档。 |
| <Intel Compiler directory>/man/en_US/man3 | 包含 Intel C++ Compiler Professional Edition 或 Intel Fortran Professional Edition 中 MKL 函数的页。 |

## 分级模型概念

从 10.0 版本开始，Intel MKL 采用了分级模型。
该库包含四个核心部分：

- 1. 接口层
- 2. 线程层
- 3. 计算层
- 4. 编译器支持运行时库。

第一部分使 Intel MKL 适配于接口相关的问题，例如是否使用 32 位或 64 位整数类型，或者不同的编译器如何返回函数值。第二部分将库适配到使用不同编译器的 OpenMP 实现，或适配到非线程用法。计算层是库的主体，在空间上进行了分离。为了避免这些部分中的每种情况生成一个库（从而导致可能性的几何级爆炸），Intel MKL 将每个部分拆分为对应于情况的独立库。你可以组合这些库来满足你的需求。一旦选择了接口库，线程库将接管该接口，而计算库将使用在前两层中选定的接口。

**接口层。** 该层提供了应用程序的编译代码与库的线程和/或计算部分之间的匹配。该层提供了：

- * LP64 和 ILP64 接口（详情请参见“支持 ILP64 编程”）
- 与不同方式返回函数值的编译器的兼容性
- 对于使用 Cray* 风格命名的应用程序，单精度名称与双精度名称之间的映射（SP2DP 接口）

# Intel® Math Kernel Library 用户指南

注意。SP2DP 接口支持针对 Intel 64 或 IA-64 架构并使用 ILP64 接口的应用程序中的 Cray 风格命名。SP2DP 接口在应用程序中的单精度名称（适用于实数和复合类型）与 Intel MKL BLAS 和 LAPACK 中的双精度名称之间提供了映射。函数名的映射如下例 BLAS 函数 * GEMM 所示：
SGEMM -> DGEMM
DGMM -> DGEMM
CGEMM -> ZGEMM
GEMM -> ZGEMM
请注意，双精度名称没有进行任何更改。

线程层。该层提供了：

- * 一种将线程 Intel MKL 与不同的线程编译器链接的方法。
- 用户与库的线程模式或顺序模式进行链接的能力。

该层针对不同的环境（线程的或顺序的）和编译器（来自 Intel、GNU* 等）进行了编译。

计算层。该层是 Intel MKL 的核心。对于任何处理器架构（IA-32、IA-64 或 Intel® 64）和 操作系统，无论接口层和线程层如何，都只有一个计算层可供链接。计算层通过识别架构特征来适应多种架构，并在运行时选择合适的二进制文件。

编译器运行时库（简称为 RTL）。该层提供 RTL 支持。并非所有的 RTL 都是为 Intel MKL 开发的。除了与 Intel MKL 集群软件相关的之外，提供的唯一 RTL 只有 Intel® RTL：Intel® 兼容 OpenMP* 运行时库 (libomp) 和 Legacy OpenMP* 运行时库 (libguide)。要使用第三方编译器，请使用线程层中的库或适当的兼容库（更多信息，请参见“与线程库链接”）。

## 库的顺序模块

你可以以顺序模式（非线程）使用 Intel MKL。该模式不需要兼容 OpenMP* 或 Legacy OpenMP* 运行时库，并且响应 OMP_NUM_THREADS 或其 Intel MKL 等效变量。在此模式下，Intel MKL 运行非线程代码。然而，线程安全意味着你可以在 OpenMP* 代码的并行区域中使用它。当使用非 Intel 编译器运行 Intel MKL 或在其他情况下（例如 MPI 案例）时，你应该使用顺序库。为了获得在顺序模式下运行的 Intel MKL，请选择 *sequential.* 库。注意*sequential.* 库依赖于 POSIX 线程 (pthread)，用于使 Intel MKL 软件线程安全并列在列表中。

另见：

- 目录结构
- 使用 Intel® MKL 并行
- 避免执行环境中的冲突
- 链接示例

## 对 ILP4 的支持

Intel MKL ILP4 库使用 64 位整数类型（用于索引超过 $2^{31}-1$ 个元素的巨大数组），而 LP64 使用 32 位整数类型。

LP64 和 ILP4 接口在接口层受支持（更多信息请参见“分级模型”和“目录结构”）。提供 ILP4 接口出于以下两个原因：

- 支持巨大的数组（超过 $2^{31}-1$ 个元素）
- 允许使用 -i8 编译器编译 Fortran 代码

使用哪种接口取决于你。为了与低于 9 的 Intel MKL 版本兼容，请选择 LP64 接口。如果你的应用程序使用 Intel MKL 处理巨大数组或未来可能使用该库，请选择 ILP4 接口。Intel MKL 为 ILP4 和 LP64 接口提供了相同的包含目录。

1. 弃用的例程 ?lacon、?lasq3 和 ?lasq4 之外。

# 3 Intel® Math Kernel 用户指南

## 为 LP64/ILP64 编译

表 3-2 显示了如何为 ILP64 和 LP64 接口编译：

## 表 3-2 为 ILP64 和 LP64 接口编译

### Fortran

```
为 LP64 编译
ifort -i8 -I<mkl directory>/include
```

```
为 LP64 编译
ifort -I<mkl directory>/include
```

### C 或 C++

```
为 LP64 编译
icc -DMKL_IL64 -I<mkl directory>/include
```

```
为 LP64 编译
icc -I<mkl directory>/include
```

> 注意。将 i8 或 -DMKL_IL64 编译的应用程序链接到 LP64 可能导致不可预测的后果和错误输出。

## ILP64 代码

如果不使用 IL64，则不需要更改现有代码。迁移到 LP64，请为 MKL 函数和子程序使用适当类型：

## 表 3-3 整数类型

| 32 位整数 | Fortran | C 或 C++ |
|---|---|---|
| | INTEGER*4 or INTEGER(KIND=4) | int |
| LP64/ILP64 通用整数 | INTEGER without specifying KIND | MKL_INT |
| - LP64 为 64 位 | | |
| - 其他为 32 位 | | |
| LP64/LP64 通用整数 | INTEGER*8 or INTEGER(KIND=8) | MKL_INT64 |
| - 64 位整数 | | |
| LP64 的 FFT 接口 | INTEGER without specifying KIND | MKL_LONG |

# Intel® Math Kernel Library 

## 浏览 MKL 包含文件

对于带有整数参数的函数，参考手册没有解释为什么 IL64 变为 64 位而保持 32 位，建议你浏览 IL64 接口的包含文件、示例和测试。它们的位置见表 3-1。

建议从浏览表 A-2 列出的包含文件开始。某些仅支持 Fortran 接口的函数（参见表 A-1）在包含目录中为 C/C++ 提供头文件。此类 *.h 文件允许从 C/ 代码中使用 Fortran 二进制接口。这些文件也可用于理解 IL64 的用法。

## 限制

所有 Intel MKL 函数域均支持 ILP64 编程，以下是例外：

- FFTW 2.x 包装不支持 ILP64。
- FFTW 3.2 包装通过专用函数集 plan_guru64 支持 ILP64。
- GMP* 术函数不支持 ILP64。

# 架构支持

针对 Linux* 系统的 Intel MKL 提供三种特定架构的实现。表 3-4 列出了支持的架构以及每个特定架构实现的位置。

表 3–4 针对架构的实现

| 架构 | 位置 |
|---|---|
| IA-32 或兼容 | <mkl directory>/lib/32 |
| Intel® 64 或兼容 | <mkl directory>/lib/64t |
| IA-64 | <mkl directory>/lib/64 |

有关这些目录的详细结构请参见表 3-5、表 3-6 和表 3-7。

