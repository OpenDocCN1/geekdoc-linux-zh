
- 转换并赋值 `realloc(a)` 的返回值。关于这一点稍后将进行讨论。
- 与 `malloc(a)` 一样，检查返回值以确保它不是 `NULL`。任何内存分配例程都可能失败。

在扩展内存块时，`realloc(a)` 通常会分配一个大小合适的新块，将数据从旧块复制到新块，并返回指向新块的指针。

在缩小数据块时，`realloc(a)` 通常只需更新内部的管理信息并返回相同的指针。这避免了复制原始数据。但是，如果发生了这种情况，不要假设你仍然可以使用新大小之外的内存！

在这两种情况下，你可以假设如果 `realloc(a)` 没有返回 `NULL`，旧数据已经为你复制到了新的内存中。此外，旧指针不再有效，就像你调用 `free(a)` 处理它一样，你不应该再使用它。这对于该数据块中的所有指针都适用，而不仅仅是用于调用 `free(a)` 的那个特定指针。

你可能注意到，我们的示例代码使用了一个独立的变量来指向更改后的存储块。虽然有可能（但是是个坏主意）使用相同的初始变量，如下所示：

```c
coordinates = realloc(coordinates, new_amount);
```

这是一个坏主意，原因如下。当 `realloc(a)` 返回 `NULL` 时，原始指针仍然有效；继续使用该内存是安全的。然而，如果你重用同一个变量且 `realloc(a)` 返回 `NULL`，你就失去了指向原始内存的指针。该内存无法再被使用。更重要的是，该内存无法再被释放！这会导致内存泄漏，应尽量避免。

标准 C 版本的 `realloc(a)` 有一些特殊情况：当 `ptr` 参数为 `NULL` 时，`realloc(a)` 的行为类似于 `malloc(a)`，分配一块新的存储区。当 `size` 参数为 0 时，`realloc(a)` 的行为类似于 `free(a)`，释放 `ptr` 指向的内存。因为 (a) 这可能会令人困惑，且 (b) 旧系统未实现此功能，我们建议在意指 `malloc(a)` 时使用 `malloc(a)`，在意指 `free(a)` 时使用 `free(a)`。

这里有一个相对微妙且容易出错的“陷阱”⁴。考虑一个维护指向动态分配数据*静态*指针的例程，该例程偶尔需要扩展该数据。它也可能维护指向此数据的自动（即局部）指针。（为了简洁，我们省略了错误检查代码。在生产代码中，不要这样做。）例如：

```c
void manage_table(void)
{
    static struct table *table;
    struct table *cur, *p;
    int i;
    size_t count;
    ...
    table = (struct table *) malloc(count * sizeof(struct table));
    /* fill table */
    cur = & table[i];      /* point at i'th item */
    ...
    cur->i = j;             /* use pointer */
    ...
    if (some condition) {   /* need to grow table */
    count += count/2;
    p = (struct table *) realloc(table, count * sizeof(struct table));
    table = p;
    }

    cur->i = j;             /* PROBLEM 1: update table element */

    other_routine();        /* PROBLEM 2: see text */
    cur->j = k;             /* PROBLEM 2: see text */
    ...
}
```

这看起来很直接；*manage_table()* 分配数据，使用它，改变大小，等等。但有一些问题在你查看这段代码时并没有跳出来显眼地显示（无论是在页面上还是在屏幕上）。

在标记为“PROBLEM 1”的那一行中，*cur* 指针被用于更新表格元素。然而，*cur* 是基于 *table* 的*初始*值分配的。如果 *some condition* 为真且 *realloc()* 返回了不同的内存块，*cur* 现在指向的是原始的、已释放的内存！每当 *table* 改变时，指向该内存的任何指针都需要更新。这里缺少的是在 *table* 在调用 *realloc()* 后重新赋值之后的语句 `*cur = & table[i];*`。

标记为 `PROBLEM 2` 的两行甚至更微妙。特别是，假设 `other_routine()` 对 `manage_table()` 进行了*递归*调用。table 变量可能会被再次改变，完全不可见！从 `other_routine()` 返回后，`cur` 的值可能再次无效。

人们可能会认为（我们也是这样认为的）唯一的解决方案是意识到这一点，并在函数调用后提供带有适当注释的 `cur` 重新赋值。然而，Brian Kernighan 善意地纠正了我们。如果我们使用索引，指针维护问题甚至不会出现：

```c
  table = (struct table *) malloc(count * sizeof(struct table));
  /* fill table */
  ...
  table[i].i = j;                 /* Update a member of the i'th element */
  ...
  if (some condition) {   /* need to grow table */
    count += count/2;
    p = (struct table *) realloc(table, count * sizeof(struct table));
    table = p;
  }

  table[i].i = j;                 /* PROBLEM 1 goes away */
  other_routine();                 /* Recursively calls us, modifies table */
  table[i].j = k;                 /* PROBLEM 2 goes away also */
```

如果你拥有分配数据的原始指针的*全局*副本，使用索引并不能解决问题；在这种情况下，你仍然必须担心在调用 `realloc()` 后更新你的全局结构。

> **注意** 与 `malloc()` 一样，当你扩展一块内存时，从 `realloc()` 返回的新分配内存并非全零填充。如果必要，你必须使用 `memset()` 自行清除它，因为 `realloc()` 只分配新的内存；它不做其他任何事情。

### 3.2.1.5 分配并零填充：`calloc()`

`calloc()` 函数是 `malloc()` 的直接封装。它的主要优点是零初始化动态分配的内存。它还将大小计算工作委托给你，通过接受项目数量和每个项目的大小作为参数：

```c
  coordinates = (struct coord *) calloc(count, sizeof(struct coord));
```

至少在概念上，`calloc()` 的代码相当简单。以下是其中一种可能的实现：

```c
void *calloc(size_t nmemb, size_t size)
{
    void *p;
    size_t total;

    total = nmemb * size;         /* Compute size */
    p = malloc(total);           /* Allocate the memory */

    if (p != NULL) {             /* If it worked ... */
        memset(p, '\0', total); /* fill it with zeros */
    }
    return p;                    /* Return value is NULL or pointer */
}
```

许多有经验的程序员更喜欢使用 `calloc()`，因为这样可以彻底消除关于新分配内存内容的疑问。

此外，如果你知道需要零填充的内存，你应该使用 `calloc()`，因为 `malloc()` 返回的内存可能已经是零填充的。虽然你（程序员）无法知道这一点，但 `calloc()` 可以知晓并避免调用 `memset()`。

### 3.2.1.6 总结 GNU 编码标准

总而言之，以下是 GNU 编码标准关于使用内存分配例程的说法：

- 检查每次对 `malloc` 或 `realloc` 的调用，查看它是否返回了零。即使你正在缩小块，也要检查 `realloc`；在一个将块大小舍入为 2 的幂的系统中，如果你要求更少的空间，`realloc` 可能会获得不同的块。

- 在 Unix 中，如果 `realloc` 返回零，它可能会销毁存储块。GNU `realloc` 没有这个 bug：如果它失败，原始块保持不变。请假设该 bug 已修复。如果你希望程序在 Unix 上运行，并希望避免在这种情况下丢失数据，你可以使用 GNU `malloc`。你必须预期 `free` 会更改已释放块的内容。你想从该块中获取的任何内容，必须在调用 `free` 之前获取。

Richard Stallman 在短短三段话中提炼出了使用 `malloc()` 进行动态内存管理的重要原则。动态使用的

