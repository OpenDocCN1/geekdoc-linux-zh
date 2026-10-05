
## 328 TCP/IP and Linux Protocol Implementation

Figure 6.169 ICMP address reply:linux/net/ipv4/icmp.c.

```c
/*
* RFC 1812 (4.3.3.9). A ROUTER should listen all replies, and complain
* loudly if an inconsistency is found.
*/
static void icmp_address_reply(struct icmphdr *icmphdr, struct sk_buff *skb, int len)
{
    struct rtable *rt = (struct rtable*)skb->dev;
    struct net_device *dev = skb->dev;
    struct in_device *in_dev;
    struct if_addr *ifa;
    u32 mask;

    if (len < 4 || (rt->rt_flags&RTF_DIRECTSRC)) {
        return;
    }

    in_dev = in_dev->get(dev);
    if (in_dev) {
        read_lock(in_dev->lock);
        if (in_dev->ifa_list &&
            IN_DEV_LOG_MARTIANS(in_dev) &&
            IN_DEV_FORWARD(in_dev)) {
            mask = (u32*)icmphdr[1];
            for (ifa=in_dev->ifa_list; ifa; ifa=ifa->next) {
                if (mask == ifa->ifa_mask && inet_ifa_match(rt->rt_src, ifa)) {
                    break;
                }
            }
            printk(KERN_INFO "Wrong address %Xu.%Xu.%Xu.%Xu from %s/%Xu.%Xu.%Xu.%Xu\n",
                   NIPQUAD(in_dev), dev->name, NQUAD(rt->rt_src));
        }
        read_unlock(in_dev->lock);
        in_dev->put(in_dev);
    }
}
```

Figure 6.170 ICMP discard: linux/net/ipv4/icmp.c.

```c
static void icmp_discard(struct icmphdr *icmphdr, struct sk_buff *skb, int len)
{
}
```

### Figure 6.171 ICMP receive general packet: linux/net/ipv4/icmp.c.

```c
1005 int icmp_rcv(struct sk_buff *skb, unsigned short len)
1006 {
1007     struct icmphdr *icmp = skb->hdr->icmp;
1008     struct rtable *rt = (struct rtable*)skb->dst;
1009
1010     ICMP_INC_STATS_BH(icmpInMsgs);
1011
1012     /*
1013      * 18 is the highest 'known' ICMP type. Anything else is a mystery
1014      */
1015     RFC 1122: 3.2.2 Unknown ICMP messages types MUST be silently discarded.
1016     /*
1017      if(len < sizeof(struct icmphdr))
1018          icmp_csum(unsigned char *)icmp, len) ||
1019          icmp->type > NR_ICMP_TYPES
1020             goto error;
1021
1022     /*
1023      * Parse the ICMP message
1024      */
1025     if (rt->rt_flags& (RTFC_BROADCAST|RTFC_MULTICAST)) {
1026         /*
1027          RFC 1122: 3.2.2.6 ICMP ECHO to broadcast MAY be silently
1028          ignored (let user decide with sysctl).
1029          RFC 1122: 3.2.2.8 ICMP_TIMESTAMP MAY be silently
1030          discarded to broadcast/multicast.
1031         */
1032         if (icmp->type == ICMP_ECHO &&
1033             icmp_echo_ignore_broadcasts) {
1034                 goto error;
1035         }
1036
1037         if (icmp->type != ICMP_ECHO &&
1038             icmp->type == ICMP_TIMESTAMP &&
1039             icmp->type == ICMP_ADDRESS &&
1040             icmp->type == ICMP_ADDRESSREPLY) {
1041                 goto error;
1042         }
1043 }
1044
1045     len = sizeof(struct icmphdr);
1046     icmp_pointers[icmp->type].input[sm_id_]*sizeof(struct icmp_mib)/sizeof(
1047          unsigned long)++;
1048     (icmp_pointers[icmp->type].handler(icmp, mkb, len);
1049 drop:
1050     kfree_skb(skb);
1051     return 0;
1052 error:
1053     ICMP_INC_STATS_BH(icmpInErrors);
1054     goto drop;
1055 }
```

