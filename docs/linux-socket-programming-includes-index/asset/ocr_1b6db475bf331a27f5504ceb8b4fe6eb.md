# **TABLE A.1** Continued

| Type | Description and Example | Affiliated Data |
| :--- | :--- | :--- |
| PF_NETROM | Amateur Radio Net-ROM | |
| PF_ATMUBRIDGE | Multiprotocol Bridge | |
| PF_AIMCPVC | ATM PVCs | |
| PF_X25 | (Reserved for X.25 project) | |
| | `#include <linux/x25.h>` | |
| PF_INET6 | IPv6 protocol family | |
| | `#include <linux/in6.h>` | `typedef struct {`<br>`char x25_addr[16];`<br>`} x25_address;`<br><br>`struct sockaddr_x25 {`<br>`sa_family_t x25_family;` /* X.121 family */<br>`x25_address x25_addr;`<br>`};`<br><br>`struct in6_addr`<br>`{`<br>`union {`<br>`__u8 in6_addr8[16];`<br>`__u16 in6_addr16[8];`<br>`__u32 in6_addr32[4];`<br>`} __u32 in6_addr32[4];`<br>`#if ( < 0UL) _RELAX_IN6ADDR_ALIGNMENT`<br>/* Alias, protocols do not respect`<br>`64bit alignment. rsvp/pim/... are`<br>`broken. However, it is good idea to`<br>`force correct alignment, when`<br>`it is possible. */`<br>`#endif`<br>`__u64 in6_addr64[2];`<br>`};`<br>`#endif` |

*(Note: The table cells contain mixed text and code blocks. The 'Affiliated Data' column for the X.25 and INET6 rows contains the code snippets and comments respectively.)*

![](bbox=[0.9, 0.84, 0.96, 0.89])

![](bbox=[0.82, 0.9, 0.97, 0.94])