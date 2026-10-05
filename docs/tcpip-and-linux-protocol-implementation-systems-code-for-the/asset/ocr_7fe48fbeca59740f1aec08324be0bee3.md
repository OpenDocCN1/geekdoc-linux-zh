# 404 TCP/IP and Linux Protocol Implementation

```
130 /* Tunnel hash table */
131 /\*
132
133 4 hash tables:
134
135 3: (remote,local)
136 2: (remote,*)
137 1: (*,local)
138 0: (*,*)
139
140 require exact key match i.e. if a key is present in packet
141 it will match only tunnel with the same key; if it is not present,
142 it will match only keyless tunnel.
143
144 All keyless packets, if not matched configured keyless tunnels
145 will match fallback tunnel.
146 */
147
148 #define HASH_SIZE 16
149 #define HASH_addr(addr) ((addr)>>4)&0xF
150
151 static struct ip_tunnel *tunnel[4] [HASH_SIZE];
152
153 #define tunnels_r_1 (tunnels[3])
154 #define tunnels_r (tunnels[2])
155 #define tunnels_l (tunnels[1])
156 #define tunnels_wc (tunnels[0])
157
158 static rwlock_t ipgre_lock = RW_LOCK_UNLOCKED;
```

Figure 6.284 GRE tunnels-hashing function: linux/net/ipv4/ip_gre.c.

```
/* Given arc
```