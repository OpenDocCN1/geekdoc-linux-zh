Another advantage to `memcmp()` is that it’s faster than the typical C implementation:

```
```c
/* memcmp --- example C implementation, NOT for real use */
int memcmp(const void *buf1, const void *buf2, size_t count)
{
    const unsigned char *cp1 = (const unsigned char *) buf1;
    const unsigned char *cp2 = (const unsigned char *) buf2;
    int diff;

    while (count-- != 0) {
        diff = *cp1++ - *cp2++;
        if (diff != 0)
            return diff;
    }
    return 0;
}
```
```

The speed can be due to special “block memory compare” instructions that many architectures support or to comparisons in units larger than bytes. (This latter operation is tricky and is best left to the library’s author.)

For these reasons, you should *always* use your library’s version of `memcmp()` instead of rolling your own. Chances are excellent that the library author knows the machine better than you do.

# 12.2.4 Searching for a Byte Value: memchr()

The `memchr()` function is similar to the `strchr()` function: It returns the location of a particular value within an arbitrary buffer. As for `memcmp()` vs. `strcmp()`, the principal reason to use `memchr()` is that you have arbitrary binary data.

GNU `wc` uses `memchr()` when counting only lines and bytes,$^4$ and this allows `wc` to be quite fast. From `wc.c` in the GNU Coreutils:

$^4$ See `wc(1)`. `wc` counts lines, words, and characters.