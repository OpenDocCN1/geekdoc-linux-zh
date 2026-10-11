The `memcpy()` function was the original System V API for copying blocks of memory; its behavior for overlapping blocks of memory wasn't particularly defined one way or the other. For the 1989 C standard, the committee felt that this lack of defined behavior was a problem; thus they invented `memmove()`. For historical compatibility, `memcpy()` was left alone, with the behavior for overlapping memory specifically stated as undefined, and `memmove()` was invented to provide a routine that would correctly deal with problem cases.

Which one should you use in your own code? For a library function that has no knowledge of the memory areas being passed into it, you should use `memmove()`. That way, you're guaranteed that there won't be any problems with overlapping areas. For application-level code that “knows” that two areas don't overlap, it's safe to use `memcpy()`.

For both `memcpy()` and `memmove()` (as for `strcpy()`), the destination buffer is the first argument and the source is the second one. To remember this, note that the order is the same as for an assignment statement:

```
dest = src;
```

(Many systems have manpages that don't help, providing the prototype as `void *memcpy(void *buf1, void *buf2, size_t n)`' and relying on the prose to explain which is which. Fortunately, the GNU/Linux manpage uses better names.)

# 12.2.3  Comparing Memory Blocks: `memcmp()`

The `memcmp()` function compares count bytes from two arbitrary buffers of data. Its return value is like `strcmp()`: negative, zero, or positive if the first buffer is less than, equal to, or greater than the second one.

You may be wondering “Why not use `strcmp()` for such comparisons?” The difference between the two functions is that `memcmp()` doesn't care about zero bytes (the `\'0'` string terminator). Thus, `memcmp()` is the function to use when you need to compare arbitrary binary data.