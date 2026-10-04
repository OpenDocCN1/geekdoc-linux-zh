# 41.4.1 更多的理论

其实，我们都知道，乘法和除法是互逆运算。因此下面的除法可以用乘法来代替。我们可以表示为

```
$\frac{x}{c} = x * \frac{1}{c}$
```

1/c可以称为乘法的逆运算，是c的倒数。可以用编译器来做提前运算。

但是为了浮点计算用的，有没有整数数呢？在算术计算环境下，是可能会有的。CPU寄存器的长度是非常规整的，因此几乎所有的寄存器的算术操作都是对的32位或者对的64位，因此要进行操作。

可以查War02的第10章第3节。

# 41.5 计算除数

# 41.5.1 位移系数的代码

通常我们看到的代码可能就像这样：

```
mov     eax, MAGICAL CONSTANT
imul    input value
sar     edx, SHIFTING COEFFICIENT ; signed division
by      2using arithmetic shift right
mov     eax, edx
shr    eax, 31
add     eax, edx
```

我们这里用大字母M代表32位的魔术因子，把位移系数标记C，把除数标记为D。

在此除数可以表示为

```
$D = \frac{2^{32+c}}{M}$
```