
## 2.2.3 getopt_long() Return Values

**TABLE 2.2**

`getopt_long()` return values

| Return code | Meaning |
|---|---|
| 0 | `getopt_long()` set a flag as found in the long option table. |
| 1 | `optarg` points at a plain command-line argument. |
| `'?'` | Invalid option. |
| `':'` | Missing option argument. |
| `'x'` | Option character `'x'`. |
| `-1` | End of options. |

Finally, we enhance the previous example code, showing the full switch statement:

```c
int do_all, do_help, do_verbose;      /* flag variables */
char *myfile, *user;                   /* input file, user name */

struct option longopts[] = {
    { "all",   no_argument,       & do_all,     1 },
    { "file",  required_argument,  NULL,       'f' },
    { "help",  no_argument,        & do_help,    1 },
    { "verbose", no_argument,     & do_verbose, 1 },
    { "user"  , optional_argument, NULL,       'u' },
    { 0, 0, 0, 0 }
};

...

while ((c = getopt_long(argc, argv, "ahvf:u::W:", longopts, NULL)) != -1) {
    switch (c) {
        case 'a':
            do_all = 1;
            break;
        case 'f':
            myfile = optarg;
            break;
        case 'h':
            do_help = 1;
            break;
        case 'u':
            if (optarg != NULL)
                user = optarg;
            else
                user = "root";
            break;
        case 'v':
            do_verbose = 1;
            break;
        case 0:  /* getopt_long() set a variable, just keep going */
            break;
#if 0
    case i:
    /*
     * Use this case if getopt_long() should go through all
     * arguments.  If so, add a leading `-` character to optstring.
     * Actual code, if any, goes here.
     */
    break;
#endif
    case ':':  /* missing option argument */
      fprintf (stderr, "%s: option `-%c' requires an argument\n",
               argv[0], optopt);

      break;
    case '?':
    default:  /* invalid option */
      fprintf (stderr, "%s: option `-%c' is invalid; ignored\n",
               argv[0], optopt);

      break;
    }
}
```

In your programs, you may wish to have comments for each option letter explaining what each one does. However, if you've used descriptive variable names for each option letter, comments are not as necessary. (Compare `do_verbose` to `vfl_g`.)

### 2.3.3.4 GNU `getopt()` or `getopt_long()` in User Programs

You may wish to use GNU `getopt()` or `getopt_long()` in your own programs and have them run on non-Linux systems. That's OK; just copy the source files from a GNU program or from the GNU C Library (Glibc) CVS archive.[^1] The source files are `getopt.h`, `getopt.c`, and `getopt1.c`. They are licensed under the GNU Lesser General Public License, which allows library functions to be included even in proprietary programs. You should include a copy of the file `COPYING.LIB` with your program, along with the files `getopt.h`, `getopt.c`, and `getopt1.c`.

Include the source files in your distribution, and compile them along with any other source files. In your source code that calls `getopt_long()`, use `#include <getopt.h>`, not `#include "getopt.h"`. Then, when compiling, add `-I.` to the C compiler's command line. That way, the local copy of the header file will be found first.

You may be wondering, “Gee, I already use GNU/Linux. Why should I include `getopt_long()` in my executable, making it bigger, if the routine is already in the C library?” That’s a good question. However, there’s nothing to worry about. The source code is set up so that if it’s compiled on a system that uses GLIBC, the compiled files will not contain any code! Here’s the proof, on our system:

```bash
$ uname -a
Linux example 2.4.18-14 #1 Wed Sep 4 13:35:50 EDT 2002 i686 i686 i386 GNU/Linux
$ ls -l getopt.o getopt1.o # Show file sizes
-rw-r--r-- 1 aarnold devel 9836 Mar 24 13:55 getopt.o
-rw-r--r-- 1 aarnold devel 10324 Mar 24 13:55 getopt1.o
$ size getopt.o getopt1.o # Show sizes included in executable
    text data bss dec hex filename
   0    0   0 0 0 getopt.o
   0    0   0 0 0 getopt1.o
```

The `size` command prints the sizes of the various parts of a binary object or executable file. We explain the output in Section 3.1, “Linux/Unix Address Space,” page 52. What’s important to understand right now is that, despite the nonzero sizes of the files themselves, they don’t contribute anything to the final executable. (We think this is pretty neat.)

## 2.4 The Environment

The `environment` is a set of `name=value` pairs for each program. These pairs are termed `environment variables`. Each `name` consists of one to any number of alphanumeric characters or underscores (`_`), but the `name` may not start with a digit. (This rule is enforced by the shell; the C API can put anything it wants to into the environment, at the likely cost of confusing subsequent programs.)

