we used in C. Exceptions have their own pitfalls, but if used carefully they're easier to use and more reliable than the “ec” macros, which don’t protect you from, say, using `ec_null` when you meant to use `ec_neg1`.

As the library that contains the system-call wrapper code is usually set up just for C, it won’t throw exceptions unless someone’s made a special version for C++. So, to use exceptions you need another layer of wrapping, something like this for the `close` system call:

```
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

If you want the exception information to include location information such as file and line, you need to define *another* wrapper, this time a macro, to capture the preprocessor data (e.g., via `_LINE_`),\u00b9³ so here’s an even fancier couple of classes: