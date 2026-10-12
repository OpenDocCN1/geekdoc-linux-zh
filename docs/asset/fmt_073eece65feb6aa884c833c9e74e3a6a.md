
```asm
DEFB    26h,30h,32h,26h,30h,32h,0,0,32h,72h,73h,32h,72h,73h,32h
        60h,61h,32h,40h,40h,32h,42h,45h,32h,42h,45h,32h,4C0
        52h,4Ch,52h,5Ch,5Dh,5Eh,5Fh,59h,5Ch,5Dh,5Eh,5Fh,5Ch
        66h,67h,32h,72h,73h,4C0,4C0,45h,45h,45h,57h,52h,50h,CC0h
        13h,80h,0,19h,80h,81h,32h,82h,80h,CC0h,0FFh

T$58C:
DEFB    80h,72h,66h,54h,56h,60h,56h,60h,51h,56h,51h,66h
        54h,56h,58h,5Ch,72h,56h,60h,56h,4Eh,54h,51h,60h,51h,51h
        5Eh,5Eh,56h,56h,50h,50h,72h,66h,60h,4Eh,5Ch,51h,56h,51h,66h
        51h,51h,54h,56h,54h,56h,56h,72h,4C0,60h,56h,4Eh,54h,60h
        56h,66h,60h,56h,56h,56h,5Eh,5Eh,56h

        ; Game restart point
        
START:  XOR     A
        LD      (RESET),A
        LD      (XEMP),A
        LD      (REDO),A
        LD      (B$458),A
        LD      (B$459),A
        LD      A,2           ;Initial lives count
        LD      (LIVES),A
        LD      HL,T$45C
        SET     0,(HL)
        LD      HL,SCREEN
        LD      DE,SCREEN+1
        LD      BC,77FB       ;Clear screen image
        LD      (HL),0
        LDIR
        LD      HL,0A000h     ;Title screen bitmap
        LD      DE,SCREEN
        LD      BC,4096
        LDIR
        LD      HL,SCREEN+80h + 1*32 + 29
        LD      DE,MAM03+44
        CALL        C,0
        LD      (EMPKP
        LD      HL,0FC00h   ;Attributes for the last room
        LD      DE,ATTR   ;top third
        LD      BC,716
        LDIR
        LD      HL,09E00h   ;Attributes for title screen
        LD      BC,512      ;(bottom two-thirds)
        LDIR
        LD      BC,31
        RET
B$6621:  XOR     A
        IN      E,(C)
        OR      E
        DJNZ    B$6621    ;8+03
        AND     230h
        JR      NZ,B$662F    ;8+07
        LD      A,1
```

## C++ 注释

在 C++ 中注释涉及使用双斜杠 `//` 或斜杠和星号 `/*`。你之前已经看过一些简短的示例，以下是它们的工作方式。

### 步骤 1

以 Hello World 代码为例，你可以轻松使用双斜杠对代码的不同部分进行注释：

```cpp
//My first C++ program

cout << "Hello, world!\n";
```

![](img/4aefeb2d095f688b34af6207870c5f39_50_0.png)

### 步骤 2

然而，你也可以在代码行的末尾添加注释，以更好地描述正在发生什么：

```cpp
cout << "Hello, world!\n"; //This line outputs the words ‘Hello, world!’. The `\n` denotes a new line.
```

注意，你不需要在注释末尾加分号。这是因为它是代码中被编译器忽略的一行。

![](img/4aefeb2d095f688b34af6207870c5f39_50_1.png)

### 步骤 3

你可以使用斜杠和星号注释掉多行代码：

```cpp
/* This comment can
cover several lines
* without the need to add more slashes */
```

只需记住用相反的星号和斜杠结束块注释。

![](img/4aefeb2d095f688b34af6207870c5f39_50_2.png)

### 步骤 4

注释时要小心，特别是对于块注释。很容易忘记添加闭合的星号和斜杠，从而否定落在注释块内的任何代码。

![](img/4aefeb2d095f688b34af6207870c5f39_50_3.png)

### 步骤 5

显然，如果你尝试构建并执行代码，它会报错，抱怨缺少用于结束代码块的右大括号 `}`。如果你犯了这个错误好几次，那么回头修正可能会很耗时。幸运的是，Geany 中的颜色编码有助于识别注释与代码。

![](img/4aefeb2d095f688b34af6207870c5f39_50_4.png)

### 步骤 6

对于块注释，在 C++ 中往每个新注释行添加一个星号是良好的实践。这也帮助你记得在继续代码之前关闭注释块：

```cpp
/* This comment can
* cover several lines
* without the need to add more slashes */
```

幸运的是，Geany 会自动完成此操作，但在使用其他 IDE 时请注意这一点。

![](img/4aefeb2d095f688b34af6207870c5f39_50_5.png)

# 变量

与使用 Python 相比，在 C++ 中变量的处理方式略有不同。在 Python 中，你只需简单声明 `a` 等于 `10`，变量即可被赋值。然而，在 C++ 中，变量在使用前必须声明其类型。

## 变量的声明

你可以通过在代码中使用语句来声明 C++ 变量。有多种不同的变量类型可以声明。以下是具体操作方法。

### 步骤 1

打开一个新的空白 C++ 文件，并输入常用的代码头文件：

```cpp
#include <iostream>
using namespace std;

int main()
{

}
```

![](img/4aefeb2d095f688b34af6207870c5f39_51_0.png)

### 步骤 2

从简单开始，创建两个变量 `a` 和 `b`，其中一个值为 `10`，另一个为 `5`。你可以使用数据类型 `int` 来声明这些变量。在大括号内输入：

```cpp
int a;
int b;

a = 10;
b = 5;
```

![](img/4aefeb2d095f688b34af6207870c5f39_51_1.png)

### 步骤 3

你可以编译并运行代码，但它除了将值 `10` 和 `5` 存储到整数 `a` 和 `b` 中之外，不会做太多事情。请忽略关于“变量已设置但未使用”的警告，代码仍然可以正常工作。为了输出变量的内容，请添加：

```cpp
cout << a;
cout << "\n";
cout << b;
```

`cout << "\n";` 部分只是在 `10` 和 `5` 的输出之间放置了一个新行。

![](img/4aefeb2d095f688b34af6207870c5f39_51_2.png)

### 步骤 4

当然，你可以声明一个新变量，命名为 `result` 并输出一些简单的算术运算：

```cpp
int result;
result = a + b;
cout << result;
```

按照截图所示，将上述内容插入到代码中。

![](img/4aefeb2d095f688b34af6207870c5f39_51_3.png)

### 步骤 5

你在声明变量时就可以立即为其赋值。你输入的代码可以替换为如下形式：

```cpp
int a = 10;
int b = 5;
int result = a + b;

cout << result;
```
