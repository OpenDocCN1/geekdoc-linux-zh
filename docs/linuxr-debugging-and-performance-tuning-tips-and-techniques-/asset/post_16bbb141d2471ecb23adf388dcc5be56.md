
## 12.8 Regular Expressions

```
106 while (getline(& buf, &size, fp) != -1) {
107 ret = regexec(& pattern, buf, 0, NULL, 0);
108 if (ret != 0) {
109 if (ret != REG_NOMATCH) {
110 (void) regerror(ret, & pattern, error, sizeof error);
111 fprintf(stderr, "%s: file %s: %s\n", myname, name, error);
112 free(buf);
113 errors++;
114 return;
115 }
116 } else
117 printf("%s: %s", name, buf); /* print matching lines */
118 }
119 free(buf);
120 }
```

Lines 97–120 define process(), which reads the file and does the regular expression match. The outer loop (lines 106–119) reads input lines. We use getline() (see Section 3.2.1.9, “glibc Only: Reading Entire Lines: getline() and getline()”, page 73) to avoid line-length problems. Line 107 calls regexec(). A nonzero return indicates either failure to match or some other error. Thus, lines 109–115 check for REG_NOMATCH and print an error only if some other problem occurred—failure to match isn’t an error.

If the return value was 0, the line matched the pattern and thus line 117 prints the filename and matching line.

```
122 /* usage --- print usage message and exit */
123
124 void usage(void)
125 {
126 fprintf(stderr, "usage: %s [-i] [-E] pattern [ files ... ]\n", myname);
127 exit(1);
128 }
```

The usage() function prints a usage message and exits. It’s called when invalid options are provided or if no pattern is provided (lines 38–40 and 44–45).

That’s it! A modest, yet useful version of grep, in under 130 lines of code.

## 12.9 Suggested Reading

- _Programming Pearls_, 2nd edition, by Jon Louis Bentley. Addison-Wesley, Reading, Massachusetts, USA, 2000. ISBN: 0-201-65788-0. See also this book’s web site.[^10]
    - Program design with assertions is one of the fundamental themes in the book.
- _Building Secure Software: How to Avoid Security Problems the Right Way_, by John Viega and Gary McGraw. Addison-Wesley, Reading, Massachusetts, USA, 2001. ISBN: 0-201-72152-X.
    - Race conditions are only one of many issues to worry about when you are writing secure software. Random numbers are another. This book covers both, among other things. (We mentioned it in the previous chapter.)
- _The Art of Computer Programming: Volume 2: Seminumerical Algorithms_, 3rd edition, by Donald E. Knuth. Addison-Wesley, Reading, Massachusetts, USA, 1998. ISBN: 0-201-89684-2. See also the book’s web site.[^11]
    - This is the classic reference on random number generation.
- _Random Number Generation and Monte Carlo Methods_, 2nd edition, by James E. Gentle. Springer-Verlag, Berlin, Germany, 2003. ISBN: 0-387-00178-6.
    - This book has wide coverage of the methods for generating and testing pseudo-random numbers. While it still requires background in mathematics and statistics, the level is not as high as that in Knuth’s book. (Thanks to Nelson H.F. Beebe for the pointer to this reference.)
- _sed & awk_, 2nd edition, by Dale Dougherty and Arnold Robbins. O’Reilly and Associates, Sebastopol, California, USA, 1997. ISBN: 1-56592-225-5.
    - This book gently introduces regular expressions and text processing, starting with `grep`, and moving on to the more powerful `sed` and `awk` tools.
- _Mastering Regular Expressions_, 2nd edition, by Jeffrey E.F. Friedl. O’Reilly and Associates, Sebastopol, California, USA, 2002. ISBN: 0-59600-289-0.
    - Regular expressions are an important part of Unix. For learning how to chop, slice, and dice text using regular expressions, we recommend this book.
- The online manual for GNU grep also explains regular expressions. On a GNU/Linux system, you can use `info grep` to look at the local copy. Or use a web browser to read the GNU Project’s online documentation for grep.

[^10]: http://www.gnu.org/software/grep/doc/grep.html

## 12.10 Summary

- Assertions provide a way to make statements about the expected state of a program. They are a useful design and debugging tool and should generally be left in production code. Be careful, however, not to confuse assertions with runtime checks for possible failure conditions.

- The `memXXX()` functions provide analogues to the better-known `strXXX()` functions. Their greatest value is that they can work on binary data; zero bytes are no different from other bytes. Of particular note is `memcpy()` vs. `memmove()` and the handling of overlapping copies.

