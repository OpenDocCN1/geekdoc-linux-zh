# $ netstat -r

Routing tables  
| Destination | Gateway | Flags | Refs | Use | Interface | Pmtu |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| hp/00 | localhost | UH | 0 | 28 | lo0 | 4608 |
| default | router1 | UG | 0 | 0 | lan0 | 4608 |
| 128.185.61 | system1 | U | 347 | 28668 | lan0 | 1500 |

# $ netstat -rn

Routing tables  
| Destination | Gateway | Flags | Refs | Use | Interface | Pmtu |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 127.0.0.1 | 127.0.0.1 | UH | 0 | 28 | lo0 | 4608 |
| default | 128.185.61.1 | UG | 0 | 0 | lan0 | 4608 |
| 128.185.61 | 128.185.61.2 | U | 347 | 28668 | lan0 | 1500 |

With **netstat**, some information is provided about the router, which is the middle entry. The *-r* option shows information about routing, but there are many other useful options to this command are available. Of particular interest in this output is "Flags," which defines the type of routing that takes place. Here are descriptions of the most common flags, which may be different among UNIX variants, from the online manual page on my HP-UX system.

$1$ = $U$	 Route to a *network* via a gateway that is the local host itself.

$3$ = $UG$	 Route to a *network* via a gateway that is the remote host.

$5$ = $UH$	 Route to a *host* via a gateway that is the local host itself.

$7$ = $UGH$	 Route to a *host* via a remote gateway that is a host.

The first line is for the local host, or loopback interface called, *lo0* at address 127.0.0.1 (you can see this address in the **netstat -rn** example). The *UH* flags indicate that the destination address is the local host itself. This