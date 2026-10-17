
`-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_intel_thread.a -Wl,--end-group`

`-liomp5 -lpthread`

### 6. `myprog.f` 与支持 LP64 接口的并行 Intel MKL 的动态链接：

```
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE
-lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -liomp5 -lpthread
```

### 7. `myprog.f`、Fortran 95 LAPACK¹以及支持 LP64 接口的并行 Intel MKL 的静态链接：

```
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -I$MKLINCLUDE/em64/lp64
-lmkl_lapack_95_lp64
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_intel_thread.a -Wl,--end-group
-liomp5
```

### 8. `myprog.f`、Fortran 95 BLAS¹以及支持 LP64 接口的并行 Intel MKL 的静态链接：

```
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -I$MKLINCLUDE/em64/lp64
-lmkl_blas_95
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_intel_thread.a -Wl,--end-group
-liomp5
```

### 9. `myprog.f`、迭代稀疏求解器并行版以及支持 LP64 接口的并行 Intel MKL 的静态链接：

```
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -lmkl_solver
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_intel_thread.a $MKLPATH/libmkl_core.a -Wl,--end-group
-liomp5
```

### 10. `myprog.f`、迭代稀疏求解器顺序版以及支持 LP64 接口的顺序版 Intel MKL 的静态链接：

```
ifort myprog.f -L$MKLPATH -I$MKLINCLUDE -lmkl_solver_sequential
-Wl,--start-group $MKLPATH/libmkl_intel_lp64.a $MKLPATH/libmkl_sequential.a $MKLPATH/libmkl_core.a -Wl,--end-group
-lpthread
```

## 管理性能与内存

本章介绍了使用 Intel® Math Kernel Library (Intel® MKL) 获取最佳性能的各种方法：主要讨论了线程化（参见“使用 Intel® MKL 并行化”），然后展示了编码技巧并提供了提高性能的硬件配置建议。本章还讨论了 Intel MKL内存管理以及如何重新定义库使用的内存函数。

## 使用 Intel® MKL 并行化

Intel MKL 在许多地方使用了多线程处理：

- 直接稀疏矩阵求解器。
- LAPACK
  - 线性方程，计算例程：
    - 分解：`*getrf`, `*gbtrf`, `*potrf`, `*pptrf`, `*sytrf`, `*hetrf`, `*sptrf`, `*htprf`
    - 求解：`*gbstr`, `*gttrs`, `*ptprs`, `*pbrts`, `*pttrs`, `*sytrs`, `*sptrs`, `*hptrs`
    - `*tptrs`, `*tbtrs`。
  - 正交因子化，计算例程：
    - `*geqrf`, `*ormqr`, `*ormliq`, `*unmqr`, `*unmlq`, `*ormql`, `*unmql`, `*unmrq`。
- 奇异值分解，计算例程：`*gebrd`, `*bdsqr`。
- 对称特征值问题，计算例程：
  - `*sytrd`, `*hetrd`, `*sptrd`, `*hptrd`, `*steqr`, `*stedc`。

注意，许多其他基于线程 LAPACK 和 BLAS 例程的 LAPACK 例程也有效利用了并行性：`*gesv`, `*posv`, `*gels`, `*gesvd`, `*syev`, `*heev` 等。

## Intel® Math Kernel Library 用户指南

- 1级和 2级 BLAS 函数：
  - 1级 BLAS：`*axpy`, `*copy`, `*swap`, `/sdot`, `ddot/ddot`, `drot/srot`
  - 2级 BLAS：`*gemv`, `*rmv`, `dsyr/ssyr`, `dsyr2/ssyr2`, `dsymv/ssym`

注意这些函数针对以下情况进行了线程化：

- Intel® Core™2 Duo 和 Intel® Core™ i7 处理器
- 所有 3级 BLAS 和除 2级三角求解器外的所有稀疏 BLAS 例程。
- VML。
- FFT。

由于 Intel MKL 是为多线程设计的，它是线程安全的，这意味着所有 Intel MKL 在多个线程同时执行时都能正常工作。特别是，任何块线程化的 Intel MKL 代码都允许多个线程访问相同的共享数据，但在任何时刻只允许一个线程访问共享数据块。有不同的使用方法。你可以使用环境变量 `OM_NUM_THREADS` 来指定要使用的线程数。Intel MKL 10.0 之前的发布版本可以使用 OpenMP 环境变量（详情见环境变量）或等效的 OpenMP 运行时函数调用（详见“在运行时更改线程数”）。从 10.0 版本开始，Intel MKL 还提供了用于线程管理的变量和相应的 MKL 函数（详情参见“使用附加线程控制”）。Intel MKL 变量 `M_NUM_THREADS` 总是第一个检查，然后检查 OpenMP 变量，如果两者都没有使用，则由 OpenMP 软件选择默认线程数。这与 MKL 9.x 或更低版本有所不同。

![](img/78e923baedeba397a89d376927830122_54_0.png)

注。从 Intel MKL 10.0 开始，由 OpenMP* 软件决定默认线程数。对于 Intel OpenMP*，默认线程数等于系统中的逻辑处理器的数量。

为了获得更高的性能，请将线程数设置为实际处理器或物理核心的数量，如“设置线程数的技巧”摘要概述。

- 除 LAPACK 已弃用的例程 `?lacon`, `?las3` 和 `?las4` 外均如此。

另见：[管理多核性能]()。

## 设置线程数的技巧

你可以采用不同的技术来更改 Intel MKL 中使用的线程数：

- 设置 OpenMP 或 Intel MKL 环境变量之一：
  - `OMP_NUM_THREADS`
  - `MKL_NUM_THREADS`
  - `MKL_DOMAIN_NUM_THREADS`
- 调用 OpenMP 或 Intel MKL 函数之一：
  - `omp_set_num_threads()`
  - `mkl_set_num_threads()`
  - `mkl_domain_set_num_threads()`

在选择合适的技术时，请考虑以下规则：

- Intel MKL 线程控制优于任何环境变量。一个例外（即调用优于之前的规则）是 OpenMP 子程序 `omp_set_num_threads()`，它的优先级不高于 Intel MKL 变量（如 `MKL_NUM_THREADS`）。
- 环境变量无法用于在运行时更改行为，因为它们只在第一次调用 Intel MKL 时读取一次。

## 避免执行环境中的冲突

某些情况会导致执行环境发生冲突，使得在 Intel MKL 中使用线程出现问题。首先，本节简要讨论存在的问题。

如果你使用 OpenMP 指令对程序进行线程化并使用 Intel® 编译器编译程序，Intel MKL 将使用相同的线程库。（注：此处原文中存在大量重复内容，已进行清理）。

#### 表 6-1 如何避免执行环境中的冲突

| 线程模型 | 讨论 |
| :--- | :--- |
| 使用 OpenMP 指令对程序进行线程化（Linux  pthreads）。 | 如果通过任何可用方法设置了多个线程（参见“设置线程数的技巧”）。 |
| 使用 OpenMP 指令对程序进行线程化并使用 Intel 以外的编译器编译程序。 | 这更为困难，因为线程数的设置会影响顺序模式（参见“编译器支持链接”）。 |
| 在多 CPU 系统上运行多个程序，每个处理器被视为节点。 | 在这种情况下，解决方案之一是将线程数设置为任何可用方法（参见“设置线程数的技巧”）。 |
| 混合 (OpenMP*) 模式。 | 针对集群优化的 LINPACK。 |

## Intel® Math Kernel Library 用户指南（续）

- 1级和 2级 BLAS 函数：
