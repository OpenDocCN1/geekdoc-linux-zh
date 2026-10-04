
```cpp
basic_string。这是为了兼容各种类型的字符元素。现在，至少支持char（标准字符）以及wchar_t（宽字符）。

因此，std::string是以8字节字符为基本类型的类，而std::wstring则是是以16/32位字符wchar_t为基本类型的类。

### MSVC

当字符字符串长度在16字符以内时，MSVC将字符串直接存储在缓冲区里，不再使用“指针+长度”的复杂结构。

这意味着在32位系统中，字符串至少占用24字节（16+4=24）个字节；在64位环境下，字符串至少占用32字节（16+8=32）个字节。如果字符串的长度超过16字符的，这16字节空间就相当于白浪费了。

```cpp
#include <string>
#include <stdio.h>

struct std_string {
    union {
        char buf[16];
        char* ptr;
    };
    size_t size; // AKA 'nsize' in MSVC
    size_t capacity; // AKA 'nalloc' in MSVC
};

void dump_std_string(struct std_string *p=(struct std_string&)&s) {
    printf("[%s] %zu capacity:%d\n", p->size>16 ? p->ptr : p->buf, p->size, p->capacity);
}

int main() {
    std::string s1="short string";
    std::string s2="string longer that 16 bytes";

    dump_std_string(s1);
    dump_std_string(s2);

    // that works without using c_str()
    printf("%s\n", &s1[0]);
}
```

源代码的功能应当不需要解释。

# 需要注意的是有几点：

只要字符串没有超过16个字符，编译器就不会使用堆（heap）存储字符串的缓冲区。在实际的程序中，数字字符串确实是短字符串。显然，微软研发人员将16个字符作为长短字符串的分隔点。

虽然我们没有在程序main()的最后调用成员函数c_str()，但是这个程序可以通过编译在屏幕上显示字符串的内容。

这就是为什么这个程序不能运转起来。

第一个字符串的小于16个字符，这个缓冲区实际位于string::string的起始地址（可视为结构体数据）。这个区域的数据，采用了标准的ASCII的数据结构。因此printf()函数在处理指针时直接处理了所有的ASCII字符串，所以程序会显示第一个字符串。

第二个字符串的长度大于16字节，更危险。编程人员很容易在此处忽略、忘记此时应该使用string的成员函数c_str()。之所以本例这样正常工作，是因为指向缓冲区的指针恰好位于结构的开始部分。某些可能在相当的时间里一直这么写代码，而一直不觉得有问题，直到他们遇到指向长字符串导致程序崩溃的时候，他们才会意识到问题的严重。

### GCC

GCC在实现std::string的时候使用了MSVC的变量——reference count。

另一个有趣的事是：指向std::string实例的指针，并不是指向结构的起始地址，而是指向字符串缓冲区的指针。文件libstdc++/include/bits/basic_string.h解释了这一问题。这是为了方便调试程序：

```cpp
+ The you want M_data pointing to the character &array and
* not the _Rep is so that the debugger can see the string
* contents. (Probably we should add a non-inline member to get
* _Rep for the debugger, so users can check the actual
* string length.)
```

- 所以使用_M_data (而不采用_MRep) 指向字符序列array，原因在于调试员能够看到字符串的内容。也许我们可以增加一个非内联的成员_MRep 用于调试，但是用户可以检查实际的字符串长度。

感兴趣的读者可以下载：
http://gcc.gnu.org/linedocs/libstdc++/libstdc++-html-USERS-4.4/a010.68.html

考虑到有关问题之后，我们调整了上一个小节使用的源程序：

指令令清单51.22 GCC例子

```cpp
#include <string>
#include <stdio.h>

struct std_string
{
    size_t length;
    size_t capacity;
    size_t refcount;
};

void dump_std_string(std::string &s)
{
    char *p1=(char(**))&s; // GCC type checking workaround
    struct std_string *p2=(struct std_string*)(p1-sizeof(struct std_string));
    printf("[%s] size:%d capacity:%d\n", p1, p2->length, p2->capacity);
}

int main()
{
    std::string s1="short";
    std::string s2="string longer than 16 bytes";

    dump_std_string(s1);
    dump_std_string(s2);

    // GCC type checking workaround
    printf("%s\n", (char(**))&s1);
    printf("%s\n", (char(**))&s2);
}
```

因为GCC的类型检查规则是非常苛刻的，所以我们不得不做很多对齐性的修改。即使这个程序的printf()函数同样可以在不依赖c_str()函数的情况下打出字符串内容。

# 一个更加复杂的例子

```cpp
#include <string>
#include <stdio.h>

int main()
{
    std::string s1="Hello, ";
    std::string s2="world!\n";
    std::string s3=s1+s2;

    printf("%s\n", s3.c_str());
}
```

指令清单51.23 MSVC 2012 编译的程序

```asm
$SG39512 DB 'Hello, '00H
$SG39514 DB 'world!', 0AH, 00H
$SG39581 DB 's', 0AH, 00H

$s2 = -72; size = 24
$s3 = -48; size = 24
$s1 = -24; size = 24
_main PROC
```

```asm
sub esp, 72
push OFFSET $SG39512
lea eax, DWORD PTR _s1$[esp+80]
mov DWORD PTR _s1$[esp+100], 15
mov DWORD PTR _s1$[esp+96], 0
mov BYTE _s1$[esp+80], 0
call ?assign@?$basic_string@DT?$char_traits@D@V
$allocator@D@2@std@QAV12@PBDIZ ; ✓
```

```asm
std::basic_string<char, std::char_traits, std::allocator<char>>::assign
```asm
push 7
push OFFSET $SG39514
lea eax, DWORD PTR _s2$[esp+80]
mov DWORD PTR _s2$[esp+100], 15
mov DWORD PTR _s2$[esp+96], 0
mov BYTE _s2$[esp+80], 0
call ?assign@?$basic_string@DT?$char_traits@D@V
$allocator@D@2@std@QAV12@PBDIZ ; ✓
```

