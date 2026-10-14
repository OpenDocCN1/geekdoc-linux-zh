Ring topology was designed by IBM and is illustrated in Figure B-5.

![](bbox=[0.1, 0.16, 0.6, 0.42])

Figure B-5

It is not practical to have pure ring topology implementations because a network based on a ring topology cannot be easily reconfigured. To add or remove computers from a network using the ring topology, you have to break the ring.

A network based on the ring topology uses a method called token passing to transmit data. In this method, an empty token is passed around the ring. Tokens travel around a 600-meter ring about 477,000 times per second.

The device that wants to transmit data signals acquires the token. Data signals pass through each device on the ring and reach the destination computer. When the destination device receives the data, it sends back a signal acknowledging receipt of data to the source device.

The signal is called as an acknowledgement signal. After receiving an acknowledgement signal, the token is emptied and passed to another device on the network that wants to start data transmission.

A network based on the ring topology uses unshielded twisted pair and fiber-optic cables. The cost of a network based on this topology varies depending upon the type of cable used. This topology is not used widely because it requires expensive and specialized equipment.

Data transmission on this type of network is fast. The network does not weaken the strength of the signal and enables data to travel large distances. Therefore, a large number of devices can be attached to the network.

However, the failure of a computer or a cable segment can cause the entire network to stop functioning. Therefore, a network based on a ring topology is not easy to troubleshoot.

# Star

In a star topology, all computers are connected to a switch, and all data passes through the switch before reaching its destination. Although a switch is involved, the underlying topology is still a bus or a ring.

A star topology is the most popular technology used to network computers. Networks using the star topology are easy to install and manage.