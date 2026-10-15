
```c
/* convert tabs in standard input to spaces in */
/* standard output while maintaining columns */
#include <stdio.h>
#define TABSIZE 8

/* Preprocessor directives function findstop */
int findstop(int *);

int main() {
    int c; /* character read from stdin */
    int posn = 0; /* column position of character */
    int inc; /* column increment to tab stop */
    while ((c = getchar()) != EOF) {
        switch (c) {
            case '\t': /* c is a tab */
                inc = findstop(&posn);
                for (; inc > 0; inc--)
                    putchar(' ');
                break;
            case '\n': /* c is a newline */
                putchar(c);
                posn = 0;
                break;
            default:
                putchar(c);
                posn++; /* c is anything else */
                break;
        }
    }
    return 0;
}

/* compute size of increment to next tab stop */
int findstop(int *col) {
    int colindex, retval;
    retval = (TABSIZE - (*col % TABSIZE));
    /* increment argument (current column position) to tabstop */
    *col += retval; /* main gets how many blanks for filling */
    return retval;
}
```

## `DDD`: `/home/mark/tabs.c` 命令 状态 源数据

```c
/* convert tabs in standard input to spaces in */
/* standard output while maintaining columns */
#include <stdio.h>
#define TABSIZE 8

/* prototype for function findstop */
int findstop(int *);

int main() {
    int c;
    /* character read from stdin */
    int posn = 0;      /* column position of character */
    int inc;           /* column increment to tab stop */

    while ((c = getchar()) != EOF) {
        switch (c) {
            case '\t':      /* c is a tab */
                inc = findstop(&posn); inc--;
                for ( ; inc > 0; ----) putchar(' ');
                break;
            case '\n':     /* c is a newline */
                putchar(c);
                posn = 0;
                break;
            default:        /* c is anything else */
                putchar(c);
                posn++;
                break;
        }
    }
}
```

`GNU DDD 3.3.11 (i386-redhat-linux-gnu), by Dorothea L"/home/mark/tabs.c": not in`

`executable format: File format not recognized`

`(gdb) file /home/mark/tabs`

`Using host libthread_db library "/lib/libthread_db.so.1"`

`(gdb)`

## `CVS` 工作目录
