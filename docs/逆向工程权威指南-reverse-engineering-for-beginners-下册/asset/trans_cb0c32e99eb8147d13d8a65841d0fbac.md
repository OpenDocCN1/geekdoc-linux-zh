

```
mov     [esp, eax]
call    Z4dumpP14vector_of_ints ; dump(vector_of_ints *)
mov     dptr [esp+10h], 3
lea     eax, [esp+4], eax
mov     eax, [esp+14h]
mov     [esp, eax]
call    Zns6ctvectorisAIIEE9_push_backKI;
std::vector<int,std::allocator<int>>::push_back(
    int const&
lea     eax, [esp+14h]
mov     [esp], eax
call    Z4dumpP14vector_of_ints ; dump(vector_of_ints *)
mov     dptr [esp+10h], 4
lea     eax, [esp+10h]
lea     [esp+4], eax
mov     eax, [esp+14h]
mov     [esp], eax
call    Zns6ctvectorisAIIEE9_push_backKI;
std::vector<int,std::allocator<int>>::push_back(
    int const&
lea     eax, [esp+14h]
mov     [esp], eax
call    Z4dumpP14vector_of_ints ; dump(vector_of_ints *)
mov     ebx, [esp+14h]
mov     eax, [esp+1Ch]
sub     eax, 17h
cmp     short loc_80001CF
ja      edi, [esp+18h]
mov     edi, ebx
sub     edi, ebx
sar     edi, 2
mov     dptr [esp], 18h
call    Znwj ; operator delete(uint)
mov     esi, eax
test    edi, edi
jz      short loc_80001AD
lea     eax, ds:0[edi*4]
mov     [esp+8], ebx         ; n
mov     [esp+4], ebx         ; src
mov     [esp], esi         ; dest
call   memmove
loc_80001AD: ; CODE XREF: main+F8
mov     eax, [esp+14h]
jz      short loc_80001BD
mov     [esp], eax          ; void *
call   _ZdlPv               ; operator delete(void *)
loc_80001BD: ; CODE XREF: main+117
mov     [esp+14h], esi
lea     eax, [esi+edi*4]
mov     [esp+18h], eax
add     esi, eax
mov     [esp+1Ch], esi

loc_8001CF: ; CODE XREF:DD
lea     eax, [esp+14h]
mov     [esp], eax
call    Z4dumpPl14vector_of_ints ; dump(vector_of_ints *)
mov     dword ptr [esp+10h], 5
lea     eax, [esp+10h]
mov     [esp+4], eax
lea     eax, [esp+14h]
mov     [esp], eax
lea     [esp], eax
call    Z2ST6vectorIsaIEE9push_backERKI ; 
       std::vector<int,std::allocator<int>>::push_back(
       int const&);
lea     eax, [esp+14h]
mov     [esp], eax
call    Z4dumpPl14vector_of_ints ; dump(vector_of_ints *)
mov     dword ptr [esp+10h], 6
lea     eax, [esp+10h]
lea     eax, [esp+4], eax
lea     eax, [esp+14h]
mov     [esp], eax
call    Z2ST6vectorIsaIEE9push_backERKI ; 
       std::vector<int,std::allocator<int>>::push_back(
       int const&);
lea     eax, [esp+14h]
mov     [esp], eax
call    Z4dumpPl14vector_of_ints ; dump(vector_of_ints *)
mov     eax, [esp+14h]
mov     edx, [esp+18h]
sub     edx, eax
cmp     edx, 17h
ja     short loc_8000246
mov     dword ptr [esp], offset aVector_m_range ;
"vector::M_range_check*"
call    Z2St20_throw_out_of_rangePKC;
std::throw_out_of_range(char const*)

loc_8000246: ; CODE XREF:main+1C
mov     eax, [eax+14h]
mov     [esp+8], eax
mov     dword ptr [esp+4h], offset AD ; "%d\n"
mov     dword ptr [esp], 1
call    __printf_chk
mov     eax, [esp+14h]
mov     eax, [esp+20h]
mov     [esp+8], eax
mov     dword ptr [esp+4h], offset AD ; "%d\n"
mov     dword ptr [esp], 1
```

