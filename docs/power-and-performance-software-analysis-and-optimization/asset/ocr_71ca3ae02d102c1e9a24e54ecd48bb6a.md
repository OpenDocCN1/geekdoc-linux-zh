about future instructions. In order to ensure accurate results, a fully serializing instruction, typically CPUID, is used. Listing 5.2 demonstrates two small inline functions for accessing the TSC, along with their serializing CPUID instructions on lines 8 and 26. Note that line 9 uses a regular RDTSC instruction, since it is protected by the prior CPUID, whereas line 23 uses RDCP instruction to ensure that the benchmarked code has finished execution before making the measurement. The final CPUID instruction on line 26 ensures that no later instructions begin before the TSC has been read.

Notice that since TSC is a MSR, and therefore duplicated per hardware, and increments at a fixed rate regardless of the core state, the cycle count corresponds to the wall time, not the process time.

```
#include <inttypes.h>
static inline uint64_t start_cycle(void) {
    register unsigned __asm__ __volatile (
        "cpuid\n\t"
        "rdtsc\n\t"
        : "=a" (a), "=d" (d)
        :
        : "ebx", "ecx", "ecx"
    );
    return ((uint64_t)d << 32) | a;
}
static inline uint64_t stop_cycle(register unsigned high, low) {
    register unsigned __asm__ __volatile (
        "rdtsc\n\t"
        "mov %%ax, %%[low]\n\t"
        "mov %%edx, %%[high]\n\t"
        "cpuid\n\t"
        : [high] "r" (high),
        [low] "r" (low)
        : "eax", "ebx", "ecx", "edx"
    );
    return ((uint64_t)high << 32) | low;
}
```

# LISTING 5.2

Functions for measuring cycle count.