dlsym searches for the symbol or function specified by the symbol argument in the loaded object (the object loaded by dlopen) to which handle refers. handle must be a handle returned by dlopen; symbol is a standard, C-style string. dlsym returns a void pointer to the symbol or NULL on failure.

Robust code checks for and handles as many errors as possible. The dlerror function allows you to find out more about an error that occurs when using dynamically loaded objects. Its prototype is as follows:

```
const char *dlerror(void);
```

If any of the other dl interface function calls fail, dlerror returns a string describing the error. Calling dlerror also resets the error string to NULL. As a result, a second immediate call to dlerror will return NULL. dlerror returns a string describing the most recent error, or NULL otherwise.

To conserve system resources, particularly memory, be sure to unload the code in a shared object when you are finished using it. However, because of the overhead involved in loading and unloading shared objects, be certain that you will not need it before unloading it. dlclose, prototyped as follows, unloads a shared object:

```
int dlclose(void *handle);
```

dlclose unloads the object to which handle refers. The call also invalidates handle. Because the dl library maintains link counts for dynamically loaded objects, the objects are not deallocated and unloaded until dlclose has been called on an object as many times as dlopen was successfully called on it.

# ### Using the dl Interface

To illustrate using the dl interface, return again to the trusty errorhandling library used throughout this chapter. This time, however, use a new driver program, as shown in the following example.

# **Example**

![](bbox=[0.045, 0.67, 0.11, 0.73])

# **Example**

Before using this example, make sure you have built the shared library version of librerr, librerr.so, using the instructions provided in the "Creating a Shared Library" section earlier in this chapter.

```
/*
 * dltest.c - Dynamically load librerr.so and call err_ret
 */
#include <stdio.h>
#include <stdlib.h>
#include <dlfcn.h>

int main(void)
```