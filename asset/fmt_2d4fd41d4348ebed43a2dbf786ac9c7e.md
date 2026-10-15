
### 4. 运行 HPL，使用如 `ASYOUGO`、`ASYOUGO2` 和 `ENDEARLY` 等编译选项来辅助搜索（这些选项让你比 HPL 更快地获得性能洞察）。

在这样做时，请遵循以下建议：

## LINPACK 和 MP LINPACK 基准测试

- 使用 MP LINPACK（HPL 的补丁版本）来节省搜索时间。

使用补丁版本的 HPL 不会影响你的性能。这就是为什么可能影响性能的功能是可选的（在下文 MP LINPACK 中解释）。也就是说，如果你不使用“减少搜索时间”中解释的新选项，这些更改将被禁用。这些新增的主要目的是协助你找到解决方案。

HPL 需要大量时间来搜索许多参数。在 MP LINPACK 中，目标是获得可能的数值。

由于输入是不固定的，你必须搜索一个巨大的参数空间。对于强大的集群，穷尽搜索所有可能的输入可能是巨大的。

此补丁版本的 HPL 只在执行过程中提高性能，或者根据你的要求提前结束。

通过编译 `-DENDERALLY-DASYOUGO2`（“减少搜索时间”中描述）并使用负阈值来节省时间（在打算提交的 Top500 条目的最终运行中不要使用负阈值）。你可以在 HPL 2.0 输入文件的第 13 行设置阈值。

如果你运行完整个问题，请使用 `-ASYOUGO`（参见“减少搜索时间”）。

- 使用快速反馈，返回第 3 步并更新，直到你确定性能尽可能好。

## 减少搜索时间的选项

在大量节点上运行完大型问题可能需要数小时。MP LINPACK 的搜索是巨大的：你不仅可以运行任何尺寸，还可以针对块大小、网格布局、预取步（lookahead steps）、使用不同的分解方法等。运行完大型问题却发现它比你之前的最佳结果慢了 0.01%，这可能是极大的时间浪费。有 3 个选项：谨慎使用 `ASYOUGO2`，因为它会有细微影响。要查看 DGEMM 内部性能，请使用 `ASYOUGO` 和 `ASYOUGO2_DISPLAY` 进行编译。这些选项提供了大量的 DGEMM 信息，代价是大约 0.2% 的损失。如果你想使用旧版 HPL，只需跳过这些选项并从头编译（尝试 `make clean_all`）。

## MP LINPACK 基准测试

- `ASYOUGO2`：提供详细的单节点 DGEMM 信息。它捕捉所有的 DGEMM 调用（如果你使用 Fortran BLAS）并记录其数据。由于此，该程序有细微的开销。与相当非侵入的 `ASYOUGO` 不同，`ASYOUGO2` 会中断每一个 DGEMM 调用以监控其性能。你应该意识到这一点，尽管对于大问题，这种开销小于 1/10。

`ASYOUGO`：在运行期间提供非侵入性的性能信息。只有少量输出且不影响性能。这非常有用，因为许多运行可能会持续小时而没有任何信息。

以下是 DGEMM 性能示例：

| Col | DT | DF | M |
| :--- | :--- | :--- | :--- |
| 128 | 0.5 | 0.0 | 40 |
| 160 | 0.0 | 0.0 | 128 |
| 128 | 0.0 | 0.0 | 160 |
| 128 | 0.0 | 0.0 | 128 |

基于 128 列 LU 带有预取步的估计值，在输出结果时该工作尚未完成。然而，这是识别运行的良好估计。以 LU flops 的数量为基准，通过与 DGEMM 比较，你可以获得我们性能的下限。

# 11 Intel® Math Kernel Library 用户指南

例如，通过性能值来估算问题规模从 700,000 到 701,000 之间的差异。影响性能下降的另一个因素是网格维度（`P` 和 `Q`）。对于大型问题，当 `P` 和 `Q` 的取值大致相等时，性能在前几个步骤的下降幅度往往较小。你可以利用大量的参数（如广播类型）并更改它们，使得最终性能非常紧密地取决于前几个步骤。

使用这些工具将极大地帮助你增加测试的数据量。

## Intel® Math Kernel Library 语言接口支持

表 A-1 显示了 Intel® Math Kernel Library (Intel® MKL) 为每个领域提供的语言接口，表 A-2 列出了相应的头文件。可以使用混合语言编程从其他语言中调用 Intel MKL 例程。例如，请参阅《使用 Intel® MKL 进行混合语言编程》，了解如何从 C/C++ 调用 Fortran 例程。

### 表 A-1 语言接口支持

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

### 表 A-2 头文件

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
