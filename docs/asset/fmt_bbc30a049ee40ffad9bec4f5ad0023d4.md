
`tcsetattr(fd, TCSANOW, &cur_tty);`

}

```
set_non_block() 函数与我们上面使用的相同，这里省略。
```

`get_response()` 函数将提示用户输入一个字符，并返回一个指示用户输入了什么的值。为简单起见，它将要求是或否的答案。它在屏幕上打印一个问题，并给用户一个机会提供有效响应。如果用户输入了有效响应或已尝试 `max_tries` 次，则返回。

```
int get_response( FILE* fp, ui_params uip )
{
    int input, n;
    unsigned char c;
    time_t time0, time_now;
    time(&time0);
    while ( TRUE ){
        printf( "%s (y/n)?", uip.prompt );
        fflush(stdout);
        if ( !uip.isblocking )
            sleep(uip.sleeptime);
        if ( ( n = read( fileno(fp), &c, 1) ) > 0 ) {
            tcflush( fileno(fp), TCIFLUSH );
            input = tolower(c);
            if ( input == 'y' || input == 'n' ) {
                return input;
            }
        }
        else {
            printf("\nInvalid input: %c\n", input);
            continue;
        }
    }
    time(&time_now);
    printf("\nTimeout waiting for input: %d secs elapsed,"
        "%d timeouts left\n",
        (int)(time_now - time0), uip.maxtries);
    if ( uip.maxtries == 0 ) {
        printf("\nTime is up.\n");
        return 0;
    }
}
```

### 注释

- `fflush()` 调用刷新传递给它的文件流关联的缓冲区。C 标准 I/O 库为文件流提供缓冲 I/O。当程序启动时，默认情况下，流 `stdin`、`stdout` 和 `stderr` 是行缓冲的。这意味着字符只有在将换行符放入流时才传输到终端。由于 `printf()`、`puts()` 等作用于 `stdout` 的函数作用于文件流，因此它们是行缓冲的。之前的 `printf()` 调用

  ```
  printf("%s (y/n)?", uip.prompt);
  ```

  将一个字符串发送到 `stdout` 而没有终止的换行符，因此该字符串不会立即出现。为了强制字符传送到终端设备，我们使用 `fflush(stdout)`，它清空缓冲区。如果我们注释掉 `fflush()` 调用，提示将不会在 `read()` 运行后之前出现在屏幕上。

  注意，为流提供的缓冲与终端在行规程内完成的缓冲是独立的。即使你将终端置于非规范模式，如果你使用更高级别的 C 库函数，C 仍将继续行缓冲。你必须使用较低级别的文件描述符操作来避免缓冲。

- 调用刷新终端输入队列的 `tcflush()` 是必要的，以防程序以规范模式运行且输入被缓冲。在这种情况下，用户必须输入换行符，终端才会将字符传送到 `read()` 调用，并且 `get_response()` 需要删除该换行符，否则它将在再次调用时被用作下一个输入字符。

- `get_response()` 调用 `sleep()` 使自身阻塞 `uip.sleeptime` 给出的秒数。`sleep()` 函数的原型是

  ```
  unsigned int sleep(unsigned int seconds);
  ```

  该进程将休眠，直到给定的时间过去或它收到一个不会忽略的信号为止。（信号将在后面介绍。）这给了用户在非阻塞输入生效时输入响应的机会。如果没有这个延迟，`read()` 调用会在用户眨眼之前就返回。输入阻塞时不需要延迟。有比 `sleep()` 更精细的替代方案，例如 `usleep()` 和 `nanosleep()`。

最后，`get_response()` 通过在最初调用 `time()` 函数，并在用户在时间耗尽前未能输入任何字符时每次调用，并计算秒数差，来计算自原始提示显示以来经过的总时间。

### 主程序

主程序，省略了包含文件和一些其他实用程序，见下文。这是 `term_demo1.c`。

#### Listing 5.11: term_demo1.c

```
#define PROMPT              "Do you want to continue?"
#define MAX_TRIES              3                  // max tries
#define SLEEPTIME_DEFAULT      2                  // delay after prompt
#define BEEP                   putchar('a')       // alert user
#define RETRIEVE               1                  // action for save_restore
#define RESTORE                2                  // action for save_restore
#define FALSE                  0
#define TRUE                   1
int main(int argc, char* argv[])
{
    int                     response;
    tty_opts                ttyopts = {1,0,1,1};
    ui_params               ui_parameters = {
                                SLEEPTIME_DEFAULT, TRUE,
                                MAX_TRIES, PROMPT
                                };
    int                     fflags = 0;
    struct termios          ttyinfo;
    int                     fd;
    FILE*                   fp;
    get_options(&argc, &argv, &fflags, &ttyopts,
                &(ui_parameters.sleeptime));
    if ( !isatty(0) || !isatty(1) )
        exit(1);
    fp = stdin;
    save_restore_tty(fileno(fp), RETRIEVE, &ttyinfo);
    modify_termios( &ttyinfo , ttyopts);
    apply_termios_settings( fileno(fp), ttyinfo);
```

```
// If fflags != 0 then the O_NONBLOCK flag is set on fp
if ( fflags ) {
    ui_parameters.isblocking = FALSE;
    set_non_blocking_mode(fileno(fp), fflags);
}
while ( TRUE ) {
    response = get_response(fp, ui_parameters );
    if ( response ) {
        printf("\nMain: Response from user = %c\n", response );
        if ( 'u' == response )
            break;
    }
    else
        printf("\nMain: No response from user\n" );
}
save_restore(fileno(fp), RESTORE, NULL);
tcflush(0,TCIFLUSH);
return response;
}
```
