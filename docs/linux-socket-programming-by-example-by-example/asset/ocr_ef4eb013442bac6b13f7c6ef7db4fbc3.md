If the function is successful, the value zero is returned. Otherwise, a return value of -1 indicates that a failure has occurred, and that *errno* should be consulted for the specific reason.

# **CAUTION**

Always test the function return value for success or failure. The value *errno* should only be consulted when it has been determined that the function call has indicated that it failed. Only errors are posted to *errno*; it is never cleared to zero upon success.

# Using *socketpair*(2) in an Example

To demonstrate how the *socketpair*(2) function is used, the program in Listing 1.1 is presented for your experimentation.

# **CAUTION**

If you type example programs manually from the listings shown in this book, do not include the line number shown at the extreme left. The line number is shown for ease of reference only.

# **Listing 1.1: 01LIST01.—Example Use of *socketpair*(2) Function**

```
```
   1:  /* Listing 1.1:
   2:  *
   3:  *   Example of socketpair(2) function:
   4:  */
   5:  #include <stdio.h>
   6:  #include <stdlib.h>
   7:  #include <unistd.h>
   8:  #include <errno.h>
   9:  #include <string.h>
  10:  #include <sys/types.h>
  11:  #include <sys/socket.h>
  12:  
  13:  int
  14:  main(int argc,char **argv) {
  15:      int z;                  /* Status return code */
  16:      int s[2];               /* Pair of sockets */
  17:  
  18:      /*
  19:       * Create a pair of local sockets:
  20:       */
  21:      z = socketpair(AF_LOCAL,SOCK_STREAM,0,s);
  22:  
  23:      if ( z == -1 ) {
  24:          fprintf(stderr,
  25:              "%s: socketpair(AF_LOCAL,SOCK_STREAM,0)\n",
  26:              strerror(errno));
```
```