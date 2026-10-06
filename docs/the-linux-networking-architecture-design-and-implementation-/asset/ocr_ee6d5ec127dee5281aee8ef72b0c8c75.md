# CHAPTER 17

# IP Multicast for Group Communication

The history of telecommunication was characterized mainly by two technologies in the past hundred years (before the Internet era began): telephony, and radio and television broadcasting. These two technologies cover two fundamentally different communication areas or needs:

+   Individual communication (unicast): Connections between two communication partners, where the direction of data exchange can be unidirectional (simplex) or bidirectional (duplex).
Mass communication (broadcast): One station sends data to all stations reachable over a medium, where data distribution is normally unidirectional.

After these two technologies, the Internet followed as the third communication technology, changing the telecommunication world. Though the Internet was initially designed for individual communication, the protocols and mechanisms added at the beginning of the nineties introduced a new communication form: group communication- (multicast). Multicast makes possible an efficient data distribution to several receivers. By contrast with the mass communication of (radio) broadcasting, where data is distributed to all participants within one single transmission medium, group communication delivers to those receivers explicitly interested in this data. In addition, group communication in the Internet (IP multicast) enables each Internet computer to send data directly to the members of a multicast group.

Consequently, in the designing of mechanisms and protocols, two specific tasks can be deduced for the functionality of group communication in Internet systems:

+   managing memberships in group communication groups; and
efficient distribution of data packets to all members of a group.