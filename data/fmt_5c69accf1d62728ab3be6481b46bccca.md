
其中，第一列是文件偏移，中间是二进制操作码，最后一行是汇编列。

然后你可以获取第二列，计算其长度并除以 `2`，你就能得到了指令的字节长度。

回答者：`dougall`

许多人提到了英特尔手册，那是无价的参考资料，但非常厚重。我建议查看这个 OSDev wiki 页面，以了解指令在更简单的层面上是如何编码的。

对于所有实际的寻找指令长度的问题，我建议使用反汇编器。

函数挂钩（Function hooking）是一个有趣的挑战。这篇 MSDN 博客解释了一些困难之处。根据需要，使用操作系统的调试功能附加到进程、在函数处“打断点”并在单独的进程中实现你的挂钩可能更好。

标签：`assembly` (上一个问题) (下一个问题)，`x86` (上一个问题) (下一个问题)

# Q: 机器码中的哪些提示可以指向生成它的编译器？

标签：`assembly` (上一个问题) (下一个问题)

当我查看应用程序的机器码时，是否有可以从生成的机器码中识别出的提示和模式，可以指示是用哪种编译器（可能还有哪个版本）生成的？

知道用于生成应用程序的编译器有助于我更有效地从生成的对象文件反向工程出可能对应的源代码吗？如果是，是如何做到的？

标签：`assembly` (上一个问题) (下一个问题)，`x86` (上一个问题) (下一个问题)

用户：`willamkf`

回答：`byandrew`

该领域有一些学术研究，你想要的关键词是“工具链”(`toolchain`)。有一篇 Nate Rosen 撰写的关于此主题的优秀论文，讨论了在某些情况下使用启发式方法(`heuristics`)来识别编译器。

## 用户视角

从用户的角度来看，在采用分页机制的现代操作系统中，内存以所谓的“扁平模型”（`flat module`）工作。每个进程都以线性方式拥有自己的内存（`4GB`），因此基本上不需要段寄存器。

它们仍然是寄存器，当然可以可以用于各种其他的汇编操作。

`lunadir` 的回答为：

`FS` 指向异常处理链，`CS` 和 `DS` 由操作系统填充代码段和数据段。`SS` 是基础/堆栈段。据我记忆，`GS` 和 `ES` 是空闲的。

内核态或用户态区别并不大（它们被如 `XLAT`、`MOVS` 等指令使用，所以必须用相同的方式使用它们），但以防万全，我是在讨论用户空间的编程。

我之前没有注意到，你使用的是符号 `%fs` 而不是 `FS`，所以你可能在学习 Linux，那是另一个话题（你也可以在保护模式/实时模式上说明得更清楚）。你可以使用 `GS`，根据 stackexchange 上其他人的说法，Linux 显然会让你在 `FS` 和 `GS` 中分别获得“线程本地存储”和“处理器数据区域”。`CS`、`DS` 和 `SS` 应该是代码/数据/堆栈。

为了讨论起见，我不知道在 Mac 上你是否使用这些寄存器。

对于 64 位，这取决于情况：如果不在兼容模式（可以在其中执行 64 位和 32 位代码），则 `DS`、`ES` 和 `SS` 被忽略，且像 `POP SS` 这样的指令会导致错误。没有段（内存模型是扁平的），不应该有实时模式但我认为你指的是保护模式？），而且如果我没记错，没有硬件任务切换。

64 位模式下关于 `CS`、`FS`、`GS`（特别是隐藏部分）还有更多细节，但由于它们不经常使用，也许省略它们会更好。

你可以查看 AMD 家族处理器的手册，特别是在 64 位遗留模式的情况下：
`http://developer.amd.com/resources/documentation-articles/developer-guides-manuals/`

标签：`assembly` (Pre Q) (Next Q), `x86` (Pre Q) (Next Q), `linux` (Next Q)

## Q: 如何将这段 x86 汇编转换为 C 语言？

标签：`assembly` (Pre Q) (Next Q), `x86` (Pre Q) (Next Q), `c` (Pre Q) (Next Q)

