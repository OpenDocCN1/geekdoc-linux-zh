```
$nc
```

+   1) Netcat for Port Scanning Beginners always get confused with the term port scanning due to its popularity in penetration testers. If we want to explain about port scanning in layman terms it is a process of trying to find open ports that are vulnerable via tools for hope to find a vulnerability or backdoor which can be used for exploitation. Here is the command to do port scanning using netcat utility.

```
$nc -z -v -n 192.232.2.3 21-25
```

+   2) Using Netcat to start a chat server Imagine yourself in a restricted location like in workspace where you can't use messaging services. netcat can solve you that problem by creating a chat server that can be used to converse with other systems in the Network. You can then create a server that will act as a chat system to whoever you want to communicate within the network.

Server $ nc -l 2343
Client $ nc 192.232.2.1 2343
All your messages will be transported to the client using netcat server and the best thing is that the communications will be encrypted and cannot be caught by any sniffing software like Wireshark.

+   3) File Transfer A lot of hackers when attacking in premises of a network are required to exchanges files between two computers or devices. Normally people use File transfer protocol to transfer files between hosts. But when you are in a private network that doesn't allow you to install additional software Netcat is your safe bet to transfer files. You can send for example an .avi file from X to Y system by making either one of them as a client and other as the server.

Server
$nc -l 6870 < example.avi

Client
$nc -n 192.232.2.1 6870 > example.avi