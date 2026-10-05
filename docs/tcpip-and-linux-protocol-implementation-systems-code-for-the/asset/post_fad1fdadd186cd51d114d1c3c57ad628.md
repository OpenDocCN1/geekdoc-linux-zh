
# TCP/IP and Linux Protocol Implementation

```
1022  int len=0;
1023  off_t pos=0;
1024  int size;
1025  char hbuffer[HBUFFERLEN];
1026  int i,j,k;
1027  const hexbuf[] = "0123456789ABCDEF";
1028
1029  size = sprintf(buffer,"IP address HW type Flags HW address Mask Device="%s");

1030
1031  pos+=size;
1032  len+=size;

1033
1034  for(i=0; i<NEIGH_HASHMASK; i++) {
1035    struct neighbour *n;
1036    read_lock_bh(&arp_tbl[i]);
1037    for (n=arp_tbl[i].hsb_buckets[j]; n; n=n->next) {
1038      struct net_dev *dev = n->dev;
1039      int intype = dev->type;

1040
1041      /* Do not confuse users "arp -a" with magic entries */
1042      if ((n->nud_state&NUD_NOARP))
1043        continue;
1044  }

1045
1046  read_lock(kn->lock);
```

![](img/06c11ba8be5c1c24aa633e12618e2ebd_361_0.png)

```
1047  /*
1048   * Convert hardware address to XX:XX:XX ... form. 
1049   */
1050  #if defined(CONFIG_AX25) || defined(CONFIG_AX25_MODULE)
1051    if (intype == ARPHRD_AX25 || intype == ARPHRD_NETROM)
1052      asc2c((ax25_address)n->ha, hbuffer);
1053    else {
1054
1055  endif
1056  for (k=0; k<HBUFFERLEN-3 && dev->addr_len>j; j++) {
1057    hbuffer[k++]=hexbuf[n->ha[j]]>>4];
1058    hbuffer[k++]=hexbuf[n->ha[j]&15];
1059    hbuffer[k++]=';';

1060
1061  }
1062  hbuffer[k--]=0;
1063  }
1064  #if defined(CONFIG_AX25) || defined(CONFIG_AX25_MODULE)
1065  #endif

1066
1067  {
1068    char tbuffer[16];
1069    sprintf(tbuffer,"%Xu.%Xu.%Xu.%Xu",NIPQUAD(*(u32*)n->primary_key));
1070    size = sprintf(buffer+len,"X-%16s 0x-%10x-%10xs",
```

```
tbuf,
hatype,
arp_state_to_flags(n),
hbuffer,
dev->name);
}
read_unlock(an->lock);
len += size;
pos += size;
if (pos <= offset) {
len=0;
if (pos >= offset+length) {
read_unlock_bb(&arp_tbl.lock);
goto done;
}
}
read_unlock_bb(&arp_tbl.lock);
```

# Figure 6.139 ARP--user interface--procs entry point--table: linux/net/ipv4-arp.c.

```
for (i=0; i<=PNEIGH_HASHMASK; i++) {
  struct peigh_entry *n;
  for (arp_tbl->phaas_buckets[i]; n; n=n->next) {
    struct net_dev *dev = n->dev;
    int hatype = dev ? dev->type : 0;

    char tbuf[16];
    sprintf(tbuf, "%hu,%xu,%xu,%xu+(%hu", NIPQUAD((u32)n->key));
    size = snprintf(buffer+len, "-16s 0x%02x-0x%02x * %s\n",
    tbuf,
    hatype,
    ATF_PUBL|ATF_PERM,
    "%00:00:00:00:00:00",
    dev ? dev->name : "s");
  }
}
len += size;
pos += size;

if (pos <= offset) {
len=0;
if (pos >= offset+length) {
goto done;
}
```

# 308 TCP/IP and Linux Protocol Implementation

```
1121 done:

1122
1123     *start = buffer-len-(pos-offset);  /* Start of wanted data */
1124 len = pos-offset;      /* Start slop */
1125 if (len<length)
1126     len = length;          /* Ending slope */
1127     if (len<0)
1128         len = 0;
1129         return len;

1130 
}
1131 #endif
```

Figure 6.140 ARP-interface down: linux/net/ipv4/arp.c.

```
1133 /* Note, that it is not on notifier chain.
1134 It is necessary, that this routine was called after route cache be
1135 flushed.
1136 */
1137 void arp_ifdown(struct net_device *dev)
1138 {
1139     neigh_ifdown(&arp_tbl, dev);
1140 }
```

# ARP Initialization and Usage Example

Figure 6.141 ARP-initialize: linux/net/ipv4/arp.c.

