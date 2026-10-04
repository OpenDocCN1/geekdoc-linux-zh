basic_string 。这是为了兼容各种类型的字符元素。现在，至少支持char（标准字符）以及wchar_t（宽字符）。

因此，std::string是以8字节字符为基本类型的类，而std::wstring则是是以16/32位字符wchar_t为基本类型的类。

MSVC

当字符字符串长度在16字符以内时，MSVC将字符串直接存储在缓冲区里，不再使用“指针+十长度”的复杂结构。

这意味着在32位系统中，字符串至少占用24字节（16+4=24）个字节；在64位环境下，字符串至少占用32字节（16+8=32）个字节。如果字符串的长度超过16字符的，这16字节空间就相当于白浪费了。

```
#include <string>
#include <stdio.h>

struct std_string {
    union {
        char buf[16];
        char* ptr;
    };
    size_t size; // AKA 'Mysise' in MSVC
    size_t capacity; // AKA 'Myres' in MSVC
};

void dump_std_string(struct std_string *p=(struct std_string&)&s) {
    printf("%s] %zu capacity:%d\n", p->size>16 ? p->ptr : p->buf, p->size, p->capacity);
}

int main() {
    std::string s1="short string";
    std::string s2="string longer that 16 bytes";

    dump_std_string(s1);
    dump_std_string(s2);

    // that works without using c_str()
    printf("%s\n", &s1[0]);
}}
```