- Temporary files are useful in many applications. The `tmpfile()` and `mkstemp()` APIs are the preferred way to create temporary files while avoiding race conditions and their security implications. Many programs use the `TMPDIR` environment variable to specify the location for their temporary files, with a meaningful default (usually `/tmp`) if that variable isn’t defined. This is a good convention, one you should adopt for your own programs.

- The `abort()` function sends a `SIGABRT` to the calling process. The effect is to kill the process and create a core dump, presumably for debugging.

- `setjmp()` and `longjmp()` provide a nonlocal goto. This is a powerful facility that must be used with care. `sigsetjmp()` and `siglongjmp()` save and restore the process signal mask when a program does a nonlocal jump. The problems with nonlocal gotos sometimes outweigh their benefits; thus, use these routines only if there isn’t a better way to structure your application.

- Random numbers are useful in a variety of applications. Most software uses pseudorandom numbers—sequences of numbers that appear random but that can be reproduced by starting with the same seed each time. `rand()` and `srand()` are the original API, standardized by the C language. On many systems, `rand()` uses a subpar algorithm. `random()` and `srandom()` use a better algorithm, are included in the POSIX standard, and are preferred over `rand()` and `srand()`. Use the `/dev/random` and `/dev/urandom` special files (a) if they’re available and (b) if you need high-quality random numbers.

- Three APIs provide increasingly powerful facilities for metacharacter expansion (wildcarding).
    - `fnmatch()` is the simplest, returning true/false as a given string does or doesn’t match a given wildcard pattern.
    - `glob()` works its way through the filesystem, returning a list of pathnames that match a given wildcard. When the standard `glob()` functionality is all that’s needed, it should be used. While the GLIBC version of `glob()` has some extensions, portable programs needing the extra power should use `wordexp()` instead. (Programs that will only run on GNU/Linux systems should feel free to use the full power of the GLIBC `glob()`.)
    - `wordexp()` not only does what `glob()` does, but it also does full shell word expansion, including tilde expansion, shell variable expansion, and command substitution.
    - The `regcomp()` and `regexec()` functions give you access to POSIX basic and extended regular expressions. By using one or the other, you can make your program behave identically to the standard utilities, making it much easier for programmers familiar with GNU/Linux and Unix to use your program.

## Exercises

1. Use `read()` and `memcmp()` to write a simple version of the `cmp` program that compares two files. Your version need not support any options.
2. Use the `<stdio.h>` `getc()` macro and direct comparison of each read character to write another version of `cmp` that compares two files. Compare the performance of this version against the one you wrote for the previous exercise.
3. (Medium.) Consider the `<stdio.h> fgets()` and Glibc `getline()` functions. Would `memcpy()` be useful for implementing them? Sketch a possible implementation of `fgets()` using it.
4. (Hard.) Find the source to the Glibc version of `memcpy()`. This should be on one of the source code CD-ROMs in your GNU/Linux distribution, or you can find it by a Web search. Examine the code, and explain it.
5. Test your memory. How does `tmpfile()` arrange for the file to be deleted when the file pointer is closed?
6. Using `mkstemp()` and `fdopen()` and any other functions or system calls you think necessary, write your own version of `tmpfile()`. Test it too.
7. Describe the advantages and disadvantages of using `unlink()` on the filename created by `mkstemp()` immediately after `mkstemp()` returns.
8. Write your own version of `mkstemp()`, using `mktemp()` and `open()`. How can you make the same guarantees about uniqueness that `mkstemp()` does?
9. Programs using `mkstemp()` should arrange to clean up the file when they exit. (Assume that the file is not immediately unlinked after opening, for whatever reason.) This includes the case in which a terminating signal could arrive. So, as part of a signal catcher, the file should be removed. How do you do this?
10. (Hard.) Even with the first-cut signal-handling cleanup, there's still a race condition. There's a small window between the time `mkstemp()` creates the temporary file and the time its name is returned and recorded (for use by the signal handling function) in a variable. If an uncaught signal is delivered in that window, the program dies and leaves behind the temporary file. How do you close that window? (Thanks to Jim Meyering.)
11. Try compiling and running `ch12-setjmp.c` on as many different systems with as many different compilers as you have access to. Try compiling with and without different levels of optimizations. What variations in behavior, if any, did you see?
12. Look at the file `/usr/src/libc/gen/sleep.c` in the V7 Unix source distribution. It implements the `sleep()` function described in Section 10.8.1, “Alarm Clocks: sleep(), alarm(), and SIGALRM,” page 382. Print it, and annotate it in the style of our examples to explain how it works.
