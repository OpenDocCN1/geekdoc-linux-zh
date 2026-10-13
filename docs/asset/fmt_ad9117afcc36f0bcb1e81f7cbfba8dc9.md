
# 硬核方式的终端控制

```c
#include <stdio.h>
#include <term.h>
#include <curses.h>

#define NUMCAPS 3

void clrscr(void);
void mv_cursor(int, int);

int main(void)
{
    char *boolcaps[NUMCAPS] = { "am", "bce", "km" };
    char *numcaps[NUMCAPS] = { "cols", "lines", "colors" };
    char *strcaps[NUMCAPS] = { "cup", "flash", "hpa" };
    char *buf;
    int retval;
    if(setterm(NULL, fileno(stdout), NULL) != 0) {
        perror("setterm");
        exit(EXIT_FAILURE);
    }
    clrscr();
    for(i=0; i < NUMCAPS; i++) {
        /* 定位光标 */
        mv_cursor(i, 10);
        retval = tigetflag(boolcaps[i]);
        if(retval == FALSE)
            printf("%s unsupported\n", boolcaps[i]);
        else
            printf("%s supported\n", boolcaps[i]);
    }
    sleep(3);
    for(i=0; i < NUMCAPS; i++) {
        /* 定位光标 */
        mv_cursor(i, 10);
        retval = tigetnum(numcaps[i]);
        if(retval == ERR)
            printf("%s unsupported\n", numcaps[i]);
        else
            printf("%s is %d\n", numcaps[i], retval);
    }
    sleep(3);
    clrscr();
    for(i=0; i < NUMCAPS; i++) {
        /* 定位光标 */
        mv_cursor(i, 10);
        buf = tigstr(strcaps[i]);
        if(buf == NULL)
            printf("%s unsupported\n", strcaps[i]);
        else
            printf("%s \E%s\n", strcaps[i],&buf[1]);
    }
}
```

## 编写用户界面

### 列表 26.4 续

```c
}
sleep(3);
exit(0);
}
/*
 * 清除屏幕
 */
void clrscr(void)
{
    char *buf = tigstr("clear");
    putp(buf);
}
/*
 * 将光标移动到指定的行和列
 */
void mv_cursor(int row, int col)
{
    char *cap = tigstr("cup");
    putp(cap, row, col);
}
```
