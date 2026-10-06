# Chapter 17 IP Multicast for Group Communication

# Membership report
(Group 233.31.7.73)

![](bbox=[0.155, 0.085, 0.843, 0.269])

Host A:
233.31.7.73 (8)
228.7.6.95 (7)

Host B:
233.31.7.73 (2)
228.7.9.97 (9)

Host C:
233.31.7.73 (6)
228.7.9.97 (11)

Timer for report
of group 228.7.9.97

FIGURE 17–7

Membership report of a group by the participant with the smallest timer value in that group.

If the router does not receive reports for a specific group over a period of time, it assumes that there are no more interested computers and deletes this group from its list. If a computer wants to join a group, it can explicitly request this in IGMPv2 by sending a New Membership Report packet. In older protocols, the computer may have had to wait a few minutes until the router sends a query message.

When IGMPv2 routers send their queries, they write a specific value to the Max Resp time field. A larger value than null tells the computers that this is IGMPv2 computers can send version-2 reports (IGMP_HOST_NEW_MEMBERSHIP_REPORT).

In addition, IGMPv2 computers can leave a specific group by sending an IGMP_HOST_LEAVE message to the all-routers. The group to leave is identified in the group field. Early notification of a station to leave a group can help reduce the load in the local area network. However, each group member request to leave a group are sent to the local area network not when it is no longer interested in this data, but only if the group member was the reporter—the computer that originally sent the membership report for that group. This approach avoids a large number of Leave packets. If the reporter was the only group member, then the router can stop delivering packets of that group in any event. If there are other members than the reporter in the local area network, these members can react to a Leave message immediately by sending a report to the router telling it there is still an interest in this data.

A conflict can arise if there is more than one multicast-capable router in one local area network. In such a situation, two routers could transport redundant multicast packets to the LAN. The question is: who decides which router will serve which group? The problem is solved by a simple mechanism known from other protocols: the router with the smallest IP address assumes the role of a coordinator. The other routers just listen to the traffic until the coordinator fails. In this case, the router with the next smallest address assumes the role of the multicast router, a good indicator that a multicast router has failed occurs when no group queries arrive.