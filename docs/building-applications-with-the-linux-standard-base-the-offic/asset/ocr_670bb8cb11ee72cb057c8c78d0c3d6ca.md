Linux can be used to ease the migration of that application. This library provides the Solaris thread interfaces built upon the POSIX thread library.

# 5.7    ABSOLUTE ADDRESSES

Applications that use hard-coded addresses might be difficult to port. Some applications use m\_map() calls for page fixing. Since each platform has its own way of handling the program stack, heap, system libraries, and so on, such a call to m\_map() with a hard-coded address might result in a segment violation.

For instance, some addressing schemes ignore the high-order bits. So a hard-coded address of 0x80000000 might get translated to 0x00000000 and cause unintentional results. It is desirable to eliminate the usage of hard-coded addresses in the code. If an application mandates the use of hard-coded addresses, then it has to be changed to use only an allowed memory range, which you can obtain from /proc/application\_pid/map.

# 5.8    PADDING

When a structure or an aggregate data type are used in the code, each platform has its own way of laying out the constituent elements. This arrangement is dependent on structure, architectural limitations, efficiency, and compiler. Most of the architectures cannot read data from odd addresses. Architectures such as PowerPC are inefficient in reading the data if it starts at an address not divisible by four. So, for efficiency purposes, compilers add the so-called *pad bytes*. The function of these bytes is to maintain byte alignment so that the code can perform efficiently.

On a 4-byte alignment platform, the compiler would lay out the structure in Example 5.6 as shown in Table 5.5, where *P* is padding, d1₀, d1₁ are bytes of d1, and d2₀₋₃ are bytes of d2.

In Table 5.5, the data structure occupies eight bytes because of the padding. On a platform that does not need any alignment, the compiler would lay out the same structure differently (Table 5.6).