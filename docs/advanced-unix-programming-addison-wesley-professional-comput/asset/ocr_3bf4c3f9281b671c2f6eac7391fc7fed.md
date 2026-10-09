clever solution is used in virtual-memory versions of UNIX, in which copying is particularly expensive, called copy-on-write. It works this way: On a fork, the parent and child share the data segment, which consists of a collection of pages. As long as a page stays unmodified, this shortcut works OK. Then as soon as parent or child attempts to write on a page, just that page is copied to give each its own version. This is transparent and efficient with the right kind of dynamic address-translation hardware, which almost all modern-day computers have. Since the exec follows very quickly in almost all cases, very few pages will have to be copied. But even if they all have to be copied, we are no worse off—in fact, we're better off, since we were able to start running the child earlier. Remember that a copy-on-write scheme is internal to the kernel; it does not change the semantics of fork, and, apart from better performance, users are unaware of it.

Even more efficient than copy-on-write, but not as transparent, is a variation on fork called vfork:

```
vfork—create new process; share memory (obsolete)

#include <unistd.h>
pid_t vfork(void);
/* Returns child process-ID and 0 on success or -1 on error (sets errno) */
```

vfork behaves exactly like fork insofar as creating the child process is concerned, but parent and child share the same data segment. There’s no copy-on-write—they both read and write the same variables, so havoc ensues unless the child immediately exits or does an exec, which is what normally happens anyway (see the example function execute2 in the next section).5 In early versions of BSD UNIX, vfork was important; however, its performance advantages over fork are no longer substantial and its use is dangerous, so you should not use it, which is why it’s marked “obsolete” in the synopsis.

A more recent attempt to improve the efficiency of fork and exec is posix_spawm, part of a 1999 POSIX update. Because its end result is a child process running a different program, it avoids the problems of vfork. It doesn’t offer all the flexibility of a separate fork and exec, but it does handle the most common cases (e.g., duplicating a file descriptor). The real purpose of

> 5. Two processes concurrently reading and writing the same variables is similar to threads, with similar potential dangers. Section 5.17 has more.