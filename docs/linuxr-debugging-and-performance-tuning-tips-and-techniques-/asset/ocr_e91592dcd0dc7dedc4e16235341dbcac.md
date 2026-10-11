This approach guarantees that the `malloc()` will allocate the correct amount of memory without your having to consult the declaration of `pointer`. If `pointer`’s type later changes, the `sizeof` operator automatically ensures that the count of bytes to allocate stays correct. (Geoff’s technique omits the cast that we just discussed. Having the cast there also ensures a diagnostic if `pointer`’s type changes and the call to `malloc()` isn’t updated.)

# 3.2.1.3 Releasing Memory: `free()`

When you’re done using the memory, you “give it back” by using the `free()` function. The single argument is a pointer previously obtained from one of the other allocation routines. It is safe (although useless) to pass a null pointer to `free()`:

```
free(coordinates);  
coordinates = NULL;  /* not required, but a good idea */
```

Once `free(coordinates)` is called, the memory pointed to by `coordinates` is off limits. It now “belongs” to the allocation subroutines, and they are free to manage it as they see fit. They can change the contents of the memory or even release it from the process’s address space! There are thus several common errors to watch out for with `free()`:

# *Accessing freed memory*

If unchanged, `coordinates` continues to point at memory that no longer belongs to the application. This is called *a dangling pointer*. In many systems, you can get away with continuing to access this memory, at least until the next time more memory is allocated or freed. In many others, though, such access won’t work.

In sum, accessing freed memory is a bad idea: It’s not portable or reliable, and the GNU Coding Standards disallows it. For this reason, it’s a good idea to immediately set the program’s pointer variable to `NULL`. If you then accidentally attempt to access freed memory, your program will immediately fail with a segmentation fault (before you’ve released it to the world, we hope).

# *Freeing the same pointer twice*

This causes “undefined behavior.” Once the memory has been handed back to the allocation routines, they may merge the freed block with other free storage under management. Freeing something that’s already been freed is likely to lead to confusion or crashes at best, and so-called double frees have been known to lead to security problems.