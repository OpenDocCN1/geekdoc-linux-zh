

# 11 Intel® Math Kernel Library 用户指南

例如，通过性能值来估算问题规模从 700,000 到 701,000 之间的差异。影响性能下降的另一个因素是网格维度（P 和 Q）。对于大型问题，当 P 和 Q 的取值大致相等时，性能在前几个步骤的下降幅度往往较小。你可以利用大量的参数（如广播类型）并更改它们，使得最终性能非常紧密地取决于前几个步骤。

使用这些工具将极大地帮助你增加测试的数据量。

## Intel® Math Kernel Library 语言接口支持

表 A-1 显示了 Intel® Math Kernel Library (Intel® MKL) 为每个领域提供的语言接口，表 A-2 列出了相应的头文件。可以使用混合语言编程从其他语言中调用 Intel MKL 例程。例如，请参阅《使用 Intel® MKL 进行混合语言编程》，了解如何从 C/C++ 调用 Fortran 例程。

## 表 A-1 语言接口支持

| 功能领域 | FORTRAN 77 接口 | Fortran 90/95 接口 | C/C++ 接口 |
| --- | --- | --- | --- |
| 线性代数子程序 (BLAS) | 是 | | |
| 类 BLAS 扩展转置例程 | | 是 | 是 |
| 稀疏 BLAS Level 1 | 是 | 是 | 通过 CBLAS |
| 稀疏 BLAS Level 2 和 3 | 是 | 是 | 是 |
| 用于求解线性方程组的 LAPACK 例程 | 是 | | |
| 用于求解最小二乘问题、特征值和奇异值问题以及 Sylvester 方程的 LAPACK 例程 | | 是 | † |
| 辅助和工具 LAPACK 例程 | 是 | | † |
| 并行线性代数子程序 (PBLAS) | 是 | | |
| ScLAPACK 例程 | 是 | | † |
| DSS/DPARISO* 求解器 | 是 | 是 | 是 |
| 其他直接和迭代求解器例程 | 是 | 是 | 是 |
| 向量数学库 (VML) 函数 | 是 | 是 | 是 |
| 向量统计库 (VSL) 函数 | 是 | 是 | 是 |
| 傅叶变换函数 (FFT) | | 是 | 是 |
| 聚类 FFT 函数 | | 是 | 是 |

## A Intel Math Kernel Library 用户指南

表 A-1 语言接口支持（续）

| 功能领域 | FORTRAN 77 接口 | Fortran 90/95 接口 | C/C++ 接口 |
| --- |---|---|--|
| 三角函数变换例程 | | 是 | 是 |
| 快速泊松、拉普拉斯和亥姆霍兹求解器（Poisson 库）例程 | | 是 | 是 |
| 优化（信赖区域）求解器例程 | 是 | 是 | 是 |
| GMP* 算术函数 | | | 是 |
| 服务例程（包括内存分配） | | | 是 |

† 使用混合语言编程调用。相应的头文件请见表 A-2。

表 A-2 列出了所有 Intel MKL 功能领域的可用头文件。

## 表 A-2 头文件

| 功能领域 | Fortran | C 或 C++ |
| --- | --- | --|
| 所有功能领域 | mkl.fi | mkl.h |
| BLAS 例程 | blas.f90 | mkl_blas.h |
| | mkl_blas.fi | |
| 类 BLAS 扩展转置例程 | mkl_trans.fi | mkl_trans.h |
| BLAS 的 CBLAS 接口 | mkl_cblas.fi | mkl_cblas.h |
| 稀疏 BLAS 例程 | mkl_spblas.fi | mkl_spblas.h |
| LAPACK 例程 | lapack.f90 | mkl_lapack.h |
| | mkl_lapack.fi | |
| ScalAPACK 例程 | | mkl_scalapack.h |
| 所有稀疏求解器例程 | mkl_solver.f90 | mkl_solver.h |
| | mkl_pardiso.f77 | mkl_pardiso.h |
| | mkl_pardiso.f90 | |
| DSS 接口 | mkl_dss.fi | mkl_dss.h |
| | mkl_dss.f90 | |
| RCI 迭代求解器 | mkl_rci.fi | mkl_rci.h |
| ILU 分解 | | | |
| 优化求解器例程 | mkl_rci.fi | mkl_rci.h |
| 向量数学函数 | mkl_vml.f77 | mkl_vml.h |
| | mkl_vml.fi | |

