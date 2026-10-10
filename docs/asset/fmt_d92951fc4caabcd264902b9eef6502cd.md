
| :--- | :--- |
| **SMP** | **32 位** |
| | `cc_r -O xyz.c -lesslsmp -lxlf90_r -lxlsm -lxlfmath` |
| | `-L/opt/ibmcmp/xlf/8.1/lib -R/opt/ibmcmp/xlf/8.1/lib` |
| | **64 位** |
| | `cc_r -O -q64 xyz.c -lesslsmp -lxlf90_r -lxlsm -lxlfmath` |
| | `-L/opt/ibmcmp/xlf/8.1/lib64 -R/opt/ibmcmp/xlf/8.1/lib64` |
| **串行 (Serial)** | **32 位** |
| | `cc_r -O xyz.c -lessl -lxlf90_r -lxlfompsr -lxlfmath` |
| | `-L/opt/ibmcmp/xlf/8.1/lib -R/opt/ibmcmp/xlf/8.1/lib` |
| | **64 位** |
| | `cc_r -O -q64 xyz.c -lessl -lxlf90_r -lxlfompsr -lxlfmath` |
| | `-L/opt/ibmcmp/xlf/8.1/lib64 -R/opt/ibmcmp/xlf/8.1/lib64` |

### C++ 程序过程

用于 C 和 C++ 程序的 ESSL 头文件 `essl.h` 安装在 `/usr/include` 目录中（用于 32 位支持）以及 `/opt/cross/powerpc64-linux/include` 目录中（用于 64 位支持）。

ESSL 头文件支持两种声明标量输出参数的替代方案。默认情况下，参数被声明为引用类型。如果您希望它们被声明为指针，请向您的命令中添加 `-D_ESSVCPR`。

在链接和运行程序时，您必须为 ESSL 修改现有的作业过程，以设置必要的库。

如果您是从 C++ 程序访问 ESSL，可以使用下表所示的命令进行编译和链接。

| ESSL 库名称 | 命令 |
| :--- | :--- |
| **SMP** | **32 位** |
| | `xlc_r -O xyz.C -lesslsmp -lxlf90_r -lxlsmp -lxlfmath` |
| | `-L/opt/ibmcmp/xlf/8.1/lib -R/opt/ibmcmp/xlf/8.1/lib` |
| | **64 位** |
| | `xlc_r -O -q64 xyz.C -lesslsmp -lxlf90_r -lxlsmp -lxlfmath` |
| | `-L/opt/ibmcmp/xlf/8.1/lib64 -R/opt/ibmcmp/xlf/8.1/lib64` |
| **串行 (Serial)** | **32 位** |
| | `xlc_r -O xyz.C -lessl -lxlf90_r -lxlfompsr -lxlfmath` |
| | `-L/opt/ibmcmp/xlf/8.1/lib -R/opt/ibmcmp/xlf/8.1/lib` |
| | **64 位** |
| | `xlc_r -O -q64 xyz.C -lessl -lxlf90_r -lxlfompsr -lxlfmath` |
| | `-L/opt/ibmcmp/xlf/8.1/lib64 -R/opt/ibmcmp/xlf/8.1/lib64` |

### 第 6 章。迁移您的程序

本章解释了将您的应用程序迁移到使用 ESSL 子例程的诸多方面。它涵盖了：

- 将 ESSL 3 版程序迁移到 4.1 版
- 规划未来的迁移
- 在 IBM pSeries 和 R5/6000 处理器之间迁移
- 从其他库迁移到 ESSL

#### 将 ESSL 3 版 3 发行版程序迁移到 4 版 1 发行版

对称不定矩阵分解和多元右端项求解子例程 `DBSSV` 已修改，使得在 *n* 大于零且 `nrhs` 为零的情况下对矩阵进行分解。以前，这是快速返回条件，且不对矩阵进行分解。（请参阅第 504 页的子例程说明。）

对于所有其他子例程，如果您是从 ESSL 3 版 3 发行版迁移到 ESSL 4 版 1 发行版，则不需要对您的应用程序进行任何更改。

> **注意：** 如果您是从早于 ESSL 3 版 3 发行版的版本迁移，请参阅以下 IBM 网站上的 ESSL 3 版 3 发行版文档：
>
> http://www-1.ibm.com/servers/eserver/pseries/library/sp_books/essl.html

#### ESSL 子例程

ESSL 3 版 3 发行版和 ESSL 4 版 1 发行版中子例程的调用序列是相同的。

