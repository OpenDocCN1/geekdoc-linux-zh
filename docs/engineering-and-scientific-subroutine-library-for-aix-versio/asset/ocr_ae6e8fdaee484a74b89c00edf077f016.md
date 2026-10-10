Specified as: a fullword *integer*; *ldb* $\gg$ 0 and *ldb* $\ge$ *n*.

*nsinfo*  is the number of elements in array, *AP*.

If *n* $\le$ *nco*, *nsinfo* = *n*( *n* + 1 ) / 2

Where:

$$\underline{nco = \sqrt{2.0(ics)}}$$

*ics* is the size in doublewords of the data cache. The data cache size can be obtained by utilizing the following C language code fragment:

```
```c
#include <sys/systemcfg.h>
int  ics;
        .
        .
        .
        ics=_system_configuration.dcache_size/8;
```
```

Otherwise, to determine a sufficient amount of storage, use the following processor-independent formula:

```
```c
n0 =  100
ns =  (n + n0)( n + n0 + 1) / 2 + n(n0)
For uplo = ‘L’,
       nsinfo \>= ns
For uplo = ‘U’,
       n1 = (n + 1) / 2
       nt = n((n + 1) / 2)
       nt1 = n1(n1 + 1)
       ns1 = nt + nt1
       nsinfo \>= max(ns, ns1)
```
```

To determine the minimal amount of storage see “Notes” on page 506.

Specified as: a fullword *integer*; *nsinfo* $>$ 0.

# ### On Return:

*ap*      is the transformed matrix $A$ of order *n*, containing the results of the factorization.

If *nsinfo* $\ge$ 0 and *n* $>$ *nco*, additional information that can be used to obtain a minimum *nsinfo* is stored in *AP*(1). See “Notes” on page 506 and “Function” on page 506.

Returned as: a one-dimensional array, containing numbers of the data type indicated in Table 104 on page 504.

*ipvt*   is an integer vector of length *n*, containing the pivot information necessary to construct the factored form of $A$.

Returned as: a one-dimensional array of (at least) length *n*, containing numbers of the data type indicated in Table 104 on page 504.

*bx*     is the matrix **X**, containing the *nrhs* solutions to the system. The solutions, each of length *n*, reside in the columns of **X**.

Returned as: an *ldb* by (at least) *nrhs* array, containing numbers of the data type indicated in Table 104 on page 504.

*nsinfo*   indicates the result of the computation.