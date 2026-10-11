# 12.7.1 Simple Pattern Matching: fnmatch()

We start with the `fnmatch()` (“filename match”) function:

```
#include <fnmatch.h>
int fnmatch(const char *pattern, const char *string, int flags);
```

This function matches string against pattern, which is a regular shell wildcard pattern. The `flags` value (described shortly) modifies the function’s behavior. The return value is `0` if string matches pattern, FNM_NOMATCH if it doesn’t, and a nonzero value if an error occurred. Unfortunately, POSIX doesn’t define any specific errors; thus, you can only tell that something went wrong, but not what.

The `flags` variable is the bitwise-OR of one or more of the flags listed in Table 12.1.

TABLE 12.1
Flag values for fnmatch()

| Flag name | GLIBC only | Meaning |
| --- | --- | --- |
| FNM_CASEFOLD | ✓ | Do case-insensitive matching. |
| FNM_FILE_NAME | ✓ | This is a GNU synonym for FNM_PATHNAME. |
| FNM_LEADING DIR | ✓ | This is a flag for internal use by GLIBC; don’t use it in your programs. See *fnmatch*(3) for the details. |
| FNM_NOESCAPE | | Backslash is an ordinary character, not an escape character. |
| FNM_PATHNAME | | Slash in string must match slash in pattern; it cannot be matched by `*`, `?`, or `['.']`. |
| FNM_PERIOD | | A leading period in string is matched only if pattern also has a leading period. The period must be the first character in string. However, if FNM_PATHNAME is also set, a period following a slash is treated as a leading period. |

`fnmatch()` works with strings from any source; strings to be matched need not be actual filenames. In practice though, you would use `fnmatch()` from code that reads a directory with readd ir() (see Section 5.3.1, “Basic Directory Reading,” page 133):