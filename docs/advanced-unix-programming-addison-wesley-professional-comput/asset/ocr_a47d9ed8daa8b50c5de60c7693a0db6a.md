*posix_spawn* is to provide an efficient way to invoke a program as a child process in a realtime system when swapping would be too slow and the hardware lacks dynamic address translation. It’s possible to implement *posix_spawn* as a library function that uses *fork* and *exec* (Exercise 5.8), although in a realtime system of the sort its designers envisioned *posix_spawn* would have to be implemented as a system call.

It’s a good time to mention the Standard C function *system*:

```
system—run command

\#include <stdlib.h>

int system(  const char \*command  /\* command \*/
);  /* Returns exit status or -1 on error (sets errno) \*/
```

This function does a *fork* followed by an *exec* of the shell, passing the command argument as a shell command line. It’s a handy way to execute a command line from within a program, but it doesn’t provide the efficiency (the shell is always invoked) or flexibility of a separate *fork* followed by an *exec*, or of *posix_spawn*.

# ## 5.6 Implementing a Shell (Version 2)

Now let’s put *fork* and *execvp* together to make our shell from the previous section far more useful—it won’t just exit after running a command but will actually prompt for another one! We replace the function *execute* with *execute2*:

```
static void execute2(int argc, char \*argv[])  {
    pid_t pid;

    switch (pid = fork()) {
    case -1:  /\* parent (error) \*/
    EC_PFAIL
    case 0:  /\* child \*/
    execvp(argv[0], argv);
    EC_PFAIL
    default:  /\* parent \*/
    ec_neg1( wait(NULL) )
    }
    return;

```