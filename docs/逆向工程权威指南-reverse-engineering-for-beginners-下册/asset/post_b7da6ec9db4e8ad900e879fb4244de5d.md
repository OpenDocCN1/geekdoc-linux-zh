
```cpp
element at .end(): 6226002 4522072
3rd element: 5 6
2nd element: 1 2
1st element: 3 4
removing last element...
MyHead=00003CC258, Size=2
ptr=00003CC258 Next=00003CC288 Prev=00003CC270 x=6226002 y=4522072
ptr=00003CC288 Next=00003CC270 Prev=00003CC270 x=3 y=4
ptr=00003CC270 Next=00003CC258 _Prev=00003CC288 x=1 y=2
```

## C++11 std::forward_list单向链

std::forward_list和std::list的结构基本相同，只是它是单向链，它的迭代器（链式）只有“next”字段而没有“prev”字段。虽然双向链的内存开销变小了，但是无法进行逆向。

## 5.1.3 std::vector容器

我们将std::vector称为为POD容器的安全封装容器。其内部结构和标准字符std::string字符十分相似（参见5.1.1.4节）。它有一个数据缓冲区的专用指针，一个指向数据组组尾部的专用指针，以及一个指向分配缓冲区尾部的专用指针。

这种数组采取的每个元素彼此相邻的方式存储在内存之中，此点和常数数组没有任何区别（参见第18章）。新推出的C++11标准，为其定义了内置函数data()。std::vector::data()的作用和std::string中的.c_str()一样，用于返回缓冲区的地址。

这种数据结构利用堆/堆来存储数据缓冲区，而堆栈的空间消耗可能会比数组本身还要。

MSVC和GCC的实现原理基本相同，只是结构体的变量名称稍微有些不同。因此，在这里使用同一个例子来进行说明。下述源程序用于遍历std::vector的数据结构。

```cpp
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <functional>

struct vector_of_ints
{
    // Mynames:
    int *MyFirst;
    int *MyLast;
    int *MyEnd;
    // GCC structure is the same, but names are: _M_start, _M_finish, _M_end_of_storage
};

void dump(struct vector_of_ints *in) {
    printf("Myfirst=%p, _Mylast=%p, _Myend=%p\n", in->Myfirst, in->Mylast, in->Myend);
    size_t size=(in->Mylast-in->Myfirst);
    size_t capacity=(in->Myend-in->Myfirst);
    printf("size=%d, capacity=%d\n", size, capacity);
    for (size_t i=0; i<size; i++) {
        printf("element %d: %d\n", i, in->Myfirst[i]);
    }
}

int main() {
    std::vector<int> c;
    dump ((struct vector_of_ints*)void*)&c);
    c.push_back(1);
    dump ((struct vector_of_ints*)void*)&c);
    c.push_back(2);
    dump ((struct vector_of_ints*)void*)&c);
    c.push_back(3);
    dump ((struct vector_of_ints*)void*)&c);
    c.push_back(4);
    dump ((struct vector_of_ints*)void*)&c);
    c.reserve(6);
    dump ((struct vector_of_ints*)void*)&c);
    c.push_back(5);
    dump ((struct vector_of_ints*)void*)&c);
    c.push_back(6);
    dump ((struct vector_of_ints*)void*)&c);
    printf("%d\n", c.at(5)); // with bounds checking
    printf("%d\n", c[8]); // operator[], out of bounds checking
}
```

下面是用MSVC编译后的程序输出：

```
Myfirst=00000000, _Mylast=00000000, _Myend=00000000
size=0, capacity=0
Myfirst=0051CF48, _Mylast=0051CF4C, _Myend=0051CF4C
size=1, capacity=1
element 0: 1
Myfirst=0051CF58, _Mylast=0051CF60, _Myend=0051CF60
size=2, capacity=2
element 0: 1
element 1: 2
Myfirst=0051C278, _Mylast=0051C284, _Myend=0051C284
size=3, capacity=3
element 0: 1
element 1: 2
element 2: 3
_MyFirst=+0051C90, _Mylast=0051CA0, _Myend=0051CA0
size=4, capacity=4
element 0: 1
element 1: 2
element 2: 3
element 3: 4
_MyFirst=+0051B80, _Mylast=0051B90, _Myend=0051B90
size=4, capacity=6
element 0: 1
element 1: 2
element 2: 3
element 3: 4
element 4: 5
_MyFirst=+0051B80, _Mylast=0051B94, _Myend=0051B98
size=5, capacity=6
element 0: 1
element 1: 2
element 2: 3
element 3: 4
element 4: 5
_MyFirst=+0051B80, _Mylast=0051B98, _Myend=0051B98
size=6, capacity=6
element 0: 1
element 1: 2
element 2: 3
element 3: 4
element 4: 5
element 5: 6
```

