correspond to specific services. Some available port numbers can be defined by the user. Port numbers are combined with the source and destination addresses of the data to create a socket. Each network interface may have multiple open sockets at a given time that are both transmitting and receiving data. These sockets organize all of these transmissions and prevent them from being scrambled.

Because the port numbers for commonly used services are predefined, they are stored on each computer. On Linux systems the port assignments are located in the /etc/services file, which is discussed later in this chapter. Table 15-3 lists the most commonly used applications and their default port assignments.

![](bbox=[0.13, 0.31, 0.19, 0.37])

**Exam Tip**  It is important to memorize the standard list of port assignments for the exam.

Table 15-3
**Port Assignments**

| Application | Port |
| :--- | :--- |
| FTP-DATA | 20 |
| FTP | 21 |
| SSH | 22 |
| Telnet | 23 |
| SMTP | 25 |
| DNS | 53 |
| finger | 79 |
| HTTP | 80 |
| WWW | 80 |
| POP2 | 109 |
| POP3 | 110 |
| NNTP | 119 |
| NETBIOS-SSN (session service) | 139 |
| IMAP | 143 |
| SNMP | 161 |
| IRC | 194 |
| HTTPS | 443 |