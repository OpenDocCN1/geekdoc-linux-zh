
`atomic_read(&v);` /* 将打印 7 */

`printk("%d\n", atomic_read(&v));`

如果需要将`atomic_t`转换为`int`，请使用`atomic_read()`：`printk("%d\n", atomic_read(&v));` /* 将打印 "7" */

原子整数操作的一个常见用途是实现计数器。使用复杂的锁定方案来保护单个计数器是多余的，因此开发者通常使用更轻量级的`atomic_inc()`和`atomic_dec()`。

原子整数运算符的另一个用途是原子地执行操作并测试其结果。一个常见的例子是原子递减并测试：`int atomic_dec_and_test(atomic_t *v)`

此函数将给定的原子值减一。如果结果为零，则返回`true`；否则返回`false`。标准原子整数操作（在所有体系结构上找到的那些）的完整列表见表 10.1。特定体系结构上实现的所有操作都可以在`asm/atomic.h`中找到。

| **原子整数操作** | **描述** |
|:---------------------------|:----------------|
| `ATOMIC_INIT(int i)` | 在声明时初始化为`i`。 |
| `int atomic_read(atomic_t *v)` | 原子地读取`v`的整数值。 |
| `void atomic_set(atomic_t *v, int i)` | 原子地将`v`设置为`i`。 |
| `void atomic_add(int i, atomic_t *v)` | 原子地将`i`加到`v`上。 |
| `void atomic_sub(int i, atomic_t *v)` | 原子地从`v`中减去`i`。 |
| `void atomic_inc(atomic_t *v)` | 原子地将`v`加一。 |
| `void atomic_dec(atomic_t *v)` | 原子地将`v`减一。 |
| `int atomic_sub_and_test(int i, atomic_t *v)` | 原子地从`v`中减去`i`，如果结果为零则返回`true`，否则返回`false`。 |
| `int atomic_add_negative(int i, atomic_t *v)` | 原子地将`i`加到`v`上，如果结果为负则返回`true`，否则返回`false`。 |
| `int atomic_add_return(int i, atomic_t *v)` | 原子地将`i`加到`v`上并返回结果。 |
| `int atomic_sub_return(int i, atomic_t *v)` | 原子地从`v`中减去`i`并返回结果。 |
| `int atomic_inc_return(int i, atomic_t *v)` | 原子地将`v`递增一并返回结果。 |
| `int atomic_dec_return(int i, atomic_t *v)` | 原子地将`v`递减一并返回结果。 |
| `int atomic_dec_and_test(atomic_t *v)` | 原子地将`v`递减一，如果结果为零则返回`true`，否则返回`false`。 |
| `int atomic_inc_and_test(atomic_t *v)` | 原子地将`v`递增一，如果结果为零则返回`true`，否则返回`false`。 |

原子操作通常通过包含内联汇编的内联函数来实现。如果某个函数本身具有原子性，那么该函数通常只是一个宏。例如，在大多数体系结构上，字大小的读取操作始终是原子的。也就是说，读取单个字的操作不可能在一个对该字的写入操作进行到一半时完成。读取操作总是返回该字的一致状态，要么在写入完成之前，要么在写入完成之后，但绝不会在写入过程中。因此，`atomic_read()`通常只是一个返回`atomic_t`整数值的宏：

```c
/**
 * atomic_read - read atomic variable
 * @v: pointer of type atomic_t
 *
 * Atomically reads the value of @v.
 */
static inline int atomic_read(const atomic_t *v)
{
    return v->counter;
}
```

## 原子性与顺序性

前文关于原子读取的讨论引发了关于原子性与顺序性之间差异的讨论。如前所述，字大小的读取操作总是原子性地发生的。它永远不会与对同一字的写入操作交错；读取操作总是返回该字的一致状态——也许是在写入完成之前，也许是在写入完成之后，但绝不是在写入过程中。例如，如果一个整数最初是`42`，然后被设置为`365`，那么对该整数的读取操作总是返回`42`或`365`，而绝不会返回这两个值的某种混合体。我们称之为原子性。

然而，你的代码可能有更严格的要求：也许你要求读取操作始终发生在待处理的写入操作之前。这种要求不是原子性，而是顺序性。原子性确保指令在没有中断的情况下执行，并且要么完全完成，要么完全不完成。另一方面，顺序性确保两个或更多指令所需的相对顺序——即使它们在不同的执行线程中发生，甚至在不同的处理器上发生——得以保持。

本节讨论的原子操作仅保证原子性。顺序性通过屏障操作来强制，我们将在本章后面讨论这一点。

在你的代码中，通常更倾向于选择原子操作而不是更复杂的锁定机制。在大多数体系结构上，一个或两个原子操作所带来的开销和缓存行抖动比更复杂的同步方法要少。但是，与任何对性能敏感的代码一样，测试多种方法总是明智的。

### 64 位原子操作

随着`64`位体系结构日益普及，Linux内核开发者为`32`位`atomic_t`类型增加了`64`位变体`atomic64_t`也就不足为奇了。为了可移植性，`atomic_t`的大小不能在不同体系结构之间改变，因此在`64`位体系结构上，`atomic64_t`也是`32`位的。相反，`atomic64_t`类型提供了一个`64`位原子整数，其功能与其`32`位的“兄弟”完全相同。用法完全一样，只是整数的可用范围是`64`位，而不是`32`位。几乎所有经典的`32`位原子操作都有`64`位变体实现；它们以前缀`atomic64`代替`atomic`。表 10.2 列出了标准操作的全集；某些体系结构实现了更多操作，但它们不具有可移植性。与`atomic_t`一样，`atomic64_t`类型也只是围绕一个整数的简单包装器，该类型为`long`：

```c
typedef struct {
    volatile long counter;
} atomic64_t;
```