## 330 TCP/IP and Linux Protocol Implementation

Figure 6.172 ICMP statistics: linux/net/ipv4/icmp.c.

```c
1061 static unsigned long dummy;
1062 /*
1063   * Configurable rate limits;
1064   * Someone should check if these default values are correct.
1065   * Note that these values interact with the routing GC timeout
1066   * If you choose them too high they won't take effect because
1067   * dst_entry gets expired too early. The same happens when
1068   * the cache grows too big.
1069 */
1070 int sysctl_icmp_destunreach_time = 1*HZ;
1071 int sysctl_icmp_timeexceeded_time = 1*HZ;
1072 int sysctl_icmp_paramprob_time = 1*HZ;
1073 int sysctl_icmp_reply_time = 0; /* don't limit per default. */

Figure 6.173 ICMP statistics: linux/net/ipv4/icmp.c.

```c
1076 /*
1077   * This table is the definition of how we handle ICMP.
1078 */
1079 static struct icmp_control icmp_pointers[NR_ICMP_TYPES+1] = {
1080   /* ECHO REPLY (0) */
1081   &icmp_statistics[0].ImpInEchochos, &icmp_statistics[0].ImpInEchochos, &icmp_statistics[0].ImpInEchochos, icmp_discard, 0,
1082   sysctl_icmp_reply_time,
1083   &dummy, &icmp_statistics[0].ImpInErrors, icmp_discard, 1,
1084   &dummy, &icmp_statistics[0].ImpInErrors, icmp_discard, 1,
1085   /* DEST UNREACH (3) */
1086   &icmp_statistics[0].ImpInDestreaches, &icmp_statistics[0].ImpInDestreaches, icmp_unreach,
1087   1, sysctl_icmp_destunreach_time,
1088   /* SOURCE QUEN (4) */
1089   &icmp_statistics[0].ImpInSrcquenchos, &icmp_statistics[0].ImpInSrcquenchos, icmp_unreach,
1090   1,
1091   /* REDIRECT (5) */
1092   &icmp_statistics[0].ImpInRedirects, &icmp_statistics[0].ImpInRedirects, icmp_redirect,
1093   &dummy, &icmp_statistics[0].ImpInErrors, icmp_discard, 1,
1094   /* ECHO (8) */
1095   &icmp_statistics[0].ImpInEchos, &icmp_statistics[0].ImpInEchos, 0, 0,
1096   &icmp_statistics[0].ImpInErrors, icmp_discard, 1,
1097   /* TIME EXCEEDED (11) */
1098   &icmp_statistics[0].ImpInTimeExcds, &icmp_statistics[0].ImpInTimeExcds, icmp_unreach, &1
1099   sysctl_icmp_timeexceeded_time,
1100   /* PARAMETER PROBLEM (12) */
1101   &icmp_statistics[0].ImpInParambs, &icmp_statistics[0].ImpInParambs, icmp_unreach, &1
1102   sysctl_icmp_paramprob_time,
1103   /* TIMESTAMP (13) */
```

## Infrastructure Protocols 331

```c
1102      { icmp_statistics[0].IcmpOutTimestamps, &icmp_statistics[0].IcmpInTimestamps, icmp_timestamp
1103               , 0 },
1104      /* TIMEOUT REPLY (14) */
1105      { icmp_statistics[0].IcmpOutTimestampReps, &icmp_statistics[0].IcmpInTimestampReps,
1106               icmp_discard, 0 },
1107      /* INFO (15) */
1108      { &dummy, icmp_discard, 0 },
1109      /* INFO REPLY (16) */
1110      { &dummy, icmp_discard, 0 },
1111      /* ADDR MASK (17) */
1112      { icmp_statistics[0].IcmpOutAddrMasks, &icmp_statistics[0].IcmpInAddrMasks, icmp_address, 0,
```

```c
1113      /* ADDR MASK (18) */
1114      { icmp_statistics[0].IcmpOutAddrMaskReps, &icmp_statistics[0].IcmpInAddrMaskReps,
1115               icmp_address_reply, 0 },
1116      };
```

![](img/06c11ba8be5c1c24aa633e14)

```c
1115      void __init icmp_init(struct net_proto *ops)
1116      {
1117          int err;
1118
1119          icmp_inode.af = AF_INET;
1120          icmp_inode.protocol = IPPROTO_ICMP;
1121          icmp_inode.state = 0;
1122          icmp_inode.uid = 0;
1123          icmp_inode.gid = 0;
1124          icmp_inode.ttl = 1;
1125          init_queue_head(&icmp_inode.socket_wait);
1126          init_queue_head(&icmp_inode.u_wait);
1127
1128          icmp_socket->inode = &icmp_inode;
1129          icmp_socket->state = SOCK_UNCONNECTED;
1130          icmp_socket->proto = ops;
1131          icmp_socket->type = SOCK_RAW;
1132
1133          if ((err = socket(AF_INET, SOCK_RAW, IPPROTO_ICMP))<0)
1134              panic("Failed to create ICMP socket.\n");
1135          icmp_socket->alloc = kmalloc(GFP_ATOMIC);
1136          icmp_socket->ndbuf = SK_WMEM_MAX;
1137          icmp_socket->proto->af_inet.ttl = MAXTTL;
1138
1139          /* Unhash so that IP processing does not see incoming
1140           * packets, we do not wish this socket to see
1141           */
1142          icmp_socket->proto->unhash(icmp_socket);
1143      }
```

## 6.5 Group Management—IGMP

A reasonable fraction of the Internet supports multicast, particularly in tier-one ISPs and in academic and research networks where the access networks are LANs. The host membership system is managed through the host-router communications, Internet Group Protocol (IGMP). The Linux implementation is covered here.

### 6.5.1 IGMP

In this section we take a tour around multicast support in Linux. Multicast is a tricky concept and is intimately bounded between host and router functions, so rather than defer the main discussion to the chapter on routing, we look through most of the code here. The rationale is also that multicast makes use of encapsulation (tunnels) which is also discussed here as it is part host and router functionality.

> Figure 6.175 IGMP—data: linux/net/ipv4/icmp.c.

```c
#define IP_MAX_MEMBERSHIP 20

#ifdef CONFIG_IP_MULTICAST

/* Parameter names and values are taken from igmp-v2-06 draft */
#define IGMP_V1_Router_Present_Timeout (400*HZ)
#define IGMP_Unsolicited_Report_Interval (10*HZ)
#define IGMP_Query_Response_Interval (10*HZ)
#define IGMP_Unsolicited_Report_Count 2

#define IGMP_Initial_Report_Delay (1*HZ)

/* IGMP.Initial_Report_Delay is not from IGMP specs!
 * IGMP specs require to report membership immediately after
 * joining a group, but we delay the first report by a
 * small interval. It seems more natural and still does not
 * contradict to specs provided this delay is small enough.
 */
#define IGMP_V1_SEEN(in_dev) ((in_dev)->mr_v1_seen && (long)(jiffies - (in_dev)->mr_v1_seen
                                > 0))

#endif
```

```c
void __init icmp_init(struct net_proto *ops)
{
    int err;

    icmp_inode.af = AF_INET;
    icmp_inode.protocol = IPPROTO_ICMP;
    icmp_inode.state = 0;
    icmp_inode.uid = 0;
    icmp_inode.gid = 0;
    icmp_inode.ttl = 1;
    init_queue_head(&icmp_inode.socket_wait);
    init_queue_head(&icmp_inode.u_wait);

    icmp_socket->inode = &icmp_inode;
    icmp_socket->state = SOCK_UNCONNECTED;
    icmp_socket->proto = ops;
    icmp_socket->type = SOCK_RAW;

    if ((err = socket(AF_INET, SOCK_RAW, IPPROTO_ICMP))<0)
        panic("Failed to create ICMP socket.\n");
    icmp_socket->alloc = kmalloc(GFP_ATOMIC);
    icmp_socket->ndbuf = SK_WMEM_MAX;
    icmp_socket->proto->af_inet.ttl = MAXTTL;

    /* Unhash so that IP processing does not see incoming
     * packets, we do not wish this socket to see
     */
    icmp_socket->proto->unhash(icmp_socket);
}
```
