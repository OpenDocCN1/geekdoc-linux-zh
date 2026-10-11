Upon reaching line 83, the program needs more space in the buffer. Here's where the dynamic memory management comes into play. Note the comment about preserving p (lines 83-84); we discussed this earlier in terms of reinitializing pointers into dynamic memory. end is also reset. Line 89 resizes the memory.

Note that here the function being called is xrealloc(). Many GNU programs use “wrapper” functions around malloc() and realloc() that automatically print an error message and exit if the standard routines return NULL. Such a wrapper might look like this:

```
extern const char *myname;     /* set in main() */

void *xrealloc(void *ptr, size_t amount)
{
    void *p = realloc(ptr, amount);
    if (p == NULL) {
        fprintf(stderr, "%s: out of memory!\n", myname);
        exit(1);
    }
}
```

Thus, if xrealloc() returns, it’s guaranteed to return a valid pointer. (This strategy complies with the “check every call for errors” principle while avoiding the code clutter that comes with doing so using the standard routines directly.) In addition, this allows valid use of the construct `ptr = xrealloc(ptr, new_size)`, which we otherwise warned against earlier.

Note that it is not always appropriate to use such a wrapper. If you wish to handle errors yourself, you shouldn’t use it. On the other hand, if running out of memory is always a fatal error, then such a wrapper is quite handy.

```
97      if (ferror (ebuf->fp))
98        fatal_with_name (ebuf->floc.filename;
99
100     /* If we found some lines, return how many.
101      If we didn't, but we did find *something*, that indicates we read the last
102      line of a file with no final newline; return 1.
103      If we read nothing, we're at EOF; return -1. */
105     return nlines ? nlines : p = ebuf->bufstart ? -1 : 1;
106   }
```