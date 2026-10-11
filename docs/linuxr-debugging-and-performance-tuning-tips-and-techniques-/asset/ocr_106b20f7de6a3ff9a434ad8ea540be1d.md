# 4.4 Doing Input and Output

current line number in that file. These have been available in C since its beginning. C99 defines an additional predefined identifier, `__func__`, which represents the name of the current function as a character string. The macros are used like this:

```
if (some_system_call(param1, param2) < 0) {
    fprintf (stderr, *%s: *%s *%s *d*: some_system_call(*%d, *%d) failed: *%s\n*,
        argv[0], __func__, __FILE__, __LINE__,
        param1, param2, strerror(errno));
    return 1;
}
```

Here, the error message includes not only the program's name but also the function name, source file name, and line number. The full list of identifiers useful for diagnostics is provided in Table 4.2.

TABLE 4.2
C99 diagnostic identifiers

| Identifier | C version | Meaning |
| :--- | :--- | :--- |
| `__DATE__` | C89 | Date of compilation in the form "Mmm dd yyyy". |
| `__FILE__` | Original | Source-file name in the form "program.c". |
| `__LINE__` | Original | Source-file line number in the form 42. |
| `__TIME__` | C89 | Time of compilation in the form "hh:mm:ss". |
| `__func__` | C99 | Name of current function, as if declared `const char __func__[] = *name`. |

The use of `__FILE__` and `__LINE__` was quite popular in the early days of Unix, when most people had source code and could find the error and fix it. As Unix systems became more commercial, use of these identifiers gradually diminished, since knowing the source code location isn't of much help to someone who only has a binary executable.

Today, although GNU/Linux systems come with source code, said source code often isn't installed by default. Thus, using these identifiers for error messages doesn't seem to provide much additional value. The GNU Coding Standards don't even mention them.

# 4.4 Doing Input and Output

All I/O in Linux is accomplished through file descriptors. This section introduces file descriptors, describes how to obtain and release them, and explains how to do I/O with them.