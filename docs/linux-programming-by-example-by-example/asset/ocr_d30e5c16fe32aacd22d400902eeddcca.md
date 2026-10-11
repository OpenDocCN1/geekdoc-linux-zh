You must use the -x option to tell g c c to begin compilation at a certain step, in this case, with preprocessed source code. Linking the object file, finally, creates a binary:

```
$ gcc hello.o -o hello
```

Hopefully, you can see that it is far simpler to use the "abbreviated" syntax, g c c hello.c -o hello. The step-by-step example demonstrated that you can stop and start compilation at any step, should the need arise.

One situation in which you want to step through compilation is when you are creating libraries. In this case, you only want to create object files, so the final link step is unnecessary. Another circumstance where you would want to walk through the compilation process is when an # i n c l u d e d file introduces conflicts with your own code or perhaps with another # i n c l u d e d file. Stepping through the process will make it clearer which file is introducing the conflict.

# ## Using Multiple Source Code Files

Most C programs consist of multiple source files, so each source file must be compiled to object code before the final link step. This requirement is easily met. Just provide g c c with the name of each source code file it has to compile. It handles the rest. The g c c invocation would resemble:

```
$ gcc file1.c file2.c file3.c -o progname
```

g c c first creates file1.o, file2.o, and file3.o before linking them all together to create progname.

# ### Example

![](bbox=[0.05, 0.53, 0.15, 0.58])

# ### Example

Suppose you are working on n e w h e l l o, which uses code from s h o w i t . c and m s g . c :

```
```c
showit.c
/* showit.c _ Display driver */
#include <stdio.h>
#include "msg.h"

int main(void)
{
    char msg_hi[] = {"Hi there, programmer!"};
    char msg_bye[] = {"Goodbye, programmer!"};
```
```