
由于这是一个固件更新，通常会有一个头部或尾部。看起来有一个偏移量的列表或之类的头部，但什么都不符合逻辑。继续向下滚动文件，在大约 `35000` 处，似乎有一个结构化数据块，后面是一个 `0xff` 块，并靠近一个 `16` 位的“尾部”：

```
03F1F0: 4B 95 74 64 64 63 13 14 00 00 00 30 3C C5 C6 ..t.d.c....k...
```

前 `8` 个字节看起来是一个很好的开始点。尝试了几个常见的 XOR 策略但一无所获。我注意到这些字节具有 `3`、`4` 或 `5` 的半字节，这会将字节置于可打印 ASCII 范围内。因此，每个字节的半字节（即左旋转 `4` 位）... ：：

```
03F1F0: 48 59 47 46 46 36 31 41 00 00 00 C3 C5 5C C6  HYGFK61A....
```

搞定！由于固件更新的标题是“HY USB Firmware Loader”，我认为这对了。将生成的文件加载到 IDA 中，使用 Cortex-M Thumb 2 设置，果如其然，我们在偏移 `0x0120` 处有有效的代码字符串，在偏移 `0x32121` 处有 ASCII 字符串。

总结：通过合并每个字节来解码这 `4` 位：

```
c = (((c & 0xf0) << 4) ^ ((c & 0xff) >> 4)) ^ 0xff
```

标签：反汇编 (上一个 Q) (下一个)，二进制分析 (上一个 Q) (下一个)，固件 (上一个 Q) (下一个)

## Q：专业逆向软件工程的目标是什么？

标签：反汇编 (上一个 Q) (下一个)

在专业层面，逆向工程的目的是什么？目标软件是什么？为什么？

对于正在执行新颖功能的相当复杂的编译代码，通过逆向工程对代码如何运行产生有意义的见解，似乎需要大量的专业知识、劳动和时间。特别是，我设聘佣胜任的汇编程序员极其困难且可能昂贵。然而，我完全不知道拥有资源做此事的实体想要将这些资源花在什么地方。

这是我的可能性列表...

- 1. 编写恶意软件
- 2. 编写反恶意软件
- 3. 也许分析竞争对手的产品？

这不是一个很好的列表。现实情况是怎样的？什么样的值得花费成本进行逆向工程？

查看 `0xC000022L` 回答中的注释以对问题进行完善。

标签：反汇编 (上一个 Q) (下一个)

用户：`praxe`

`praxe` 回答：

逆向工程通常用于许多方式。这里是涉及逆向工程的一些常见活动：

- 1. 恶意软件研究。没有逆向工程，很难确定恶意软件在做什么。
- 2. 逆向工程经常用于检测抄袭。
- 3. 法律取证。
- 4. 兼容性。通过逆向工程获取文件格式。
- 5. 漏洞研究。通过逆向工程来发现未文档的功能。
- 6. 修改程序。通过逆向工程来修复漏洞。
- 7. 分析保护程序。特别是当程序被保护时，自然需要逆向工程。
- 8. 源代码恢复。逆向工程来重构代码。
- 9. 分析竞争对手产品。逆向工程来获取源代码。
- 10. 接口。

`stolas` 回答：

作为一个专业的逆向工程师，我处理：

- 故障排除
- 漏洞利用开发
- 恶意软件分析
- 文档良好的 API

因此我们逆向这种程序，增加了你的知识。

标签：反汇编 (上一个 Q) (下一个)

## Q：从 IDA 中提取参数

标签：反汇编 (上一个 Q) (下一个)，`ida` (上一个 Q) (下一个)，`python` (上一个 Q) (下一个)

假设我们在 IDA 中有一个函数：

```
int __usercall(char* message, unsigned int count)
```

使用 IDAPython 提取参数的最快方法是什么，以便得到如下：

```
[['char*', 'message', 'ebp'], ['unsigned int', 'count']]
```

这不需要处理类似的情况：

```
void __usercall_sub_458b0@rax>(void __usercall function)@rax);
```

它应该给我类似：

```
['void ', ..., 'function', 'rax']
```

用户：`zach-riggle`

`zach-riggle` 回答：

我收到的 HexRays 支持解决方案并不依赖于解析 `getType` 获取的 C 字符串。

假设我们有一个函数原型：

```
int _cdecl main(int argc, const char *argv, const char *envp)
```

这是来自 ELF 文件，`x86`；内容被放在栈上。

然后，我可以执行操作：

