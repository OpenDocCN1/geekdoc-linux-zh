Of course, the disadvantage to using environment variables is that they can *silently* change a program's behavior. Jim Meyering, the maintainer of the Coreutils, put it this way:

> It makes it easy for the user to customize how the program works without changing how the program is invoked. That can be both a blessing and a curse. If you write a script that depends on your having a certain environment variable set, but then have someone else use that same script, it may well fail (or worse, silently produce invalid results) if that other person doesn't have the same environment settings.

# 2.4.1 Environment Management Functions

Several functions let you retrieve the values of environment variables, change their values, or remove them. Here are the declarations:

```
```
#include <stdlib.h>
char *getenv(const char *name);                 /* ISO C: Retrieve environment variable */
int setenv(const char *name, const char *value,  /* POSIX: Set environment variable */
           int overwrite);
int putenv(char *string);                        /* XSI: Set environment variable, uses string */
void unsetenv(const char *name);                 /* POSIX: Remove environment variable */
int clearenv(void);                              /* Common: Clear entire environment */
```
```

The `getenv()` function is the one you will use 99 percent of the time. The argument is the environment variable name to look up, such as `"HOME"` or `"PATH"`. If the variable exists, `getenv()` returns a pointer to the character string value. If not, it returns `NULL`. For example:

```
```
char *pathval;

/* Look for PATH; if not present, supply a default value */
if ((pathval = getenv("PATH")) == NULL)
    pathval = "/bin:/usr/bin:/usr/ucb";
```
```

Occasionally, environment variables exist, but with empty values. In this case, the return value will be non-NULL, but the first character pointed to will be the zero byte, which is the C string terminator, `'\0'`. Your code should be careful to check that the return value pointed to is not NULL. Even if it isn't NULL, also check that the string is not empty if you intend to use its value for something. In any case, don't just blindly use the returned value.