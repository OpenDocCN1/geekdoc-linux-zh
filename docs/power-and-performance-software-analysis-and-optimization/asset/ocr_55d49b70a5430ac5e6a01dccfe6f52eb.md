# 15.1 SIMD 271

Assuming that foo() shows up on a performance profile as consuming a large percentage of cycles, this function is a good candidate for vectorization. Unfortunately the current memory organization, an array of structures, is less optimal for vertical vectorization. This organization leads to poor utilization of the caches and memory bandwidth, since more data is fetched than required, and the extra fields increase the chance for the data to be evicted from the cache before it is needed again. Additionally, there will be overhead for swizzling the data into the correct format, which potentially negate any benefit from parallelizing the calculation.

The most efficient method for loading this data into the SIMD registers is sequential. By reorganizing the layout of memory, it is possible to better accommodate this data flow. Ideally, the structure would be organized as groups of multiple units, rather than each struct representing a single unit. In other words, rather than organizing memory as an array of structures it would be better to organize them as a structure of arrays, but it will benefit performance. Continuing the previous example, the function foo() is easy to vectorize once the data is arranged accordingly:

```
#include <intypes.h>
#include <immintrin.h>

struct soa {
    double *x;
    double *y;
    size_t len;
    /* other fields */
}

void foo_avx(struct soa *in, double *out) {
    size_t sz = in->len;
    double *x = in->x;
    double *y = in->y;

    while ((uintptr_t)out & (32 - 1)) && sz) {
        *out = *x + *y;

        x++;
        y++;
        out++;
        sz--;
    }

    while (sz >= 4) {
        __m256d x_ymm, y_ymm, r_ymm;
        x_ymm = _mm256_loadu_pd(x);
```