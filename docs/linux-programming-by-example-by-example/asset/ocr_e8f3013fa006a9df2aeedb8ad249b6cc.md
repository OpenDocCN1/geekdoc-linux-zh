# Example

![](bbox=[0.04, 0.1, 0.1, 0.15])

# Example

The `trunc` program that follows is a handy utility for shortening files. It expects the name of the file to shorten followed by the new length to be passed on the command line.

```
"""
* trunc.c - Shorten named file to specified length:
 */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>

int main(int argc, char **argv)
{
    long len;

    if (argc != 3)
        exit(EXIT_FAILURE);
    len = (long) strtol(argv[2], NULL, 10);
    if (truncate(argv[1], len)) {
        perror ("truncate");
        exit(EXIT_FAILURE);
    }

    exit(EXIT_SUCCESS);
}
"""
```

Running this program on `test.txt` in the current directory yielded the following results:

![](bbox=[0.04, 0.66, 0.1, 0.7])

# Output

```
$ ls -l test.txt
-rw-r--r-- 1 kwall users 56561 Jul 24 15:56 test.txt
$ trunc test.txt 2000
$ ls -l test.txt
-rw-r--r-- 1 kwall users 2000 Jul 24 15:58 test.txt
```

After confirming that it was passed two arguments, `trunc` uses `strtol` to convert the passed-in length argument from a string to a long. It then immediately calls `truncate` using the passed-in filename and the requested length. If the `truncate` call fails, the program prints an error message and