```
return 0;
}
```

In general, one should try to avoid the use of ioctl() if there is an alternative means of performing the same task, as it is not completely portable. There are many IOCTLs for which alternative functions exist. For example, there are IOCTLS for the terminal interface. The tty_ioctl manpage has a complete list of them. Some have equivalents and others do not:

| IOCTL | argument | equivalent to |
|---|---|---|
| TCGETS | struct termios *argp | tcgetattr(fd, argp) |
| TCSETS | const struct termios *argp | tcsetattr(fd, TCSANOW, argp) |
| TCSETSW | const struct termios *argp | tcsetattr(fd, TCSADRAIN, argp) |
| TCSETSF | const struct termios *argp | tcsetattr(fd, TCSAFLUSH, argp) |
| TCSBRK | int arg | tcsendbreak(fd, arg) |
| TIOCINQ | int *argp | none - counts bytes in the input buffer |
| TIOCOUTQ | int *argp | none - counts bytes in output buffer |
| TCFLSH | int arg | tcflush(fd, arg). |
| TIOCSTI | char *argp | none - inserts *argp into input queue |

We could rewrite the setecho program to use these IOCTLs instead of using tcgetattr() and tcsetattr(), simply as an exercise. It is displayed in the listing that follows.

# Listing setecho_ioctl.c

```
int main(int argc, char *argv[])
{
    struct termios info;
    FILE *fp;

    if ( argc < 2 ) {
        printf("usage: %s [y|n]\n", argv[0]);
        exit(1);
    }

    if ((fp = fopen(ctermid(NULL), "r+")) === NULL)
        return(1);

    /* retrieve termios struct */
    if ( ioctl( fileno(fp), TCGETS, &info ) === -1 )
        die("ioctl","1");

    /* If second argument starts with 'y' it is yes, echo on otherwise off */
    if ( 'y' === argv[1][0] )
        info.c_lflag |= ECHO ;
    else
        info.c_lflag &= ~ECHO ;

    /* replace termios with the modified copy */
    if ( ioctl(fileno(fp),TCSETS, &info) === -1 )
        die("ioctl","2");
```