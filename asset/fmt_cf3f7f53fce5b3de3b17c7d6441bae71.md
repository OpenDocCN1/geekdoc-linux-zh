
`asm ("fmacs s3, s9, s2\n\t" : : "s3");`

`asm ("fmacs s4, s9, s3\n\t" : : "s4");`

`asm ("fmacs s5, s9, s4\n\t" : : "s5");`

`asm ("fmacs s6, s9, s5\n\t" : : "s6");`

`asm ("fmacs s7, s6\n\t" : : "s7");`

`asm ("fsts s7,[mem]\n\t" : : [mem]="m (d[i++])");`

在每个指令之前，每一行代码都存在依赖关系。我们的目标是构建一个具有九阶段的软件流水线，对应加载-乘法之后的每条指令。序言部分（`prorolog`）将开始执行迭代 0 中除最后一条以外的所有指令，使 `s7` 留存最终要存储到 `d` 数组中的值。然后，它将执行所有的最后一条指令，使寄存器 `s6` 留下迭代 2 的值以此类推。

为了实现双缓冲技术（其中一组八个寄存器将交替持有原始系数和多项式值的运行和），像之前的实现一样将循环展开 2 次。

在外层循环的每次迭代中，从 `x` 数组加载一个值。然而，由于软件流水线在同一个体中执行所有七条 `fmac` 指令，因此需要始终维护 `x` 数组的七个不同值。为了做到这一点，使用寄存器 `s9-s15`。这些值在外层循环的每次迭代中必须相对于 `fmac` 指令进行移位。我们的主循环将执行原始外层循环的两个展开体，通过更改代码来实现这种移位。

之后，使用 `fcopy` 指令适当地重新排列值。`fcopy` 在两个浮点寄存器之间复制寄存器的内容。其延迟为四。

```c
for (i=0;i<N/4;i+=2) {
    asm ("fsts s7,[mem]\n\t" : : [mem]="m (d[i])");
    asm ("fmacs s23, s10, s6\n\t" : : "s23");
    asm ("fmacs s22, s11, s5\n\t" : : "s22");
    asm ("fmacs s21, s12, s4\n\t" : : "s21");
    asm ("fmacs s20, s13, s3\n\t" : : "s20");
    asm ("fmacs s19, s14, s2\n\t" : : "s19");
    asm ("fmacs s18, s15, s1\n\t" : : "s18");
}
```

## 第 2 章 多核与数据级优化：OpenMP 和 SIMD

```asm
asm ("fmacs s17, s9, s16\n\t" : : "s17");
asm ("fldmias %[mem],{s0,s1,s2,s3,s4,s5,s6,s7})\n\t" : : [mem]r" (&coeff[0]): "s0", "s1", "s2", "s3", "s4");
```

```asm
asm ("s5", "s6", "s7");
asm ("lds s10, %[mem]\n\t" : [mem]"m(x[i+8])" : "s10");
asm ("fts s23,%[mem]\n\t" : [mem]"m(d[i+1])");
```

```asm
asm ("fmacs s7, s11, s22\n\t" : : "s7");
asm ("fmacs s6, s12, s21\n\t" : : "s6");
asm ("fmacs s5, s13, s20\n\t" : : "s5");
asm ("fmacs s4, s14, s19\n\t" : : "s4");
asm ("fmacs s3, s15, s18\n\t" : : "s3");
asm ("fmacs s2, s9, s17\n\t" : : "s2");
asm ("fmacs s1, s0, s0\n\t" : : "s1");
```

```asm
"s16", "s17", "s18", "s19";
"s20", "s21", "s22", "s23");
```

```asm
// 保 s10
asm ("fcpys s31, s10\n\t" : : "s31");
asm ("fcpys s10, s12\n\t" : : "s10");
asm ("fcpys s11, s13\n\t" : : "s11");
asm ("fcpys s12, s14\n\t" : : "s12");
asm ("fcpys s13, s15\n\t" : : "s13");
asm ("fcpys s14, s9\n\t" : : "s14");
asm ("fcpys s15, s31\n\t" : : "s15");
asm ("lds s9, %[mem]\n\t" : [mem]"m(x[i+9])" : "s9");
)
```

无法在循环中添加 `OpenMP parallel-for`，因为每个线程必须包含它自己的序言（`prolog`）和结尾（`epilogue`）。这排除了 `OpenMP` 的

### 2.9 优化 #2：降低 CPI 到 87

对于循环的自动调度机制，只要将迭代手动分配到每个线程，`OpenMP` 仍然适用。为了做到这一点，请根据线程数计算每个线程中 `$i$` 的第一个值和最后一个值。

在序言部分之前添加 `#pragma omp parallel private(i)`，并将序言、循环和结尾封装在花括号中。这告诉 `OpenMP` 运行时在每个线程中运行整个软件流水线实现的一个实例，并允许每个线程拥有变量 `$i$` 的私有版本。

接下来，在并行区域的第一行插入以下内容：

```c
i=omp_get_thread_num() * N / NUM_THREADS;
```

这将初始化每个线程的 `$i$`。在序言和结尾中引用此 `$i$` 变量。

然后将循环改为：

```c
for(;i<(omp_get_thread_num()+1) * N / NUM_THREADS; i+=5) {
```

序言和结尾将位于循环之前之后。序言是：

```asm
// prolog
// it0
asm("fldmias %[mem],s0,s1,s2,s3,s4,s5,s6,s7)\n\t" : [mem]r(&coeff[0]); "s0", "s1", "s2", "s3", "s4", "s5", "s6", "s7");
asm("fldmias %[mem],s16,s17,s18,s19,s20,s21,s22,s23)\n\t" : [mem]r(&coeff[0]); "s16", "s17", "s18", "s19", "s20", "s21", "s22", "s23");
asm("flds s9,[mem],m(x[i])\n\t" : "s9");
asm("fmacs s1,s9,s0\n\t" : : "s1");
asm("fmacs s2,s9,s1\n\t" : : "s2");
asm("fmacs s3,s9,s2\n\t" : : "s3");
asm("fmacs s4,s9,s3\n\t" : : "s4");
asm("fmacs s5,s9,s4\n\t" : : "s5");
asm("fmacs s6,s9,s5\n\t" : : "s6");
```

结尾是：

```asm
// epilog
// it7
asm("fsts s7,[mem]\n\t" : [mem]d[i]);
```

多核与数据级优化：OpenMP 和 SIMD

```asm
asm ("fmacs s7, s9, s6\n\t" : : "s7");
// it1
asm ("fldmias %[mem],s10\n\t" : [mem]r(&x[i+1]);
asm ("fldmias %[mem],s0,s1,s2,s3,s4,s6\n\t" : [mem]r(&coeff[0]); "s0", "s1", "s2", "s3", "s4", "s6");
asm ("fmacs s1,s10\n\t" : : "s1");
asm ("fmacs s2,s10\n\t" : : "s2");
asm ("fmacs s3,s10,s2\n\t" : : "s3");
asm ("fmacs s4,s10,s3\n\t" : : "s4");
asm ("fmacs s5,s10,s4\n\t" : : "s5");
asm ("fmacs s6,s10,s5\n\t" : : "s6");
// it2
asm ("fldmias %[mem],s11\n\t" : [mem]r(&x[i+2]);
// it2
asm ("fldmias %[mem],s0,s1,s2,s3,s4,s5\n\t" : [mem]r(&coeff[0]); "s0", "s1", "s2", "s3", "s4", "s5");
asm ("fmacs s1,s11,s0\n\t" : : "s1");
asm ("fmacs s2,s11\n\t" : : "s2");
```