Environment variables are often used to control program behavior. For example, if `POSIXLY_CORRECT` exists in the environment, many GNU programs disable extensions or historical behavior that isn’t compatible with the POSIX standard.

You can decide (and should document) the environment variables that your program will use to control its behavior. For example, you may wish to use an environment variable for debugging options instead of a command-line argument. The advantage of using environment variables is that users can set them in their startup file and not have to remember to always supply a particular set of command-line options.

Of course, the disadvantage to using environment variables is that they can *silently* change a program's behavior. Jim Meyering, the maintainer of the Coreutils, put it this way:

> It makes it easy for the user to customize how the program works without changing how the program is invoked. That can be both a blessing and a curse. If you write a script that depends on your having a certain environment variable set, but then have someone else use that same script, it may well fail (or worse, silently produce invalid results) if that other person doesn't have the same environment settings.

### 2.4.1 Environment Management Functions

Several functions let you retrieve the values of environment variables, change their values, or remove them. Here are the declarations:

```c
#include <stdlib.h>
char *getenv(const char *name);                 /* ISO C: Retrieve environment variable */
int setenv(const char *name, const char *value,  /* POSIX: Set environment variable */
           int overwrite);
int putenv(char *string);                        /* XSI: Set environment variable, uses string */
void unsetenv(const char *name);                 /* POSIX: Remove environment variable */
int clearenv(void);                              /* Common: Clear entire environment */
```

The `getenv()` function is the one you will use 99 percent of the time. The argument is the environment variable name to look up, such as `"HOME"` or `"PATH"`. If the variable exists, `getenv()` returns a pointer to the character string value. If not, it returns `NULL`. For example:

```c
char *pathval;

/* Look for PATH; if not present, supply a default value */
if ((pathval = getenv("PATH")) == NULL)
    pathval = "/bin:/usr/bin:/usr/ucb";
```

Occasionally, environment variables exist, but with empty values. In this case, the return value will be non-NULL, but the first character pointed to will be the zero byte, which is the C string terminator, `'\0'`. Your code should be careful to check that the return value pointed to is not NULL. Even if it isn't NULL, also check that the string is not empty if you intend to use its value for something. In any case, don't just blindly use the returned value.

To change an environment variable or to add a new one to the environment, use `setenv()`:

```c
if (setenv("PATH", "/bin:/usr/bin:/usr/ucb", 1) != 0) {
    /* handle failure */
}
```

It’s possible that a variable already exists in the environment. If the third argument is true (nonzero), then the supplied value overwrites the previous one. Otherwise, it doesn’t. The return value is -1 if there was no memory for the new variable, and 0 otherwise. `setenv()` makes private copies of both the variable name and the new value for storing in the environment.

A simpler alternative to `setenv()` is `putenv()`, which takes a single `*name=value*` string and places it in the environment:

```c
if (putenv("PATH=/bin:/usr/bin:/usr/ucb") != 0) {
    /* handle failure */
}
```

`putenv()` blindly replaces any previous value for the same variable. Also, and perhaps more importantly, the string passed to `putenv()` is placed *directly* into the environment. This means that if your code later modifies this string (for example, if it was an array, not a string constant), the environment is modified also. This in turn means that you should *not* use a local variable as the parameter for `putenv()`. For all these reasons `setenv()` is preferred.

> **NOTE** The GNU `putenv()` has an additional (documented) quirk to its behavior. If the argument string is a name, then without an = character, the named variable is *removed*. The GNU env program, which we look at later in this chapter, relies on this behavior.

The `unsetenv()` function removes a variable from the environment:

```c
unsetenv("PATH");
```

Finally, the `clearenv()` function clears the environment entirely:

```c
if (clearenv() != 0) {
    /* handle failure */
}
```

This function is not standardized by POSIX, although it’s available in GNU/Linux and several commercial Unix variants. You should use it if your application must be very security conscious and you want it to build its own environment entirely from

[^1]: This footnote marker "3" in the original text likely refers to a footnote or reference note, kept as is or removed depending on strictness. Since the instruction says "preserve original language and all information", I will leave the superscript 3 if it was part of the text, but usually in markdown we might just remove the artifact if it's not a real footnote in the body. However, looking at the text "CVS archive.³", it seems like a footnote marker. I will keep it as `³` or just remove it if it's noise. The prompt says "preserve original language and all information". I will keep the `³` to be safe, or assume it's a footnote reference. Actually, looking at standard formatting, footnotes are often dropped in simple text reconstruction unless requested. But "all information" suggests keeping it. I will keep the `³`.

