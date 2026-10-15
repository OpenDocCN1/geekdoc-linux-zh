
```c
for ( i = win.line_at_top; i < lineno; i++ ) {

    if ( buf.line_len[i] < win.cols )

        total_lines_before++;

    else

        total_lines_before += (int) ceil((double)buf.line_len[i]/win.cols);

}

rows_in_current_textline = index/win.cols;

curs->r = total_lines_before + rows_in_current_textline;

curs->c = index - rows_in_current_textline * win.cols;

}
```

程序必须实现的四种移动是：上、下、左和右。我们在这里只展示其中一种。完整程序在附录中。上和下移动比左右移动稍微复杂一些。

当按下向下箭头键或 `'j'` 键时，光标必须移动到下一行文本中相对于行开头相同偏移量的位置，除非该行更短

## Terminal Support Functions

有三个函数用于修改或查询终端状态，如以下程序清单所示。

### Listing 5.7: Terminal support functions

```
void modify_termios(int fd, int echo, int canon)

{
    struct termios cur_tty;
    tcgetattr(fd, &cur_tty);
    if ( canon )
        cur_tty.c_lflag |= ICANON;
    else
        cur_tty.c_lflag &= ~ICANON;
    if ( echo )
        cur_tty.c_lflag |= ECHO;
    else
        cur_tty.c_lflag &= (~ECHO & ~ECHOE);
    cur_tty.c_lflag &= ~ISIG;
    cur_tty.c_cc[VMIN] = 1;
    cur_tty.c_cc[VTIME] = 0;
    tcsetattr(fd, TCSADRAIN, &cur_tty);
}

void save_restore_tty(int fd, int action)

{
    static struct termios original_state;
    static int retrieved = FALSE;
    if ( RETRIEVE == action ){
        retrieved = TRUE;
        tcgetattr(fd, &original_state);
    }
    else if (retrieved && RESTORE == action ) {
        tcsetattr(fd, TCSADRAIN, &original_state);
    }
    else
        fprintf(stderr, "Illegal action to save_restore_tty().\n");
}

void init_window( int fd, Window *win )

{
    struct winsize size;
    if (ioctl(fd, TIOCGWINSZ, &size) < 0) {
        perror("TIOCGWINSZ error");
        return;
    }
    win->rows = size.ws_row;
    win->cols = size.ws_col;
    win->line_at_top = 0;
}

void get_erase_char(int termfd, Window *win )
```

```
struct termios cur_tty;
tcgetattr(termfd, &cur_tty);
win->erase_char = cur_tty.c_cc[VERASE];
}
```

`modify_termios()` 可以启用或禁用回显和规范模式，并禁用键盘信号。它还将 `MIN` 和 `TIME` 行规程值分别设置为 `1` 和 `0`，以便程序一次读取一个字符并且不会超时。`save_restore_tty()` 可用于将当前终端状态保存到本地静态变量中以便以后恢复。`get_winsize()` 使用 `ioctl()` 函数在程序启动时获取当前窗口大小。如果程序运行期间窗口被调整大小，一切都将失效——它不处理调整大小事件。

由于输出操作必须绕过 C 标准 I/O 库以避免其内部缓冲的影响，程序将仅使用内核的 `write()` 系统调用来向屏幕写入。向终端设备的写入将始终把要写入的字节放置在当前光标位置。写入完成后，光标会向前移动到最后一个写入字符的右侧，除非写入的是不会实际写入屏幕的 ANSI 转义序列。因为 `write()` 系统调用需要要写入字符串的长度，为了提高性能，每个转义序列的长度都被硬编码为常量。下面列出的是程序使用的完整转义序列集合。

### Listing 5.8: ANSI escape sequences

```
/* ANSI Escape Sequences and their lengths (for speed */
const char CLEAR_DOWN[] = "\033[0J";
const int ICLEAR_DOWN   = 4;
const char CLEAR_RIGHT[] = "\033[0K";
const int ICLEAR_RIGHT  = 4;
const char CURSOR_HOME[] = "\033[1;1H";
const int ICURSOR_HOME  = 6;
const char CLEAR_SCREEN[] = "\033[2J";
const int ICLEAR_SCREEN = 4;
const char CLEAR_LINE[] = "\033[2K";
const int ICLEAR_LINE   = 4;
const char RIGHT[] = "\033[1C";
const int IRIGHT       = 4;
const char LEFT[] = "\033[1D";
const int ILEFT        = 4;
const char BACKSPACE[] = "\033[1D \033[1D";
const int IBACKSPACE   = 9;
/* The following cannot be declared statically as the dimensions are unknown */
char PARK[20];        /* string to park cursor at lower left */
int  IPARK;           /* length of PARK string */
```

用于将光标停靠在窗口最后一行的字符串 `PARK` 是动态定义的，因为它取决于屏幕大小。它定义如下：

```
get_winsize(STDIN_FILENO, &rows, &cols);
sprintf(PARK, "\033[%d;1H", rows);
```

#### 5.2.2.4 主程序

主函数初始化所有必要的内容，然后进入一个循环，保持在此循环中，直到用户在 `lastline` 模式下输入退出命令。下面的列表中仅显示了主循环。

##### Listing 5.9: main program loop

```
while ( !quit ) {
    if ( in_input_mode ) {
        if ( read(STDIN_FILENO, &c, 1) > 0 ) {
            if ( c == ESCAPE ) {
                in_input_mode = 0;
                write_status_message( "", curs);
            }
            else {
                in_input_mode = handle_insertion(&buf, &win, &curs, c);
                if ( in_input_mode == UNHANDLEDCHAR )
                    in_input_mode = 1;
                else
                    write_status_message( INSERT, curs);
```
