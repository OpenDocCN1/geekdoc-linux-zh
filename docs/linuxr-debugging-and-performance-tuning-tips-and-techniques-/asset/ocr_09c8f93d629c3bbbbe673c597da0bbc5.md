```
```C
void *calloc(size_t nmemb, size_t size)
{
    void *p;
    size_t total;

    total = nmemb * size;         /* Compute size */
    p = malloc(total);           /* Allocate the memory */

    if (p != NULL) {             /* If it worked ... */
        memset(p, '\0', total); /* fill it with zeros */
    }
    return p;                    /* Return value is NULL or pointer */
}
```
```

Many experienced programmers prefer to use `calloc()` since then there’s never any question about the contents of the newly allocated memory.

Also, if you know you’ll need zero-filled memory, you should use `calloc()`, because it’s possible that the memory `malloc()` returns is already zero-filled. Although you, the programmer, can’t know this, `calloc()` can know about it and avoid the call to `memset()`.

# 3.2.1.6 Summarizing from the GNU Coding Standards

To summarize, here is what the GNU Coding Standards has to say about using the memory allocation routines:

Check every call to `malloc` or `realloc` to see if it returned zero. Check `realloc` even if you are making the block smaller; in a system that rounds block sizes to a power of 2, `realloc` may get a different block if you ask for less space.

In Unix, `realloc` can destroy the storage block if it returns zero. GNU `realloc` does not have this bug: If it fails, the original block is unchanged. Feel free to assume the bug is fixed. If you wish to run your program on Unix, and wish to avoid lossage in this case, you can use the GNU `malloc`. You must expect `free` to alter the contents of the block that was freed. Anything you want to fetch from the block, you must fetch before calling `free`.

In three short paragraphs, Richard Stallman has distilled the important principles for doing dynamic memory management with `malloc()`. It is the use of dynamic