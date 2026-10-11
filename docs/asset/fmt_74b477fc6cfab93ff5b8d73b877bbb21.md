
## 表 3-7 IA-64 架构特定目录 lib/64 详细结构（续）

| 文件 | 内容 |
|---|---|
| `libmkl_blacs_openmpi_ilp64.a` | 支持 OpenMPI 的 LP64 版本 BLAS 例程 |
| `libmkl_blacs_openmpi_ilp64.a` | 支持 OpenMPI 的 LP64 版本 BLAS 例程 |
| `libmkl_blacs_sgimpt_ilp64.a` | 支持 SGI MPT 的 LP64 版本 BLAS 例程。 |
| `libmkl_blacs_sgimpt_ilp64.a` | 支持 SGI MPT 的 LP64 版本 BLAS 例程。 |

| 文件 | 内容 |
|---|---|
| 接口层 |  |
| `libmkl_gf_ilp64.so` | 用于 GNU Fortran 和 Absoft 编译器的 ILP64 接口库 |
| `libmkl_gf_lp64.so` | 用于 GNU Fortran 和 Absoft 编译器的 LP64 接口库 |
| `libmkl_intel_ilp64.so` | Intel 编译器的 LP64 接口库 |
| `libmkl_intel_lp64.so` | Intel 编译器的 LP64 接口库 |
| `libmkl_intel_sp2dp.so` | Intel 编译器的 SP2DP 接口库 |
| 线程层 |  |
| `libmkl_gnu_thread.so` | 用于 GNU Fortran 和 C 编译器的线程库 |
| `libmkl_intel_thread.so` | Intel 编译器的线程库 |
| `libmkl_pgi_thread.so` | 用于 PGI* 编译器的线程库 |
| `libmkl_sequential.so` | 顺序执行库 |

| 文件 | 内容 |
|---|---|
| 计算层 | `libmkl_avx.so` | 针对 Intel® 高级向量扩展 (Intel® AVX) 优化的内核 |
| `libmkl_core.so` | 用于动态加载特定处理器的内核的库分发器 |
| `libmkl_def.so` | 默认内核库 |
| `libmkl_mc.so` | 基于 Intel® Core™ 微架构的处理器的内核库 |
| `libmkl_mc3.so` | 用于 Intel® Core™ 处理器的内核库 |
| `libmkl_lapack.so` | LAPACK 和 DSS/PARDISO 例程及驱动程序 |
| `libmkl_scalapack_lp64.so` | 支持 LP64 接口的 ScLAPACK 例程库 |
| `libmkl_scalapack_lp64.so` | 支持 LP64 接口的 ScLAPACK 例程库 |
| `libmkl_vml_avx.so` | 针对 Intel® 高级向量扩展 (Intel® AVX) 优化的 VML/VSL |
| `libmkl_vml_def.so` | 默认内核的 VML/VSL 部分 |
| `libmkl_vml_mc.so` | 基于 Intel® Core™ 微架构的处理器的 VML/VSL |
| `libmkl_vml_mc3.so` | 用于 Intel® Core™ 处理器的 VML/VSL |
| `libmkl_vml_p4n.so` | 使用 Intel® 64 架构的 Intel® Xeon® 处理器的 VML/VSL |
| `libmkl_vml_mc2.so` | 用于 45nm Hi-k Intel® Core™2 和 Intel® Xeon® 家族的 VML/VSL |
| RTL |  |
| `libguide.so` | 用于动态链接的 Intel® legacy OpenMP* 运行时库 |
| `libomp5.so` | 用于动态链接的 Intel® 兼容 OpenMP* 运行时库 |
| `libmkl_intelmpi_lp64.so` | 支持 Intel MPI 2.0/3.x 和 MPICH2 的 LP64 版本 BLACS 例程 |
| `libmkl_intelmpi_lp64.so` | 支持 Intel MPI 2.0、3.x 以及 MPICH2 的 LP64 版本 BLACS 例程 |
| `locale/en_US/mkl_msg.cat` | 英文 Intel MKL 消息目录 |
| `locale/ja_JP/mkl_msg.cat` | 日文 Intel MKL 消息目录 |

