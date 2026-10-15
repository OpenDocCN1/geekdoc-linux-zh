
提供给间隔定时器的值必须是 1000/k 毫秒。由于 speed 包含对象移动时每秒的字符数，因此提供给定时器的间隔是 1000/speed，因为 set_timer() 函数（定义在清单 6.11 中）期望间隔以毫秒为单位。

举个具体例子，如果 speed = 10，那么定时器必须每 1000/10 = 100 毫秒到期一次，这样我们才能每秒移动对象 10 次。如果 speed 增加 2，变为 12 字符/秒，那么间隔必须是 1000/12 ≈ 83 毫秒，这样定时器将每 83 毫秒到期一次。

4. 我们通过防止用户将 speed 减小到低于 1 来确保避免除零，这是通过确保 1000/speed ≤ 500 来实现的。我们设置速度上限，仅仅是因为高速不易观看。

重绘的逻辑现在在信号处理程序 move_msg() 中，如下所示：

### 清单 6.14：move_msg()

```c
void move_msg(int signum)
{
    static int row = ROW;
    static int col = 0;
    char msg[40];
    mvaddstr(row, col, BLANK);   /* erase old string */
    col += dir;                  /* advance one column */
    move(row, col);              /* move to new location */
    if ( RIGHT == dir ) {
        addstr( MESSAGE );       /* add forward string */
        if ( col+strlen(MESSAGE) >= COLS-1 )
            dir = LEFT;          /* reverse if hitting edge */
    }
    else {
        addstr( REVMSGE );      /* add reverse string */
        if ( col <= 0 )
            dir = RIGHT;         /* reverse if hitting edge */
    }
    refresh();
}
```

请注意

- 处理程序使用静态变量（又称全局变量），使其不可重入。
- 它调用了一些不安全的函数。

然而，由于这是一个 SIGALRM 处理程序，并且时间间隔相对于代码长度来说极长，因此实际上不可能在处理程序运行期间递送 SIGALRM 信号。这就是它实际上是安全的原因。当然，你可以发送多个 Ctrl-C，对于它们来说它是不安全的。

如果信号处理程序是使用 signal() 系统调用安装的，那么处理程序将不得不通过立即调用 signal() 来重置自身。我们改用 sigaction() 调用。如果允许用户将动画加速到足够快，SIGALRM 信号可能会来得太快，在处理程序执行完毕之前就到达。在这种情况下，处理程序的行为将是不安全的。通过使用 sigaction()，我们可以确保当程序在处理程序内部执行时信号被阻塞。

下面是不包含清单 6.13 中主处理循环的程序。

### 清单 6.15：bouncestr.c 的主程序

```c
#include <stdio.h>
#include <string.h>
#include <curses.h>
#include <signal.h>
#include "timers.h"

#define INITIAL_SPEED 50
#define RIGHT 1
#define LEFT -1
#define ROW 12
#define MESSAGE "0000000=>"
#define REVMSGE "<=0000000"
#define BLANK "        "

int dir; /* Global variable to store direction of movement */
int speed; /* Current speed in chars/second */

int main()
{
    int finished;
    int is_changed;
    int c;

    /* Set up signal handling */
    struct sigaction newhandler; /* for installing handlers */
    sigset_t blocked; /* to set mask for handler */

    newhandler.sa_handler = move_msg; /* name of handler */
    newhandler.sa_flags = SA_RESTART; /* flag is just RESTART */
    sigemptyset(&blocked); /* clear all bits of blocked set */
    newhandler.sa_mask = blocked; /* set this empty set to be the mask */

    if ( sigaction(SIGALRM, &newhandler, NULL) == -1 ) { /* try to install */
        perror("sigaction");
        return (1);
    }

    /* Prepare the terminal for the animation */
    initscr(); /* initialize the library and screen */
    cbreak(); /* turn off line buffering and editing */
    noecho(); /* turn off echo */
    clear(); /* clear the screen */
    curs_set(0); /* hide the cursor */

    /* Initialize the parameters of the program */
    dir = RIGHT;
    finished = 0;
```
