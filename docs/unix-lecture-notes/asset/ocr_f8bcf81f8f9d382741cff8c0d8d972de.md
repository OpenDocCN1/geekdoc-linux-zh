```
{    char      line[LINE LEN];        // buffer to store line of input    int       num_of_lines = SCREEN_ROWS; // # of lines left on screen    int       getmore     = 1;    // boolean to signal when to stop    int       reply;                // input from user

    while ( getmore && fgets( line , LINE LEN, fp ) ){
        // fgets() returns pointer to string read or NULL        if ( num_of_lines == 0 ) {
            // reached screen capacity so display prompt            reply = get_user_input();
            switch ( reply ) {
                case SPACEBAR:
                    // allow full screen
                    num_of_lines = SCREEN_ROWS;
                    break;
                case RETURN:
                    // allow one more line
                    num_of_lines++;
                    break;
                case QUIT:
                    getmore = 0;
                    break;
                default:  // in case of invalid input
                    break;
            }
        }
        if ( fputs( line , stdout ) == EOF )
            exit(1);
        num_of_lines--;
    }
}

int get_user_input()
/*
 *  display message, wait for response, return key entered as int
 *  Returns SPACEBAR, RETURN, QUIT, or INVALID
 */
{
    int     c;

    printf("\033[7m more? \033[m"); /* reverse on a VT100     */
    while( (c = getchar()) != EOF )   /* wait for response      */
        switch ( c ) {
            case 'q':               /* 'q' pressed */
                return QUIT;
            case ' ':               /* ' ' pressed */
                return SPACEBAR;
```