

```
mov dword ptr [esp4], offset a3rdElementDD; "3rd element: %d\n\n"
mov dword ptr [esp], 1
mov [esp8], eax
call _printf
mov esi, [esi+4]; operator--: 获取前一个指针
mov eax, [esi+0Ch]
mov [esp0Ch], eax
mov eax, [esp8]
mov dword ptr [esp4], offset a2ndElementDD; "2nd element: %d\n"
mov dword ptr [esp], 1
mov [esp8], eax
call _printf
mov eax, [esi+4]; operator--: 获取前一个指针
mov edx, [esi+0Ch]
mov [esp0Ch], eax
mov eax, [esp8]
mov dword ptr [esp4], offset a1stElementDD; "1st element: %d\n"
mov dword ptr [esp], 1
mov [esp8], eax
call _printf
mov dword ptr [esp], offset aRemovingLastEl; "正在移除元素..."
call puts
mov esi, [esp+14h]
mov [esp], esi
call _ZNSt8_detail15_List_node_base9_M_unhookEv;
std::detail::List_node_base::NM_unhook(void)
mov [esp], esi; void *
call _ZdlpV; operator delete (void *)
mov [esp], ebx
call _Zl13dump_List_valPj; dump_List_val(uint *)
mov [esp], ebx
call _ZNSt10_List_baseIa5ISEE8_M_clearEv;
std::List_base<a,std::allocator<a>>::NM_clear(void)
lea esp, [ebp-8]
xor eax, eax
pop ebx
pop esi
pop ebp
pop
retn
main endp
```

运行上面这个由 GCC 编译的程序，可以得到如下数据：

# 指令清单 51.30 整个输出

```
* 空列表: Next=0x00028fe90_Prev=0x00028fe90 x=3 y=0
* 包含3个元素的列表:
ptr=0x000349a90_Next=0x000349888_Prev=0x00028fe90 x=3 y=4
ptr=0x000349888_Next=0x00034b40_Prev=0x000349a90 x=1 y=2
ptr=0x00034b40_Next=0x00028fe90_Prev=0x000349888 x=5 y=6
ptr=0x0028fe90_Next=0x000349a90_Prev=0x00034b40 x=5 y=6
节点位于,_begin:
ptr=0x000349a90_Next=0x000349888_Prev=0x00028fe90 x=3 y=4
节点位于,_end:
ptr=0x0028fe90_Next=0x000349a90_Prev=0x00034b40 x=5 y=6
* 让我们从开始计数:
第1元素: 3 4
第二个元素: 1 2
第3元素: 5 6
.end() 处的元素: 5 6
* 让我们从末尾计数:
.end() 处的元素: 5 6
第3元素: 5 6
第二个元素: 1 2
第1元素: 3 4
正在移除最后一个元素...
ptr=0x000349a90_Next=0x000349888_Prev=0x00028fe90 x=3 y=4
ptr=0x000349888_Next=0x00034b40_Prev=0x000349a90 x=1 y=2
ptr=0x0028fe90_Next=0x000349a90_Prev=0x00034b40 x=5 y=6
```

在编译 `std::list` 时，MSVC 12 会存储链长度。此以外，它的实现方法与 GCC 基本一致。这意味着内置函数 `size()` 只需要从内存中一个值，速度相当快。不过这意味着每次增加/删除节点都需要调整这个值。

MSVC 的链存储结构和 GCC 有区别：![](img)

可见，GCC 构造的节点在链尾，而 MSVC 构造的节点在链首。使用 MSVC 12（启用 /GS 选项）编译上述程序，可以得到：

```
命令行 51.31 MSVC 12 参数/GS-/O1 优化的程序
_list = -16; size = 8
_list = -8; size = 8
_main PROC
```

```
sub esp, 16
push ebx
push esi
push edi
push 0
lea ecx, DWORD PTR [esp+36]
mov DWORD PTR [esp+40], 0; 分配第一个"垃圾"类型
call ?Buynode@U$List_alloc@Ua@@V$Allocator@Ua@@std@@QAEU?
V = ?List_node@Ua@PAX1@PAU2@Z; std::List_base<allocator<a>>::??Buynode
mov edi, DWORD PTR _imp_printf
push ebx
push OFFSET $465; * 空列表:
mov DWORD PTR [esp+32], ebx
lea eax, printf
mov DWORD PTR [esp+32]
push eax
call ?dump_List_val@
mov esi, ebx
add esp, 8
lea esi, DWORD PTR [esp+28]
push ecx
mov DWORD PTR [esi+4]
push esi
mov DWORD PTR [esp+40], 1; 新节点数据
mov DWORD PTR [esp+44], 2; 新节点数据; 分配新节点
call ?Buynode@U?$List_buy@Ua@@V$Allocator@Ua@@std@@QAEU?
V = ?List_node@Ua@PAX1@PAU2@Z; std::List_base<allocator<a>>::??Buynode; const
mov edi
mov ecx
mov DWORD PTR [esp+28], 3; 新节点数据
mov DWORD PTR [ecx], eax
mov esi
lea eax, esi
push eax
push DWORD PTR [esi+4]
lea ecx, DWORD PTR [esp+36]
push eax
mov DWORD PTR [esp+44], 4; 新节点数据; 分配新节点
call ?Buynode@U?$List_buy@Ua@@V$Allocator@Ua@@std@@QAEU?
V = ?List_node@Ua@PAX1@PAU2@Z;
```

