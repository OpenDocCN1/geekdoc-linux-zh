would be a copy of the directories on a system not permanently connected to the network. If this system uses another processor architecture and a different kind of *NIX, then the commands would be even more secure. This system or the CD can be used to supply the commands to analysis scripts like chkrootkit or aide.

# 5.1.5 ntp Setup

The importance of a consistent time and date inside a network was already mentioned. The ntp protocol was created to gather this information and distribute it inside the network. If you want to keep things simple, then you just have to configure two machines inside the network either to get the time from a reliable time source inside your network or to connect to a reliable time source outside of your local area network (LAN). An internal time source could be a device that is either a reliable clock by itself, for example, an atomic clock, or a device receiving a time signal via the airwaves. The first solution could be expensive, though. Both solutions require some kind of device driver to access the current time and date. If you don’t want to deal with attaching hardware to one of your servers, the other solution would be getting the time from a time server. A list of time servers is available at http://www.ntp.org.

# Common Rules Regarding the Use of Time Servers

There are two types of time servers (actually, there are more, but for the sake of clarity the author assumes that there are two), primary time servers are called stratum 1, and secondary time servers called stratum 2. Some rules of thumb for using a stratum 1 server are as follows:

+   1. Your internal server serves at least 100 other computers inside your network.
+   2. Your internal server supplies the information to two to three other internal time servers as a failsafe measure (including routers equipped to function as time server).
+   3. You provide ntp access as a service for other networks in your geographical region to minimize network traffic.

These rules count on the fact that all users of the Internet try to save bandwidth; it is impossible, though, to enforce these rules. The fact that a significant number of stratum 1 servers that used to be available to the public have switched from unmonitored access to monitored access—this means to get data from the time host, you are supposed to register with the administrators