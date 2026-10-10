
```
*((float32x_t*)&bb((i+j)*4)));

vmlaq_f32(*(float32x_t*)&bb((i+j)*4));

*((float32x_t*)&ba((i+j)*4)));

dupq_n_f32(coeff));

*((float32x_t*)&a((i+j)*4)));

vmlaq_f32(*(float32x_t*)&a((i+j)*4));

*((float32x_t*)&a((i+j)*4)));

dupq_n_f32(coeff));
```

`a` 和 `b` 数组必须作为 `float32x4_t` 指针被引用，然后对向量输入和输出都进行解引用。此外，`coeff` 标量值必须使用重复（`vdupq`）内建函数从标量转换为向量。

高斯消元的下一步是使用类似的方法通过将上三角形的每个元素设置为零来完善矩阵：

- 1. 将元素 (2,3) 设置为零
- 2. 将元素 (1,2) 设置为零
- 3. 将元素 (1,3) 设置为零
- 4. 将元素 (0,1) 设置为零
- 5. 将元素 (0,2) 设置为零
- 6. 将元素 (0,3) 设置为零

| R0 | 1.0 | 0 | 0 | -0.6 | 0.3 | 0 | 0.1 |
| R1 | 0 | -3.0 | 0 | 0 | -0.9 | 0.7 | -0.8 | 0.5 |
| R2 | 0 | 0 | -10.3 | 0 | 1.1 | -4.3 | -2.5 | 2.9 |
| R3 | 0 | 0 | 0 | 0.9 | 1.2 | -1.0 | -1.2 |

得到结果：

| R0 | 1.0 | 0 | 0 | -0.6 | 0.3 | 0 | 0.1 |
| R1 | 0 | -3.0 | 0 | 0 | -0.9 | 0.7 | -0.8 | 0.5 |
| R2 | 0 | 0 | -10.3 | 0 | 1.1 | -4.3 | -2.5 | 2.9 |
| R3 | 0 | 0 | 0 | 0.9 | 1.2 | -1.0 | 0 |

## B.4 使用 NEON 优化浮点代码

可以使用以下循环进行操作：

```
for (i=2; i>=0; i--) {
    for (j=i+1; j<4; j++) {
        coeff = -a[i*4+j]/a[j*4];
        for (k=0; k<4; k++) {
            b[i*4+k]+=coeff * b[j*4];
            a[i*4+k]+=coeff * a[j*4];
        }
    }
}
```

再次，最内层循环可以用 NEON 内建函数替换：

```
*((float32x_t*)&b2[i*4]) =
    vmlaq_f32(*(float32x_t*)&b2[j*4]),
    *((float32x_t*)&b2[j*4]),
    dupq_n_f32(coeff));

*((float32x_t*)&a2[i*4]) =
    vmlaq_f32(*(float32x_t*)&a2[j*4]),
    *((float32x_t*)&a2[j*4]),
    dupq_n_f32(coeff));
```

最后一步是将每行除以其对角线值以完成单位矩阵：

- 1. 将元素 (0,0) 设置为 1 `R_{0,0}`
- 2. 将元素 (1,1) 设置为 1 `R_{1,1}`
- 3. 将元素 (2,2) 设置为 1 `R_{2,2}`
- 4. 将元素 (3,3) 设置为 1 `R_{3,3}`

得到如下结果：

| R0 | 1.0 | 0 | 0 | -0.6 | 0.3 | 0 | 0.1 |
| R1 | 0 | 1.0 | 0 | 0 | -0.2 | 0.3 | -0.2 |
| R2 | 0 | 0 | 1.0 | 0 | -0.1 | 0.4 | 0.2 |
| R3 | |00 | 0 |   .. | 1.. | -1.1 | -1.3 | 1.3 |

可以使用以下代码执行：

```
for (i=0;i<4;i++) for (j=0;j<4; j++) b[i*4+j] = a[i*4+j];
```

## B.5 NEON 内建函数总结

NEON 内建函数以字母 “v” 开头，并遵循以下命名方案：

```
v{prefix}{operation}{modifier}_{operand type}{operand width}
```

前缀是可选的，取决于内建函数，用于指定可用的舍入和饱和模式之一。

操作通常命名与内建函数的关联指令相同或相似。

修饰是可选的，用于不使用标准 64 位操作数和结果的内建函数。

操作数类型和宽度定义了每个向量的数据类型。

### B.5.1 前缀

允许的前缀值取决于操作。示例前缀包括：

- h（半）：将每个输出元素向右移
- d（双）：将每个输出元素向左移一位
- r（舍入）：对每个输出元素进行舍入（配合 hh 修饰使用）
- rh（舍入半）：将每个输出元素向右移一位并舍入
- q（饱和）：在溢出时将每个输出元素设置为最大值，在下溢时设置为最小值
- qd（饱和双倍）：饱和并双倍
- qrd（饱和、舍入和双倍）：饱和、舍入并双倍

### B.5.2 操作

NEON 操作可以分为几类基本类别：

算术：

- add, sub, mul：加、减、乘
- mla, mls：乘加、乘减
- padd, padd：（或加并累加）每个输入向量中的每对相邻元素
- recipe, rsqte：倒平方根估计（可以是浮点型）
- abs, neg：绝对值和取反（可以是浮点型）
- fma：融合乘加
- fms：融合乘减

位操作：

- shl, shr：左移、右移（逻辑的）？
- sra：位与移位累加。每个元素都移位。
- sli, sri：左移插入、右移插入。位不跨越元素边界。每个元素都移位。[这些支持前缀吗？]
- and（位与）、vbic（位清零）、veor（位异或）、vorn（位非或）、and vor（位或）：两个寄存器之间的位逻辑操作，并将结果置于目标器中
- mov, mvn：移动取反
- cls, cl, cnt：计算前导位、计算前导零、计算置位位

比较：

- ceq, cge, cgt, cle, clt：比较相等、大于或等于、大于、小于或等于、小于
- tst：对两个向量中的对应元素执行位与操作，如果与结果不为零，则将输出元素设置为全1，否则将输出元素设置为全零
- abd, aba：绝对差和累加
- max, min：将每个输出设置为两个对应元素的最大值或最小值
- pmin, pmax：将每个输出设置为两个向量中每对相邻元素的最大值或最小值

### B.5.3 修饰

默认情况下，内建函数使用 64 位输入和输出宽度，这意味着向量大小为 64/(操作数宽度)。以下是修饰：

- q 指定 128 位输入和输出宽度。

# 252 APPENDIX B NEON Intrinsic

* l specifies 64-bit input width but generates a 128-bit output width.
* hn stores the high half of each result element.
* q specifies 128-bit input and output width.
* l specifies 64-bit input width but generates a 128-bit output width.
* w allows the operation to accept one 128-bit operand and a second 64-bit operand and generate a 128-bit result.
* hn stores the high half of each result element.

### B.5.4 Operand type and width

operand width is:

* s8, s16, s32: signed integer
* u8, u16, u32: unsigned integer
* p8: integer
* f16, f32: floating point

# OpenCL reference

This appendix provides a reference for the most common features of OpenCL versions 1.1 and 1.2. These are older versions but are most likely to be supported on embedded GPUs at the time of writing.
