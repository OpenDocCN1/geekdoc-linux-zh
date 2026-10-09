![](bbox=[0.14, 0.05, 0.82, 0.29])

DMZs place more than one barrier between the Internet and the intranet (see Figure 16.2).

> Figure 16.2. A DMZ requires conduits through the firewall to pass information.

![](bbox=[0.14, 0.36, 0.82, 0.54])

To get the most out of a DMZ, you must establish rules about what goes inside it. Firewalls rarely provide many services; the servers behind the firewall do. However, if you expose too much inside the DMZ, you might as well forget DMZs and save your money. The rules of conduct become (by necessity) more relaxed as you get closer to the intranet. The following list offers several common rules:

+   Minimize ports (exposed firewalls)— Most firewalls exposed to the outside world limit the number of ports available. These ports provide precisely what the client needs to get information offered by the company. The ports that are exposed provide more ways an attacker may gain access.

# NOTE

The RPC Hole

Many network programmers recognize the potential for intrusion as the number of ports rises. However, less-experienced programmers may not realize that they may use tools that create ports on-the-fly. For example, the portmap program for Remote Procedure Calls (RPCs) creates ports. Furthermore, Java's Remote Method Invocation (RMI) and Microsoft's COM/COM\+ sit on top of RPCs. Webmasters who write script for servers may not realize that they are opening new security holes with each new object.