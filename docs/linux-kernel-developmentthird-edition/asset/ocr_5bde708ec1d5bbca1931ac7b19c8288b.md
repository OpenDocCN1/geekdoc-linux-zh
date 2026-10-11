All 64-bit architectures provide atomic64_t and a family of arithmetic functions to operate on it. Most 32-bit architectures do not, however, support atomic64_t—x86-32 is a notable exception. For portability between all Linux’s supported architectures, developers should use the 32-bit atomic_t type. The 64-bit atomic64_t is reserved for code that is both architecture-specific and that requires 64-bits.

# Atomic Bitwise Operations

In addition to atomic integer operations, the kernel also provides a family of functions that operate at the bit level. Not surprisingly, they are architecture-specific and defined in `asm/biop.h`.

What might be surprising is that the bitwise functions operate on generic memory addresses. The arguments are a pointer and a bit number. Bit zero is the least significant bit of the given address. On 32-bit machines, bit 31 is the most significant bit, and bit 32 is the least significant bit of the following word. There are no limitations on the bit number supplied; although, most uses of the functions provide a word and, consequently, a bit number between 0 and 31 on 32-bit machines and 0 and 63 on 64-bit machines.

Because the functions operate on a generic pointer, there is no equivalent of the atomic integer’s atomic_t type. Instead, you can work with a pointer to whatever data you want. Consider an example:

```
unsigned long word = 0;

set_bit(0, &word);           /* bit zero is now set (atomically) */
set_bit(1, &word);           /* bit one is now set (atomically) */
printk("%ul\n", word);      /* will print "3" */
clear_bit(1, &word);        /* bit one is now unset (atomically) */
change_bit(0, &word);       /* bit zero is flipped; now it is unset (atomically) */

/* atomically sets bit zero and returns the previous value (zero) */
if (test_and_set_bit(0, &word)) {
    /* never true ... */
}

/* the following is legal; you can mix atomic bit instructions with normal C */
word = 7;
```