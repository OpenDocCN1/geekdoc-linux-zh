
| `complex_quad`, `complex_quad` | 128位复数，向量 | | |
| `imaginary_quad`, `imaginary_quad` | 128位虚数，向量 | | |
| `floatnxm` | nxm 个 32位浮点数的矩阵 | | |
| `doublenxm` | nxm 个 64位浮点数的矩阵 | | |

在这种情况下，程序员可以以属性的形式向内核提供工作组和向量大小信息，如下所示。

### 内核属性

```
__attribute__((vec_type_hint(type)))
__attribute__((work_group_size_hint(X, Y, Z)))
__attribute__((reqd_work_group_size(X, Y, Z)))
```

OpenCL 还允许为声明的变量赋予属性，用于对齐、紧凑和字节序。

### 类型属性

```
__attribute__((aligned(n)))
__attribute__((aligned))
```

```
__attribute__((packed))
__attribute__((endian(host)))
__attribute__((endian(device)))
__attribute__((endian))
```

# C.9 常量

OpenCL 定义了一组单精度浮点数常量，如表 C.3 所示。当 OpenCL 实现支持，每个以 "_F" 结尾的常量都有对应的不带 "_F" 后缀的双精度版本，以及通过将该后缀替换为 "_H" 得到的半精度版本。

# C.10 内置函数

OpenCL 提供了一组可在内核代码中使用的内置函数。其中一些函数是标准的数学原语，许多函数接受向量操作数。其他是用于工作项识别和向量加载/存储的实用函数。

### C.10.1 整数函数

表 C.4 列出了整数函数。这些函数接受向量操作数。

### C.10.2 浮点数函数

表 C.5 列出了浮点数函数。这些函数大部分接受向量操作数。

### C.10.3 向量函数

OpenCL 内核应始终使用向量加载和存储函数在向量变量和数组之间交换数据（表 C.6）。

### C.10.4 工作项函数

OpenCL 内核可以作为 1 、2 维 3 维的工作项数组进行调度。工作项数组可选地划分为 1 、2 或 3 维组（当调用 `get_local_id()` 并传入 `local_work_size` 参数时）。工作负载分布取决于每个工作项在该坐标系中自我识别的能力，而其全局 ID 是相对于其在所在工作组内的位置计算的（表 C.7）。工作组内的工作项可以通过屏障（barrier）操作进行同步，并对其内存操作进行顺序排序（表 C.8）。

## 表 C.3 OpenCL 常量

| 常量 | 描述 |
|---|---|
| `MAXFLOAT` | 最大有限单点数的值 |
| `HUGE_VAL` | 正数浮点数表达式，求值为 +infinity |
| `HUGE_VAL` | 正数双精度表达式，求值为 +infinity |
| `INFINITY` | 常数浮点数表达式，无符号 |
| `NAN` | 常数浮点数表达式，NaN |
| `M_E_F` | e 的值 |
| `M_LOG2E_F` | log$_2$ 的值 |
| `M_LOG10E_F` | log$_{10}$ 的值 |
| `M_LN2_F` | log$_e$ 的值 |
| `M_LN10_F` | log$_{10}$ 的值 |
| `M_PI_F` | $\pi$ 的值 |
| `M_PI_2_F` | $\pi$/2 的值 |
| `M_PI_4_F` | $\pi$/4 的值 |
| `M_1_PI_F` | $1/\pi$ 的值 |
| `M_2_PI_F` | $2/\pi$ 的值 |
| `M_2_SQRTPI_F` | $2/\sqrt{\pi}$ 的值 |
| `M_SQRT2_F` | $\sqrt{2}$ 的值 |
| `M_1_SQRT2_F` | $1/\sqrt{2}$ 的值 |

## 表 C.4 内置函数

