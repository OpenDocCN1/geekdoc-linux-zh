
这种边界检查是否存在明显的开销？调用输入值的边界使用了`assert()`宏，性能影响非常。以`MSVC`为例，`Debug`版的`MSVC`还有`assert()`，而发行版的`MSVC`就不再使用了。`Windows`内核也有“`checked`”和“`free`”两个版本，前一个还在检查，后面的版本就不再使用。

## 18.6 多维数组

多维数组和线性数组在本质上是相同的。计算机内存是连续的线性空间，它可以与一维数组对应。分成多个一维数组后，多维数组与线性空间直接存储。例如，二维数组`a[3][4]`转化为`a[12]`这样的12个元素，如表18.1所示。

### 表18.1 使用多维数组

| 存储地址 | 元素 |
| :--- | :--- |
| 0 | [0] |
| 1 | [1] |
| 2 | [2] |
| 3 | [3] |
| 4 | [1] |
| 5 | [1] |
| 6 | [2] |
| 7 | [3] |
| 8 | [2] |
| 9 | [1] |
| 10 | [2] |
| 11 | [3] |

### 表18.2 二维数组在内存中的存储

在内存之中，3×4的二维数组依次存储为连续的12个元素，如表18.2所示。在上述线性数组中某个元素的内存存储时，可以将二维数组的第一个索引乘以4（矩阵宽度），加上第二个索引号。这种方式就是`C/C++`、`Python`所用的“行优先（`row-major`）”顺序。所谓行优先，就是先用第一行元素，然后再排列行。相应的，也有“列优先（`column-major`）”顺序。`Fortran`、`Matlab`、`R`语言使用了这种顺序。从性能和缓存的角度，存储（`scheme`）和组织（`data organization`）匹配最优。只要匹配，程序就可以连续访问数据，整体性能就会提高。如果程序以行的方式访问，应当以行优先的顺序数组；反之亦如此。

## 18.6.1 二维数组实例

本例用`char`构造二维数组，其中每个元素占用1字节。以行优先的顺序填充数据。下面例子将数组的第二行。

## 指令清单18.20 运行数据

```c
#include <stdio.h>

char a[3][4];

int main () {
    int x, y;
    // 清空数组
    for (x=0; x<3; x++)
        for (y=0; y<4; y++)
            a[x][y]=0;
    // 填充第二行
    for (y=0; y<4; y++)
        a[1][y]=y;
}
```
图18.7所示的3个红圈代表不同的行。我们可以看到第二行的值是0、1、2、3。

| Address | Hex dump |
| :--- | :--- |
| 00C33370 | 00 00 00 00 01 02 03 00 00 00 0E |
| 00C33380 | 02 00 00 00 C3 66 47 4E 00 00 00 0E |
| 00C33390 | 00 00 00 00 00 00 00 0E |
| 00C333A0 | 00 00 00 00 00 00 00 0E |
| 00C333BB 00 00 00 00 00 00 00 0E |

以列优先的顺序填充数据，第三列填充0、1、2。下列程序将数组的第三列填充0、1、2。

```c
#include <stdio.h>

char a[3][4];

int main() {
  int x, y;
  // 清空数组
  for (x=0; x<3; x++)
    for (y=0; y<4; y++)
      a[x][y]=0;
  // 填充第三列
  for (x=0; x<3; x++)
    a[x][2]=x;
}
```
图18.8所示的3个红圈代表不同的行。各行的列分别是0、1、2。

## 一维数组的方式访问二维数组

一维数组访问二维数组的方法有两种。

```c
#include <stdio.h>

char a[3][4];

char get_by_coordinates1(char array[3][4], int a, int b) {
    return array[a][b];
}

char get_by_coordinates2(char *array, int a, int b) {
    // 将输入数组视为一维数组
    // 4是数组宽度
    return array[a*4+b];
}

char get_by_coordinates3(char *array, int a, int b) {
    // 将输入数组视为指针
    // 计算地址，获取该处的值
    // 4是数组宽度
    return *(array+a*4+b);
}

int main() {
    a[2][3]=3;
    printf("%d\n", get_by_coordinates1(a, 2, 3));
    printf("%d\n", get_by_coordinates2(a, 2, 3));
    printf("%d\n", get_by_coordinates3(a, 2, 3));
}
```
编译并运行上述程序，观测到元素的对应数值。`MSVC 2013`的编译方法完全一致。

## 指令清单18.22 MSVC 2013 优化

```
get_by_coordinates1, get_by_coordinates2, get_by_coordinates3：
```
```c
char get_by_coordinates1(char array[3][4], int a, int b) {
    return array[a][b];
}

char get_by_coordinates2(char *array, int a, int b) {
    // 将输入数组视为一维数组
    // 4是数组宽度
    return array[a*4+b];
}

char get_by_coordinates3(char *array, int a, int b) {
    // 将输入数组视为指针
    // 计算地址，获取该处的值
    // 4是数组宽度
    return *(array+a*4+b);
}
```

```
get_by_coordinates1 PROC
    push    ebp
    mov     ebp, esp
    push    ebx
    mov     eax, DWORD [ebp+8]
    mov     edx, DWORD [ebp+12]
    mov     eax, DWORD PTR [eax+edx*4]
    pop     ebx
    pop     ebp
    ret
ENDP

get_by_coordinates2 PROC
    push    ebp
    mov     ebp, esp
    push    ebx
    mov     eax, DWORD PTR [ebp+8]
    mov     edx, DWORD PTR [ebp+12]
    shl     eax, 2
    add     eax, edx
    mov     eax, DWORD PTR [eax]
    pop     ebx
    pop     ebp
    ret
ENDP

get_by_coordinates3 PROC
    push    ebp
    mov     ebp, esp
    push    ebx
    mov     eax, DWORD PTR [ebp+8]
    mov     edx, DWORD PTR [ebp+12]
    shl     eax, 2
    add     eax, edx
    mov     eax, DWORD PTR [eax]
    pop     ebx
    pop     ebp
    ret
ENDP
```
