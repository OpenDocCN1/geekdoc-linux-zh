# 3.9 EISDIR(3)

If the path argument of unlink(3) specifies a directory, the implementation may return EISDIR instead of EPERM as specified by the Single UNIX Specification (Example 3.5).

> Example 3.5: EISDIR

```
#include <sys/stat.h>
#include <sys/types.h>
#include <fcntl.h>
#include <errno.h>
#include <stdio.h>

main() {

    char *newdir = "/tmp/example_dir";

    if (0 != mkdir(newdir, O_CREAT)) {
        printf("mkdir %s: %s\n", newdir, strerror(errno));
    }

    if (0 != unlink(newdir)) {

        switch (errno) {
        case EISDIR:
            printf("EISDIR: %s is a directory\n", newdir);
            break;
        case EPERM:
            printf("EPERM: operation not permitted for %s\n", newdir);
            break;
        default:
            perror("unlink");
            break;
        }
    }
}
```