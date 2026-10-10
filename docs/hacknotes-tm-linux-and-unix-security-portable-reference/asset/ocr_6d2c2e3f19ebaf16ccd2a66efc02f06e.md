# Class B

Class B addresses are assigned to organizations that consist of a large number of networks and hosts. Therefore, many ISPs are assigned class B addresses.

| 0 | 1 | 1 | 6 | 31 |
|---|---|---|---|---|
| 1 | 0 | NETWORK |  | HOST |

+   -   **First Octet** Ranges from 128 to 191. The first two bits are 1 and 0.

+   -   **Maximum Networks** The network address is denoted by first and second octet. Therefore, $2^{14}$ = 16,384 class B networks are possible.

+   -   **Maximum Hosts per Network** Hosts are denoted by the last two octets. Therefore, $2^{16}$ - 2 = 65,534 hosts are possible per network.

# Class C

Class C addresses are used by organizations consisting of a small number of hosts per network.

| 0 | 1 | 2 | 24 | 31 |
|---|---|---|---|---|
| 1 | 1 | 0 | NETWORK | HOST |

+   -   **First Octet** Ranges from 192 to 233. The first three bits are 1, 1, and 0.

+   -   **Maximum Networks** The network address is denoted by the first, second, and third octets. Therefore, $2^{21}$ = 2,097,152 class C networks are possible.

+   -   **Maximum Hosts per Network** Hosts are denoted by the last octet. Therefore, $2^{8}$ - 2 = 254 hosts are possible per network.