
```c
#include <curses.h>

char *ncolor(int color);

int main(void)
{
short pair,f,b;

initscr();
start_color();

/* 创建颜色对 */
init_pair(1,COLOR_WHITE,COLOR_BLUE);
init_pair(2,COLOR_BLACK,COLOR_RED);
init_pair(3,COLOR_YELLOW,COLOR_RED);
init_pair(4,COLOR_BLUE,COLOR_GREEN);
init_pair(5,COLOR_CYAN,COLOR_MAGENTA);

/* 显示颜色对 */
for(pair=1;pair<=5;pair++)
{
attrset(COLOR_PAIR(pair));
pair_content(pair,&f,&b);
printf("Pair %d: %s foreground, %s background.\n",
pair,ncolor(f),ncolor(b));
}
refresh();
getch();

endwin();
return 0;
}

char *ncolor(int color)
{
switch(color)
{
case COLOR_BLACK:
return("Black");
case COLOR_RED:
return("Red");
case COLOR_GREEN:
return("Green");
case COLOR_YELLOW:
return("Yellow");
case COLOR_BLUE:
return("Blue");
case COLOR_MAGENTA:
return("Magenta");
case COLOR_CYAN:
return("Cyan");
case COLOR_WHITE:
return("White");
)
return("?");
)
}
```

示例输出：

`Pair 1: White foreground, Blue background.`

`Pair 2: Black foreground, Red background.`

`Pair 3: Yellow foreground, Red background.`

`Pair 4: Blue foreground, Green background.`

`Pair 5: Cyan foreground, Magenta background.`

这里的代码似乎已根据指示的颜色进行了格式化。

# 另请

`start_color()`, `init_pair()`, `COLOR_PAIRS`

# `PAIR_NUMBER()`

`PAIR_NUMBER()` 伪函数用于返回正在使用哪个颜色对来格式化文本。

## 手页格式

不适用。

## 格式参考

```
PAIR_NUMBER(attr)
```

`attr` 是由 `COLOR_PAIR(n)` 属性产生的值。它是 NCurses 在构建存储在 `chtype` 变量中用于屏幕的属性信息时，在内部使用的值。（参见附录 C。）

# 返回值

`PAIR_NUMBER()` 返回的值是一个 `int`，等于用于格式化文本和背景颜色的颜色对编号。其范围于 0 到 `COLOR_PAIRS` 的值减 1。

## 注意事项

在实际上，`COLOR_PAIR(n)` 仅仅是 `ctypes` 值中的一组位，用于定义 NCurses 窗口中字符的格式。`PAIR_NUMBER()` 伪函数只是简单地从 `ctypes` 值中提取 `COLOR_PAIR(n)` 值本身。这就是为什么人们常说 `PAIR_NUMBER()` 是 `COLOR_PAIR(n)` 函数的“反向”函数。

## 示例

```
n = PAIR_NUMBER(a)
```

变量的值等于特定 `COLOR_PAIR(n)` 的值。变量 `n` 中返回的值将与 `COLOR_PAIR(a)` 的值相同。

```
x = PAIR_NUMBER(COLOR_PAIR(n));
```

这条语句基本上与 `x = n` 相同。

## 示例程序

```
#include <ncurses.h>

int main(void)
{
int c,p;

initscr();
start_color();

init_pair(1,COLOR_RED,COLOR_WHITE);

c = COLOR_PAIR(1);
p = PAIR_NUMBER(c);
printf("COLOR_PAIR(1) = %d\n",c);
printw("PAIR_NUMBER(%d) = %d\n",c,p);

refresh();
getch();
endwin();

return 0;
}
```

示例输出：

```
COLOR_PAIR(1) = 256
PAIR_NUMBER(256) = 1
```

# 另请

`init_pair()`, `COLOR_PAIR`

# `echochar()`

`echochar()` 函数用于将单个字符放入填充区（pad）中并在标准屏幕上显示这些字符。

## 手页格式

```
int echochar(WINDOW *pad, ctype ch);
```

## 格式参考

`pad` 是 `WINDOW` 指针的名称，引用由 `newpad()` 函数创建的填充区。

`ch` 是一个 `ctype` 变量，一个长 int 值。它可以是一个单个字符或字符与格式属性的组合。有关 c 的更多信息请参见附录 C。

# 返回值

成功返回 `OK`，失败返回 `ERR`。

## 注意事项

为了让 `echochar()` 函数工作，必须先使用 `prefetch()` 函数。`prefetch()` 定义了标准屏幕上文本出现的区域，以及写入文本的填充区部分。参见“示例程序”。

在 `refresh()` 之后，可以使用 `echochar()` 将填充区显示到标准屏幕上。`echochar()` 的行为与 `addch()` 函数一致。这里是：

```
int echochar(WINDOW *pad, ctype ch);
```

`echochar(pad)` 将 `ch` 放置在填充区。

## 示例

`echochar(pad,c)` 将 `c` 放置在填充区。

## 示例程序

```
#include <ncurses.h>
int main(void)
{
    WINDOW *pad;
    char text[] = "Greetings from pad.";
    char *t;

    initscr();
    p = newpad(50,100); /* 创建填充区 */
    if(p == NULL) {
        endwin();
        puts("无法创建填充区");
        return(1);
    }

    t = text;
    prefetch(p,0,0,25);
    while(*t)
    {
        echochar(p, *t);
        t++;
    }
    refresh(50);
    getch(pad);
    endwin();
    return 0;
}
```

示例输出：

`Greetings from pad.`

# 另请

`addch()`, `newpad()`, `refresh`

# `prefetch()`

`prefetch()` 函数用于将存储在填充区结构中的信息显示到窗口。

# 解释

填充区的工作方式与窗口类似，但它们不会显示在屏幕上。为了查看放入填充区的信息，需要使用 `refresh()` 函数。与 `refresh()` 函数不同，`refresh()` 从填充区获取一个矩形文本（以及属性）并将其放在窗口中。这就是从填充区显示信息的方式。

## 手页格式

```
int prefetch(WINDOW *pad, int pminrow, int pmincol,
 int smrow, int smcol, int smaxrow, int smaxcol);
```
