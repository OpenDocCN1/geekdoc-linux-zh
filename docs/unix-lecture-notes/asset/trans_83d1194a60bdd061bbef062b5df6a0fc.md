

/* This will wrap across the screen */
move(LINES/2,0);
for ( i == 1; i <= 8; i++ ) {
    addstr( pattern );
    addch( ' ' );
}

/* Park the cursor at bottom */
move(LINES-1,0);
addstr("Type any char to quit:");
refresh(); /* not needed */

/* Wait for the user to type something, otherwise
   the screen will clear. */
getch();
endwin();
return 0;
}

## 注释

- 1. NCurses 有一个预定义常量 LINES，它表示终端窗口中的行数，还有一个常量 COLS 存储列数。
- 2. 还要注意，程序每次更改屏幕时都会调用 refresh()。这是不必要的，因为 addstr() 会自动强制刷新。
- 3. 如果删除对 getch() 的调用，你将看不到任何内容；如果删除对 endwin() 的调用，屏幕将无法恢复。

下一个程序在屏幕中央绘制一个句点网格。

## 清单 6.3：drawgrid.c

```
#define CENTERY (LINES/2 -2)   /* The middle line in terminal */
#define CENTERX (COLS/2 -2)   /* The middle column in terminal */
#define NUMROWS (LINES/2)
#define NUMCOLS (COLS/2)

int main()
{
    int r, c;
    char MESSAGE[] = "Press any character to exit:";
    int length, i, j;
    length = strlen(MESSAGE);

    initscr();   /* Initialize screen */
    clear();     /* Clear the screen */
    noecho();    /* turn off character echo */

    char grid[NUMROWS][NUMCOLS];

for ( i = 0; i < NUMROWS; i++ ) {
    for ( j = 0; j < NUMCOLS-1; j++ )
        grid[i][j] = '.';
    grid[i][NUMCOLS-1] = '\0';
}

/* move to center to draw grid */
r = CENTERY - (NUMROWS/2);
c = CENTERX - (NUMCOLS/2);
move(r,c);

/* Draw each row of grid as a string */
for ( i = 0; i < NUMROWS; i++ ) {
    mvaddstr(r+i,c,grid[i]);
}

/* Move to bottom of screen , post message to display */
move(LINES-1,0);
addstr(MESSAGE);

getch();        /* wait for the user to type something */
clear();        /* clear the screen */
endwin();       /* delete curses window and quit */;
return 0;
}
```

NCurses 使得将任意窗口保存到文件变得很容易。putwin() 函数会将窗口的内容写入一个 FILE 流，可以通过 getwin() 将其读回到程序中。接下来的两个清单展示了如何完成这两项操作。第一个是一个程序，它在一个窗口中绘制一张脸，并将其保存到命令行指定的文件中。

## 清单 6.4：保存窗口：drawface2.c

```
#include <stdio.h>
#include <string.h>
#include <ncurses.h>
#include <stdlib.h>

#define CENTERY   (LINES/2 -2)    /* The middle line in terminal */
#define CENTERX   (COLS/2 -2)     /* The middle column in terminal */

void addhappyface(int * y, int * x)
{
    int orig_y = *y;
    addstr(" ^  ^ "); move(++(*y),*x);
    addstr(" o  o "); move(++(*y),*x);
    addstr("   ^   "); move(++(*y),*x);
    addstr(" \___/ "); move(++(*y),*x);
    addstr("");
    *y = orig_y;
    *x = (*x) + 5;
    move(*y, *x);
}
```
```c
int main(int argc, char *argv[])
{
    int    r, c;
    char   MESSAGE[] = "Press any character to exit:";
    int    length;
    FILE *fp;        /* for writing window contents */

    length = strlen(MESSAGE);
    if ( argc < 2 ) {
        printf("usage: %s window-file\n", argv[0] );
        return 0;
    }

    fp = fopen(argv[1], "w");
    if ( NULL == fp ) {
        printf("Error opening %s for writing.\n", argv[1]);
        return 0;
    }

    initscr();       /* Initialize curses library and the drawing screen */
    clear();         /* Clear the screen */

    /* Move to bottom of screen and post message to display */
    move(LINES - 1, 0);
    addstr(MESSAGE);

    /* move to center of screen - width of face */
    r = CENTERY;
    c = CENTERX - 5;
    move(r, c);
    addhappyface(&r, &c);
    addhappyface(&r, &c);
    addhappyface(&r, &c);

    /* Park cursor at bottom at the right side of the message */
    move(LINES-1,length);
    refresh();

    /* Write the standard screen to a file */
    if ( ERR == putwin(stdscr, fp) ) {
        printf("Error saving window.\n");
    }

    fclose(fp);

    getch();         /* wait for the user to type something */
    clear();         /* clear the screen */
    endwin();        /* delete curses window and quit */
    return 0;
}
```

下一个清单是一个程序，它可以读取任何由使用 putwin() 保存数据的 NCurses 程序创建的文件。该程序尝试打开文件并显示存储在其中的窗口。由于 getwin() 在失败时返回 NULL 指针，它会先检查返回的指针是否为非 NULL，然后再显示数据。

