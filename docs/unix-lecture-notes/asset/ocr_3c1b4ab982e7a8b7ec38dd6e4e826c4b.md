```
if ( c == win.erase_char )
    moveLeft(&buf, &win, &curs );
}
}
}
printf("\n");
tcflush(STDIN_FILENO,TCIFLUSH);
clearandhome();
save_restore_tty(STDIN_FILENO, RESTORE);
return 0;
}
/********************************************************************************/
int pars lastline( char *str, int len, Buffer buf, char *statusstr )
{
    int i = 0;
    int foundquit = 0;
    int foundwrite = 0;
    int badchar = 0;
    int done = 0;
    char *filename = NULL;
    int state;

    state = 1;
    while ( ( i < len ) && !done ) {
        switch ( state ) {
        case 1:
            if ( str[i] == ' ' )
                state = 1;
            else if ( str[i] == 'w' ) {
                foundwrite = 1;
                state = 2;
            }
            else if ( str[i] == 'q' ) {
                foundquit = 1;
                state = 7;
            }
            else
                state = 5;
            i++;
            break;
        case 2:
            if ( str[i] == 'q' ) {
                foundquit = 1;
                state = 3;
            }
            else if ( str[i] == ' ' )
                state = 4;
            else
                state = 5;
            i++;
            break;
        case 3:
```