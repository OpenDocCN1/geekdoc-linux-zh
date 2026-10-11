# **Listing 11.4:** continued

```
```
--- 45,51 ----
/*
 * Free an allocated mpz_t value:
*/
! void
rpn_free(mpz_t **v) {
    mpz_clear(**v);
    free(*v);
}
$```

```

The major change that is present in the rpneg2.c module is that the RPN stack array (variable stack) and its stack pointer (variable sp) are declared to be external in scope. Static function rpn_free() is made external also. This allows the variables and the function to be accessed from the main source module, which you’ll examine in the example in Listing 11.5.

# **Listing 11.5:** rpnsvr2.c—The RPN Server Using select(2)

```
```
1:   /* rpnsvr2.c:
2:   *
3:    * Example RPN Server
4:    * using select(2):
5:    */
6:    #include <stdio.h>
7:    #include <unistd.h>
8:    #include <stdlib.h>
9:    #include <errno.h>
10:   #include <string.h>
11:   #include <time.h>
12:   #include <sys/time.h>
13:   #include <sys/types.h>
14:   #include <sys/socket.h>
15:   #include <netinet/in.h>
16:   #include <arpa/inet.h>
17:   #include <netdb.h>
18:   #include <sys/wait.h>
19:   #include <gmp.h>
20:
21:   #ifndef SHUT_RDWR
22:   #define SHUT_RDWR 3
23:   #endif
24:
25:   extern int mkaddr(void *addr,
26:        int *addr_len,
27:        char *input_address,
28:        char *protocol);
29:```

```