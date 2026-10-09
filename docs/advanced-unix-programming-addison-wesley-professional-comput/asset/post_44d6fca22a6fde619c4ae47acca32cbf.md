
# 1.4.3 Using C++ Exceptions

Before you spend too much time and energy deciding whether you like the “ec” macros in the previous section and coming up with some improvements, you might ask yourself whether you’ll even be programming in C. These days it’s much more likely that you’ll use C++. Just about everything in this book works fine in a C++ program, after all. C is still often preferred for embedded systems, operating systems (e.g., Linux), compilers, and other relatively low-level software, but those kinds of systems are likely to have their own, highly specialized, error-handling mechanisms.

C++ provides an opportunity to handle errors with exceptions, built into the C++ language, rather than with the combination of gotos and return statements that we used in C. Exceptions have their own pitfalls, but if used carefully they're easier to use and more reliable than the “ec” macros, which don’t protect you from, say, using `ec_null` when you meant to use `ec_neg1`.

As the library that contains the system-call wrapper code is usually set up just for C, it won’t throw exceptions unless someone’s made a special version for C++. So, to use exceptions you need another layer of wrapping, something like this for the `close` system call:

```cpp
class syscall_ex {
    public:
        int se_errno;
        
        syscall_ex(int n) 
            : se_errno(n)
        { }
        void print(void)
        {
            fprintf(stderr, "ERROR: %s\n", strerror(se_errno));
        }
};

class syscall {
    public:
        static int close(int fd)
        {
            int r;
            if ((r = ::close(fd)) == -1)
                throw(syscall_ex(errno));
            return r;
        }
};
```

Then you just call `syscall::close` instead of plain `close`, and it throws an exception on an error. You probably don’t want to type in the code for the other 1100 or so UNIX functions, but perhaps just the ones your application uses.

If you want the exception information to include location information such as file and line, you need to define *another* wrapper, this time a macro, to capture the preprocessor data (e.g., via `__LINE__`), so here’s an even fancier couple of classes:

```cpp
class syscall_ex {
 public:
  int se_errno;
  const char *se_file;
  int se_line;
  const char *se_func;

  syscall_ex(int n, const char *file, int line, const char *func)
    : se_errno(n), se_file(file), se_line(line), se_func(func)
  { }
  void print(void)
  {
    fprintf(stderr, "ERROR: %s (%s:%d %s())\n",
            strerror(se_errno), se_file, se_line, se_func);
  }
};

class syscall {
 public:
  static int close(int fd, const char *file, int line, const char *func)
  {
    int r;
    if ((r = ::close(fd)) == -1)
      throw(syscall_ex(errno, file, line, func));
    return r;
  }
};

#define Close(fd) (syscall::close(fd, __FILE__, __LINE__, __func__))
```

This time you call `Close` instead of `close`.

You can goose this up with a call-by-call trace, as we did for the “ec” macros if you like, and probably go even further than that.

There’s an example C++ wrapper, Ux, for all the system calls in this book that’s described in Appendix B.

# 1.5 UNIX Standards

Practically speaking, what you’ll mostly find in the real world is that the commercial UNIX vendors follow the Open Group branding (Section 1.2), and the open-source distributors claim only conformance to POSIX1990, although, with few exceptions, they don’t bother to actually run the certification tests. (The tests have now been made freely available, so future certification is now more likely.)

## 1.5.1 Evolution of the API Standards

Enumerating all the various POSIX and Open Group standards, guides, and specifications would be enormously complicated and confusing. For most purposes, the relevant developments can be simplified by considering them as a progression of standards relevant to the UNIX API, of which only the eight shown in Table 1.2 are important for the purposes of this book.

**Table 1.2 POSIX and Open Group API Standards**

