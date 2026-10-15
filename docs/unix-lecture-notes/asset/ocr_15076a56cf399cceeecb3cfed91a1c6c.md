```
int pthread_attr_setstacksize(pthread_attr_t *attr, size_t stacksize);
```

The first argument is the address of the threads attribute structure and the second is the size that you want to set for the stack. This function will fail if the attribute structure does not exist, or if the stack size is smaller than the allowed minimum (PTHREAD_STACK_MIN) or larger than the maximum allowed. See the man page for further caveats about its use.

To get the stack's current size, use

```
int pthread_attr_getstacksize(pthread_attr_t *attr, size_t *stacksize);
```

This retrieves the current size of the stack. It will fail of course if attr does not reference an existing structure.

The problem trying to use this function is that it must be passed the attributes structure of the thread. There is no POSIX function to retrieve the attribute structure of the calling thread, but there is a GNU extension, pthread_getattr_np(). If this extension is not used, the best that the calling thread can do is to get a copy of the attribute structure with which it was created, which may have different values than the one it currently using. The following listing is of a program that prints the default stack size then sets the new stack size based on a command line argument, and from within the thread, displays the actual stack size it is using, using the GNU pthread_getattr_np() function. To save space, some error checking has been removed.

# Listing 10.3: Setting a new stack size (with missing error checking)

```
#define _GNU_SOURCE      /* To get pthread_getattr_np() declaration */
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>

void *thread_start(void *arg)
{
    size_t          stack_size;
    pthread_attr_t  gattr;

    pthread_getattr_np  ( pthread_self(), &gattr);
    pthread_attr_getstacksize(&gattr, &stack_size);
    printf("Actual stack size is %ld\n", stack_size);
    pthread_exit(0);
}

int main(int argc, char *argv[])
{
    pthread_t       thr;
    pthread_attr_t  attr;
    int             retval;
    size_t          new_stack_size, stack_size;
    void            *sp;

    if ( argc < 2 ) {
        printf("usage: %s stacksize\n", argv[0] );
```