
```c
((unsigned short *)(fbp + i*(row_size) + j*2) = (red << 11) | (green << 5) | blue);
```

Linux framebuffer 是一个零拷贝缓冲区，这意味着程序的单次写入就会更新显示器上的像素。根据第 1 节中的写内存带宽实验，我们的每秒帧数（fps）上限。

例如，树莓派的写带宽为 325 MB/s，而一个 $1920 \times 1080 \times 16$ 的帧由 $4,147,200$ 字节组成，因此程序可以达到 $1/(4,147,200/325 \times 20) = 82$ fps。

一旦完成 framebuffer 的操作，你应该取消映射并关闭文件：

```c
munmap(fbp, screensize);
close(fd);
```

## 3.2 仿射变换（AFFINE IMAGE TRANSFORMATIONS）

任何玩过视频游戏、在个人媒体设备上翻过虚拟封面或使用过图像编辑软件的人对图像变换的概念都很。图像变换描述了一种改变或扭曲图像的操作。特别是线性图像变换，用于旋转、缩放、剪切、反射或投影图像等操作。

假设像素的位置（表示为行和列值）存储为列向量 `c`。线性图像变换可以描述为 $2 \times 2$ 矩阵 `A`，并通过乘法应用到该像素上；`c' = A \cdot c` 是表示变换后图像中像素位置的列向量。

在*仿射变换（affine transformation）*中，矩阵 `A` 是 $3 \times 3$ 矩阵，并且必须向像素位置向量添加一个额外的元素。

例如，以下三个仿射矩阵允许图像绕 $X, Y, Z$ 维度顺时针旋转角度 $\theta$：

```
$A_x = \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta & \cos\theta \end{bmatrix}$
```

```
$A_y = \begin{bmatrix} \cos\theta & 0 & \sin\theta \\ 0 & 1 & 0 \\ -\sin\theta & 0 & \cos\theta \end{bmatrix}$
```

```
$A_z = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}$
```

仿射变换的效果可以通过组合这些矩阵来合并。例如，`A_{XYZ} = A_x \cdot A_y \cdot A_z`。

## 3.3 双线性插值（BILINEAR INTERPOLATION）

执行逆变换时，变换图像中的许多像素将对应源图像中的分数位置。由于源图像是在整数像素位置离散采样的，程序必须使用某种技术来计算像素之间的颜色。这种插值有多种方法，但从最简单的方法开始：双线性插值。

当逆变换将目标像素映射到分数源像素时，程序必须根据周围的采样像素来估计这个“虚拟”值。双线性插值的基本思想是二维空间内的分数坐标位于 2x2 像素块内部。插值像素可以通过这四个像素的加权平均值来计算，其中每个像素的权重是根据两个维度上的分数部分的函数计算的。

图 3.1 描述了这种情况，假设逆变换给了我们 $(i,j)$ 且 $i_{int} = i, i_{rac} = i - int$，$j_{int} = j, j_{rac} = j - j$。

权重计算如下：

```
$weight(i_{int}, j_{int}) = (1 - i_{rac}) \cdot (1 - j_{rac})$
weight(i_{int}+1, j_{int}) = (1 - i_{rac}) \cdot j_{rac}$
weight(i_{int}, j_{int}+1) = i_{rac} \cdot (1 - j_{rac})$
weight(i_{int}+1, j_{int}+1) = i_{rac} \cdot j_{rac}$
```

## 3.4 浮点图像变换（FLOATING-POINT IMAGE TRANSFORMATION）

图像变换和插值计算必须使用分数值进行，浮点似乎是一个显而易见的选择。使用浮点的问题是，每个变换像素的开始和结束都是像素位置和颜色值，两者都是整数。这需要在整数和浮点数之间进行类型转换，以

## 3.4 浮点图像变换

![](img/e6ebc663bbb86c6e7bf9ef22ad136e6f_115_0.png)

- 图 3.1 分数源像素。

中间计算。在整数和浮点数之间的类型转换需要使用高延迟的转换指令。

为了表征这些操作所增加的开销，首先使用浮点数实现图像变换，并使用性能计数器测量其性能。

我们的目标是生成一段视频，视频由一系列帧组成，描述图像绕所有三个轴平滑旋转。从图形上看，这将表现为 2D 图像在 3D 空间中旋转。

为了实现这一点，可以在每一帧中逐渐改变图像的 X、Y 和 Z 旋转角度。对于此程序，你需要在每一帧之前调用一个函数，根据给定的 X、Y 和 Z 旋转角计算变换矩阵。由于该函数每帧只调用一次（而不是每个像素调用一次），预计它对性能的影响是微乎其微的。

以下函数将作为 X、Y、Z 角的函数计算变换矩阵，并将变换矩阵的前两行和第一列作为数组 `c_row` 和 `c_col` 返回：

```c
void calc_coeffs(float c_row[2], float c_col[2], float scale, float rot_x, float rot_y, float rot_z) {
    int i, j, k;
    float rotm_x[3][3] = {{1.0, 0.0, 0},
                          (0, 1.0/cos(rot_x), tan(rot_x)},
                          (0, tan(rot_x), -1.0/cos(rot_x))};
    float rotm_y[3][3] = {{1.0/cos(rot_y), 0, -tan(rot_y)},
                          (0, 1.0, 0),
                          (tan(rot_y), 0, 1.0/cos(rot_y))};
    float rotm_z[3][3] = {{cos(rot_z), -sin(rot_z), 0},
                          (sin(rot_z), cos(rot_z), 0},
                          {0, 0, 1.0}};
    float tempm0[3][3], tempm1[3][3], tempm2[3][3], sum;

    for (i=0; i<3; i++) // (temp = Ax * Ay)
        for (j=0; j<3; j++) {
            sum=0.0;
            for (k=0; k<3; k++) sum+=rotm_x[i][k]*rotm_y[k][j];
            tempm0[i][j] = sum;
        }
    for (i=0; i<3; i++) // (temp = temp * Az)
        for (j=0; j<3; j++) {
            sum=0.0;
            for (k=0; k<3; k++) sum+=tempm0[i][k]*rotm_z[k][j];
            tempm1[i][j] = sum;
        }
    c_row[0] = tempm1[0][0];
    c_row[1] = tempm1[0][1];
    c_col[0] = tempm1[1][0];
    c_col[1] = tempm1[1][1];
}
```

### 3.4.1 加载图像

首先将源图像加载到内存中。在网上找一个合适的图像，例如常用于图像处理工作的著名的 512 像素 512 像素“Lena”图像的彩色版本。首先，你需要使用工作站上的图像编辑工具将图像转换为 PPM 格式。

PPM 文件格式是一种未压缩或“原始”格式，在不需要任何特殊图像库的情况下，在程序中读取和写入非常简单。

PPM 文件包含 ASCII 文本和二进制数据。文件开头有一个由 ASCII 文本组成的头部。头部之后是二进制数据，按行升序顺序（从上到下）表示图像的每一行。每一行由按列升序顺序（从左到右）排列的像素组成。每个像素通常存储为三个连续的字节，分别对应红、绿、蓝（RGB）颜色通道。

PPM 头部包含以下由空白字符（空格、制表符、换行符、行）分隔的 ASCII 值：

1. 格式的“魔数” P6，

2. 列数，

3. 行数，以及

4. 最大颜色值（通常为 255）。

PPM 文件还可以包含以 # 开头的注释行。