```
std::List_buy<a:allocator<a>>:?Buynode<a> const &
mov DWORD PTR [esi+4], eax
mov ecx, DWORD PTR [eax+4]
mov DWORD PTR [esp+28], 5; 新节点数据
mov DWORD PTR [ecx], eax
lea eax, esi
push eax
push DWORD PTR [ebx+4]
lea ecx, DWORD PTR [esp+36]
push ebx
mov DWORD PTR [esp+44], 6; 新节点数据; 分配新节点
call ?$_BuynodeABua@@$List_buy_Ua@V?$Allocator<a>@std@@$QAEPU@?
call ?$_List_node@@UA@PAX1@PAU2ua@@Z
std::List_buy<a:allocator<a>>:?Buynode<a> const &
mov DWORD PTR [ebx+4], eax
mov ecx, DWORD PTR [eax+4]
push OFFSET $469; '* 包含3个元素的列表':
mov DWORD PTR [esp+36], 3
mov DWORD PTR [ecx], eax
call edi; printf
lea eax, DWORD PTR [esp+32]
push eax
push eax
call ?$_List_val@@UAXYPAI@@Z; dump_List_val
push OFFSET $431; ' .begin:'
call edi; printf
push DWORD PTR [ebx]; 获取变量 l1 指向的节点的下一个字段
call ?$_List_node@@UAXUList@@Z
push OFFSET $435; ' .end:'
call edi; printf
push ebx; 指向节点 l1 的指针
call ?$_List_node@@UAXUList@@Z
push OFFSET $437; '* 我们从开始计数:'
call edi; printf
mov esi, DWORD PTR [ebx]; operator++: 获取下一个指针
mov DWORD PTR [esi+12]
push DWORD PTR [esi+8]
push eax
push OFFSET $466; '第1元素: %d'
call edi; printf
mov esi, DWORD PTR [esi]; operator++: 获取下一个指针
mov DWORD PTR [esi+12]
push DWORD PTR [esi+8]
push eax
push OFFSET $468; '第二个元素: %d'
call edi; printf
mov esi, DWORD PTR [esi]; operator++: 获取下一个指针
mov DWORD PTR [esi+12]
push DWORD PTR [esi+8]
push eax
push OFFSET $450; '第3元素: %d'
call edi; printf
mov eax, DWORD PTR [esi]; operator++: 获取下一个指针
add esp, 64
push DWORD PTR [eax+12]
push DWORD PTR [ebx+8]
push OFFSET $452; '.end(): %d'
call edi; printf
push OFFSET $453; '我们从末尾计数:'
call edi; printf
push DWORD PTR [ebx]; 使用节点中的 x 和 y 字段
push DWORD PTR [ebx]
push OFFSET $460; '.end(): %d'
call edi; printf
mov eax, DWORD PTR [ebx]; operator--: 获取前一个指针
mov DWORD PTR [eax+12]
push DWORD PTR [ebx+8]
push OFFSET $464; '第二个元素: %d'
call edi; printf
mov eax, DWORD PTR [esi]; operator--: 获取前一个指针
mov DWORD PTR [esi+12]
push DWORD PTR [ebx+8]
push OFFSET $466; '第1元素: %d'
call edi; printf
add esp, 64
push OFFSET $467; '正在移除最后一个元素...'
call edi; printf
mov edx, DWORD PTR [ebx+4]
add, 4
; prev=next? 是唯一的元素，“垃圾”吗？
; 如果是，则删除它！
mp edx, ebx
je SHORT _LN349@main
mov ecx, DWORD PTR [edx+4]
mov eax, DWORD PTR [edx]
mov ecx, DWORD PTR [ecx], eax
mov eax, DWORD PTR [edx+4]
push edx
mov eax, DWORD PTR [ebx+4], DWORD PTR [eax+4]
call ??@YAXPA@2; operator delete
add esp, 4
mov edx, DWORD PTR [esp+32], 2
_LN349@main:
lea eax, DWORD PTR [esp+28]
push eax
call ?dump_List_val@YAXPAI@Z; dump_List_val
mov eax, DWORD PTR [ebx]
add esp, 4
mov DWORD PTR [ebx], ebx
mov DWORD PTR [ebx+4], ebx
cmp eax, ebx
je SHORT _LN412main
$LL414:main:
mov esi, DWORD PTR [eax]
push eax
call ?3@YPAX@Z; operator delete
add esp, 4
mov eax, esi
cmpl esi, ebx
jnne SHORT $LL414main
LN412:main:
push ebx
call ?3@YPAX@Z; operator delete
add esp, 4
xor eax, edi
pop edi
pop esi
pop ebx
add esp, 16
ret
0
_main ENDP
```

构造数据链的时候，MSVC通过“node”函数分配了虚拟节点的空间；此后，这个节点同样用于分配其他节点的存储空间。相比之下，GCC则会在局部存储链表的第一个节点。

指令清单.51.32 整个程序的输出

+   * 空列表:
MyHead=0x003CC258, _Size=0
ptr=0x0003CC258, Next=0x0003CC258 _Prev=0x0003CC258 x=6226002 y=4522072
* 包含3个元素的列表:
MyHead=0x003CC258, _Size=3
ptr=0x0003CC258, Next=0x0003CC288 _Prev=0x0003CC20 x=6226002 y=4522072
ptr=0x0003CC288, Next=0x0003CC270 _Prev=0x0003CC270 x=3 y=4
ptr=0x0003CC270, Next=0x0003CC2A0 _Prev=0x0003CC288 x=1 y=2
ptr=0x0003CC2A0, Next=0x0003CC258 _Prev=0x0003CC270 x=5 y=6
节点位于,_begin:
ptr=0x0003CC270 _Prev=0x0003CC258 x=3 y=4
节点位于,_end:
ptr=0x0003CC288 _Prev=0x0003CC2A0 x=6226002 y=4522072

