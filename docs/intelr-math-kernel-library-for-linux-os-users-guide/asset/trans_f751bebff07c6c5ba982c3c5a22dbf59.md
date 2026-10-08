

# 在链接行上列出库

要链接 Intel MKL 库，请如下所示在链接行上指定路径和库。

![](img/78e923baedeba397a89d376927830122_43_0.png)

> **注意。** 该语法用于动态链接。对于静态链接，请将每个带有 "-l" 前缀的库名替换为库文件的路径，例如，将 -imkl_core 替换为 $MKLPATH/libmkl_core.a，其中 $MKLPATH 是适当的用户定义环境变量。请参阅“链接示例”（Linking Examples）章节中的特定示例。

```
files to link
-LMKL path -IMKL include
[-IMKL include/][32|em64c|[il64|ip64]|64/{il64|ip64}]
-lmkl_blas[95|95_ip64|95_ip64]
-lmkl_lapack[95|95_ip64|95_ip64]
<cluster components>
-lmkl_intel_ilp64|intel_ip64|intel_sp2dp[gf|gf_il64|gf_ip64]
-lmkl_{intel_thread|gnu_thread|pgi_thread|sequential]
-lmkl_solver,[ilp64|ip64]
-lmkl_lapack -lmkl_core
-lmomp5-lguide [-lpthread]-[-lm]
```

请参考“选择要链接的库”（Selecting Libraries to Link）以了解此语法用法的详情，以及根据您的 Intel MKL 使用场景建议链接哪些库。
请参阅“带有标记为 <cluster components> 的链接库使用 Intel 数学内核库集群软件”（Working with the Intel Math Kernel Library Cluster Software）。

在静态链接的情况下，请将集群组件、接口、线程和计算库包含在分组符号中（例如，-W1,--start-group $MKLPATH/libmkl_cdft.a $MKLPATH/libmkl_blacs_intpi_ilp64.a $MKLPATH/libmkl_intel_ilp64.a $MKLPATH/libmkl_intel_thread.a $MKLPATH/libmkl_core.a -W1,--end-group）。请参阅“链接示例”章节中的特定示例。

在链接行上列出库的顺序至关重要，对于上述分组符号中的库。

# 选择要链接的库

本节根据您的 Intel MKL 使用场景建议链接哪些库，并在子节中提供了链接的细节：

- 为 Fortran 95 接口库进行链接
- 与线程库链接
- 与计算库链接
- 与编译器 RTL 链接
- 与系统库链接
- 链接示例

# 为 Fortran 95 接口库进行链接

libmkl_blas_95.a、libmkl_blas_95_ilp64.a、libmkl_blas_95_ilp64.a、libmkl_lapack_95.a 和 libmkl_lapack_95_ilp64.a 库分别包含 BLAS 和 LAPACK 的 Fortran 95 接口，这些接口取决于编译器。在 Intel MKL 包中，它们已为 Intel 编译器预先构建。如果您使用不同的编译器，请在使用接口之前构建这些库。（请参阅“LAPACK 和 BLAS 的 Fortran 95 接口”以及“取决于编译器的函数和 Fortran 90 模块”以了解构建库的详情以及在此情况下源码依赖编译的原因。）

# 与线程库链接

Intel MKL 支持的几种编译器支持 OpenMP* 线程技术。从 10.0 版本开始，Intel MKL 支持编译器提供的 OpenMP* 实现。如果应用程序使用 OpenMP* 且使用此类编译器编译，并调用 Intel MKL 10.0 或更低版本（该版本使用 Intel 编译器进行线程处理），可能会出现性能问题甚至失败，因为来自不同编译器的线程库是不兼容的。从 Intel MKL 10.0 开始，线程层（Threading Layer）和编译器运行时库（RTL）提供了这些问题的解决方案。

线程层。由于库的内部结构，线程代表少量的代码。这些代码由不同的编译器（Linux*上的 Intel、Gnu 和 PGI* 编译器）编译，您应该链接相应的线程层。

