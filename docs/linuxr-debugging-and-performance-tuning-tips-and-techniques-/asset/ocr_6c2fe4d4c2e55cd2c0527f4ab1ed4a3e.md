# 9.4.1 Duplicating Open Files: dup() and dup2()

Two system calls create a copy of an open file descriptor:

```
```
#include <unistd.h>
int dup(int oldfd);
int dup2(int oldfd, int newfd);
```
```

The functions are as follows:

```
`int dup(int oldfd)`
```

Returns the lowest unused file descriptor value; it is a copy of oldfd. dup() returns a nonnegative integer on success or -1 on failure.

```
`int dup2(int oldfd, int newfd)`
```

Makes newfd be a copy of oldfd; if newfd is open, it's closed first, as if by close(). dup2() returns the new descriptor or -1 if there was a problem.

Remember Figure 9.1, in which two processes shared pointers to the same file entry in the kernel's file table? Well, dup() and dup2() create the same situation, within a single process. See Figure 9.4.

![](bbox=[0.08, 0.72, 0.62, 0.9])

**FIGURE 9.4** File descriptor sharing after `dup2(1, 3)`

In this figure, the process executed `dup2(1, 3)` to make file descriptor 3 a copy of standard output, file descriptor 1. Exactly as described before, the two descriptors share the file offset for the open file.