```python
from idaapi import *
tif = tinfo_t()
get_tinfo2(here), .tif
True
fundacata = func_type_data_t(func)
tif.get_func_details(fundacata)
True
fundacata.size()
3
for i in range(fundacata.size):
    print("Arg %d: %s (of type %s, and of location: %s)") (i, fundacata[i].name, print_info(\Arg 0: argc (of type int, and of location: 1)
Arg 1: argv (of type const char **, and of location: 1)
Arg 2: envp (of type const char **, and of location: 1))
```

注意它显示位置类型为 `1`，对应于 'stack'：https://www.hex-rays.com/products/ida/support/sdkdoc/a_l_o_c____html

现在，假设我选择的原型如下：

```cpp
.text:0884ABA1; int _usercall main<eip>(int argc@<, const char **argv@<esp, const char **envp
```

那么：

## 跳过代码块（这里，tif）

```python
Python-tif.get_func_details(funcdata)
True
Python-tif.for i in range(funcdata.size):
    Python> print("Arg %d (of type %s, and of location: %s") % (i, funcdata[i].name, printf_into(
Pyth
Arg 0: argc (of type char **, and of location: 3)
Arg 1: argv (of type char **, and of location: 3)
Arg 2: envp (of type char **, and of location: 3)
```

参数位置现在是 `3`，对应于‘inline register’

（然后，我想使用 `reg1()` 来获取实际寄存器编号，以便知道参数是通过哪个寄存器传递的）

感谢 Hex Rays 的 Arnaud。

标签：disassembly (上一篇) (下一篇) ida (上一篇) (下一篇) python (上一篇) (下一篇)

## Q：理解循环反汇编

标签：disassembly (上一篇) (下一篇), binary-analysis (上一篇) (下一篇)

这是我正尝试理解的反汇编的循环代码：

跳过代码块

```cpp
#include <stdio.h>
#include <iostream>

using namespace std;

int main() {
    int i, arr[50], num;

    printf("\nEnter no of elements :\n");
    cin >> num;

    //将值读入数组
    printf("\nEnter the values :\n");
    for (i = 0; i < num; i++)
        cin >> arr[i];

    return 0;
}
```

这是反汇编代码：

```assembly
; int _cdecl main(int argc, const char **argv, const char **envp)
public
  main proc near

var_D8 = byte ptr -0D8h
num_of_element = dword ptr -10h
Counter = dword ptr -0Ch
var a = dword ptr -4
argc = dword ptr -0Ch
argv = dword ptr -10h
envp = dword ptr -10h

lea
and
push
mov\esp, 0xFFFFFF0h
push
dword ptr [ecx-4]
push
ebp
mov
ebp, esp
mov
ecx
sub
esp, 0E4h
call
mov
eax, [ebp+num_of_element]
mov\ecx, _2Z3sticcin; std::cin
sub
_2Nis1rsERi; std::istream::operator>>(int &)
call
mov
dword ptr [ecx], a
enterTheValues; "\nenter the values :"
printf
mov
[ebp-Counter], 0
jmp
short loc_40156F
```

![](img/6b9e3d3281d0838532edd532056c8b57_101_0.png)

```assembly
loc_40156F:
mov
eax, [ebp+num_of_element]
mov
[ebp-Counter], eax
jl
short loc_40154D
loc_40154D:
lea
eax, [ebp+var_D8]
mov
[ebp-Counter], eax
shl
edx, 2
mov
eax, edx; 为什么对 edx 左移？
mov
[esp+offset]
mov
ecx, _2Z3sticcin; std::cin
sub
_2Nis1rsERi; std::istream::operator>>(int &)
call
sub
esp, 4
add
[ebp-Counter], 1
```

你能解释一下高亮部分吗？`var_D8` 是干什么用的？编译器为什么要对 `edx` 左移？

标签：disassembly (上一篇) (下一篇), binary-analysis (上一篇) (下一篇)

用户：`vlad`

回答由 `spl3en`

`var_D8` 就是你的 `int arr[50]`。

你可以通过名字快速识别出它：`50 * sizeof(int) = 200 = 0xC8`。栈上的下一个变量是 `num_of_elements`，它位于栈上的 `-0x10`，因此我们拥有内存 `-0xD8` 和 `-0x10`，对应于该 `int` 数组。

以下是对后续指令的解释：

```assembly
lea eax, [ebp+var_D8] ; 获取数组第一个元素的地址。
mov edi, [ebp+Counter]; 获取当前元素索引。
shl edx, 2             ; 因为每个元素的大小为 4，将索引乘以 4
add eax, edi           ; eax[1] = 当前元素的地址
mov [esp], eax        ; 将其移动到栈中以便通过 std::cin 写入
```

`var_D8` 就是你的 `int arr[50]`。

你可以通过名字快速识别出它：`50 * sizeof(int) = 200 = 0xC8`。栈上的下一个变量是 `num_of_elements`，它位于栈上的 `-0x10`，因此我们拥有内存 `-0xD8` 和 `-0x10`，对应于该 `int` 数组。

