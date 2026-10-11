+   3. In an internal loop, print all protocol alias names, if any.

+   4. Repeat step 1 until there are no more protocol entries.

Listing 7.6 shows how to compile and run the demonstration program.

# Listing 7.6: Compiling and Running the protoent.c Program

```
$ make protoent
gcc -o -D.gnu_SOURCE -Wall protoent.c
gcc protoent.o -o protoent
$ ./protoent | head

ip:
	Protocol:	0
	Aliases:	IP
icmp:
	Protocol:	1
	Aliases:	ICMP

igmp:
	Protocol:	2
	Aliases:	IGMP


\$g:
$
```

![](bbox=[0.07, 0.2, 0.18, 0.32])

The example command session in Listing 7.6 had its output piped to the head command to keep the listing short. Notice the protocol name of the first entry shown was “ip” and its one and only alias was the uppercase name “IP”.

# Using the setprotoent(3) Function

The file that is opened implicitly for getprotoent(3) can be rebound by calling the setprotoent(3) function. The function synopsis for it is as follows:

```
#include <netdb.h>

void setprotoent(int stayopen);
```

This function accepts one argument, stayopen, which is interpreted as a Boolean value:

+   • When stayopen is non-zero (TRUE), this indicates that the implicitly opened file is left opened and merely rewound to the start of the file.

+   • When stayopen is zero (FALSE), this indicates that the implicitly opened file is closed and then re-opened, effectively rewinding the file.

Best performance is obtained by setting stayopen as TRUE.