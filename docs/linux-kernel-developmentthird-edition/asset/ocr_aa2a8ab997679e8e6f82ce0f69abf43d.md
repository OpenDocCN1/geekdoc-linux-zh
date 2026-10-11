# # 64-Bit Atomic Operations

With the rising prevalence of 64-bit architectures, it is no surprise that the Linux kernel developers augmented the 32-bit atomic_t type with a 64-bit variant, atomic64_t. For portability, the size of atomic_t cannot change between architectures, so atomic64_t is 32-bit even on 64-bit architectures. Instead, the atomic64_t type provides a 64-bit atomic integer that functions otherwise identical to its 32-bit brother. Usage is exactly the same, except that the usable range of the integer is 64, rather than 32, bits. Nearly all the classic 32-bit atomic operations are implemented in 64-bit variants; they are prefixed with atomic64 in lieu of atomic. Table 10.2 is a full listing of the standard operations; some architectures implement more, but they are not portable. As with atomic_t, the atomic64_t type is just a simple wrapper around an integer, this type a long:

```
```c
typedef struct {
	volatile long counter;
} atomic64_t;
```
```

Table 10.2 Atomic Integer Methods
| Atomic Integer Operation | Description |
| :--- | :--- |
| ATOMIC64_INIT(long i) | At declaration, initialize to *i*. |
| long atomic64_read(atomic64_t *v) | Atomically read the integer value of *v*. |
| void atomic64_set(atomic64_t *v, int i) | Atomically set *v* equal to *i*. |
| void atomic64_add(int i, atomic64_t *v) | Atomically add *i* to *v*. |
| void atomic64_sub(int i, atomic64_t *v) | Atomically subtract *i* from *v*. |
| void atomic64_inc(atomic64_t *v) | Atomically add one to *v*. |
| void atomic64_dec(atomic64_t *v) | Atomically subtract one from *v*. |
| int atomic64_sub_and_test(int i, atomic64_t *v) | Atomically subtract *i* from *v* and return true if the result is zero; otherwise false. |
| int atomic64_add_negative(int i, atomic64_t *v) | Atomically add *i* to *v* and return true if the result is negative; otherwise false. |
| long atomic64_add_return(int i, atomic64_t *v) | Atomically add *i* to *v* and return the result. |
| long atomic64_sub_return(int i, atomic64_t *v) | Atomically subtract *i* from *v* and return the result. |
| long atomic64_inc_return(int i, atomic64_t *v) | Atomically increment *v* by one and return the result. |
| long atomic64_dec_return(int i, atomic64_t *v) | Atomically decrement *v* by one and return the result. |
| int atomic64_dec_and_test(atomic64_t *v) | Atomically decrement *v* by one and return true if zero; false otherwise. |
| int atomic64_inc_and_test(atomic64_t *v) | Atomically increment *v* by one and return true if the result is zero; false otherwise. |