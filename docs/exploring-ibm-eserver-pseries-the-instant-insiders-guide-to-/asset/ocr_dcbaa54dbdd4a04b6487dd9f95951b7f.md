# Exploring IBM @serverSeries

ring from node to node in a continuous circle. The token is the “mailbag” of the network. It carries the network messages (one at a time) from the transmitting node to all other nodes in the network until the recipient is reached and the message is delivered. When a node receives a frame, it looks to see if it is a message or a token frame. If it is a token frame, it means the network is idle and that node can send a message. If it is a message frame, the node will examine the address contained in the token to see if the message is intended for that node. If not, the frame will be passed unchanged to the next node in the ring.

Although IBM offers a 100/16/4 Mbps Token-Ring for some servers and personal computers, the pSeries emphasis is on Ethernet communications and only a 16/4 Mbps Token-Ring adapter (#4959) is available for pSeries servers.

# ASCII Terminal Networks

Although the use of ASCII terminals attached to pSeries systems is almost a thing of the past, it should be noted that pSeries provides support for users at ASCII terminals. Local terminals and printers are attached via industry-standard EIA-232 async communications ports (one port per terminal or printer). pSeries systems can stand with two or more ports. The 8-Port async Adapter EIA-232 (#2943) will provide the additional ports needed in our example configuration, for a total of 10 EIA-232 ports. The AIX operating system comes with the necessary support for the EIA-232 ports and the async protocols they use.

If it is necessary to attach a remote terminal to the pSeries system, a modem must be attached to a telephone line at each end (server and remote terminal). “Modem” stands for “modulator-demodulator” and is a device for modulating or translating digital signals into analog telephone-line signals for transmission, and versa (modulating) for receiving signals from other systems. IBM does not sell modems, but many industry-standard modems are available. With dialup telephone lines, 56 KBps modems are commonly used, and higher-speed modems are available for use on leased telephone circuits.

# Clustering for High Availability

We have already seen that pSeries systems can communicate with another over various types of LANs to implement data sharing, pro-