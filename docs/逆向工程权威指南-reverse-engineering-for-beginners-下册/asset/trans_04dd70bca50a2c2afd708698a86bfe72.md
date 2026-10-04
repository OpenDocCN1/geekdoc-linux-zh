

## 指令清单51.27 MSVC 2012 在退出之前，析构函数的调用过程

```
ret 0
main ENDP

??_Fs@YAXX PROC
push ecx
cmp DWORD PTR PTR?@s@3V$basic_string@DU$?char_traits@D@std@V$
$allocator@D2@$std@A+20, 16
jb SHORT LN23dynamic
mov esi
esi, DWORD PTR PTR?@s@3V$basic_string@DU$
$char_traits@D@std@V$allocator@D2@$std@A
lea ecx, DWORD PTR $2[esp+0]
call ??$07?Wrap_allocator@D@std@std@QAEXV
push OFFSET ?@s@3V$basic_string@DU$?char_traits@D@std@V
$allocator@D2@$std@A+20, 15
lea ecx, DWORD PTR $2[esp+12]
call ??$destroy@PAD?$Wrap_alloc@V
$allocator@Dstd@$std@QAEXAPAD@V
lea ecx, esi, $1[esp+8]
call ??$07?Wrap_alloc0V$allocator@D@std@std@QAEXV
push esi
add esp, 4
pop esi
LN23:dynamic:
mov DWORD PTR PTR?@s@3V$basic_string@DU$?char_traits@D@std@V
$allocator@D2@$std@A+20, 16
mov DWORD PTR PTR?@s@3V$basic_string@DU$?char_traits@D@std@V
$allocator@D2@$std@A+16, 0
mov BYTE PTR PTR?@s@3V$basic_string@DU$?char_traits@D@std@V
$allocator@D2@$std@A, 0
pop esi
ret 0
??_Fs@YAXX END
```

实际上，函数 `main()` 没有调用那个全局变量的构造函数，这部分任务是 CRT 在启动 `main(void)` 函数之前就已经完成的操作。不止如此，全局变量的析构函数由 `stdlib` 声明的 `atexit()` 函数提供，只有在 `main` 结束之后才会被调用。

GCC 的处理方法十分相似。经 GCC 4.8.1 编译上述源程序，可以得到：

```
main:
push ebp
mov esp, esp
and esp, -16
sub esp, 16
```

## 指令清单51.28 GCC 4.8.1 函数

```
mov     eax, DWORD PTR s
mov     DWORD PTR [esp], eax
call    puts
xor     eax, eax
leave
ret
.LC:
.string "a string"
.__sub_I_4:
sub     esp, 44
lea     eax, [esp+31]
mov     DWORD PTR [esp+8], eax
mov     DWORD PTR [esp+4], OFFSET FLAT:.LC
mov     DWORD PTR FLAT:ZNSsclIEpRCkSaIceE
mov     DWORD PTR [esp+8], OFFSET FLAT:_dso_handle
mov     DWORD PTR [esp+4], OFFSET FLAT:ZNSd1Ev
mov     DWORD PTR [esp], OFFSET FLAT:s
call    cxa_atexit
add     esp, 44
ret
.LFE64:
.size   __sub_I_s,.-__sub_I_s
.section .init_array,"aw"
.align  4
.long   __sub_I_s
.glob  s
.bss
.align  4
.type   s, @object
.size   s, 4
.zero  44
.hidden _dso_handle
```

但是 GCC 没有单独建立一个专用函数，而是把每个结构表的容器逐一传递给 `atexit()` 函数。

## 51.4.2 std::list

`std::list` 是众所周知的双向链表容器，它的每个元素可以通过指针（链域）串连接逻辑意义上的线性表。这种结构的每个元素都有 2 个指针，一个指针指向一个元素，另一个指针指向下一个元素。

链域的存在决定了，每个节点比单纯的数据节点元素多占用 2 个字节的空间，即 32 位系统下占用 8 字节，而 64 位系统下会占用 16 字节。

