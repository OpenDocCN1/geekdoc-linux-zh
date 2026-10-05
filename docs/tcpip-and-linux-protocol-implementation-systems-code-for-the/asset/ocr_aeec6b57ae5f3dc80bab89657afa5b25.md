# 6.5 Group Management—IGMP

A reasonable fraction of the Internet supports multicast, particularly in tier-one ISPs and in academic and research networks where the access networks are LANs. The host group membership system is managed through the host-router communications protocol, Internet Group Management Protocol (IGMP). The Linux implementation is covered here.

# 6.5.1 IGMP

In this section we take a tour around IP multicast support in Linux. Multicast is a tricky concept and is intimately bounded between host and router functions, so rather than defer the main discussion to the chapter on routing, we look through most of the code here. The rationale is also that UP multicast makes use of encapsulation (tunnels) which is also discussed here as it is part host and router functionality.

> Figure 6.175 IGMP—data: linux/net/ipv4/igmp.c.

```
102 #define IP_MAX_MEMBERSHIP 20
103 
104 #ifdef CONFIG_IP_MULTICAST
105 
106 
107 /* Parameter names and values are taken from igmp-v2-06 draft */
108 
109 #define IGMP_V1_Router_Present_Timeout (400*HZ)
110 #define IGMP_Unsolicited_Report_Interval (10*HZ)
111 #define IGMP_Query_Response_Interval (10*HZ)
112 #define IGMP_Unsolicited_Report_Count 2
113 
114 
115 #define IGMP_Initial_Report_Delay (1*HZ)
116 
117 /* IGMP.Initial_Report_Delay is not from IGMP specs!
118 * IGMP specs require to report membership immediately after
119 * joining a group, but we delay the first report by a
120 * small interval. It seems more natural and still does not
121 * contradict to specs provided this delay is small enough.
122 */
123 
124 #define IGMP_V1_SEEN(in_dev) ((in_dev)->mr_v1_seen && (long)(jiffies - (in_dev)->mr_v1_seen
125                                > 0))
126 
127 #endif
```