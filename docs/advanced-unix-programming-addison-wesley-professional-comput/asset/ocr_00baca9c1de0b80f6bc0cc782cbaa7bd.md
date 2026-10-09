```
unlockpt—unlock pty

```c
#include <stdlib.h>
int unlockpt(
 int fd /* file descriptor */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

Step 3 is to get the name of the slave side. On SUS1 systems there’s a system call for it:

```
ptsname—get name of slave side of pty

```c
#include <stdlib.h>
char *ptsname(
 int fd /* file descriptor */
);
/* Returns name or NULL on error (errno not defined) */
```
```

On BSD systems (MASTER_NAME_SEARCH defined) you get the name from the name of the master by replacing the “p” in /dev/ptyXY with a “t.” That is, if you discovered that /dev/ptyK4 could be opened as the master side, the corresponding slave side’s name will be /dev/ttyK4.

Here’s the code for the function pt_open_master that calls the function find_and_open_master shown previously for step 1 and then does steps 2 and 3, ending up with the slave side named but not open:

```
PTINFO *pt_open_master(void) {

    PTINFO *p = NULL;
    char *s;

    ec_null( p = calloc(1, sizeof(PTINFO)) )
    p->pt_fd_m = -1;
    p->pt_fd_s = -1;
    ec_false( find_and_open_master(p) )
    #ifdef _XOPEN_UNIX
    ec_neg1( grantpt(p->pt_fd_m) )
    ec_neg1( unlockpt(p->pt_fd_m) )
    ec_null( s = ptsname(p->pt_fd_m) )
    if (strlen(s) >= PT_MAX_NAME) {
        errno = ENAMETOOLONG;
        EC_FAIL
    }
    ```
```