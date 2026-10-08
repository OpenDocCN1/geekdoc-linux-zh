# Task 24.1: Your First Program

Conditional statements
Looping statements
Functions
Arrays
Pointers
Structures

First, you learn a simple program and how to make it run. After that, you learn the different data types and how to manipulate the data. Control flow follows, where you learn how to make your program execute alternate statements. You'll wind up with some of the more advanced topics in C programming.

Historically, the first program is called the “Hello, World” program because it simply outputs that sentence. However, with the recent discovery of life on meteoroids from Mars, and the suspicion that the oceans of Europa may also support life, we should instead be greeting the universe.

![](bbox=[0.166, 0.406, 0.25, 0.433])

![](bbox=[0.166, 0.5, 0.244, 0.526])

The first program is actually very simple:

```
#include <stdio.h>

main(){
    printf("Hello, universe!\n");
}
```

Six simple lines; the first is an include line. This is a pre-processor instruction that tells the compiler when you build this program, it should include the contents of the named file in addition to the code in this file. When included in <>, the compiler looks in the standard directory, /usr/include. If the filename is quoted (as in #include "test.h") it looks in the current directory for the specified file.

| A compiler is a special program found on any development system. It reads in your program (source code), checks to make certain that it is correct, and creates an executable program. |

![](bbox=[0.16, 0.789, 0.275, 0.863])