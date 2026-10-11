
nftw() from processing hierarchies that are more than depth levels deep; but smaller values for depth mean that nftw() has to do more work.

### flags

A set of flags, bitwise OR’ed, that direct how nftw() should process the hierarchy.

The nftw() interface has two *disjoint* sets of flags. One set controls nftw() itself (the flags argument to nftw()). The other set is passed to the user-supplied function that nftw() calls (the flag argument to (*fn)()). However, the interface is confusing, because both sets of flags use names starting with the prefix `FTW_`. We’ll do our best to keep this clear as we go. Table 8.3 presents the flags that control nftw().

#### TABLE 8.3 Control flags for nftw()

| Flag | Meaning |
| :--- | :--- |
| `FTW_CHDIR` | When set, change to each directory before opening it. This action is more efficient, but the calling application has to be prepared to be in a different directory when nftw() is done. |
| `FTW_DEPTH` | When set, do a “depth-first search.” This means that all of the files and subdirectories in a directory are processed before the directory itself is processed. |
| `FTW_MOUNT` | When set, stay within the same mounted filesystem. This is a more specialized option. |
| `FTW_PHYS` | When set, do not follow symbolic links. |

`FTW_CHDIR` provides greater efficiency; when processing deep file hierarchies, the kernel doesn’t have to process full pathnames over and over again when doing a stat() or opening a directory. The time savings on large hierarchies can be quite noticeable.⁸

`FTW_DEPTH` may or may not be what you need; for some applications it’s just right. Consider `chmod -R u-rx .`. This removes read and execute permission for the owner of all files and subdirectories in the current directory. If this permission change is applied to a directory before it’s applied to the directory’s contents, any subsequent attempt to process the contents will fail! Thus, it should be applied after the contents have been processed.⁹ The GNU/Linux nftw(3) manpage notes for FTW_PHYS that “this is what you want.” This lets you process symbolic links as themselves, which is usually what’s necessary. (Consider du; it should count the link’s space separately from that of the linked-to file.)

### 8.4.3.2 The nftw() Callback Function

As nftw() runs, it calls a function to which you supply a pointer. (Such functions are termed *callback functions* since they are “called back” from library code.) The callback function receives four arguments:

- `const char *file`
  The name of the current file (directory, symbolic link, etc.) being processed.
- `const struct stat *sb`
  A pointer to a `struct stat` for the file.
- `int flag`
  One of several flag values (described below) indicating what kind of file this is or whether an error was encountered for the object.
- `struct FTW *s`
  This structure provides two separate pieces of information:

```c
struct FTW {
    int base;      /* Index in file of base part of filename */
    int level;     /* Depth of this item relative to starting point */
};
```

The flag parameter has one of the values listed in Table 8.4.

#### TABLE 8.4 Flag values for nftw() callback function

| Flag | Meaning |
| :--- | :--- |
| FTW_F | Object is a regular file. |
| FTW_D | Object is a directory. |
| FTW_DNR | Object is a directory that wasn't readable. |
| FTW_SL | Object is a symbolic link. |
| FTW_NS | Object is not a symbolic link, and stat() failed. |
| FTW_DP | Object is a directory whose children have already been processed. This can only happen if FTW_DEPTH was used in the call to nftw(). |
| FTW_SLN | Object is a symbolic link pointing to a nonexistent file. This can only happen if FTW_PHYS was not used in the call to nftw(). |

The `struct FTW *s` provides additional information that can be useful. `s->base` acts as an index into `file`; `file` is the full pathname of the object being processed (relative to the starting point). `file` + `s->base` points to the first character of the filename component of the file.

`s->level` indicates the current depth in the hierarchy; the original starting point is considered to be at level 0.

