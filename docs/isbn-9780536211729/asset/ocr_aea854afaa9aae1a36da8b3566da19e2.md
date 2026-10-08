# Table 2.3 Dangerous Services (Continued)

| Danger Level | Name | Where Discussed |
|---|---|---|
| ❌❌ | pop3 & imap | “POP and IMAP Servers” on page 152 |
| ❌❌ | systat and netstat | “Turn Off systat and netstat” on page 96 |
| ❌❌ | linuxconf | “Linuxconf via TCP Port 98” on page 581 |
| ❌❌ | named (DNS) | “DNS (named, a.k.a. BIND)” on page 149 |
| ❌❌ | rwhod | “Turn Off rwhod” on page 89 |
| ❌❌ | rwalld* | “Turn Off rwalld” on page 90 |
| ❌❌ | syslog | “The syslog Service” on page 178 |
| ❌❌ | ingresslock | “The Mysterious Ingresslock” on page 573 |
| ❌❌ | talk & ntalk* | “Turn Off talk and ntalk” on page 95 |
| ❌❌ | charger* | “Turn Off Echo and Chargers” on page 95 |

* Has DoS Potential. Do not allow service from external sites.

The C program (ports.c) is discussed here will list all your TCP and UDP ports that are open; state what they are in; the remote IP, host, and port that they are connected to (if any); and will note possible security breaches due to unusual port usage. Its ability to generate alerts for unusual port activity that might be cracker activity is an advantage over

```
netstat -atuvp
```

A copy of ports.c is on the CD-ROM.