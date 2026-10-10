# ## Include

`#include filename`

The `#include` directive inserts the contents of *filename* into the source text. The *filename* is usually called a header file, whose name traditionally ends with `.h`.

There are two possible forms of `#include`:

+   - `#include <filename>`	Searches for the file in some “standard” location before trying the current directory (or other locations specified as options to the compiler.) This form is used for standard and system header files.

+   - `#include "filename"`	Searches for the file in the current directory or other locations specified as options to the compiler. This form is used for header files you write that are not part of the standard or system header files.

# ## Define

`#define macro text`

The `#define` directive defines a macro. Whenever the macro name is encountered in the C source code, it is replaced by its definition. This may trigger another round of macro replacement. Consider this example:

```
```
#define N 100
#define BIG (N*N)
int a = BIG;
```
```

# **Note**

Macro names are typically uppercase, but this is tradition, not law.

The line `int a = BIG;` is replaced with `int a = (100*100);`. Macros are not replaced if their names appear inside string literals or comments.

You can also define macros that take arguments. Here’s an example:

```
```
#define SQUARE(x) x*x
int a = SQUARE(5);
```
```

In this case, `int a = SQUARE(5);` becomes `int a = 5*5;`. You have to be very careful when using macros with arguments, however. Consider this example:

```
```
#define SQUARE(x) x*x
int a = SQUARE(2+3);
```
```