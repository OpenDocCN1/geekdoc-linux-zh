
user's terminal. If the other user wants to reply, they must run `write` as well. When you are done, type an end-of-file or interrupt character. The other user will see the message `EOF` indicating that the conversation is over.

If the user you want to write to is logged in on more than one terminal, you can specify which terminal to write to by specifying the terminal name as the second operand to the `write` command. Alternatively, you can let the user select one of the terminals—it will pick the one with the shortest idle time. This is so that if the user is logged in at work and also dialed up from home, the message will go to the right place.

Our first version of `write` will ignore the optional line argument and will not try to pick the terminal with the smallest idle time. The main program follows. It calls two functions, `get_user_tty()` and `create_message()`, which follow thereafter.

```
int main( int argc, char *argv )
{
    int     fd;
    char    buf[BUFSIZ];
    char    *user_tty;
    char    eof[] = "EOF\n";

    if ( argc < 2 ){
        fprintf(stderr,"usage: write1 username\n");
        exit(1);
    }

    if ( ( user_tty = get_user_tty( argv[1] ) ) == NULL ) {
        fprintf(stderr, "User %s is not logged in.\n", argv[1]);
        return 1;
    }

    sprintf(buf, "/dev/%s", user_tty);
    fd = open( buf, O_WRONLY );
    if ( fd == -1 ){
        perror(buf); exit(1);
    }
    create_message(buf);

    if ( write(fd, buf, strlen(buf)) == -1 ) {
        perror("write");
        close(fd);
        exit(1);
    }
}
```

```
while( fgets(buf, BUFSIZ, stdin) != NULL )
    if ( write(fd, buf, strlen(buf)) == -1 )
        break;
    write(fd, eof, strlen(eof));
    close( fd );
    return 0;
}
```

The most important part of the main program is the loop. The while-loop looks exactly like a loop to read from one file and write to another. The only difference is that it is using fgets() instead of a read() system call, and it "hard-wires" stdin into the code. The fgets() function reads from any FILE stream until it sees an end-of-line (EOL) or end-of-file (EOF) mark. Therefore, you can see that reading from the keyboard and writing to a terminal is essentially the same as reading from one file and writing to another.

The get_user_tty() function searches through the utmp file for entries that match the given login name, returning a pointer to a static string containing the line. This could have been allocated on the stack and later freed, but for demonstration purposes, this is easier.

```
char * get_user_tty( char *logname )
{
    static struct utmp utrec;
    int             utrec_size = sizeof(utrec);
    int             utmp_fd;
    int             namelen = sizeof( utrec.ut_name );
    char            *retval = NULL ;

    if ( (utmp_fd = open( UTMP_FILE, O_RDONLY )) == -1 )
        return NULL;

    while ( read( utmp_fd, &utrec, utrec_size ) == utrec_size )
        if ( strcmp(logname, utrec.ut_name, namelen ) == 0 ) {
            retval = utrec.ut_line ;
            break;
        }

    close(utmp_fd);
    return retval;
}
```

The create_message() function constructs the message to display on the user's console. It uses the getlogin() function to get the real username of the owner of the calling process, the gethostname() function to get the hostname of the host on which the sender process is running, the ttyname() function to get the terminal device name of the controlling terminal of the sending process, and the time() function to get the current time, which it converts to a struct tm using localtime().

```
void  create_message(char buf[] )
{
    char  *sender_tty, *sender_name;
```

```
char sender_host[256];
time_t now;
struct tm *timeval;

sender_name = getlogin();
sender_tty = ttyname(STDIN_FILENO);
gethostname(sender_host, 256);
time(&now);
timeval = localtime(&now);
sprintf(buf, "Message from %s@%s on %s at %2d:%02d:%02d ...\n", sender_name, sender_host, 5+sender_tty, timeval->tm_hour, timeval->tm_min, timeval->tm_sec);
}
```

This version is relatively easy to construct. The next version must allow the user to enter a terminal device name in the form "pts/n" and try to open that specific terminal for writing, if possible. If it fails it must return an error message. The changes to allow the optional terminal name are minor:

+   1. The main program has to check the command line arguments (not shown below).
+   2. The get_user_tty() function needs a second argument that it compares to the ut_line field whenever the ut_name field matches.

```
char * get_user_tty( char *logname, char *termname )
{
    static struct utmp utrec;
    int utrec_size = sizeof(utrec);
    int utmp_fd;
    int namelen = sizeof( utrec.ut_name );
    char *retval = NULL ;

    if ( (utmp_fd = open( UTMP_FILE, O_RDONLY )) == -1 )
        return NULL;

    /* look for a line where the user is logged in */
    while ( read( utmp_fd, &utrec, utrec_size) == utrec_size )
        if ( strncmp(logname, utrec.ut_name, namelen ) == 0 )
            if ( ( termname == NULL ) ||
                 ( strncmp(termname, utrec.ut_line, strlen(termname)) == 0 ))
            {
                retval = utrec.ut_line ;
                break;
            }
    close(utmp_fd);
    return retval;
}
```

This version of the write command still does not choose the terminal line with the smallest idle time, for a given username, when the terminal line is not specified. How would you go about finding
