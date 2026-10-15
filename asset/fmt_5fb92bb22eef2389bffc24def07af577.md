
### `atomic_add_int()` 与 `atomic_inc_int()` 内联汇编示例

```c
int atomic_add_int(volatile int *address, int value ) {
  asm volatile("lock xadd $0,%1":
                "+r"(value);
                "+m"(*address);
                "memory");
  return value;
}
```

```c
int atomic_inc_int(int *address ) {
  asm volatile("lock inc %0":
                "+m"(*address);
                "memory");
  return (*address);
}
```

这些例程使用 `gcc` 内联汇编语言编写。虽然我们的意图不是在此低级进行久留，但描述这些语句是如何组合的是合适的。`asm` 关键字标识后续文本为汇编语言语句。`volatile` 关键字告诉编译器不要将语句从其所在的位置移动，因为这种移动可能会导致语句语义的差异。

汇编语言代码包含在括号中。第一个被引号包围的项目是指令。该指令使用虚拟寄存器 `$0` 和 `$1` 作为参数。编译器将分配真实的寄存器，并负责为这些寄存器填充适当的值。

在汇编语言指令之后，最多有三个由分隔符划分的列表。这些是可选的扩展语法。第一个列表指示这些是对寄存器还是内存的访问。在示例中，表达式 `"+r"(value)` 意味着输出参数是一个应该用于更新变量值的寄存器。加号表示该寄存器将被指令读取和写入。

第二个列表包含输入值及其所在。两个例程都将指针地址作为输入值，表达式 `"+m"(*address)` 表示此指针被用作内存访问。加号表示指令将同时读取和写入内存中的位置。

第三个列表是“破坏”`clobber`列表，指示指令将修改的内容。在两种情况下，指令都会修改内存。

虚拟寄存器从输入寄存器开始编号，因此寄存器 `$0` 被分配变量地址的值。输出寄存器是下一组虚拟寄存器，因此变量值被分配给 `$1`。

查看实际的汇编语言指令也是有用的。`xadd` 指令是交换加`exchange add`，它将变量值加到内存地址处的值上，但它在操作执行后返回该地址的值；这就是交换操作。该指令仅对内存中保留的值加 1，但不在寄存器中返回值。两条指令都带有 `lock` 操作前缀。`lock` 操作锁定系统总线，使得其他处理器无法触碰正在更新的内存位置；因此，是 `lock` 前缀实际上让这些指令变得原子的。如果没有它，当多个线程对同一内存进行操作时，操作的结果将是未定义的。

`atomic_add_int()` 例程将量加到内存位置的值上，并返回原子操作之前保留的值。
`atomic_inc_int()` 例程增加内存位置处的值，并返回内存中当前保留的值。由于指令不返回新值，因此返回值是对内存中保留值的加载。这可能不是操作的真实结果；该值在原子操作和最终加载之间可能被修改过。

## 使用比较并交换指令形成更复杂的原子操作

并不是所有处理器都实现了原子加或增指令。然而，大多数处理器都实现了比较并交换`compare and swap`指令的变体。这种指令可以作为大多数原子操作的基础。

一个比较并交换`CAS`操作将内存位置保留的值与寄存器中保留的值进行比较。如果该位置的值与传递给指令的期望值匹配，则内存中保留的值将使用传递给指令的第二个值进行原子更新。`CAS` 的返回值是内存中保留的原始值。如果操作成功，返回值将与期望值相同。如果操作未成功，返回值将是其他值。这使得代码能够判断操作是否成功。

这种操作在许多情况下都有用。例如，假设互斥锁是通过一个变量实现的，该变量在锁被持有时为 1，在锁可用时为 0。`CAS` 操作可将锁从“空闲”切换到“已占用”。要获取锁，变量 `lock` 必须持有值 0，并且指令需要原子地将 0 替换为 1。列表 8.2 显示了简单自旋锁的代码。`volatile` 关键字确保编译器在每次迭代中重复 `CAS` 操作。

### 列表 8.2 使用 CAS 实现的简单自旋锁

```c
#ifndef sparc
int CAS(volatile int* addr, int ov, int nv)
{
    asm volatile("cas %1, %2, %0":
        "=r"(ov)
        "*m"*(addr), "r"(ov), "0"*:(memory);
    return nv;
}
#else
int CAS(volatile int* addr, int ov, int nv)
{
    asm volatile("lock cmpxchg %2, %1, %0":
        "+a"(ov)
        "+m"*(addr), "r"(ov), "r"(nv)
        "memory");
    return ov;
}
#endif
```

```c
void lock(volatile int* lock) {
    while (CAS(lock, 0, 1) != 0) {
        // 自旋直到获取锁
    }
}

void unlock(volatile int* lock) {
    *lock = 0;
}
```

等等，人们很想想象自旋锁可以在没有原子操作的情况下实现，如 8.3 所示。该代码的问题在于它不能保证任何线程都会获取锁。8.2 中使用的原子操作确保了只有一个线程会获取锁。

### 列表 8.3 错误的自旋锁实现

```c
void lock(volatile int* lock) {
    while (*lock == 1) { // 锁忙时自旋
    }
    *lock = 1;
}

void unlock(volatile int* lock) {
    *lock = 0;
}
```

`CAS` 指令也用于需要对异常值进行原子修改的情况。考虑需要对浮点数进行原子递加的情况。列表 8.4 显示了执行此操作的代码。

### 列表 8.4 原子增加浮点数的代码

```c
void atomic_add_float(volatile float * variable, float increment )
{
  union {
    int asint;
    float asfp;
  } oldvalue, newvalue;
  do {
    oldvalue.asfp = *variable; // 行 11
    newvalue.asfp = oldvalue.asfp + increment; // 行 12
  } while (CAS(variable, oldvalue.asint, newvalue.asint) != oldvalue.asint);
}
```

对浮点变量进行原子更新的代码看起来相当复杂。很大一部分复杂度是因为 `CAS` 操作接收整数参数；因此，浮点值需要转换为整数。这就是代码中联合体`union`的作用。
代码读取被修改变量的值，并准备修改后的版本。在代码中，值只在第 11 行读取一次，并保留在局部变量 `oldvalue` 中。这是为了避免在第一次读取变量和第 12 行作为加法的一部分之间发生数据竞争。这种竞争是微妙的。假设第一次读取变量`第 11 行`时，它的值为 20；这记录为变量的原始值。此时，另一个线程更改了变量的值，第二次读取`第 12 行`时，它的值为 21。值21 被增加到 22，如果操作成功，这将成为变量的新值。假设在尝试 `CAS` 操作时，另一个线程已经将变量的值恢复为 20。由于

# 第 8 章 手动编码的同步与共享

变量包含 20，这是预期值；`CAS` 操作会将值 22 存储到变量中，而不是正确的值 21。

我们通过另一个示例来探索这种值重新加载的问题。列表 8.5 显示了向列表头部添加元素的代码。该代码创建一个新元素并在其中存储适当的值。此循环会不断尝试将此新元素添加到列表头部。循环的每次迭代都会将新元素的 `next` 字段设置为列表中的下一个元素，然后尝试将列表指针替换为指向新元素的指针，并进行原子比较并交换`CAS`。如果比较并交换成功，返回值将是曾经作为列表顶部的元素指针。如果发生这种情况，说明代码执行成功，循环可以退出。

### 列表 8.5 向列表头部添加元素的代码

```c
void element(element_t **head, int value) {
  element_t *element = (element_t*)malloc(sizeof(element_t));
  element->value = value;
  while (element) {
    element->next = *head;
    if (CAS(head, element->next, element) == element->next) {
      element = 0;
    }
  }
}
```
