

- (outer_struct.d) 值为3 的字节，以及其后 3 节的脏数数据。
- (outer_struct.c) 32位 word 数据 4。

## 21.6 结构体中的操作

### 21.6.1 CPUID

C/C++ 语言可以精确操作结构中的位。这能够帮助程序员大幅地节省程序的内存消耗。例如，`bool` 类型数据就需要 1 位空间。但是时间开销和空间效率不可兼得的，如果节约内存缓存，程序的性能就会下降。

以 CPUID 指令为例，该指令用于获取 CPU 及其特性信息。[8]

如果在执行指令之前设置 EAX 寄存器的值为 1，那么 CPUID 指令将按照排列格式在 EAX 寄存器中存储 CPU 的特征信息。

| 3:0 (bits) | Stepping |
| 7:4 (bits) | Model |
| 11:8 (4 bits) | Family |
| 13:12 (2 bits) | Processor Type |
| 19:6 (4 bits) | Extended Model |
| 27:20 (8 bits) | Extended Family |

MSVC 2010 没有 CPUID 宏，而 GCC 4.4.1 没有这个宏。所以，我们自己写一个函数，用 GCC 编译它。[9]

```cpp
#include <stdio.h>

#ifdef GNUC
static inline void __inline__ __cpuid(int code, int *a, int *b, int *c, int *d) {
	asm volatile("cpuid":"=a"(*a),"=b"(*b),"=c"(*c),"=d"(*d),"a"(code));
}
#endif
```

```cpp
#ifdef _MSVC_VER
#include <intrin.h>
#endif
```

```cpp
struct CPUID_1_EAX
{
    unsigned int stepping:4;
    unsigned int model:4;
    unsigned int family_id:4;
    unsigned int processor_type:2;
```

```cpp
    unsigned int reserved:2;
    unsigned int extended_model_id:4;
    unsigned int extended_family_id:8;
    unsigned int reserved2:4;
```

```cpp
};
int main()
{
```

```cpp
    struct CPUID_1_EAX *tmp;
    int b[4];
```

```cpp
#ifdef _MSC_VER
    __cpuid(b,1);
#endif
```

```cpp
#ifdef _GNUC
    cpuid(1, &b[0], &b[1], &b[2], &b[3]);
#endif
```

```cpp
tmp=(struct CPUID_1_EAX*)&b[0];
```

```cpp
printf("stepping=%d\n", tmp->stepping);
printf("model=%d\n", tmp->model);
printf("family_id=%d\n", tmp->family_id);
printf("processor_type=%d\n", tmp->processor_type);
printf("extended_model_id=%d\n", tmp->extended_model_id);
printf("extended_family_id=%d\n", tmp->extended_family_id);
```

```cpp
    return 0;
;
```

在 CPUID 将返回值存储到 EAX/EBX/ECX/EDX 之后，程序使用数组 `b[]` 收集相关信息。然后，我们通过指向结构体 `CPUID_1_EAX` 的指针，从数组 `b[]` 中获取 EAX 寄存器里的值。

换句话，我们将 32 位 `int` 数据分解为结构体数据，再从结构体中读取各项数据值。

MSVC

使用 MSVC 2008（启用 `/O` 选项）编译生成程序，可以获得所示的代码。

指令清单 21.25 Optimizing MSVC 2008

```asm
b = -16
_main
    PROC
    sub esp, 16
    push ebx
    xor ecx, ecx
    mov eax, 1
    cpuid
```

```asm
    push esi
    lea esi, DWORD [esp+24]
    mov ptr [esi], eax
    mov ptr [esi+4], ebx
    mov ptr [esi+8], ecx
```

```asm
    mov esi, DWORD [esp+24]
    mov eax, esi
    and eax, 15
    push esi
    push OFFSET "stepping=%d"
    call printf

    mov ecx, esi
    shr ecx, 4
    and ecx, 15
    push esi
    push OFFSET "model=%d"
    call printf

    mov edx, esi
    shr edx, 8
    and edx, 15
    push esi
    push OFFSET "family_id=%d"
    call printf

    mov eax, esi
    shr eax, 12
    and eax, 3
    push esi
    push OFFSET "processor_type=%d"
    call printf

    mov ecx, esi
    shr ecx, 16
    and ecx, 15
    push esi
    push OFFSET "extended_model_id=%d"
    call printf

    mov esi, esi
    shr esi, 20
    and esi, 25
    push esi
    push OFFSET "extended_family_id=%d"
    call printf
    add esp, 48

    xor eax
    pop ebx
    add esp, 16
ret
```

SHR 指令用于过滤寄存器右侧位。AND 指令用于筛选寄存器的特定位。现在使用 Debugger 调试程序。如图 21.6 所示，在执行 CPUID 之后，EAX/EBX/ECX/EDX 寄存器保存返回值。

| EAX | EBX | ECX | EDX |
| :--- | :--- | :--- | :--- |
| 00000000 | 74657079 | 67656730 | 25640000 |
| 00000010 | 60666461 | 67646567 | 67640000 |
| 00000020 | 60666465 | 67646564 | 00726F63 |
| 00000030 | 64657465 | 73746570 | 74797065 | 74656565 |

图 21.6 Debug：执行 CPUID 之后的寄存器情况

| EAX | EBX | ECX | EDX |
| :--- | :--- | :--- | :--- |
| 00000000 | 00000010 | 00000000 | 00000000 |
| 00000005 | 00000000 | 00000000 | 00000000 |
| 00000006 | 00000000 | 00000000 | 00000000 |
| 0000000B | 00000000 | 00000000 | 00000000 |
| 0000000E | 00000000 | 00000000 | 00000000 |
| 00000010 | 00000000 | 00000000 | 00000000 |
| 00000011 | 00000000 | 00000000 | 00000000 |
| 00000014 | 00000000 | 00000000 | 00000000 |
| 00000017 | 00000000 | 00000000 | 00000000 |
| 0000001A | 00000000 | 00000000 | 00000000 |
| 0000001D | 00000000 | 00000000 | 00000000 |
| 00000020 | 00000000 | 00000000 | 00000000 |
| 00000023 | 00000000 | 00000000 | 00000000 |
| 00000026 | 00000000 | 00000000 | 00000000 |
| 00000029 | 00000000 | 00000000 | 00000000 |
| 0000002C | 00000000 | 00000000 | 00000000 |
| 00000030 | 00000000 | 00000000 | 00000000 |
| 00000031 | 00000000 | 00000000 | 00000000 |