| 函数 | 描述 |
|---|---|
| `abs(x)` | x (无符号) |
| `abs_diff(x)` | 不溢出的 x-y (无符号) |
| `add_sat(x,y)` | x+y 并饱和结果 |
| `hadd(x,y)` | (x+y)>>1 |
| `rhadd(x,y)` | (x+y)>>1 |
| `clamp(x,minval,maxval)` | x 在 minval 和 maxval 之间截断 |
| `clz(x)` | x 前导零个数 |
| `mad_hi(a,b)` | a*b 高位 |
| `mad_sat(a,b,c)` | a*b+c 饱和 |
| `expb(x)` | x 的指数部分 |
| `ld2(x)` | 加载2 个 32 位浮点数 |
| `mul_hi(a,b)` | a*b 高位 |
| `rotate(v)` | 旋转 v |
| `sub_sat(x,y)` | x-y 饱和 |
| `popcount(x)` | x 中 1 的个数 |
| `upsample(char[n])` | 扩展为 n 个 浮点数 |
| `upsample(uchar[n])` | 扩展为 n 个 浮点数 |
| `upsample(short[n])` | 扩展为 n 个 浮点数 |
| `upsample(int[n])` | 扩展为 n 个 浮点数 |
| `upsample(float[n])` | 扩展为 n 个 浮点数 |
| `upsample(double[n])` | 扩展为 n 个 浮点数 |
| `vload.1f(ptr)` | 加载 1 个 32 位浮点数 |
| `vload.2f(ptr)` | 加载 2 个 32 位浮点数 |
| `vload.4f(ptr)` | 加载 4 个 32 位浮点数 |
| `vload.1d(ptr)` | 加载 1 个 64 位浮点数 |
| `vload.2d(ptr)` | 加载 2 个 64 位浮点数 |
| `vstore.1f(ptr,v)` | 存储 1 个 32 位浮点数 2 次 |
| `vstore.2f(ptr,v)` | 存储 2 个 32 位浮点数 |
| `vstore.4f(ptr,v)` | 存储 4 个 32 位浮点数 |
| `vstore.1d(ptr,v)` | 存储 1 个 64 位浮点数 2 次 |
| `vstore.2d(ptr,v)` | 存储 2 个 64 位浮点数 |

## 表 C.5 内置函数

| 三角函数 | 描述 |
|---|---|
| `sin(x)`, `cos(x)`, `tan(x)` | 基本三角函数 |
| `asin(x)`, `acos(x)`, `atan(x)` | 反三角函数 |
| `sinh(x)`, `cosh(x)`, `tanh(x)` | 基本双曲三角函数 |
| `asinh(x)`, `acosh(x)`, `atanh(x)` | 反双曲三角函数 |
| `sinpi(x)`, `cospi(x)`, `tanpi(x)` | 基本三角函数，基于 pi |
| `asinpi(x)`, `acospi(x)`, `atanpi(x)` | 反三角函数，基于 pi |
| `atan2(x,y)` | atan2(x,y) |
| `atan2pi(x,y)` | atan2(x,y)，基于 pi |
| 对数、指数和幂函数 | |
| `log(x)`, `log2(x)`, `log10(x)` | 对数底 e, 2 和 10 |
| `log1p(x)`, `logb(x)` | log(1+x) 和提取指数 |
| `exp(x)`, `exp2(x)`, `exp10(x)` | 指数底 e, 2 和 10 |
| `expm1(x)` | e^x-1 |
| `pow(x,y)`, `pown(x,y)`, `powr(x,y)` | 计算 xʸ |
| `rootn(x,y)` | x¹/y |
| `ldexp(x,n)` | x*² |
| `frexp(x, *exp)` | 提取尾数和指数 |
| `modf(x, *iptr)` | 分解浮点数 |

## 表 C.5 内置函数 — 续

| 几何函数 | |
|---|---|
| `cbrt(x)` | 立方根 |
| `hypot(x,y)` | $x^2+y^2$ 的平方根 |
| `cross(p0,pl)` | 叉积（向量大小为3或4） |
| `distance(p0,pl)` | 距离 |
| `dot(p0,pl)` | 点积 |
| `length(p)` | 向量长度 1 |
| `normalize(p)` | 归一化 |
| `fast_distance(p0,pl)` | 距离 |
| `fast_length(p)` | 长度 |
| `fast_normalize(p)` | 向量长度 1 |
| 表 C.5 内置浮点函数 — 续 | |
|---|---|
| 除法操作 `fmod(x,y)` | x 和 y 的浮点取模 |
| `fract(x)` | x 的小数部分 |
| `remainder(x,y)` | x 和 y 的余数 |
