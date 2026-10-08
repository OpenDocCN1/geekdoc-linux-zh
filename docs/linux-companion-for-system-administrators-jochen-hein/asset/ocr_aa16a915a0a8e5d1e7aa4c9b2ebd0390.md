adaptations made by other users. Listing 10.21 shows the two files used in the
following examples.

```
(Linux):"/examples> cat hello.c
#include <stdio.h>
main()
{
    printf("Hello World!\n");
}
(Linux):"/examples> cat hello.c
#include <stdio.h>
main()
{
    printf("Hello Welt!\n");
}
```

Listing 10.21 Sample files for the diff program.

The diff program can represent the differences between two files in a very
flexible way. This concerns both the context of the differences (just the affected
lines or a a certain number of lines before and after) and the representation itself.
The two files can be output next to each other on the screen. Some examples of
how to apply the diff command are shown in Listing 10.22.

In the first example, a simple diff is used. The output is a sed script that
can be used for automatic modification on other computers. A disadvantage of
these scripts is that the context of the changes is not considered. Therefore, this
function only makes sense with otherwise absolutely identical files.

A better solution is the creation of context diffs (-C) or unified diffs
(second example in Listing 10.22). The generation of context diffs is part of
the standard UNIX program, whereas unified diffs are an extension of the GNU
version.