这段 32 位 x86 汇编如何用 C 语言编写？

跳过代码块

```
loc_536FB0:

mov cl, [eax]

cmp cl, ' '

jb short loc_536FBC

cmp cl, ','

jnz short loc_536FBF

loc_536FBC:

mov byte ptr [eax], 

loc_536FBF

mov cl, [eax+1]

inc eax

test cl, cl
```

我已经发现出它循环了 23 次后退出。

标签：`assembly` (Pre Q) (Next Q), `x86` (Pre Q) (Next Q), `c` (Pre Q) (Next Q)

`user1365830` `igor-skochinsky` 的回答为：
这样的代码片段很难手动反编译。让我们试试吧。

你已经发现 `cl` 持有一个字符，这意味着它是从一个指针读取字符数组。我们把它称为 `p`。现在让我们对每条语句进行翻译：

```
11:

mov cl, [eax]    ; cl = *
cmp cl, ' '      ; if (cl < ' ')
jb short 12      ; goto 12
cmp cl, ','      ; if (cl = ',')
jnz short 13     ; goto 13
12:
mov byte ptr [eax], '*' ; p = '*'
13:
mov cl, [eax+1]  ; cl = *(p+1)
inc eax
test cl, cl       ; if (cl != 0)
```

清理后的：

```
l1:
cl = '*p';
if ( cl < ' ' ) goto 12;
if ( cl != ' ' ) goto 13;
l12:
*p = ' ';
l13:
cl = *(p+1);
p = p + 1;
```

现在剩下一个 `goto`。

```
void _fastcall inline RemoveChars(char* szInput) {
    int i;
    for (i = 0; i < 23 && szInput; ++i) {
        if (*szInput < '<' || *szInput == ',')
        *szInput = ',';
    }
}
```

标签：`assembly` (Pre Q) (Next Q), `x86` (Pre Q) (Next Q), `c` (Pre Q) (Next Q)

## Q: 为什么函数指针在声明于 buffer 之前被覆盖了？

标签：`assembly` (Pre Q) (Next Q), `x86` (Pre Q) (Next Q), `linux` (Pre Q) (Next Q), `c` (Pre Q) (Next Q)

我正在做 wargames，level 3：我理解为什么这段代码 `strlen(argv[1])` 中存在栈溢出，但不理解为什么它会溢出函数指针。`functionpointer` 在栈上是在 `buffer[50]` 之前定义的。它是如何覆盖它的？

这是主代码：

```c
int main(int argc, char **envp)
{
    void (*functionpointer)(void) = bad;
    char buffer[50];

    if(argc == 2 || strlen(argv[1]) < 4)
        return 0;

    memcpy(buffer, argv[1]);
    memset(buffer, strlen(argv[1]));

    printf("This is exciting we're going to %p\n", functionpointer);
    return 0;
}
```

这是用于栈溢出的 shellcode：

```
level0x804a:~/levels/level03
This is exciting we're going 0x8044a
I'm so sorry, you're at 0x8044a and you want to be at 0x8047a
level103io:~/levels/103
111111111111111111111111111111111111111
This is exciting we're going 0x31313130
Segmentation fault
```

这是利用的跳转：

```
00084c8<main>:
00084c8    push   %eb
00084c9    89 55    mov    %esp,%eb
00084cb    83 7c    sub    $0x78,%sp
00084d0    e3 f4 f0    and    0xffffff,%sp
00084d4    b8 00 00 00 mov    $0,%eax
00084d6    29 c4    mov    %esp,%eax
00084da    c7 55 84 a4 04 00 mov    0x80484a(%ebp)
00084db    72 d8 02    cmp    0x6c(%ebp)+max34
00084e3    75 17    jne    0x8048fc
00084e5    8b 4c 24    mov    4(%ebp),eax
00084eb    8b c0    mov    %eax,%ebp
00084ef    89 04 24    mov    %eax,%esp
00084f3    e8 a7 ff ff    call   0x80439c<stren>
00084f7    f8 83    cmp    $0x2,%eax
```
