A similar phenomenon occurs in programming, not related to particle physics: The act of compiling a program for debugging, or running it with debugging enabled can change the program's behavior. In particular, the original bug can disappear. Such a bug is known colloquially as a *heisenbug*.

The manpage is warning us against putting expressions with side effects into `assert()` calls:

```
assert(*p++ == '\n');
```

The side-effect here is that the `p` pointer is incremented as part of the test. When `NDEBUG` is defined, the expression argument *disappears* from the source code; it's never executed. This can lead to an unexpected failure. However, as soon as assertions are reenabled in preparation for debugging, things start working again! Such problems are painful to track down.

# ## 12.2 Low-Level Memory: The `memXXX()` Functions

Several functions provide low-level services for working with arbitrary blocks of memory. Their names all start with the prefix `mem`:

```
#include <string.h>                    ISO C

void *memset(void *buf, int val, size_t count);
void *memcpy(void *dest, const void *src, size_t count);
void *memmove(void *dest, const void *src, size_t count);
void *memcmp(void *dest, const void *src, int val, size_t count);
int memcmp(const void *buf1, const void *buf2, size_t count);
void *memchr(const void *buf, int val, size_t count);
```

# ### 12.2.1 Setting Memory: `memset()`

The `memset()` function copies the value `val` (treated as an `unsigned char`) into the first `count` bytes of `buf`. It is particularly useful for zeroing out blocks of dynamic memory:

```
void *p = malloc(count);
if (p != NULL)
  memset(p, 0, count);
```

However, `memset()` can be used on any kind of memory, not just dynamic memory. The return value is the first argument: `buf`.