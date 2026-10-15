
代码中有两个循环，尽管编译器成功并行化了第一个循环，但它未能并行化第二个循环。编译器报告第二个循环中的函数调用阻止了循环的并行化。我们将在本节稍后讨论如何避免这个问题。

# 使用自动并行化生成并行应用程序

Intel 编译器使用 `-parallel` 选项启用并行化，并使用 `-par-report` 选项报告其成功情况。编译器还具有 `-par-threshold(n)` 选项，它用于控制编译器并行化循环的阈值。`-par-threshold0` 会让编译器并行化所有循环；默认的 `-par-threshold100` 表示编译器应仅并行化那些确定能够获益的循环。列表 7.3 显示了 Intel 编译器对同一源文件的输出。`-fno-inline-functions` 标志禁用了编译器的内联，并确保两个编译器生成的代码一致。

### 列表 7.3 使用 Intel 编译器进行自动并行化

```
$ icc -std=c99 -0 -parallel -par-report -par-threshold0 \
-fno-inline-functions omp_vector.c

omp_vector.c(6): (col. 3) remark: LOOP WAS AUTO-PARALLELIZED.
```

循环中使用的线程数由环境变量 `OMP_THREADS` 控制。列表 7.4 显示了代码在单线程和双线程运行时的性能。检查串行代码和并行代码报告的时间是有用的。两种情况下都有用户时间（user time），这表明两段代码执行的工作量相同。然而，并行版本的实际时间（real time）更短。这是预料之中的。将恒定的工作量分布到两个线程上，理想情况下会导致每个线程完成一半的工作。

### 列表 7.4 并行代码在单线程和双线程下的性能

```
$ export OMP_NUM_THREADS=1
$ timex a.out
real 3.55
user 3.55
sys 0.02
$ export OMP_NUM_THREADS=2
$ timex a.out
real 2.10
user 3.55
sys 0.04
```

作为一个更复杂的自动并行化示例，考虑列表 7.5 中的循环，该循环将矩阵与向量相乘并将结果放在第二个向量中。

### 列表 7.5 矩阵乘以向量的代码

```
void matvec(double **mat, double *vec, double *out, \
{
int i, j;
for (i=0; i<row; i++) // Line 5
{
out[i]=0;
for ( j=0; j<col; j++ ) // Line 8
{
out[i] += mat[i][j] * vec[j];
}
}
}
```

列表 7.6 显示了使用 Solaris Studio 编译器编译此代码的结果。

### 列表 7.6 使用 Autopar 编译代码

```
$ cc -g -xautopar -xloopinfo -O -c floop.c
floop.c, line 5: not parallelized, not a recognized for loop
floop.c, line 8: not parallelized, not a recognized for loop
```

编译器没有识别出这两个可并行化的 `for` 循环。原因是由于对 `out[i]` 的存储操作与用于确定循环边界的值（`row` 和 `col`）之间存在别名（aliasing）的可能性。编译器自动并行化循环的要求是循环必须保持不变。对循环边界的存储操作违反了这一限制。因此，它不是一种可以自动并行化的循环形式。作为程序员，编写依赖于数组边界存储的代码是不寻常的，但对于编译器来说，唯一安全的假设是这些可能会产生别名。

纠正此问题最通用的方法是将循环限制放在局部临时变量中。这消除了循环限制与循环中某一个存储操作产生别名的可能性。对于列表 7.5 中的代码，很容易执行等效更改，并按值传递循环边界，而不是作为值的指针传递它们。

## 列表 7.7 修改代码以避免循环计数器别名

```cpp
void matVec( double *mat, double *vec, double *out,
int row, int col)
{
int i, j;
for ( i=0; i<row; i++) // Line 5
{
out[i]=0;
for ( j=0; j<col; j++) // Line 8
{
out[i] += mat[i][j] * vec[j];
}
}
}
```

# 使用自动并行化生成并行应用程序

列表 7.8 显示了编译此代码新变体时的编译器输出。

### 列表 7.8 使用自动并行化编译修改后的代码

```
$ cc -g -xautopar -xloopinfo -0 -c fploop.c
"fploop.c", line 5: not parallelized, unsafe dependence
"fploop.c", line 8: not parallelized, unsafe dependence
```

代码修改使编译器能够识别出循环为并行化候选，但编译器遇到了一个问题，因为 `out` 指向的元素与矩阵或向量 `vec` 指向的元素对齐。解决此问题的一种方法是使用带有 `restrict` 限制的指针来持有输出数组的长度。列表 7.9 显示了为此修改后的代码。

### 列表 7.9 使用 restrict 限制指针处理输出地址

```cpp
void matVec(double **mat, double *vec, double restrict out)
{
    int i,j;
    for (i=0; i<row; i++) // Line 5
    {
        out[i]=0;
        for (j=0; j<col; j++) // Line 8
        {
            out[i] += mat[i][j] * vec[j];
        }
    }
}
```

对代码进行此调整后，编译器能够产生循环的并行版本，如列表 7.10 所示。

### 列表 7.10 编译包含 restrict 指针的代码

```
$ cc -g -xautopar -xloopinfo -0 -c floop.c
floop.c, line 5: PARALLELIZED, serial generated
floop.c, line 8: unsafe dependence
```

Solaris Studio 编译器生成了循环的两个版本：并行版本和一个串行版本。在运行时，编译器将确定循环的次数是否足以让并行版本比串行版本更快。

编译器报告 7.9 中的第 8 行存在不安全依赖；其原因将在下一节“识别和并行化归约”中讨论。

## 识别和并行化归约

当循环将大量数据还原为较小的值集时，该操作被称为归约（reduction）。归约的一个经典示例是计算数组和，如列表 7.11 所示。

### 列表 7.11 计算数组和

```cpp
double sum(double* array, int length)
{
  double total=0;
  int i;
  for (i=0; i<length; i++) {
    total += array[i];
  }
  return total;
}
```
