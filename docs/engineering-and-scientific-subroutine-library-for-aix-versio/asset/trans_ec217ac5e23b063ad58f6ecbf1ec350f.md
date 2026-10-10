
# SGRAQ 和 DGRAQ——使用 Gauss-Rational 求积法对函数进行数值求积

这些函数使用指定阶数的 Gauss-Rational 求积法，近似计算实值函数在半无限区间上的积分。

## 表 172. 数据类型

| a, b, Result | 子程序 |
| :--- | :---: |
| 短精度实数 | SGRAQ |
| 长精度实数 | DGRAQ |

## 语法

| Fortran | SGRAQ \| DGRAQ (subf, a, b, n) |
| :--- | :--- |
| **C 和 C++** | sgraq \| dgraq (subf, a, b, n); |

## 输入参数

-   *subf* 是用户提供的子程序，用于计算被积函数。该子程序应定义为具有三个参数：*l*、*y* 和 *n*。详情请参见第 914 页的“SUBF 子程序的编程注意事项”。
    -   *指定方式：* subf 必须在应用程序中声明为外部子程序。它可以使用任何您选择的名称。
-   *a*
    -   具有以下含义，其中：
    -   如果 *a+b > 0*，它是积分下限。
    -   如果 *a+b < 0*，它是积分上限。
    -   *指定方式：* 表 172 中指定的数据类型的数值。
-   *b*
    -   是被积函数的中心常数 *b*。
    -   *指定方式：* 表 172 中指定的数据类型的数值。
-   *n*
    -   是要使用的求积法的阶数。
    -   *指定方式：* 全字整数；n = 1, 2, 3, 4, 5, 6, 8, 10, 12, 14, 16, 20, 24, 32, 40, 48, 64, 96, 128, 或 256。

## 返回参数

*函数值* 是积分的近似值。返回方式为：表 172 中指定的数据类型的数值。

## 说明

1.  在您的程序中将 DGRAQ 函数声明为返回长精度实数。如有必要，将 SGRAQ 函数声明为返回短精度实数。
2.  指定为 *subf* 的子程序必须在您的程序中声明为外部。此外，*subf* 使用的数据类型必须与本 ESSSL 子程序指定的数据类型一致。变量 *x*（在第 932 页的“Function”部分中描述）以及参数 $n$ 分别对应于子程序参数 $t$ 和 $n$。关于如何设置子程序的详细信息，请参见第 914 页的“SUBF 子程序的编程注意事项”。

## 功能

使用指定阶数的 Gauss-Rational 求积法，近似计算实值函数在半无限区间上的积分。积分区域为：

-   $(a, \infty) \quad \text{如果 } a+b > 0$
-   $(-\infty, a) \quad \text{如果 } a+b < 0$

对于以下形式的积分，$n$ 阶方法在理论上是精确的，其中 $f$ 是次数小于 $2n$ 的多项式：

-   $\int_{a}^{\infty} f \left( \frac{1}{x+b} \right) \frac{1}{(x+b)^2} dx \qquad \text{如果} \; a+b > 0$
-   $\int_{-\infty}^{a} f \left( \frac{1}{x+b} \right) \frac{1}{(x+b)^2} dx \qquad \text{如果} \; a+b < 0$

当被积函数能被以下形式的函数良好近似时，$n$ 阶方法是良好的近似，其中 $f$ 是次数小于 $2n$ 的多项式：

$f \left( \frac{1}{x+b} \right) \frac{1}{(x+b)^2}$

参见参考文献 [28] 和 [95]。结果作为函数值返回给 Fortran、C 或 C++ 程序。

## 错误条件

**计算错误：** 无

**输入参数错误：**
1.  $a+b=0$
2.  $n$ 不是允许的值，如该参数的语法列表中所示。

## 示例 1

此示例展示了如何计算由以下函数 $f$ 的积分：

$f(x) = \left( e^{1.0/x} \right) / x^2$

在区间 $(-\infty, -2.0)$ 上，使用 10 点 Gauss-Rational 方法：

$\int_{-\infty}^{-2.0} \left( \frac{e^{1.0/x}}{x^2} \right) dx$

用户提供的用于计算被积函数的子程序 FUN1 的 Fortran 代码如下：

```fortran
SUBROUTINE FUN1 (T,Y,N)
INTEGER*4 N
REAL*4 T(*),Y(*),TEMP
DO 1 I=1,N
 1          TEMP=1.0/T(I)
             Y(I)=EXP(TEMP)*TEMP**2
  RETURN
  END
```

**程序语句和输入：**

```fortran
EXTERNAL FUN1
.
.
.
                 SUBF      A      B      N
                 |         |      |      |
  XINT  = SGRAQ( FUN1 , -2.0 , 0.0 , 10 )
.
.
.
  FUN1      = (如上所示)
```

**输出：**

```
  XINT    = 0.393
```

## 示例 2

此示例展示了如何计算由以下函数 $f$ 的积分：

$f(x) = (x - 3.0)^{-2} + 10(x - 3.0)^{-11}$

在区间 $(4.0, \infty)$ 上，使用 6 点 Gauss-Rational 方法：

$\int_{4.0}^{\infty} \left( (x - 3.0)^{-2} + 10(x - 3.0)^{-11} \right) dx$

用户提供的用于计算被积函数的子程序 FUN2 的 Fortran 代码如下：

```fortran
SUBROUTINE FUN2 (T,Y,N)
INTEGER*4 N
REAL*4 T(*),Y(*),TEMP
DO 1 I=1,N
 1          TEMP=1.0/(T(I)-3.0)
             Y(I)=TEMP**2+10.*TEMP**11
  RETURN
  END
```

**程序语句和输入：**

```fortran
EXTERNAL FUN2
.
.
.
                 SUBF      A      B      N
                 |         |      |      |
  XINT  = SGRAQ( FUN2 , 4.0 , -3.0 , 6 )
.
.
.
  FUN2      = (如上所示)
```

**输出：**

```
  XINT    = ...
```

