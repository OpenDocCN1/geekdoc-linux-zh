```
}
        exit(1);
    }
    fputs("The first string to cat\n",pd);
    fflush(pd);
    sleep(5);
    fputs("The second string to cat\n",pd);
    fflush(pd);
    pclose(pd);
        exit(0);
}
```

Because the pipe is opened in "w" mode, this program is able to write to it. The call to `fputs()` sends strings to the `cat` command, which writes them to standard output so they appear on the display. The reason for the `fflush()` function call is because pipes are buffered fully, and actual output data is sent only when either the buffer fills up or the pipe is closed. So this buffering of pipe data has no size limitation because it stores data on disk, so writing to a pipe never blocks. This means you can queue up all the commands and data you like and the child process will read them at its own pace.

# ## Time

Linux stores the time as a count of the number of seconds since midnight January 1, 1970. The following example retrieves and displays the current time:

```
/\* showtime.c \*/
#include <time.h>
#include <limits.h>

int main(int argc,char *argv[]) {
        time_t binarytime;
        struct tm *nowtm;

        binarytime = time(NULL);
        printf("now=%d\n",binarytime);
        printf("ctime=%s",ctime(&binarytime));

        nowtm = localtime(&binarytime);
        printf("asctime=%s",asctime(nowtm));

        printf("\nHHMMSS %d:%02d:%02d\n",
                nowtm->tm_hour,nowtm->tm_min,nowtm->tm_sec);
        printf(" MMDDYY %d/%d/%d\n",
                nowtm->tm_mon + 1,nowtm->tm_mday,
                nowtm->tm_year + 1900);
        printf("  Weekday=%d\n",
                nowtm->tm_wday);
        printf("  Yearday=%d\n",
```