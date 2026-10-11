The `$Date$` value appears in UTC or Universal Coordinated Time format, formerly known as Greenwich Mean Time. The symbolic name that `$Name$` represents is an alias that you can use to refer to a particular revision. To associate a symbolic name with a specific revision number, use the `-n<name>` switch when checking in a file. The `$State$` field defaults to experimental (Exp) because RCS considers all check ins to be trial runs until they are specifically marked as stable (Stab) or released (Rel) using the `-s<state>` switch.

# The ident Command

The `ident` command locates RCS keywords in files of all types and displays them to standard output. This feature lets you find out which revisions of which modules are used in a given program release. `ident` works by extracting strings of the form `$KEYWORD: VALUE $` from source, object, and binary files. It even works on raw binary data files and core dumps. In fact, because `ident` looks for any instance of the `$KEYWORD: VALUE $` pattern, you can also use words that are not RCS keywords.

This enables you to embed additional information into programs, for example, a company name. Embedded information can be a valuable tool for isolating problems to a specific code module. The slick part of this feature is that RCS updates the identification strings automatically—a real bonus for programmers and project managers.

# *Example*

![](bbox=[0.03, 0.45, 0.12, 0.51])

# **Example**

To illustrate using `ident`, create the following source file, check it in (using `-u`), compile and link it, ignore the warning you might get that `rcsid` is defined but not used, and then run the `ident` command on it.

```
```
/*
 * $Id$
 * prnenv.c - Display values of environment variables.
 */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

static char rcsid[] = "$ Id $\n";

int main(void)
{
    extern char **environ;
    char **my_env = environ;
```

```