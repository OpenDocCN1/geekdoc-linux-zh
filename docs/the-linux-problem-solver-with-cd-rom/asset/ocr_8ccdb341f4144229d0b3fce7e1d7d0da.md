# Skipping Lines in .c and .h Files

If you have to fool around with a source file, it's probably because the compiler needs to get a line or two from it. Let's say we have an excerpt from a file like this:

```
...
#include <stdio.h>
#ifdef JUNKOS
#include <junk/extracrud.h>
extern int junkerrno;
#endif
...
```

Notice the preprocessor directive, #ifdef JUNKOS, closing with an #endif, around two lines. This means if you define the macro (text substitution) JUNKOS, the preprocessor and compiler will read the next two lines. If you're not running anything like JunkOS, then the compiler under Linux usually skips these lines.

You define macros with either the -DMACRONAME[=value] flag to the C compiler (as in -DJUNKOS or -DSKY=blue) or in a source file with the #define directive (for example, #define SKY blue).

To get rid of an offending line guarded by #ifdef directives, first attempt to make the outcome of the #ifdef test false. If you just can't find the macro definition, there's an #undef directive for undefining macros, but first try to find and verify the original definition. Other mismatches, especially those related directly to the operating system, can cause the same error to appear many times, and a program that manages to compile despite an incorrect configuration may not run properly.

If #ifdef does not enclose an offending line, you may not have any choice but to exclude a line or two with #if 0 /endif, as in this example:

```
#if 0
#ifdef JUNKOS
#include <junk/extracrud.h>
extern int junkerrno;
#endif
#endif
```

Even though it's not a true comment, #if 0 /endif is safer than using /* and */ because you don't run any risk of nested comments (which cause syntax errors).

Never delete a line. Only comment out as a last resort, and be careful when you do it. For example, if we switched the second and third lines in the first example above, catastrophic-looking errors would result.