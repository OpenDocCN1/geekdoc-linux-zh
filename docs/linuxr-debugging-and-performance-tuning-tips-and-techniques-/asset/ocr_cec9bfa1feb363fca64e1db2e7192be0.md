# ### 12.2.2  Copying Memory: `memcpy()`, `memmove()`, and `mempcpy()`

Three functions copy one block of memory to another. The first two differ in their handling of *overlapping* memory areas; the third copies memory but stops upon seeing a particular value.

```
```
void *memcpy(void *dest, const void *src, size_t count)
```
```

This is the simplest function. It copies *count* bytes from *src* to *dest*. It does not handle overlapping memory areas. It returns *dest*.

```
```
void *memmove(void *dest, const void *src, size_t count)
```
```

Similar to `memcpy()`, it also copies *count* bytes from *src* to *dest*. However, it does handle overlapping memory areas. It returns *dest*.

```
```
void *mempcpy(void *dest, const void *src, int val, size_t count)
```
```

This copies bytes from *src* to *dest* stopping *either* after copying *val* into *dest* *or* after copying *count* bytes. If it found *val*, it returns a pointer to the position in *dest* just beyond where *val* was placed. Otherwise, it returns `NULL`.

Now, what's the issue with overlapping memory? Consider Figure 12.1.

```
```c
struct xyz { ... } data[8];
mempcy( & data[3], data, sizeof(data[0]) * 4 );
```
```

vs.

```
```c
memmove( & data[3], data, sizeof(data[0]) * 4 );
```
```

![](bbox=[0.09, 0.85, 0.9, 0.96])

# #### FIGURE 12.1  Overlapping copies

The goal is to copy the four instances of `struct xyz` in `data[0]` through `data[3]` into `data[3]` through `data[6]`. `data[3]` is the problem here; a byte-by-byte copy moving forward in memory from `data[0]` will clobber `data[3]` before it can be safely copied into `data[6]`! (It's also possible to come up with a scenario where a backwards copy through memory destroys overlapping data.)