```asm
std::basic_string<char, std::char_traits, std::allocator<char>>::assign
```asm
lea eax, DWORD PTR _s2$[esp+72]
push eax
```

```asm
lea eax, DWORD PTR _s1[esp+76]
push eax
lea eax, DWORD PTR _s3$[esp+80]
push eax
call ?assign@?$basic_string@DT?$char_traits@D@V
$allocator@D@2@std@QAV12@PBDIZ ; ✓
```

```asm
; inlined c_str() method:
cmp DWORD PTR _s3[esp+104], 16
lea eax, DWORD PTR _s3[esp+84]
cmoveae eax, DWORD PTR _s3[esp+84]
push eax
push OFFSET $SG39581
call _printf
```

```asm
main:
cmp DWORD PTR __s2[esp+92], 16
mov DWORD PTR _s2[esp+92], 15
mov DWORD PTR _s2[esp+88], 0
mov BYTE _s2[esp+72], 0
call ?assign@?$basic_string@DT?$char_traits@D@V
$allocator@D@2@std@QAV12@PBDIZ ; ✓
```

```asm
main:
cmp DWORD PTR _s1[esp+92], 16
mov DWORD PTR _s1[esp+92], 15
mov DWORD PTR _s1[esp+88], 0
mov BYTE _s1[esp+72], 0
call ?assign@?$basic_string@DT?$char_traits@D@V
$allocator@D@2@std@QAV12@PBDIZ ; ✓
```

```asm
main:
xor eax, eax
add esp, 72
ret
```

编译器没有采用原有模板。使用推来存储缓冲区，数据结构自然不同。ASCII字符串通常存储于程序的数据段，在执行的时候，assign方式构造s1和s2。通过运算符"+"构造s3。

请注意此处没有调用字符串的c_str()方式。因为代码紧凑，所以编译器把c_str()的代码（内联）到了此处：如果字符串的长度不足16字符，EAX寄存器将保留缓冲区的指针；否则它将提取字符串缓冲区指针。最后，程序调用了析构函数，用于释放字符串（大于16字符的字符串）占用的空间。如果字符串小于16，std::string对象完全存储于数据区域，随函数结束而自动释放。就如此，短字符串的处理更快，因为访问堆的操作要少一些。

GCC的处理方式更为简单。GCC不会把短字符串的文本缓冲区直接存储到string结构体。使用GCC 4.8.1解析上述程序，可以得到：

> 指令清单51.24 GCC 4.8.1的程序汇编

```asm
.LCO
    .string "Hello, "
.LC1
    .string "world!\n"
main:
    push ebp
    mov ebp, esp
    push edi
    push esi
    push ebx
    and esp, -16
    sub esp, 32
    lea ebx, [esp+28]
    mov edi, [esp+20]
    lea esi, [esp+24]
    mov DWORD PTR [esp+8], ebx
    mov esi, [esp+24]
    mov DWORD PTR [esp+4], OFFSET FLAT::.LCO
    mov DWORD PTR [esp], edi

    call _ZNSsc1EPkCRSaIcE
    mov DWORD PTR [esp+8], ebx
    mov DWORD PTR [esp+4], OFFSET FLAT::.LC1
    mov DWORD PTR [esp], esi

    call _ZNSsc1EPkCRSaIcE
```

```asm
mov DWORD PTR [esp+4], edi
mov DWORD PTR [esp], ebx
```

```asm
call _ZNSsCl1ERKSs

mov DWORD PTR [esp+4], esi
mov DWORD PTR [esp], ebx
```

```asm
call _ZNSs6appendERKSs

; inlined c_str:
mov eax, DWORD PTR [esp+28]
mov DWORD PTR [esp], eax
```

```asm
call _puts

mov eax, DWORD PTR [esp+28]
lea ebx, [esp+19]
mov DWORD PTR [esp+4], ebx
sub eax, 12
mov DWORD PTR [esp], eax
call _ZNSs4Rep10_M_disposeERKSaE
mov eax, DWORD PTR [esp+24]
mov DWORD PTR [esp+4], ebx
sub eax, 12
mov DWORD PTR [esp], eax
call _ZNSs4Rep10_M_disposeERKSaE
mov eax, DWORD PTR [esp+24]
mov DWORD PTR [esp+4], ebx
sub eax, 12
mov DWORD PTR [esp], eax
call _ZNSs4Rep10_M_disposeERKSaE
lea esp, [esp+20]
```

资深的C++人员都不会把std::string当作全局变量，但实际上定义的std::string。确实如此，我们来看下面这段程序：

```cpp
#include <stdio.h>
#include <string>

std::string s="a string";

int main()
{
    printf("%s\n", s.c_str());
}
```

实际上，在函数main()启动之前，全局就已经完成初始化了。指令清单51.25 MSVC 2012 (这里我们可以看到全局变量是如何构造的以及一个注册的)

```asm
??Es@YXZ PROC 'a string'
push 8
push OFFSET $SG39512
mov ecx, OFFSET ?s@3V$basic_string_DU?$char_traits@D@V
$allocator@D@2@std@D=A
call ?assign@?$s@3V$basic_string_DU?$char_traits@D@V
$allocator@D@2@std@QAV12@PBDIZ ; ✓
    pop ecx
    ret 0, 16
??Es@YXZ END
```