C++ 标准模板类只是给结构体扩展了“next”“previous” 指针，使之形成逻辑上的有序序列。

## 我们以 2 个变量组成的结构体为例，演示 std::list 链结构。

虽然 C++ 标准（ISO/IEC 14882:2011 (C++ 11 standard））没有明确这种数据结构的具体实现方法，但是 MSVC 编译器和 GCC 编译器不约而同地选择了几乎一致的实现方法。我们就以下源代码举例进行说明：

```cpp
#include <stdio.h>
#include <list>
#include <iostream>

struct a {
    int x;
    int y;
};

struct List_node {
    struct List_node* _Next;
    struct List_node* _Prev;
    int x;
    int y;
};

void dump_List_node(struct List_node *n) {
    printf("ptr=0x%p _Next=0x%p _Prev=0x%p x=%d y=%d\n", n, n->Next, n->Prev, n->x, n->y);
}

void dump_List_vals(struct List_node* n) {
    struct List_node* current=n;
    for (;;) {
        dump_List_node(current);
        current=current->Next;
        if (current==n) // end
            break;
    }
}

void dump_List_val (unsigned int *a) {
#ifdef MS_VER
    // GCC implementation does not have "size" field
    printf("_Myhead=0x%p, Mysize=%d\n", a[0], a[1]);
#endif
    dump_List_vals ((struct List_node*)a);
}
```

```cpp
int main()
{
    std::list<struct a> l;

    printf("* empty list:\n\n");

dump_List_val((unsigned int*)(void*)&l);
}
```

## GCC

我们首先讲解 GCC 编译器的编译方式。

运行上述程序时，将会得到很多输出数据。我们进行分段讲解：

- * empty list:
ptr=0x0028fe90 _Next=0x0028fe90 _Prev=0x0028fe90 x=3 y=0
此时它还是空链。虽然我们还未对其赋值，但是变量 x 和变量 y 已经有数据（也就是哨兵节点 dummy node）。而且，“next”和“prev”指针都指向该节点。
![](img/a13a1a3f805f74b2dec756_778.png)
在这个时候，迭代器 .begin（开始）和 .end（结束）值相等。然后程序创建了 3 个节点，此后整个表的内部数据变为：
- * 3-elements list: _Next=0x00003498 _Prev=0x0028fe90 x=3 y=4
ptr=0x000034a0 _Next=0x000034b0 _Prev=0x000034a0 x=1 y=2
ptr=0x00003498 _Next=0x0028fe90 _Prev=0x000034b0 x=5 y=6
ptr=0x0028fe90 _Next=0x000034a0 _Prev=0x000034b0 x=5 y=6
最后一个元素的地址是 0x0028fe90。在实际释放之前它的地址变化。这两个字段 x 和 y 仍然是随机的，这时的值是 5 和 6。巧妙的是，这些值和上一个元素相同。这种巧妙持续下去。此时 3 个节点内存分布：
![](img/a13a1a3f805f74b2dec756_880.png)
变量指向第一个节点的迭代器开始和结束。双向链表通常采用这种特殊节点（称为哨兵 sentinel node）实现。这种方法简化链结构并提升效率。迭代器其实指向节点的指针，而 list.begin() 和 list.end() 返回的值：
- node at .begin:
ptr=0x000034a0 _Next=0x0028fe90 x=3 y=4
- node at .end:
ptr=0x00003498 _Next=0x000034b0 _Prev=0x000034a0 x=5 y=6
事实上，最后一个节点的 Next 指向第一个节点，Prev 指向最后一个元素。因此很容易想到循环表。可以利用第一个指针（实例）找到最后一个节点，不必遍历整个链。利用这种结构，我们还可以插入其他节点。运算符“++”和“--”就是迭代器的 [当前节点->prev] 或 [当前节点->next] 值。反向迭代器（reverse iterators）的作用与其相似，只是相反。运算符“*”用于返回节点。在链表插入和删除节点时，我们只需要分配（或释放）节点的内存，然后更新相关的指针，即可保证表的有效性。在删除节点之后，相邻的迭代器可能会指向无效节点，此时迭代器就会失效。指向无效节点的迭代器又叫 dangling pointer。在 GCC 4.8 版本编译 std::list 实例，它存储了总数。这意味着内置函数 size() 的运行缓慢，因为它必须遍历完整表才能返回个数。因此，那些与节点数有关的所有函数 (n) 的时间开销接近底层。

## 指令清单51.29 GCC 4.8.1 参数-fno优化

```
main proc
push ebp
mov ebp, esp
push esi
push ebx
and esp, 0xFFFFFFFF
sub esp, 20h
lea ebx, [esp+10h]
mov [esp], offset s; empty list:
```

```
mov [esp+10h], ebx
mov [esp+14h], ebx
call   puts
mov [esp], _Z13dump_List_valPj ; dump_list_val(uint *)
lea    esi, [esp+18h]
mov    [esp+4h], esi
mov    [esp], ebx
dword ptr [esp+18h], 1 ; 为 new element
dword ptr [esp+1Ch], 2 ; 为 new element
call   ZN44listSEE10_push_frontERS0_
std::list<a,allocator<a>>>::push_front(a)
mov    [esp+4h], esi
mov    [esp], ebx
dword ptr [esp+18h], 3 ; 为 new element
dword ptr [esp+1Ch], 4 ; 为 new element
call   ZN44listSEE10_push_frontERS0_
std::list<a,allocator<a>>>::push_front(a)
mov    dword ptr [esp], 10h
dword ptr [esp+18h], 5 ; 为 new element
dword ptr [esp+1Ch], 6 ; 为 new element
call   Znwj ; operator new(uint)
cmp    eax, 0FFFFFFFF
jz    short loc_802a6
mov    ecx, [esp+1Ch]
mov    edx, [esp+18h]
mov    [eax+0Ch], ecx
mov    [eax+8], edx

loc_802a6: ; CODE XREF: main+86
mov    [esp+4h], esi
mov    [esp], eax
call   ZN28_detail_detail15_List_node_base7_M_hookEPS0_
std::detail::List_node_base::M_hook
mov    dword ptr [esp], offset a3ElementsList ; * 3-elements list:
mov    puts
mov    [esp], ebx
call   _Z13dump_List_valPj ; dump_list_val(uint *)
dword ptr [esp], offset aNodeAt_begin ; * node at .begin:
call   puts
mov    eax, [esp+10h]
mov    [esp], eax
call   Z14dump_List_nodeP9List_node ; dump_List_node(List_node *)
dword ptr [esp], offset aNodeAt_end ; * node at .end:
call   puts
mov    [esp], ebx
call   Z14dump_List_nodeP9List_node ; dump_List_node(List_node *)
dword ptr [esp], offset a1SCount ; * let's count
from the begin:
call puts
mov esi, [esp+10h]
mov eax, [esp+0Ch]
mov [esp+0Ch], eax
mov eax, [esp+8]
mov dword ptr [esp+4], offset alstElement ; 1st element: %d
%n
mov dword ptr [esp], 1
mov [esp+8], eax
call __printfchk
mov esi, [esp]; operator++: ->next pointer
mov eax, [esp+0Ch]
mov [esp+0Ch], eax
mov eax, [esp+8]
mov dword ptr [esp+4], offset a2ndElement ; 2nd element: %d
%n
mov dword ptr [esp], 1
mov [esp+8], eax
call __printfchk
mov esi, [esp]; operator++: ->next pointer
mov eax, [esp+0Ch]
mov [esp+0Ch], eax
mov eax, [esp+8]
mov dword ptr [esp+4], offset a3rdElement ; 3rd element: %d
%n
mov dword ptr [esp], 1
mov [esp+8], eax
call __printfchk
```