## Intel® Math Kernel Library 语言接口支持 A

表 A-2 头文件（续）

| 功能领域 | Fortran | C 或 C++ |
| --- | --- | --- |
| 向量统计函数 | mkl_vml.f77 mkl_vsl.f9 | mkl_vsl.h |
| 傅里叶变换函数 | mkl_dfti.f90 | mkl_dfti.h |
| 聚类傅里叶变换函数 | mkl_cdft.f90 | mkl_cdft.h |
| 偏微分方程支持例程 | | |
| - 三角函数变换 | mkl_trig_transforms.f90 | mkl_trig_transforms.h |
| - 泊松求解器 | mkl_poisson.f90 | mkl_poisson.h |
| - GMP 接口 | | mkl_gmp.h |
| - 服务例程 | | mkl_service.h |
| - 内存分配 | | mkl_malloc.h |
| - MKL 示例 | | mkl_example.h |

## 第三方接口支持

本附录简述了 Intel® Math Kernel Library (Intel® MKL) 支持的某些接口。

## GMP* 函数

Intel MKL 对 GMP* 算术函数的实现包含了对整数的任意精度操作。此类函数的接口与多精度 (GMP) 算术库完全匹配。有关这些函数的规格规范，请参阅 http://www.intel.com/software/mkl/help/。如果您目前使用 GMP* 库，则需要修改程序中的语句为 `mkl_gmp.h`。

## FFTW 接口

Intel MKL 提供了两组封装器，即 FFTW 接口 (www.fftw.org)，用于调用 Intel MKL 变换函数。这些封装器对应 FFTW 2.x 和 3.x 版本，以及 Intel MKL 7.0 及更高版本。这些封装器使得目前使用 FFTW 的开发者能够在不更改程序的情况下通过 Intel MKL 获取性能。

## 索引

A
- 高级向量指令分发，6-13
- 缓存亲性，6-16
- 数据对齐支持，8-2
- 运行时支持，3-4
- 编译相关的函数，7-4
- 编译层，3-1
- 对于 Intel(R) DSS/PARISO* 的配置，4-4
- 编译环境，4-1
- Eclipse* 配置，4-2

B
- 基准测试，11-1
- 从 C 调用例程，7-6
- Fortran 95 接口到，7-3
- 混合语言编程，7-5

C
- 从 C 调用 LAPACK，7-5
- 从 C 用的 BLAS 函数，7-8
- 从 C 调用 BLAS Level 1，7-9
- 从 C++ 调用 BLAS Level 1，7-10

D
- 数据对齐，8-2
- 归一化数量，6-17
- 正则性能，6-17
- 开发环境，4-1
- 目录结构，3-20
- 高层接口，3-1
- 混合语言调用，7-8
- CBLAS 示例，7-7
- 聚类 FFT 调用，9-1
- 聚类软件，9-1
- 链接扩展，9-3
- 链接语法，9-1
- AVX 指令分发，6-1
- 文档，3-20
- 在 Eclipse IDE 中查看 Intel(R) MKL，10-1
- 代码对齐，8-1
- 性能提升技巧，4-14

E
- Eclipse 配置，4-2
- 搜索 Intel 网站，10-3

F
- FFT 函数，6-15
- 接口优化，6-18
- FFTW 接口支持，B-1
- Fortran 95 接口到 LAPACK 和 BLAS，7-3
- 链接命令示例，5-7
- 链接库，5-5
- 对于 Intel(R) 64 架构，5-5
- 线程，5-4

G
- GNU* 多精度算术库，B-1
- 链接，5-1
- 聚类 FFT 调用，9-1
- 使用 ScaLAPACK，9-1
- LINPACK 基准测试，11-1

H
- Eclipse* CDT 中 Intel(R) MKL 的帮助，10-1
- HT 技术，超线程
- 超线程技术配置提示，6-15

M
- 内存函数精炼，6-18
- 内存管理，6-18
- 内存重命名，6-18
- 混合语言编程，7-5
- Fortran 95 模块，7-4
- MP LINPACK 基准测试，11-4
- 混合版本，11-4
- 多核性能，6-16

I
- ILP64 编程支持，3-5
- 数值稳定性消除，8-1
- 安装检查，2-4
- 接口层，3-3

