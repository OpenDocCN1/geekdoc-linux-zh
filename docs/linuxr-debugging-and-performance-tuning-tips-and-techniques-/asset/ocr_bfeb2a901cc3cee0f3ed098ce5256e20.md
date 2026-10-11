This chapter describes several extended APIs. The APIs here are similar in nature to those described earlier in the book or provide additional facilities. Some of them could not be discussed easily until after the prerequisite topics were covered. The presentation order here parallels the order of the chapters in the first half of the book. The topics are not otherwise related to each other. We cover the following topics: dynamically allocating aligned memory; file locking; a number of calls that work with subsecond time values; and a more advanced suite of functions for storing and retrieving arbitrary data values. Unless stated otherwise, all the APIs in this chapter are included in the POSIX standard.

# 14.1 Allocating Aligned Memory: posix_memalign() and memalign()

For most tasks, the standard allocation routines, malloc(), realloc(), and so on, are fine. Occasionally, though, you may need memory that is aligned a certain way. In other words, the address of the first allocated byte is a multiple of some number. (For example, on some systems, memory copies are significantly faster into and out of word-aligned buffers.) Two functions offer this service:

```
#include <stdlib.h>

int posix_memalign(void **memptr, size_t alignment, size_t size); POSIX ADV
void *memalign(size_t boundary, size_t size); Common
```

posix_memalign() is a newer function; it’s part of yet another optional extension, the “Advisory Information” (ADV) extension. The function works differently from most other allocation Linux APIs. It does not return -1 when there’s a problem. Rather, the return value is 0 on success or an errno value on failure. The arguments are as follows:

+   - void **memptr
+   
+     A pointer to a void * variable. The pointed-to variable will have the address of the allocated storage placed into it. The allocated storage can be released with free().
+   
+   - size_t alignment
+   
+     The required alignment. It must be a multiple of sizeof(void *) and a power of 2.