| 文件 | 内容 |
|---|---|
| **静态库** |  |
| *接口层* |  |
| `libmkl_blas95_ilp64.a` | 用于 Intel® Fortran 编译器的 BLAS Fortran 95 接口库。支持 ILP64 接口 |
| `libmkl_blas95_lp64.a` | 用于 Intel® Fortran 编译器的 BLAS Fortran 95 接口库。支持 LP64 接口 |
| `libmkl_intel_ilp64.a` | Intel 编译器的 ILP64 接口库 |
| `libmkl_intel_lp64.a` | Intel 编译器的 LP64 接口库 |
| `libmkl_intel_sp2dp.a` | Intel 编译器的 SP2DP 接口库 |
| `libmkl_gf_ilp64.a` | 用于 GNU Fortran 编译器的 ILP64 接口库 |
| `libmkl_gf_lp64.a` | 用于 GNU Fortran 编译器的 LP64 接口库 |
| `libmkl_lapack95_ilp64.a` | 用于 Intel® Fortran 编译器的 LAPACK Fortran 95 接口库。支持 ILP64 接口 |
| `libmkl_lapack_lp64.a` | 用于 Intel® Fortran 编译器的 LAPACK Fortran 95 接口库。支持 LP64 接口 |
| *线程层* |  |
| `libmkl_intel_thread.a` | Intel 编译器的线程库 |
| `libmkl_gnu_thread.a` | 用于 GNU Fortran 和 C 编译器的线程库 |
| `libmkl_sequential.a` | 顺序执行库 |
| *计算层* |  |
| `libmkl_cdft_core.a` | 集群版本的 FFT |
| `libmkl_core.a` | 用于 IA-64 架构的内核库 |
| `libmkl_scalapack_ilp64.a` | 支持 ILP64 接口的 ScLAPACK 例程库 |
| `libmkl_scalapack_lp64.a` | 支持 LP64 接口的 ScLAPACK 例程库 |
| `libmkl_solver_ilp64.a` | 支持 ILP64 接口的迭代稀疏求解器和信域求解器库 |
| `libmkl_solver_lp64_sequential.a` | 支持 LP64 接口的迭代稀疏求解器和信域求解器的顺序版本 |
| `libmkl_solver_lp64.a` | 支持 LP64 接口的迭代稀疏求解器、信域求解器和 GMP 例程库 |
| `libmkl_solver_lp64.a` | 支持 LP64 接口的迭代稀疏求解器、信域求解器和 GMP 例程库 |

| 文件 | 内容 |
|---|---|
| RTL |  |
| `libguide.so` | 用于动态链接的 Intel® legacy OpenMP* 运行时库 |
| `libomp5.so` | 用于动态链接的 Intel® 兼容 OpenMP* 运行时库 |
| `libmkl_intelmpi_lp64.so` | 支持 Intel MPI 2.0/3.x 和 MPICH2 的 LP64 版本 BLACS 例程 |
| `libmkl_intelmpi_lp64.so` | 支持 Intel MPI 2.0、3.x 以及 MPICH2 的 LP64 版本 BLACS 例程 |
| `locale/en_US/mkl_msg.cat` | 英文 Intel MKL 消息目录 |
| `locale/ja_JP/mkl_msg.cat` | 日文 Intel MKL 消息目录 |

## 表 3-7 IA-64 架构特定目录 lib/64 详细结构（续）

| 文件 | 内容 |
|---|---|
| 动态库 |  |
| `libmkl_gf_ilp64.so` | 用于 GNU Fortran 编译器的 ILP64 接口库 |
| `libmkl_gf_lp64.so` | 用于 GNU Fortran 编译器的 LP64 接口库 |
| `libmkl_intel_ilp64.so` | Intel 编译器的 ILP64 接口库 |
| `libmkl_intel_lp64.so` | Intel 编译器的 LP64 接口库 |
| `libmkl_intel_sp2dp.so` | Intel 编译器的 SP2DP 接口库 |

## 访问 Intel® MKL 文档

本节详细介绍了 Intel MKL 文档目录的内容，并解释了如何访问该库的手页（man pages）。

## 文档目录内容
