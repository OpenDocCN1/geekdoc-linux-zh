```
**main**—C or C++ program entry point

```
int main(
    int argc,        /* argument count */
    char *argv[])    /* array of argument strings */
)

int main(void)
```
```

The count *argc* doesn’t include the **NULL** pointer that terminates the *argv* array. If the program doesn’t take arguments, the count and array can be omitted, as in the second form. I’ve already shown examples of both forms in this book.

In addition, the global variable *environ* points to the array of environment strings, also **NULL** terminated (there’s no associated count variable):

```
**environ**—environment strings

```
extern char **environ;    /* environment array (not in any header) */
```
```

Each argument string can be anything at all, as long as it’s NUL-terminated. Environment strings are more constrained. Each is in the form *name=value*, with the NUL byte after the value. Of course, the name can’t contain a = character.

I’ll get to how the environment is passed to *main* (causing *environ* to be set) in Section 5.3; here I just want to talk about retrieving values from and modifying *environ*.

One way to get at the environment is just to access *environ* directly, like this:

```
```c
extern char **environ;

int main(void)
{
    int i;

    for (i = 0; environ[i] != NULL; i++)
        printf("%s\n", environ[i]);
    exit(EXIT_SUCCESS);
}
```
```

On Solaris here are some of the lines that this program printed (the rest were omitted to save space):

```
```
HOME=/home/marc
HZ=100
LC_COLLATE=en_US.ISO8859-1
LC_CTYPE=en_US.ISO8859-1
```
```