```
1147 static struct packet_type arp_packet_type =
1148 {
1149     htons(ETH_P_ARP),
1150     /* All devices */
1151     arp_rcv,
1152     (void*)i,
1153     NULL
1154 };

1155 void __init_arp(void)
1156 {
1157     neigh_table_init(&arp_tbl);

1158     dev_add_pack(&arp_packet_type);

1159
1160     proc_create("arp", 0, arp_get_info);
1161 #ifdef CONFIG_SYSCTL
1162     neigh_sysctl_register(NULL, &arp_tbl.params, NET_IPV4, NET_IPVIGH, "ipv4");
1163 #endif
1164 }
```

Figure 6.142 ARP-X25 string conversion: linux/net/ipv4/arp.c.

```
1170 #ifdef CONFIG_FS
1171 #if defined(CONFIG_AX26) || defined(CONFIG_AX26_MODULE)
1172  /*
1173  * X25 ASCII conversion
1174  */
1175  char *ax25_asc(ax25_address, *ama, char *buf)
1176 {
1177     char c, *s;
1178     int n;
1179     for (n = 0, s = buf; n < 6; n++) {
1180         c = (a->ax26_call[n] >> 1) & 0x7F;
1181         if (c != ' ') s++ = c;
1182     }
1183     *s++ = '-';
1184     if ((n = (a->ax26_call[n] >> 1) & 0x0F) > 9) {
1185         s++ = '1';
1186         n = 10;
1187     }
1188     *s++ = n + '0';
1189     *s++ = '\0';
1190     if (*buf == '\0' || *buf == '-') {
1191         return "*";
1192     }
1193     return buf;
1194 }
1195 #endif
1204 #endif
```

# 6.4 Network-Level Debugging–ICMP

Figure 6.143 ICMP, host requirement conformance: linux/net/ipv4/icmp.c.

- RFC 1122 (Host Requirements – Comm. Layer) Status: (are there a lot of rules for ICMP)
- 3.2.2 (Generic ICMP stuff)
- MUST discard messages of unknown type. (OK)
- MUST copy the first 8 bytes from offending packet

# TCP/IP and Linux Protocol Implementation

- when sending ICMP errors. (OBSOLETE) -- RFC 1812
- MUST pass ICMP errors up to protocol level. (OK)
- SHOULD send ICMP errors with TOS = 0. (OBSOLETE -- RFC 1812)
- MUST NOT send ICMP errors in reply:
- ICMP errors (OK)
- Broadcast/multicast datagrams (OK)
- MAC broadcasts (OK)
- Non-initial fragments (OK)
- Datagram with a source address that isn't a single host. (OK)
- 3.2.2.1 (Destination Unreachable)
- All the rules govern the IP layer, and are dealt with ip.c, not here.
- 3.2.2.2 (Redirect)
- Host NOT send ICMP_REDICTS. (OK)
- MUST update routing table in response to host or network redirects.
- (Host OK, network OBSLETE)
- SHOULD drop redirects if they're not from directly connected gateway (OK -- we drop it's not from our old gateway, which is close enough

Figure 6.144 ICMP, host reinforcement conformance: linux/net/ipv4/icmp.c.

- 3.2.2.3 (Source Quench)
- MUST pass incoming SOURCE_QUENCHs to transport layer (OK)
- Other requirements are dealt with the transport layer.
- 3.2.2.4 (Time_EXCEEDED)
- MUST pass TIME_EXCEEDED to transport layer (OK)
- Other requirements are dealt with at IP (generating TIME_EXCEEDED).
- 3.2.2.5 (Parameter Problem)
- SHOULD generate these (OK)
- MUST pass received PARAPPROBLEM to transport layer (NOT YET)
- [Solaris 2.X seems to assert EPROTO when this occurs] -- AC
- 3.2.2.6 (Echo Request/Reply)
- MUST reply to ECHO_REQUEST, and give app to do ECHO stuff (OK. Configurable with a sysctl1.)
- MUST reply using same source address as the request was sent to. (OK as per ECHO (NOT YET))
- MUST pass REPLIES to transport/user layer. (OK)
- 3.2.2.7 (Information Request)
- MUST implement-this. (I guess means means silently discarded...?) (OK)
- 3.2.2.8 (Timestamp Request/Reply)
- MAY implement (OK)
- SHOULD be in-kernel for "minimum variability" (OK)
- MAY discard broadcast REQUESTS. OK, but see for inconsistency)
- MUST reply using same source address as the request was sent to. (OK as per ECHO (NOT YET))
- MUST pass REPLIES to transport/user layer. (OK)
- MUST use any provided source (reversed) for REPLY. (NOT YET)

# Infrastructure Protocols 311

- 3.2.2.9 (Address Request/Reply)
- MAY implement (OK)
- SHOULD be in-kernel for "minimum variability" (OK)
- MAY discard broadcast REQUESTS. OK, but see for inconsistency)
- MUST reply using same source address as the request was sent to. (OK as per ECHO (NOT YET))
- MUST pass REPLIES to transport/user layer. (OK)
- MUST use any provided source (reversed) for REPLY. (NOT YET)