| Name | Standard | Comments |
| --- | --- | --- |
| POSIX1988 | IEEE Std 1003.1-1988 (198808L$^{\ast}$) | First standard |
| POSIX1990 | IEEE Std 1003.1-1990/ ISO 9945-1:1990 (199009L) | Minor update of POSIX1988 |
| POSIX1993 | IEEE Std 1003.1b-1993 (199309L) | POSIX1990 + real-time |
| POSIX1996 | IEEE Std 1003.1-1996/ISO 9945-1:1996 (199506L) | POSIX1993 + threads + fixes to real-time |
| XPG3 | X/Open Portability Guide | First widely distributed X/Open guide |
| SUS1 | Single UNIX Specification, Version 1 | POSIX1990 + all commonly used APIs from BSD, AT&T System V, and OSF; also known as Spec 1170; certified systems branded UNIX 95$^{\dagger}$ |
| SUS2 | Single UNIX Specification, Version 2 | SUS1 updated to POSIX1996 + 64-bit, large file, enhanced multibyte, and Y2K; UNIX 98 brand |
| SUS3 | Single UNIX Specification, Version 3 (200112L) | Update to SUS2; API part identical to IEEE Std 1003.1-2001 (POSIX fully merged with Open Group); UNIX 03 brand |

$^{\ast}$ These huge numbers are the year and month of approval by IEEE. They’re used in feature testing as explained in the next section.

$^{\dagger}$ Spec 1170 gets its name from the total number of APIs, headers, and commands.

Actually, there is also a POSIX2001 (IEEE Std POSIX.1-2001), but as it’s contained in SUS3, we don’t need a separate row for it.

Even with this over-simplified list, we can already see that the loose statement that an OS “conforms to POSIX” is meaningless and probably indicates that whoever is making it either doesn’t really know POSIX (or SUS) or is assuming that the listener doesn’t. What POSIX? And, since newer features like real time and threads are optional, what options? Generally, here’s how to interpret what you’re hearing:

- If all you hear is POSIX, it probably means POSIX1990, which was the first and last OS standard that most people bothered to become aware of.
- Unless you know that the OS has passed certification tests established by standards organizations, all you can be sure of is that the OS developers took the POSIX standard into account somehow.
- You have to investigate the status of optional features separately (more on that shortly).

## 1.5.2 Telling the System What You Want

In this and the next section I’ll describe what you’re *supposed* to do according to the standards to ensure that your application conforms and to check what version of the standard the OS conforms to. Then you can decide how much of this you want to do and how much is just mumbo-jumbo that you can skip.

First of all, your application can state what version of the standard it expects by defining a preprocessor symbol before including any POSIX headers, such as unistd.h. This limits the standard headers (e.g., stdio.h, unistd.h, errno.h) to only those symbols that are defined in the standard. To limit yourself to classic POSIX1990, you do this:

```c
#define _POSIX_SOURCE
#include <sys/types.h>
#include <unistd.h>
```

For a newer POSIX standard you have to be more specific, with another symbol, like this:

```c
#define _POSIX_SOURCE
#define _POSIX_C_SOURCE 199506L
#include <sys/types.h>
#include <unistd.h>
```

EC_FAIL is used when an error condition arises from a test that doesn’t use the macros in the previous paragraph.
EC_CLEANUP is used when we just want to jump to the cleanup code.
EC_FLUSH is used when we just want to display the error information, without waiting to exit. It’s handy in interactive programs that need to keep going. (The argument isn’t used.)

The various service functions called from the macros won’t be shown here, since they don’t illustrate much about UNIX system calls (they just use Standard C), but you can go to the AUP Web site [AUP2003] to see them along with an explanation of how they work. Here’s a summary:

- ec_push pushes the error and context information passed to it (by the ec_cmp macro, say) onto a stack.
- There’s a function registered atexit that prints the information on the stack when the program exits:

```c
static void ec_atexit_fcn(void)
{
    ec_print();
}
```

- ec_print walks down the stack to print the trace and error information.
- ec_reinit erases what’s on the stack, so error-checking can start with a fresh trace.
- ec_warn is called from the EC_CLEANUP_BGN code if we accidentally fall into it.

All the functions are thread-safe so they can be used from within multithreaded programs. More on what this means in Section 5.17.