RTL。此层包含 Intel 编译器的运行时库：Intel 兼容 OpenMP* 运行时库 libomp 和 Intel® 遗留 OpenMP* 运行时库 libguide。兼容库 libiomp 是 libguide 的扩展，为 Linux 上的另一个线程编译器（GNU）提供支持。这意味着使用 GNU 编译器进行线程的程序可以安全地与 Intel MKL 和 libiomp 链接，并高效地运行。因此，我们鼓励您使用 libiomp 而不是 libguide，并在使用 Intel MKL 时针对每种场景选择线程库和 RTL（仅限静态情况）：

表 5-2 显示了根据所用线程编译器的不同场景

# 表 5-2 选择线程库

| 编译器 | 是否线程化 | 线程层 | 推荐的 RTL | 注释 |
|---|---|---|---|---|
| Intel | 不重要 | libmkml_intel_thread.a | libomp5.so | |
| PGI | 是 | libmkml_pgi_thread.a 或 libmkml_sequential.a | PGI* 提供的 | 使用 libmkl_sequential_a 会移除 Intel MKL 调用中的线程。 |
| PGI | 否 | libmkml_intel_thread.a | libomp5.so | |
| PGI | 否 | libmkml_pgi_thread.a | PGI* 提供的 | |
| PGI | 否 | libmkml_sequential.a | 无 | |
| gnu | 是 | libmkml_gnu_thread.a | libomp5.so 或 GNU OpenMP 运行时库 | libomp5 提供了更优的扩展性能。 |
| gnu | 是 | libmkml_sequential.a | 无 | |
| gnu | 否 | libmkml_intel_thread.a | libomp5.so | |
| other | 是 | libmkml_sequential.a | 无 | |
| other | 否 | libmkml_intel_thread.a | libomp5.so | |

# 与计算库链接

通常，在分层链接模型下，您必须仅将应用程序链接到一个计算库。然而，某些 Intel MKL 函数领域需要多个计算库。

对于每个 Intel MKL 函数领域，表 5-3 列出了您必须包含的计算库。有关关于与 ScAPACK 和 Cluster FFTs 链接的更多信息，请参阅。

# 表 5-3 按函数链接的计算库

| 函数 | IA-32 架构 | Intel® 64 或 IA-64 架构 |
|---|---|---|
| | 静态 | 动态 |
| | 静态 | 动态 |
| BLAS, CBLAS, LAPACK, VSL, FFT, 三角函数 | libmk_core.a | libmk_lapack.so libmk_core.so | libmk_core.a | libmk_lapack.so libmk_core.so |
| 迭代疏求解器、区域求解器和 GMP 常规 | libmk_solver.a | libmk_sequential.a | libmk_solver.a | libmk_sequential.a |
| 迭代疏求解器、区域求解器和 GMP 常规 | libmk_core.a | n/a | libmk_solver_lp64.a | libmk_sequential_lp64.a |
| LP64 接口 | n/a | n/a | libmk_solver_ilp64.a | libmk_sequential_ilp64.a |
| 直接疏求解器/PARDISO 求解器 | libmk_core.a | libmk_lapack.so libmk_core.so | libmk_core.a | libmk_lapack.so libmk_core.so |

# 表 5-3 按函数链接的计算库（续）

| 函数 | IA-32 架构 | Intel® 64 或 IA-64 架构 |
|---|---|---|
| ScalAPACK¹ | libmk_scalapack_core.a | libmk_lapack.so libmk_core.so | libmk_scalapack_lp64.a | libmk_sequential_lp64.a |
| | 见下文 | 见下文 | | |
| ScAPACK, IL64 接口¹ | n/a | n/a | libmk_scalapack_ilp64.a | libmk_sequential_ilp64.a |
| 集群傅里叶变换函数¹ | libmk_cdft_core.a | n/a | libmk_cdft_core.a | n/a |

+1. 还需要添加使用所用 MPI API 的带有 BLACS 例程的库。详情请参阅“与 ScAPACK 和 Cluster FFTs 链接”。

另参阅：

与编译器 RTL 链接。

# 与编译器 RTL

强烈建议动态链接 Intel 兼容 OpenMP* 运行时库 libomp 或 Intel 遗留 OpenMP* 运行时库 libguide。不建议链接静态 OpenMP* 运行时库，因为在复杂的软件中很容易链接多个库的副本（导致线程过多），并且如果初始化了其中一个副本，可能会导致正确性问题。

