
No standard requires that a given facility be implemented as a system call, rather than a library function, and I won't make much of the distinction between the two when I introduce one or when I show one being used in an example program. Don't take my use of the term “system call” too literally, either; I just mean that the facility is usually implemented that way.

### 1.3.2 Other Language Bindings

While the main UNIX standards documents, POSIX and SUS, describe the interfaces in C, they recognize that C is only one of many languages, and so they've defined bindings for other standardized languages as well, such as Fortran and Ada. No problem with easy functions like `read`, as long as the language has some way of passing in integers and addresses of buffers and getting an integer back, which most do (Fortran was a challenge). It's tougher to handle structures (used by `stat`, for instance) and linked lists (used by `getaddrinfo`). Still, language experts usually find a way.^{12}

Lots of languages, like Java, Perl, and Python, have standard facilities that support some POSIX facilities. For instance, here's a Python program that uses the UNIX system called `fork` to create a child process. (I'll get to `fork` in Chapter 5; for now all you need to know is that it creates a child process and then returns in both the child and the parent, with different values, so both the `if` and `else` are true, in the parent and child, respectively.)

```python
import os
pid = os.fork()
if pid == 0:
    print 'Parent says, "HELLO!"'
else:
    print 'Child says, "hello!"'
```

This is the output:

```text
Parent says, "HELLO!"
Child says, "hello!"
```

There won't be any further examples using languages other than C and C++ in this book other than in Appendix C, which talks about Java and Jython (a version of Python that runs in a Java environment).

- 12. For example, Jython, described in Appendix C, makes extensive use of the Java Native Interface (JNI).

### 1.3.3 Guidelines for Calling Library Functions

Here are some general guidelines for calling library functions (from C or C++), which apply to system calls or to any other functions:

- Include the necessary **headers** (as I discussed previously).
- Make sure you know how the function indicates an **error**, and check for it unless you have a *good reason not to* (Section 1.4). If you're not going to check, document your decision by casting the return value to `void`, like this:

```c
(void)close(fd);
```

We violate this guideline consistently for `printf`, but with few other exceptions I follow it in our example programs.

- Don’t use **casts** unless absolutely necessary, because they might hide a mistake. Here’s what you shouldn’t do:

```c
int n;
struct xyz *p;
...
free((void *)p); /* gratuitous cast */
```

The problem is that if you mistakenly write `n` instead of `p`, the cast will suppress a compiler warning. You don’t need the cast when the function’s prototype specifies `void *`. If you’re not sure whether the type you want to use is OK, leave the cast off so the compiler can tell you. This would apply to the case when the function calls, say, for an `int` and you want to give it a `pid_t` (the type for a process ID). Better to get the warning if there will be one than to shut the compiler up before it has a chance to speak. If you do get a warning, and you’ve determined that a cast is the fix, you can put the cast in then.

- If you’ve got more than one **thread**, know whether the function you want to call is thread safe—that is, whether it handles global variables, mutexes (semaphores), signals, etc., correctly for a multithreaded program. Many functions don’t.

- Try to write to the **standard interfaces** rather than to those on your particular system. This has a lot of advantages: Your code will be more portable, the standardized functionality is probably more thoroughly tested, it will be easier for another programmer to understand what you’re doing, and your code is more likely to be compatible with the next version of the operating system. In practice, what you can do is keep a browser open to the Open Group Web site (Section 1.9 and [SUS2002]), where there’s a terrific alphabetized reference to all standard functions (including the Standard C library) and all header files. This is a much better approach than, say, using the man pages on your local UNIX system. Sure, sometimes you do need to look up particulars for your system, and occasionally you need to use something nonstandard. But make that the exception rather than the rule, and document that it’s nonstandard with a comment. (Lots more about what I mean by “standard” in Section 1.5.)

### 1.3.4 Function Synopses

I’ll formally introduce each system call or function that I discuss in detail with a brief synopsis of it that documents the necessary headers, the arguments, and how errors are reported. Here’s one for `atexit`, a Standard C function, that we’re going to need in Section 1.4.2:

```c
atexit—register function to be called when process exits
#include <stdlib.h>
int atexit(
    void (*fcn)(void) /* function to be called */
);
/* Returns 0 on success, non-zero on error (errno not defined) */
```

(If you’re not already familiar with `errno`, it’s explained in the next section.)

The way `atexit` works is that you declare a function like this:

```c
static void fcn(void)
{
    /* work to be done at exit goes here */
}
```

and then you register it like this:

```c
if (atexit(fcn) != 0) {
    /* handle error */
}
```

Now when the process exits, your function is automatically called. You can register more than 1 function (up to 32), and they’re all called in the reverse order of their registration. Note that the test in the `if` statement was for non-zero, since that’s exactly what the wording in the synopsis said. It wasn’t a test for 1, or greater than zero, or −1, or false, or NULL, or anything else. That’s the only safe way to do it. Also, it makes it easier later if you're looking for a bug and are trying to compare the code to the documentation. You don't have to solve a little puzzle in your head to compare the two.

## 1.4 Error Handling

Testing error returns from system calls is tricky, and handling an error once you discover it is even trickier. This section explains the problem and gives some practical solutions.

### 1.4.1 Checking for Errors

Most system calls return a value. In the `read` example (Section 1.3.1), the number of bytes `read` is returned. To indicate an error, a system call usually returns a value that can't be mistaken for valid data, typically -1. Therefore, my example should have been coded something like this:

```c
if ((amt = read(fd, buf, numbyte)) == -1) {
    fprintf(stderr, "Read failed!\n");
    exit(EXIT_FAILURE);
}
```

Note that `exit` is a system call too, but it can't return an error because it doesn't return. The symbol `EXIT_FAILURE` is in Standard C.

Of the system calls covered in this book, about 60% return -1 on an error, about 20% return something else, such as `NULL`, zero, or a special symbol like `SIG_ERR`, and about 20% don't report errors at all. So, you just can't assume that they all behave the same way—you have to read the documentation for each call. I'll provide the information when I introduce each system call.

There are lots of reasons why a system call that returns an error indication might have failed. For 80% of them, the integer symbol `errno` contains a code that indicates the reason. To get at `errno` you include the header `errno.h`. You can use `errno` like an integer, although it's not necessarily an integer variable. If you're using threads, `errno` is likely to involve a function call, because the different threads can't reliably all use the same global variable. So don't declare `errno` yourself (which used to be exactly what you were supposed to do), but use the definition in the header, like this (other headers not shown):
