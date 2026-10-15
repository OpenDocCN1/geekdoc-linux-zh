to give to the interval timer must be 1000/k ms. Since speed contains the current number of chars per second for moving the object, the interval to give to the timer is 1000/speed, since the set_timer() function (defined in Listing 6.11) is expecting the interval expressed in milliseconds.

As a concrete example, if speed = 10, then the timer must expire every 1000/10 = 100 milliseconds, in order that we can move the object 10 times per second. If speed is increased by 2, to 12 chars/second, then the interval must be 1000/12 ≈ 83 milliseconds, so that the timer will expire every 83 milliseconds.

4. We make sure we avoid a division by zero, by preventing the user from decrementing speed below 1, which is achieved by making sure 1000/speed ≤ 500. We set an upper bound on the speed simply because high speeds are not easy to watch.

The logic of redrawing is now in the signal handler, move_msg(), shown below:

# Listing 6.14: move_msg()

```
void move_msg(int signum)
{
    static int row = ROW;
    static int col = 0;
    char msg[40];
    mvaddstr(row, col, BLANK);   /* erase old string */
    col += dir;                  /* advance one column */
    move(row, col);              /* move to new locataion */
    if ( RIGHT == dir ) {
        addstr( MESSAGE );       /* add forward string */
        if ( col+strlen(MESSAGE) >= COLS-1 )
            dir = LEFT;          /* reverse if hitting edge */
    }
    else {
        addstr( REVMSSGE );      /* add reverse string */
        if ( col <= 0 )
            dir = RIGHT;         /* reverse if hitting edge */
    }
    refresh();
}
```

Note that

+   - The handler uses static variables, a.k.a globals, making it non-reentrant.
+   - It makes calls to several functions that are not safe.

However, because this is a SIGALRM handler, and the time intervals are extremely long relative to the length of the code, it is essentially impossible for a SIGALRM signal to be delivered while the handler is running. That is why it is effectively safe. Of course you can send it multiple Ctrl-C's and it will be unsafe for them.

If the signal handler were installed using the signal() system call, the handler would have to reset itself by calling signal() immediately. We use the sigaction() call instead. If the user were allowed to speed up the animation enough, the SIGALRM signals might arrive so fast that they