The callback function should return 0 if all is well. Any nonzero return causes nftw() to stop its processing and to return the same nonzero value. The manpage notes that the callback function should stop processing only by using its return value so that nftw() has a chance to clean up; that is, free any dynamic storage, close open file descriptors, and so on. The callback function should not use longjmp() unless the program will immediately exit. (longjmp() is an advanced function, which we describe in Section 12.5, "Nonlocal Gotos," page 446.) The recommended technique for handling errors is to set a global variable indicating that there were problems, return 0 from the callback, and deal with the failures once nftw() has completed traversing the file hierarchy. (GNU du does this, as we see shortly.)

Let's tie all this together with an example program. ch08-nftw.c processes each file or directory named on the command line, running nftw() on it. The function that processes each file prints the filename and type with indentation, showing the hierarchical position of each file. For a change, we show the results first, and then we show and discuss the program:

```bash
$ pwd
/home/arnold/work/prenhall/proge
$ code/ch08/ch08-nftw code
code (directory)
  ch02 (directory)
    ch02-printenv.c (file)
  ch03 (directory)
    ch03-memaddr.c (file)
  ch04 (directory)
    ch04-holes.c (file)
    ch04-cat.c (file)
    ch04-maxfdA.c (file)
    v7cat.c (file)
...
```

![](img/766b5597246d532412fad21b1c59ccec_297_0.png)

### Here’s the program itself:

```c
/* ch08-nftw.c --- demonstrate nftw() */
#include <stdio.h>
#include <errno.h>
#include <getopt.h>
#include <cftw.h>          /* gets <sys/types.h> and <sys/stat.h> for us */
#include <limits.h>        /* for PATH_MAX */
#include <unistd.h>        /* for getdtablesize(), getcwd() declarations */

#define _XOPEN_SOURCE 1                /* Required under GLIBC for nftw() */
#define _XOPEN_SOURCE_EXTENDED 1       /* Same */

#define SPARE_FDS 5       /* fds for use by other functions, see text */

extern int process(const char *file, const struct stat *sb,
                  int flag, struct FTW *s);

/* usage --- print message and die */
void usage(const char *name)
{
    fprintf(stderr, "usage: %s [-c] directory ...\n", name);
    exit(1);
}

/* main --- call nftw() on each command-line argument */
int main(int argc, char **argv)
{
    int i, c, nfds;
    int errors = 0;
    int flags = FTW_PHYS;
    char start[PATH_MAX], finish[PATH_MAX];

    while ((c = getopt(argc, argv, "c")) != -1) {
        switch (c) {
            case 'c':
                flags |= FTW_CHDIR;
                break;
            default:
                usage(argv[0]);
                break;
        }
    }

    if (optind == argc)
        usage(argv[0]);

    getcwd(start, sizeof start);

    nfds = getdtablesize() - SPARE_FDS; /* leave some spare descriptors */
    for (i = optind; i < argc; i++) {
        if (nftw(argv[i], process, nfds, flags) != 0) {
            fprintf(stderr, "%s: %s: stopped early\n",
                    argv[0], argv[i]);
            errors++;
        }
    }

    if ((flags & FTW_CHDIR) != 0) {
        getcwd(finish, sizeof finish);
        printf("Starting dir: %s\n", start);
        printf("Finishing dir: %s\n", finish);
    }

    return (errors != 0);
}
```

Lines 3–11 include header files. Through at least GLIBC 2.3.2, the `#defines` for `_XOPEN_SOURCE` and `_XOPEN_SOURCE_EXTENDED` are necessary before *any* header file inclusion. They make it possible to get the declarations and flag values that `nftw()` provides over and above those of `ftw()`. This is specific to GLIBC. The need for it will eventually disappear as GLIBC becomes fully compliant with the 2001 POSIX standard.

Lines 35–44 process options. The `-c` option adds the `FTW_CHDIR` flag to the `nftw()` flags. This is an experiment to see if you can end up somewhere different from where you started. It seems that if `nftw()` fails, you can; otherwise, you end up back where you were. (POSIX doesn’t document this explicitly, but the intent seems to be that you do end up back where you started. The standard does say that the callback function should not change the current directory.)

Line 49 saves the starting directory for later use, using `getcwd()`.