从程序中看到，当主函数main()运行后并没有立即分配缓冲区。第一次调用push_back()函数时，它分配了缓冲区。此后，每次调用push_back()函数时，数组的空间和capacity都会增大，而且缓冲区的大小随之改变。这是因为每次调用push_back()函数都会重新分配空间。这种操作开销很大。想要提高效率，必须预测数组的大小并使用reserve()方式来预留空间。

最后一个数值是随机的。这里可以看到，std::vector的运算符[]不会检测索引是否越界。要进行边界检查，可以使用成员函数at()。虽然at()方法的运行较慢，但是它可以在下标越界时返回std::out_of_range错误提示。

我们来看它的汇编。使用MSVC 2012（启用Ob1选项）编译源程序，得到的：

```asm
# 指令清单 51.33 MSVC 2012 /GS- /Ob1
$SG2650 DB '%d', 0AH, 00H
$SG2651 DB '%d', 0AH, 00H
_this = -4 ; size = 4
Pos = 8 ; size = 4
?at@@vector$HV?$Allocator@H@std@QAAHI@Z PROC ;
std::vector<int,std::allocator<int>>::at@;
    this$ = ecx
    push ebp
    mov ebp, esp
    push ecx
    mov DWORD PTR $this$[ebp], ecx
    mov eax, DWORD PTR $this$[ebp]
    mov ecx, DWORD PTR $this$[ebp+4]
    mov eax
    sub edx, DWORD PTR [ecx]
    sar edx, 2
    cmp edx, DWORD PTR _Pos$[ebp]
    ja SHORT $LN1
    push OFFSET ?Q@_0BM@MNJKDPPO=invalid?vector?DMT$?DO$subscript
    call DWORD PTR __imp__X_out_range@std@YAXPFBD
$LN1@:
    mov eax, DWORD PTR $this$[ebp]
    mov ecx, DWORD PTR [eax]
    mov edx, DWORD PTR _Pos$[ebp]
    lea eax, DWORD PTR [ecx+edx*4]
$LN3@:
    mov ebp, esp
    pop ebp
    ret 4
?at@@vector$HV?$Allocator@H@std@QAAHI@Z END ;
std::vector<int,std::allocator<int>>::at;

c$ = -36 ; size = 12
$T1 = -24 ; size = 4
$T2 = -20 ; size = 4
$T3 = -16 ; size = 4
$T4 = -12 ; size = 4
$T5 = -8 ; size = 4
$T6 = -4 ; size = 4
main PROC
    push ebp
    mov ebp, esp
    sub ebp, 36
    mov DWORD PTR _c$[ebp], 0 ; Myfirst
    mov DWORD PTR _c$[ebp+4], 0 ; Mylast
    mov DWORD PTR _c$[ebp+8], 0 ; Myend
    lea eax, DWORD PTR _c$[ebp]
    push eax
    call ?dump@YAXPAUvector_of_ints@@@Z : dump
    add esp, 4
    mov DWORD PTR $T6[ebp], 1
    lea ecx, DWORD PTR $T6[ebp]
    push ecx
    lea ecx, DWORD PTR _c$[ebp]
    call ?push_back$vector@HV?$allocator@H@std@std@QAEX$$QAHZ : 
    std::vector<int,std::allocator<int>>::push_back
    lea edx, DWORD PTR _c$[ebp]
    push edx
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    mov DWORD PTR $T5[ebp], 2
    lea eax, DWORD PTR $T5$[ebp]
    push eax
    lea ecx, DWORD PTR _c$[ebp]
    call ?push_back$vector@HV?$allocator@H@std@std@QAEX$$QAHZ : 
    std::vector<int,std::allocator<int>>::push_back
    lea edx, DWORD PTR _c$[ebp]
    push edx
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    mov DWORD PTR $T4[ebp], 3
    lea eax, DWORD PTR $T4$[ebp]
    push eax
    lea ecx, DWORD PTR _c$[ebp]
    call ?push_back$vector@HV?$allocator@H@std@std@QAEX$$QAHZ : 
    std::vector<int,std::allocator<int>>::push_back
    lea edx, DWORD PTR _c$[ebp]
    push edx
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    mov DWORD PTR $T3[ebp], 4
    lea eax, DWORD PTR $T3$[ebp]
    push eax
    lea ecx, DWORD PTR _c$[ebp]
    call ?push_back$vector@HV?$allocator@H@std@std@QAEX$$QAHZ : 
    std::vector<int,std::allocator<int>>::push_back
    lea edx, DWORD PTR _c$[ebp]
    push edx
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    mov DWORD PTR $T2[ebp], 5
    lea eax, DWORD PTR $T2$[ebp]
    push eax
    lea ecx, DWORD PTR _c$[ebp]
    call ?push_back$vector@HV?$allocator@H@std@std@QAEX$$QAHZ : 
    std::vector<int,std::allocator<int>>::push_back
    lea edx, DWORD PTR _c$[ebp]
    push edx
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    mov DWORD PTR $T1[ebp], 6
    lea eax, DWORD PTR $T1$[ebp]
    push eax
    lea ecx, DWORD PTR _c$[ebp]
    call ?push_back$vector@HV?$allocator@H@std@std@QAEX$$QAHZ : 
    std::vector<int,std::allocator<int>>::push_back
    lea edx, DWORD PTR _c$[ebp]
    push edx
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    push 6
    lea eax, DWORD PTR _c$[ebp]
    call ?reserve@vector$HV?$allocator@H@std@QAEXI : 
    std::vector<int,std::allocator<int>>::reserve
    lea eax, DWORD PTR _c$[ebp]
    push eax
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    mov DWORD PTR $T2[ebp], 5
    lea eax, DWORD PTR $T2$[ebp]
    push eax
    ecdx
    lea eax, DWORD PTR _c$[ebp]
    call ?push_back@vector$HV?$allocator@H@std@QAEXSQAHZ : 
    std::vector<int,std::allocator<int>>::push_back
    lea edx, DWORD PTR _c$[ebp]
    push edx
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    mov DWORD PTR $T1[ebp], 6
    lea eax, DWORD PTR $T1$[ebp]
    push eax
    lea ecx, DWORD PTR _c$[ebp]
    call ?push_back@vector$HV?$allocator@H@std@QAEXSQAHZ : 
    std::vector<int,std::allocator<int>>::push_back
    lea edx, DWORD PTR _c$[ebp]
    push edx
    call ?dump@YAXPAUvector_of_ints@@Z : dump
    add esp, 4
    push 5
    lea eax, DWORD PTR _c$[ebp]
    call ?at@vector$HV?$allocator@H@std@QAEAAHI : 
    std::vector<int,std::allocator<int>>::at
    mov edx, DWORD PTR [eax]
    push edx
    mov OFFSET $SG2650, '%d'
    call DWORD PTR __imp_printf
    add esp, 8
    mov eax, 8
    shl eax, 2
    mov ecx, DWORD PTR _c$[ebp]
    mov edx, DWORD PTR [ecx+eax]
    push edx
    mov OFFSET $SG2651, '%d'
    call DWORD PTR __imp_printf
    add esp, 8
    lea eax, DWORD PTR _c$[ebp]
    call ?_Tidy@vector$HV?$allocator@H@std@IAEXXXZ : 
    std::vector<int,std::allocator<int>>::Tidy
    xor eax, eax
    mov esp, ebp
    pop esp
```

从我们可以看到，at() 方法检查下标边界以及异常处理的详细细节。后一个输出是printf() 函数直接从内存中提取的数值。它在取值的时候没有做任何越界检查。

有些读者可能会问，为什么标准向量的数据结构不像标准函数std::string中的那样，单独用一个字段记录size(大小)和capacity(体积)这类的信息呢？虽然笔者无法证实，但是笔者想相信是。at()在进行边界检查时效率更好吧。

GCC生成的编译指令让它如此分明，它比内联函数的实现还要快。

指令清单51.34 GCC 4.8.1 - fno-inline -small-functions - 01编译
