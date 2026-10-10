On the second discovered address, we can guess that this node is some form of UNIX server. After we run numerous scans, server port patterns such as the following emerge:

+   - **206.0.126.8:7, 11, 15, 19, 21, 23, 25, 80, 110, 111**

+   - **Port 7: echo.** A module in communications; a signal transmitted back to the sender that is distinct from the original signal. Echoing a message back to the main computer can test network connections. The primary message generation utility is PING.

+   - **Port 11: systat.** The systat service is a UNIX server function that provides the capability to remotely list running processes. From this information, a hacker can pick and choose which attacks are most successful.

+   - **Port 15: netstat.** The netstat command allows the display of the status of active network connections, MTU size, and so on. From this information, a hacker can make a hypothesis about trust relationships to infiltrate outside the current domain.

+   - **Port 19: chargen.** The chargen service is designed to generate a stream of characters for testing purposes. Remote attackers can abuse this service by forming a loop from the system’s echo service with the chargen service. The attacker does not need to be on the current subnet to cause heavy network degradation with this spoofed network session.

+   - **Port 21: FTP.** An open FTP daemon banner can assist a hacker by listing the service daemon version. Depending on the operating system and daemon version, the attacker, may be able to gain anonymous access to the system.

+   - **Port 23: telnet.** A daemon that provides access and administration of a remote computer over the network or Internet. To more efficiently attack the system, a hacker can use information given by the telnet service.

+   - **Port 25: SMTP.** With SMTP and Port 110: POP3, an attacker can abuse mail services by sending mail bombs, by spoofing mail, or simply by stealing gateway services for Internet mail transmissions.

+   - **Port 80: HTTP.** The HTTP daemon indicates an active Web server service. This port is simply an open door for several service attacks, including remote command execution, file and directory listing, searches, file exploitation, file system access, script exploitation, mail service abuse, secure data exploitation, and Web page altering.

+   - **Port 110: POP3.** With POP3 and Port 25: SMTP, an attacker can abuse mail services by sending mail bombs, by spoofing mail, or simply by stealing gateway services for Internet mail transmissions.

+   - **Port 111: Portmap.** This service allows RPC client programs to make remote connections to RPC servers. A remote attacker can use this service to poll hosts for RPC weaknesses.

Clearly, this system is a UNIX server, probably configured by a novice administrator. Keep in mind, however, that recent statistics claim that over 89 percent of all networks connected to the Internet are vulnerable to some type of serious penetration attack.

The next system was previously discovered as our target company’s Web server.

+   - **206.0.126.10:21, 23, 80**

+   - **Port 80: HTTP.** The HTTP daemon indicates an active Web server service. This port is simply an open door for several service attacks, including remote command execution, file and directory listing, searches, file exploitation, file system access, script exploitation, mail service abuse, secure data exploitation, and Web page altering.

Also in a previous discovery, we learned this next system to be our target mail server. Again, we’ll run specific penetration scans in chapters to come:

+   - **206.0.126.11:25, 110**