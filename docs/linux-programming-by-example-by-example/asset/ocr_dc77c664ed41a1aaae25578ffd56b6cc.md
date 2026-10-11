```
```c
#include <sys/resource.h>
#include <time.h>
#include <unistd.h>

void err_quit(char *);
void doIt(char *, long);

int main(void)
{
    struct rusage usage;

    /* redirect output to prevent screen clutter */
    system("grep the /usr/doc/*/* > /dev/null 2> /dev/null");

    /* get the resource structure for the parent */
    if((getrusage(RUSAGE_SELF, &usage)) == -1)
        err_quit("getrusage");

    puts("Parent times");
    doIt("\tuser CPU", usage.ru_utime.tv_sec);
    doIt("\tsys CPU", usage.ru_stime.tv_sec);

    fputs("Parent memory stats");
    doIt("\tminor faults", usage.ru_minflt);
    doIt("\tmajor faults", usage.ru_majflt);
    doIt("\tpage swaps", usage.ru_nswap);

    * get the resource structure for the child */
    if((getrusage(RUSAGE_CHILDREN, &usage)) == -1)
        err_quit("getrusage");

    puts("Child Times");
    doIt("\tuser CPU", usage.ru_utime.tv_sec);
    doIt("\tsys CPU", usage.ru_utime.tv_sec);

    puts("Child memory stats");
    doIt("\tminor faults", usage.ru_minflt);
    doIt("\tmajor faults", usage.ru_majflt);
```
```