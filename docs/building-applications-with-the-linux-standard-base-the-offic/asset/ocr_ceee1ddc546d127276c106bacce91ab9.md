Simple example.  In Example 13.1 we have a source file `hello_world.c`.

# Example 13.1: `hello_world.c` Source File

```
```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
	printf("Hello World\n");
	exit(0);
}
```
```

First, we log in into the restricted environment (Example 13.2). By default the `sshd` daemon for the environment listens on port 5436.

# Example 13.2: Logging into the Restricted Environment

```
```bash
$ slogin -p 5436 localhost
lsbdevchroot$ 
```
```

We can then build the binary as we would normally (Example 13.3).

# Example 13.3: Building and Running the Binary

```
```bash
lsbdevchroot$ gcc -Wall -o hello_world hello_world.c
lsbdevchroot$ ./hello_world
Hello World
lsbdevchroot$ 
```
```

Outside of the restricted environment, we could attach a debugger if we wish.

# 13.3.3.2 lsb-build-cc

The `lsb-build-cc` is a wrapper program for `gcc` that is invoked in place of the compiler. The wrapper program modifies the arguments passed to the actual compiler to ensure that your application uses the LSB-specified versions