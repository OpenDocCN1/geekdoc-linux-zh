
图 17.16 显示的两个函数来自 `<i386/signal.h>`，用于在 `sigset_t` 位图中设置或清除单个位。这些是 i386 特有的；同时也存在这些函数的通用版本，这些版本仅在定义了 `__HAVE_ARCH_BITOPS` 的情况下才被编译：

```
180 #define __HAVE_ARCH_BITOPS
181
182 extern __inline__ void sigaddset(sigset_t *set, int_sig)
183 {
184     asm__("btsl %1,%0" : "m"(*set):Ir(sig - 1): "cc");
185 }
186
187 extern __inline__ void sigdelset(sigset_t *set, int_sig)
188 {
189     asm__("btrl %1,%0" : "m"(*set):Ir(sig - 1): "cc");
190 }
```

图 17.16 信号位图处理器

## 17.2.1.2 位测试函数

内核提供了一些函数，用于检查给定信号位图中的特定位是否被设置。这些函数显示在图 17.17，来自 `asm-i386/signal.h`。

```c
static __inline_int __const_sigismember(sigset_t*set, int __sig)
{
    unsigned long sig=__sig-1;
    return 1& (set->sig[sig/__NSIG_BPW] >> (sig%__NSIG_BPW));
}

static __inline_int __gen_sigismember(sigset_t*set, int __sig)
{
    int ret;
    _asm_("bt%2,%1\n\tbbl%0,%0"
          :=r(ret):"m"(*set),"r"(__sig-1),"cc");
    return ret;
}

#define sigismember(set,sig) \
    (_builtin_constant_p(sig) ? \
    __const_sigismember((set),(sig)) : \
    __gen_sigismember((set),(sig)))

#define sigmask(sig) (1UL<<((sig)-1))
```

图 17.17 位测试函数

- 192–196 该函数适用于任意长度的位图。
- 194 位图是从 0 开始索引的；信号从 1 开始。因此我们使用这种转换。
- 195 这将信号掩码中的位根据该信号在字中的索引向右平移。这使得与 `sig` 对应的位移动到最低位位置。与 `1` 进行 AND 运算，如果该位被设置，则返回 TRUE；否则返回 FALSE。
- 192–204 该函数仅对位图的前 32 位有效。
- 201 `bt` 指令测试 `set` 所指向的长整数中的位 `__sig-1`。该值被写入标志位。`sbbl`（带借位的减法）指令从 `ret` 中减去标志位。如果该位被清零，则为 0。如果该位被设置，则为 -1；因此 `ret` 全为 1。
- 201 输出参数 `ret` 是只写的，并且期望位于寄存器中。对于输入参数，“set”指定了 0 到 31 范围内的整数值。信号编号为 1, . . ., 32，而位图是从 0 开始索引的。因此位 n–1 对应于信号。“r”表示可能存储在寄存器中的值。此函数只能操作前 32 位，“cc”告诉编译器此指令更改了条件码寄存器 `EFLAGS`。
- 206–209 `gcc` 内置函数在参数是编译时常量时评估为 TRUE，否则为 FALSE，因此它决定了 `sig` 的值，从而决定了是可以调用更高效的 `__const_sigismember()` 函数还是需要调用 `__gen_sigismember()` 函数。
- 211 这生成一个位图，其中有一个设置的位，对应于 `sig`。

## 17.2.2 位图操作

另有另一组函数可以对整个位图进行清零、设置或执行逻辑操作。其中一些是由参数化宏生成的；另一些是直接的函数。

### 17.2.2.1 生成位操作函数的宏

图 17.18 显示的宏来自 `<linux/signal.h>` 它生成一个名为 `name` 的函数，该函数对两个由 `a` 和 `b` 掩码的输入信号掩码执行指定的位（二进制）操作，返回由 `r` 掩码的信号掩码。在实践中，它被用于生成三个函数：`sigsetsort()`、`sigandsets()` 和 `signandsets()`（见第 17.2.2 节）。
