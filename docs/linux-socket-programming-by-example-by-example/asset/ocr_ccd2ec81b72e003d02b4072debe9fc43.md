The structure member `s_aliases` is actually an array of character pointers. If sp points to the structure, and x is an `int` subscript, then you can iterate through each alias `sp->s_aliases[x]`, until you reach a `NULL` pointer. A `NULL` pointer marks the end of this alias list. Listing 7.2 shows a simple program that lists all /etc/services entries and their aliases, if any.

![](bbox=[0.1, 0.23, 0.22, 0.34])

# **Listing 7.2**: server.c—A Program to List All Services

```
1:  /* server.c:
2:  *
3:  * Example getservent(3) program:
4:  */
5:  #include <stdio.h>
6:  #include <unistd.h>
7:  #include <stdlib.h>
8:  #include <errno.h>
9:  #include <string.h>
10: #include <netdb.h>
11: #include <netinet/in.h>
12: 
13: int
14: main(int argc,char **argv) {
15:     int x;
16:     struct servent *sp;
17: 
18:     for (;;) {
19:         errno = 0;
20:         if ( (sp = getservent()) )
21:             break;
22: 
23:         printf("%s:\n"
24:                "\tPort:      %d\n"
25:                "\tProtocol: %s\n"
26:                "\tAliases:  ",
27:                sp->s_name,
28:                ntohs(sp->s_port),
29:                sp->s_proto);
30:         for ( x=0; sp->s_aliases[x] != NULL; ++x )
31:             printf("%s ",sp->s_aliases[x]);
32:         putchar('\n');
33:     }
34: 
35:     if ( errno != 0
36:          && errno != ENOENT ) /* For RH-6.0 */
37:         fprintf(stderr,
38:                "%s: getservent() %d\n",
39:                strerror(errno),errno);
40: 
```