# Ethereal

An additional tool that can be useful in monitoring network activity is Ethereal. This tool is an advanced packet-capturing tool capable of capturing all the conversations being transmitted across a network. Once conversations are captured, the stream of these packets can be reassembled, and both sides of the network conversation can be viewed. It is therefore possible to reconstruct Telnet and FTP sessions in their entirety. This includes the transmission of cleartext usernames and passwords. It is also possible to reconstruct web pages and binary transfers. Without the proper authority, running Ethereal may be interpreted as wiretapping. For this reason, it may be in conflict with a great many IT policies. In the proper hands, when used with the approval and knowledge of responsible parties, it can be instrumental in tracking down spurious traffic.

When used in conjunction with tools such as MRTG and Cacti, Ethereal can be used to further identify the source of traffic. As an example, assume that a known non-SNMP capable switch is hosting a machine that is causing network congestion. It is difficult to tell which of the hosts is generating the traffic because SNMP is unavailable to generate port-based statistics. Placing an Ethereal sniffer downstream from the switch will quickly identify which device is the most active.

# ETHERAPE

An additional tool not bundled with SLES might be of great interest: This tool, called EtherApe, can be downloaded from the project home page at http://etherape.sourceforge.net/.

This application monitors network traffic and tracks conversations between hosts. It presents all its information in a graphical mode, tracing actual lines between the different hosts as conversations take place. The more traffic passed between the hosts, the more intense the line is drawn.

EtherApe is also capable of monitoring for specific types of traffic. From the information displayed and the protocols seen, it is fairly easy to deduce the tasking of the multiple hosts.

Again, such network monitoring should be done only with the written consent of the owners of the network.

Additionally, because Ethereal can capture whole conversations, it can be used to reconstruct network events. As you can imagine, the amount of traffic carried over a network is tremendous. Ethereal allows for the inspection of packets for particular conversations and filters for specific traffic types. It is then possible to reconstruct whole sessions and examine the individual packet content.