以下是对这些指令的解释：

```assembly
lea eax, [ebp+var_D8] ; 获取数组第一个元素的地址。
mov edi, [ebp+Counter]; 获取当前元素索引。
shl edx, 2             ; 因为每个元素的大小为 4，将索引乘以 4
add eax, edi           ; eax[1] = 当前元素的地址
mov [esp], eax        ; 将其移动到栈中以便通过 std::cin 写入
```

## 问题

## Q：如何在反汇编程序中定位结构体？

标签：`ida` (上一个问题) (下一个), `assembly` (上一个问题) (下一个)

几个前前我参加了一个为期 `40` 小时的逆向工程课程。在教我们使用 IDA Pro 时，导师很快地在没有太多解释的情况下，演示了如何将 ASM 中的变量标记为结构体的成员，这基本上等同于 C/C++ 中旧式的 `struct`，并在代码的其余地方像对待一样处理它们。这对我来说非常有用。

然而，他涵盖的是如何识别结构体。你如何知道一组变量构成了一个结构体，而不仅仅是一组相关的变量？你如何能确定作者使用了 `struct`（或类似的东西）？

标签：`ida` (上一个问题) (下一个), `assembly` (上一个问题) (下一个)

用户：`kenb`

用户 `user1354557` 回答

在代码中你会发现表示结构体使用的常见模式。

## 偏移量解引用 (Dereferencing offsets):

如果你有一个指针在某个非零偏移处被解引用，你可能正在处理一个结构体。寻找如下模式：

```
mov eax, [ebp-8]      ; 将局部变量加载到 eax
mov ecx, [eax+8]      ; 解引用 eax+8 处的 dword
```

在这个例子中，我们有一个包含指针的变量，我们关注的是指针处某个特定偏移处的内存内容。这正是结构体的使用方式：使用指向结构体的指针，然后对指针进行某个偏移的解引用以访问特定成员。在 C 中，这种语法是：`pStruct->member_at_offset_8`。

旁记：不要将在某个变量偏移处的解引用与在栈指针 (`esp`) 或帧指针 (`ebp`) 偏移处的解引用混淆。当然，你可以将局部变量和函数参数看作一个巨大的结构体，但在 C 中，它们并没有被显式地定义为结构。

## 更微妙的指针偏移 (More subtle pointer offsets):

你实际上不需要解引用任何内容就能检测结构体成员。例如：

```
mov eax, [ebp-8]      ; 将局部变量加载到 eax
push 30h               ; num = 30h
push aSampleString     ; src = "Sample String"
add eax, 0Ch
push eax               ; dst = eax + 0xC
Call strncpy
```

在这个例子中，我们正从某个源拷贝最多 `0x30` 个字符到 `eax +0xC`（参见 `strncpy`）。这告诉我们 `eax` 可能指向一个在 `0xC` 偏移处具有字符串缓冲区（至少 `0xC` 字节）的结构体。例如，该结构体可能如下：

```c
struct _MYSTRUCT {
    DWORD a;      // +0x0
    DWORD b;      // +0x4
    DWORD c;      // +0x8
    CHAR d[0x30]; // +0xC
}
```

在这种情况下，示例代码看起来像：

```c
strncpy(&pMyStruct->d, "Sample String", sizeof(pMyStruct->d));
```

**旁记：** 有可能（尽管可能性不大）我们在 `0xC` 偏移处拷贝一个大字符串缓冲区，但你可以通过上下文确定这一点。例如，如果偏移量 `+0x8` 是一个整数，那么它肯定是一个结构体。但如果我们拷贝了一个固定长度为 `0xC` 的字符串到 `eax`，然后又拷贝另一个字符串到 `eax+0xC`，它可能是一个巨大的字符串。

## 所有读取/写入 (All reads / writes):

假设你在栈上有一个结构体（而不是指向结构体的指针）作为局部变量。大多数情况下，IDA 无法区分栈上的结构体和一组独立变量。如果你只从一个变量读取而不写入，或者（较小概率）只对一个变量写入而不读取，这就是你正在处理结构体的一个巨大信号。这是一个例子：

```
lea eax, [ebp+var_58] ; 将局部变量的地址加载到 eax
push eax
call some_function
mov eax, [ebp+var_54] ; 假设我们从未碰过 var_54...
test eax, eax ; ...但我们正在检查它的值！
jz jword...
```

## igor-skochinskinsky 的回答

这里有一些我经常使用的工具：

- Microsoft VC++ RTTI 和 EH 解析器脚本。有一个作为插件的重新实现版本（但我还没有尝试过）。
