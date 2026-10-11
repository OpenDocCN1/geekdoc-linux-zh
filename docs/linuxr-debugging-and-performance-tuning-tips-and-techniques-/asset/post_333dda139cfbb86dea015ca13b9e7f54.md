
- Cast and assign the return value of `realloc(a)`. More discussion of this shortly.
- As for `malloc(a)`, check the return value to make sure it's not `NULL`. Any memory allocation routine can fail.

When growing a block of memory, `realloc(a)` often allocates a new block of the right size, copies the data from the old block into the new one, and returns a pointer to the new one.

When shrinking a block of data, `realloc(a)` can often just update the internal bookkeeping information and return the same pointer. This saves having to copy the original data. However, if this happens, don't assume you can still use the memory beyond the new size!

In either case, you can assume that if `realloc(a)` doesn't return `NULL`, the old data has been copied for you into the new memory. Furthermore, the old pointer is no longer valid, as if you had called `free(a)` with it, and you should not use it. This is true of all pointers into that block of data, not just the particular one used to call `free(a)`.

You may have noticed that our example code used a separate variable to point to the changed storage block. It would be possible (but a bad idea) to use the same initial variable, like so:

```c
coordinates = realloc(coordinates, new_amount);
```

This is a bad idea for the following reason. When `realloc(a)` returns `NULL`, the original pointer is still valid; it's safe to continue using that memory. However, if you reuse the same variable and `realloc(a)` returns `NULL`, you've now lost the pointer to the original memory. That memory can no longer be used. More important, that memory can no longer be freed! This creates a memory leak, which is to be avoided.

There are some special cases for the Standard C version of `realloc(a)`: When the `ptr` argument is `NULL`, `realloc(a)` acts like `malloc(a)` and allocates a fresh block of storage. When the `size` argument is 0, `realloc(a)` acts like `free(a)` and releases the memory that `ptr` points to. Because (a) this can be confusing and (b) older systems don't implement this feature, we recommend using `malloc(a)` when you mean `malloc(a)` and `free(a)` when you mean `free(a)`.

Here is another, fairly subtle, "gotcha."⁴ Consider a routine that maintains a *static* pointer to some dynamically allocated data, which the routine occasionally has to grow. It may also maintain automatic (that is, local) pointers into this data. (For brevity, we omit error checking code. In production code, don’t do that.) For example:

```c
void manage_table(void)
{
    static struct table *table;
    struct table *cur, *p;
    int i;
    size_t count;
    ...
    table = (struct table *) malloc(count * sizeof(struct table));
    /* fill table */
    cur = & table[i];      /* point at i'th item */
    ...
    cur->i = j;             /* use pointer */
    ...
    if (some condition) {   /* need to grow table */
    count += count/2;
    p = (struct table *) realloc(table, count * sizeof(struct table));
    table = p;
    }

    cur->i = j;             /* PROBLEM 1: update table element */

    other_routine();        /* PROBLEM 2: see text */
    cur->j = k;             /* PROBLEM 2: see text */
    ...
}
```

This looks straightforward; *manage_table()* allocates the data, uses it, changes the size, and so on. But there are some problems that don’t jump off the page (or the screen) when you are looking at this code.

In the line marked “PROBLEM 1”, the *cur* pointer is used to update a table element. However, *cur* was assigned on the basis of the *initial* value of *table*. If *some condition* was true and *realloc()* returned a different block of memory, *cur* now points into the original, freed memory! Whenever *table* changes, any pointers into the memory need to be updated too. What’s missing here is the statement `*cur = & table[i];*` after *table* is reassigned following the call to *realloc()*.

The two lines marked `PROBLEM 2` are even more subtle. In particular, suppose `other_routine()` makes a *recursive* call to `manage_table()`. The table variable could be changed again, completely invisibly! Upon return from `other_routine()`, the value of `cur` could once again be invalid.

One might think (as we did) that the only solution is to be aware of this and supply a suitably commented reassignment to `cur` after the function call. However, Brian Kernighan kindly set us straight. If we use indexing, the pointer maintenance issue doesn't even arise:

```c
  table = (struct table *) malloc(count * sizeof(struct table));
  /* fill table */
  ...
  table[i].i = j;                 /* Update a member of the i'th element */
  ...
  if (some condition) {   /* need to grow table */
    count += count/2;
    p = (struct table *) realloc(table, count * sizeof(struct table));
    table = p;
  }

  table[i].i = j;                 /* PROBLEM 1 goes away */
  other_routine();                 /* Recursively calls us, modifies table */
  table[i].j = k;                 /* PROBLEM 2 goes away also */
```

Using indexing doesn't solve the problem if you have a *global* copy of the original pointer to the allocated data; in that case, you still have to worry about updating your global structures after calling `realloc()`.

> **NOTE** As with `malloc()`, when you grow a piece of memory, the newly allocated memory returned from `realloc()` is not zero-filled. You must clear it yourself with `memset()` if that's necessary, since `realloc()` only allocates the fresh memory; it doesn't do anything else.

### 3.2.1.5 Allocating and Zero-filling: `calloc()`

The `calloc()` function is a straightforward wrapper around `malloc()`. Its primary advantage is that it zeros the dynamically allocated memory. It also performs the size calculation for you by taking as parameters the number of items and the size of each:

```c
  coordinates = (struct coord *) calloc(count, sizeof(struct coord));
```

Conceptually, at least, the `calloc()` code is fairly simple. Here is one possible implementation:

```c
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

Many experienced programmers prefer to use `calloc()` since then there’s never any question about the contents of the newly allocated memory.

Also, if you know you’ll need zero-filled memory, you should use `calloc()`, because it’s possible that the memory `malloc()` returns is already zero-filled. Although you, the programmer, can’t know this, `calloc()` can know about it and avoid the call to `memset()`.

### 3.2.1.6 Summarizing from the GNU Coding Standards

To summarize, here is what the GNU Coding Standards has to say about using the memory allocation routines:

- Check every call to `malloc` or `realloc` to see if it returned zero. Check `realloc` even if you are making the block smaller; in a system that rounds block sizes to a power of 2, `realloc` may get a different block if you ask for less space.

- In Unix, `realloc` can destroy the storage block if it returns zero. GNU `realloc` does not have this bug: If it fails, the original block is unchanged. Feel free to assume the bug is fixed. If you wish to run your program on Unix, and wish to avoid lossage in this case, you can use the GNU `malloc`. You must expect `free` to alter the contents of the block that was freed. Anything you want to fetch from the block, you must fetch before calling `free`.

In three short paragraphs, Richard Stallman has distilled the important principles for doing dynamic memory management with `malloc()`. It is the use of dynamic
