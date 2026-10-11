![](bbox=[0.28, 0.1, 0.72, 0.3])

The internal storage in memory is different on big- versus little-endian, as shown in Table 19.3.

Table 19.3 **Big Versus Little Endian**
| Address | Big Endian | Little Endian |
| :------ | :--------- | :------------ |
| 0 | 00000000 | 00000011 |
| 1 | 00000000 | 00000100 |
| 2 | 00000100 | 00000000 |
| 3 | 00000011 | 00000000 |

Notice how the big-endian architecture stores the most significant bytes in its smallest address.This is the exact inverse of little-endian.

As a final example, here is a simple code snippet to test whether a given architecture is big- or little-endian:

```
int x = 1;

if (*(char *)&x == 1)
/* little endian */
else
/* big endian */
```

This works either in user-space or inside the kernel.

# History of Big- and Little-Endian

The terms *big-endian* and *little-endian* derive from Jonathan Swift’s 1726 satirical novel, *Gulliver’s Travels*. In the novel, the fictional Lilliputians’ major political issue is whether eggs should be cracked open on the big end or the little end. Those who favor the big end are big-endians, whereas those who favor the small are little-endians.

The similarity between the Lilliputians and our big-endian versus little-endian debate is that the argument is rooted deeper in politics than technical merits.