```
*where
*
*b = exponent bias
* m = number of mantissa bits
*
*
*/
val_int -= 1 << 23; /* Subtract 2^m. */
val_int >>== 1; /* Divide by 2. */
val_int += 1 << 29; /* Add ((b + 1) / 2) * 2^m. */

return *(float*)&val_int; /* Interpret again as float * /
```

作为一个练习，你可以尝试编译这个函数，以理解它是如何工作的。还有一个非常有名的快速计算 $\sqrt{}$ 的算法。说起这一算法因为用于 Quake III Arena中变得很流行。

该算法的描述和源代码参见http://go.yurichev.com/17360

+   [1] Pseudorandom number generator, 伪随机数生成函数。
[2] 参考了网络文章 http://xor0110.wordpress.com/2010/09/24/how-to-generate-floating-point-random-numbers-efficiently.