
```
for ( i = 0; i < n; i++) {
    x[i][j] = 0;
}
}
```

哪一个更好？在 C 语言中，第二个增量比第一个快。这意味着 `x[0][1]` 紧邻 `x[0][0]`。另一方面，`x[1][0]` 在 `x[0][0]` 之后有 `n` 个元素。当 CPU 将数据取入缓存时，它获取的不仅仅是几个字节，写入内存的行为也类似，因此第一个循环更有意义。如果你极其倒霉遇到了一个大到 RAM 无法容纳的数组，那么在第二个版本中可能会遇到虚拟内存抖动（thrashing）。这可能导致每次数组访问都变成一次磁盘访问。

## 16.11 将循环不变代码移到循环外

这可能是一个相当显而易见的优化。这是另一种情况，即研究编译器生成的代码可能会指出你忽略的某些循环不变代码。

## 16.12 消除递归

如果容易消除递归，那么它几乎总是提高效率。通常，消除“尾”递归是很的，即函数的最后一个动作是递归调用。这通常可以通过跳转到函数顶部来实现。另一方面，如果你尝试消除一个像快速排序（`quicksort`）这样会产生 2 次非平凡递归调用的函数的递归，你将被迫使用你自己的堆栈来“模拟”递归。这可能会让事情变慢。无论如何，这种效果都是微小的，因为在快速排序中花费在递归调用的时间很短。

## 16.13 消除栈帧

对于叶子函数（leaf functions），没有必要使用栈帧。事实上，如果你有非叶子函数，只调用了你的函数而没有调用其他函数，那么你可以从这两个函数中省略帧指针（frame pointers）。帧指针的唯一理由是为了调试。虽然要求将栈保持在 16 字节边界上，但这只有在具有局部变量（在栈上）的函数中才会成为问题。

## 16.14 内联函数

这可能是一个相当容易执行的优化。在某些情况下，编译器可以内联（`inline`）小函数，从而显著减少开销。

## 16.15 减少循环依赖

现代 CPU 允许超标执行（super-scalar execution）。如果指令流中的指令不依赖之前的结果，它们就可以一次执行多个。通过内联函数，代码变得更易读和易写。对于 1000000 个整数的测试，耗时 2.44 秒，展开后耗时 2.75 秒。

## 16.16 使用专用指令

对于位操作，我们已经看到使用专用指令（specialized instructions）可以利用 寄存器来处理 4。使用 AVX 寄存器可以获得更好的性能。这种技术将在后续章节中进行探讨。

## 练习题

- 1. 给出一个包含 `$x, y, z$` 的结构，计算 `$x, y, z$` 之间的距离。
- 2. 给出一个 2D 数组 `$M, y$`，计算 `$M$`。
- 3. 写一个使用块（blocked）的程序来计算 1 位。

# 在数组中计算 1 位

在本章中，我们将探索在数组中计算 1 位的多种方案。这是一个直接的 C 方案：

```c
long popcnt_array(long *a, int size) {
    int w, b;
    long n;
    n = 0;
    for (w = 0; w < size; w++) {
        word = a[w];
        n += word & 1;
        for (b = 1; b < 64; b++) {
            n += (word >> b);
        }
    }
    return n;
}
```

测试 1000 次调用 `popcnt_array`（包含 800000 字节）耗时 14.63 秒。开启优化级别 2 后耗时 5.29 秒，级别 3 耗时 5.37 秒。最后加上 `-funroll-all-loops` 耗时 4.74 秒。

该算法可以通过注意到经常被测试的字字高位可能是 0 来改进。我们可以将内部循环改为 `while` 循环：

```c
long popcnt_array(unsigned long *a, int size) {
  int w;
  unsigned long word;
  long n;
  n = 0;
  for (w = 0; w < size; w++) {
    word = a[w];
    while (word != 0) {
      n += word & 1;
      word >>= 1;
    }
  }
  return n;
}
```

使用最高优化选项，该版本耗时 3.34 秒。这是一个使用更好算法的实例。

## 17.2 使用汇编计算 1 位

将处理 64 位的循环展开为 64 次处理 1 位的操作并不困难。在下面的汇编代码中，每个字的四分之一位被放在 `rbx`、`rcx` 和 `rdx` 中。然后使用不同的寄存器累加这些四分之一位。这为计算机使用乱序执行提供了相当大的自由度。

```assembly
segment .text
global popcnt_array
popcnt_array:
  push rbx
  push rbp
  push r12
  push r13
  push r14
  push r15
  xor eax, eax
  xor ebx, ebx
  xor ecx, ecx
  xor edx, edx
  xor r12d, r12d
  xor r13d, r13d
  xor r14d, r14d
  xor r15d, r15d
count_words:
  mov r8, [rdi]
  mov r9, r8
  mov r10, r8
```

```assembly
mov     r11, r9
and     r8, 0xffff
and     r9, 16
shr     r10, 32
and     r10, 0xffff
shr     r11, 48
and     r11, 0xffff
mov     r12w, r8w
and     r12w, 1
add     rax, r12
mov     r13w, r9w
and     r13w, 1
add     rbx, r13
mov     r14w, r10w
and     r14w, 1
add     rcx, r14
mov     r15w, r11w
and     r15w, 1
mov     rdx, r15
%rep 15
shr     r8w, 1
mov     r12w, r8w
and     r12w, 1
add     rax, r12
shr     r9w, 1
mov     r13w, r9w
and     r13w, 1
add     rbx, r13
shr     r10w, 1
mov     r14w, r10w
and     r14w, 1
add     rcx, r14
shr     r11w, 1
mov     r15w, r11w
and     r15w, 1
add     rdx, r15
%endrep
add     rdi, 8
dec     rsi
jg      .count_words
add     rax, rbx
add     rax, rcx
add     rax, rdx
pop     r15
pop     r14
pop     r13
pop     r12
pop     rbp
pop     rbx
ret
```

这有一个遗憾的副作用：使用了一个重复 15 次的 `rep`（repeat）区域。这导致函数大小达到了 1123 字节。也许花费 2.52 秒来执行测试是值得的。目标文件比使用循环展开的 C 代码只大了 240 字节。

## 17.3 预计算每个字节中的位数

下一个算法的改进来自于意识到：我们可以预计算字节中所有可能的位模式的位数，并使用一个包含 256 字节的数组来存储每个可能字节的位数。然后，使用四字节字（quad-word）的 8 个字节作为位计数数组的索引，计算该四字节字中的位数并求和。

以下是用于计算数组中位的 C 函数，不包含计数数组的初始化：

```c
long popcnt_array ( long *a, int size ) {
    int b;
    long n;
    int word;
    n = 0;
    for (b = 0; b < size*8; b++) {
        word = ((unsigned char*)a)[b];
        n += count[word];
    }
    return n;
}
```
