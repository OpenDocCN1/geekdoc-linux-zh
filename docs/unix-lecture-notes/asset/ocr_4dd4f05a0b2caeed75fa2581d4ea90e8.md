```
printf("\nReturn value of read() is %d; chars read are %s\n", num_bytes_read, input );
else
    printf("\nReturn value of read() is %d;" " no chars were read\n",num_bytes_read);
}
else
    printf("read() returned -1\n");
}

void set_non_canonical(int vmin, int vtime)
{
    struct termios ttystate;

    tcgetattr( 0, &ttystate);          /* read curr. setting   */
    ttystate.c_lflag   &= ~ICANON;    /* no buffering         */
    ttystate.c_cc[VMIN]  = vmin;      /* get min of vmin chars */
    ttystate.c_cc[VTIME] = vtime;     /* set timeout to vtime */
    tcsetattr( 0, TCSANOW, &ttystate); /* install settings   */
}

void tty_mode(int how)
/* if how == 0 saves the termios state and fd flags for later restoring */
/* if how == 1 restores the termios state and fd flags from the saved state */
/* CANNOT CALL with how == 1 before first calling with how == 0 */
{
    static struct termios original_mode;
    static int            original_flags = -1;

    if ( 0 == how ){
        tcgetattr(0, &original_mode);
        original_flags = fcntl(0, F_GETFL);
    }
    else {
        if ( -1 == original_flags ) {
            fprintf(stderr,"tty_mode(1) called without saving first.\n");
            exit(1);
        }
        tcsetattr(0, TCSANOW, &original_mode);
        fcntl( 0, F_SETFL, original_flags);
    }
}
```

Before we leave this topic, let us see what happens when we disable the ability to process signals from the terminal. When you type a Ctrl-C at the keyboard, you usually do so to kill the foreground process. Why does this happen? The answer is a bit deeper than we explain here, but the general idea is that the Ctrl-C is mapped by the terminal driver to a signal named SIGINT, and that signal is delivered to the foreground process. This usually results in its being terminated. A similar sequence takes place when you type other keyboard signals, such as Ctrl-\ and Ctrl-Z. These do not result in the same signals, but they are delivered to the process nonetheless.

The terminal is aware of three special control characters, known as the interrupt, quit, and suspend characters, usually Ctrl-C, Ctrl-\, and Ctrl-Z respectively. The isig switch to stty enables