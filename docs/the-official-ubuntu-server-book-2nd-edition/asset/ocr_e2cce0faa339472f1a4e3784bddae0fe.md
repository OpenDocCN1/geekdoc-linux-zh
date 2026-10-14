# LTSP Server Configurations

The LTSP server install allows a great deal of flexibility and is designed to allow it to fit into any current network configuration. Essentially these fall into two categories: those that use the LTSP server as a primary gateway for all their LTSP clients and those that do not. Let’s take a few minutes to discuss the relative merits of each system.

Using the recommended configuration requires the LTSP server machine to have two network interface cards (NICs). One of these cards is connected to the rest of the network, that is, to the Internet or to other servers on the internal network. The other card is usually connected to a private subnet of the network where only Edubuntu LTSP clients reside. Figure 5-8 shows this two-NIC setup. No network data is routed from the second network card to the first, so client machines must be authenticated on the LTSP server before having access to the Internet or the rest of the network. This makes for a secure network setup.

The benefit to this setup is that client computers cannot connect to the network unless the LTSP server permits them to. This also reduces net-

![](bbox=[0.22, 0.58, 0.85, 0.9])

Figure 5-8 Two-NIC setup