```cpp
#include <map>
#include <set>
#include <string>
#include <iostream>

// structure is not packed
struct tree_node {
    tree_node *Left;
    tree_node *Parent;
    tree_node *Right;
    char Color; // 0 - Red, 1 - Black
    std::pair Myval; // calledval in std::set
    unsigned int first;
    const char *second; // not present in std::set
};

struct tree_struct {
    tree_node *Myhead;
    size_t Msize;
};

void dump_tree(struct tree_node *n, bool is_set, bool traverse) {
    printf("ptr=0x%p Left=0x%p Right=0x%p Color=%d Isnil=%d\n",
           n->Left, n->Parent, n->Right, n->Color, n->Isnil);
    if (n->Isnil == 0) {
        if (is_set)
            printf("%d\n", n->first);
        else
            printf("%d [%s]\n", n->first, n->second);
    }
    if (traverse) {
        if (n->Isnil == 1)
            dump_tree(n->Parent, is_set, true);
        else {
            if (n->Left->Isnil == 0)
                dump_tree(n->Left, is_set, true);
            if (n->Right->Isnil == 0)
                dump_tree(n->Right, is_set, true);
        }
    }
}

void dump_as_tree(int tabs, struct tree_node *n, bool is_set) {
    const char ALOT_OF_ABS = "\t\t\t\t";
    for (int i = 0; i < tabs; i++) printf("%s", ALOT_OF_ABS);
    if (is_set)
        printf("%d\n", n->first);
    else
        printf("%d [%s]\n", n->first, n->second);
    if (n->Left->Isnil == 0) {
        printf("%s-\n", ALOT_OF_ABS);
        dump_as_tree(tabs + 1, n->Left, is_set);
    }
    if (n->Right->Isnil == 0) {
        printf("%s-\n", ALOT_OF_ABS);
        dump_as_tree(tabs + 1, n->Right, is_set);
    }
}

void dump_map_and_set(struct tree_struct *m, bool is_set) {
    printf("ptr=0x%p Myhead=0x%p Mysize=%d\n", m, m->Myhead, m->Msize);
    dump_tree(m->Myhead, is_set, true);
    printf("As a tree:\n");
    printf("---\n");
    dump_as_tree(1, m->Myhead->Parent, is_set);
}

int main() {
    // map
    std::map<int, const char*> m;
    m[10] = "ten";
    m[20] = "twenty";
    m[3] = "three";
    m[101] = "one hundred one";
    m[100] = "one hundred";
    m[12] = "twelve";
    m[107] = "one hundred seven";
    m[0] = "zero";
    m[1] = "one";
    m[6] = "six";
    m[99] = "ninety-nine";
    m[5] = "five";
    m[11] = "eleven";
    m[1001] = "one thousand";
    m[1010] = "one thousand ten";
    m[2] = "two";
    m[9] = "nine";
    printf("dumping m as map:\n");
    dump_map_and_set((struct tree_node**)&m, false);

    std::map<int, const char*>::iterator itl1 = m.begin();
    printf("m.begin():\n");
    dump_tree((struct tree_node**)&itl1, false, false);
    itl1 = m.end();
    printf("m.end():\n");
    dump_tree((struct tree_node**)&itl1, false, false);

    std::set<int> s;
    s.insert(123);
    s.insert(456);
    s.insert(11);
    s.insert(12);
    s.insert(100);
    s.insert(1001);
    printf("dumping s as set:\n");
    dump_map_and_set((struct tree_node**)&s, true);
    std::set<int>::iterator it2 = s.begin();
    printf("s.begin():\n");
    dump_tree((struct tree_node**)&it2, true, false);
    it2 = s.end();
    printf("s.end():\n");
    dump_tree((struct tree_node**)&it2, true, false);
}
```

从程序可以看到，GCC 缓冲区的增长方式与 MSVC 不同。具体来说，通过一个例子可以看到：由 MSVC 编译的程序都会把缓冲区增加 50%。