#### 规划未来迁移

关于未来规划，如果工作存储在子例程调用后不需要持久保留，您应该使用动态分配。否则，您应该使用与处理器无关的公式或简单公式来计算 ESSL 调用序列中 `naux` 参数的值。可能会发生以下两件事，导致 ESSL 错误处理返回的 `naux` 最小值在未来增加：

- 如果对 ESSL 子例程进行了修改以提高性能
- 如果需要支持未来的处理器

这些公式允许您指定足够大的辅助存储，以适应 ESSL 的任何未来改进以及任何未来的处理器。如果您未提供至少这些数量的存储，您的程序将来可能无法运行。

您应该遵循以下经验法则：为了保护您的应用程序在未来因辅助存储需求可能增加而无需重新编码，如果可能，请使用动态分配。如果工作存储在子例程调用后必须持久保留，则您应该在当前应用程序中提供尽可能多的存储。在确定要指定多少时，您应该权衡存储约束与将来进行修改的便利性。

未来的变更，然后指定你认为最佳的选择。如果可能，你应该提供更大容量的存储空间，以防止未来的迁移问题。

#### 在 IBM @server pSeries 和 RS/6000 处理器之间迁移

本节介绍了在 PowerPC®、POWER、POWER2、POWER3、POWER3-Il 和 POWER4 处理器之间（双向）迁移 ESSL 应用程序的所有方面。

#### 辅助存储

ESSL 错误处理返回的最小辅助存储量可能因 IBM @server pSeries 和 RS/6000 处理器之间的以下子程序而异：所有傅里叶变换子程序、`SCONF`、`SCORE` 和 `SACORF`。因此，为了确保你的应用程序始终可以从任何平台迁移到任何其他平台，你应该使用与处理器无关的公式来确定要使用的辅助存储量。

#### 按位相同的结果

由于硬件和 ESSL 设计上的差异，当你从一个 ESSL 库迁移到另一个 ESSL 库时，获得的结果可能不是按位相同的。然而，结果在数学上是等价的。

#### 从其他库迁移到 ESSL

本节介绍了一些从 IBM 或非 IBM 工程科学库迁移到 ESSL 的通用方面。

##### 从 ESSL/370 迁移

ESSL/370 和 ESSL for AIX 之间具有很高的兼容性。但是，你可能需要对某些子程序进行一些编码更改。

##### 从其他 IBM 子程序库迁移

如果你正在从其他 IBM 库产品（例如具有与 ESSL 类似功能的子程序库—数学（SL MATH）或科学子程序包（SSP））迁移，那么 ESSL 的调用序列与你当前使用的调用序列不同。你的程序必须经过修改，以添加 ESSL 调用序列并进行其他与 ESSL 相关的编码更改。

如果你正在从随 RS/6000 基本操作系统提供的基本线性代数子程序库迁移，你的调用序列无需更改。

##### 从 LAPACK 迁移

ESSL 包含一些符合 LAPACK 接口的子程序。如果你正在使用这些子程序，迁移到 ESSL 时无需进行编码更改。

**注意：** 你应该意识到，有一些 ESSL 子程序的名称与现有的 LAPACK 子程序名称匹配，但其调用序列参数和功能与那些 LAPACK 子程序不同。（参见第 989 页的附录 B，“LAPACK”。）

此外，你可能有兴趣使用随 LAPACK 提供的调用转换接口（CCI）。每当 ESSL 子程序提供功能或近似功能等价时，CCI 会用 ESSL 子程序的调用替代 LAPACK 子程序的调用。使用 CCI 可以让 LAPACK 用户针对 LAPACK 子程序的额外子集获得 ESSL 的优化性能。有关详细信息，请参见参考文献 [42]。

##### 从非 IBM 子程序库迁移

如果你正在使用非 IBM 库，ESSL 可能提供与你当前使用的子程序对应的子程序。你可以选择迁移你的程序，以受益于 ESSL 子程序提供的性能提升。在这种情况下，你可能需要重新编码你的程序以使用 ESSL 调用序列，因为 ESSL 使用的名称和参数可能与非 IBM 库使用的不同。另一方面，如果你使用的是与 ESSL 子程序对应的任何标准 Level 1、2 和 3 BLAS 或 LAPACK 例程，则无需重新编码调用序列。ESSL 调用序列与公共领域代码相同。

### 第 7 章. 处理问题

本章提供以下信息供你在处理错误时使用：

- 如何获得 IBM 支持。
- 如何处理 NLS（自然语言支持）问题。
