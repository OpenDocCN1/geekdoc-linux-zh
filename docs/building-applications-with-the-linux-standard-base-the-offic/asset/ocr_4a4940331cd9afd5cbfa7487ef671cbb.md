of header files and libraries instead of those installed on the system. However, the full functionality of the native system is available to build, develop, and debug the application. To use `lsb-build-cc`, you can use either of the commands shown in Example 13.4.

```
**Example 13.4: lsb-build-cc**
```bash
# CC=lsbcc ./configure
# CC=lsbccc ./configure (for C++)
```
or
```bash
# CC=lsbcc make
# CC=lsbccc make (for C++)
```
```

Further information about using **lsbcc** can be found in the man page included with the lsb-build-cc package.

**Simple example.** In Example 13.5 we have a source file hello_world.c.

```
**Example 13.5: hello_world.c Source File**
```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    printf("Hello World\n");
    exit(0);
}
```
```

Instead of calling gcc directly, we use **lsbcc** (Example 13.6).

```
**Example 13.6: Using lsbcc**
```bash
$ lsbcc -Wall -o hello_world hello_world.c
$ ./hello_world
Hello World
$```
```