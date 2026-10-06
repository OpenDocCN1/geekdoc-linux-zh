# Active Scanning

Although passive scanning can yield a lot of useful information, at some point the attacker needs to do an active scan, which involves some level of actual connection to the target system. It is the most likely to be detected, but also the most likely to yield actionable information. Several types of active scanning exist:

+   **Port scanning**: This is a process of scanning the 1024 well-known ports or even all the ports (there are 65,535) and seeing which ports are open. This can tell an attacker a great deal. For example, port 116 indicates the target is using Simple Network Management Protocol, which might provide a vulnerability that can be exploited. Port 88 tells an attacker that the target system uses Kerberos authentication.

+   **Enumeration**: This is a process whereby the attacker tries to find out what is on the target network. Items such as shared folders, user accounts, and similar items are sought after. Any of these can provide a point of attack. 

+   **Vulnerability assessment**: This is the use of some tool to seek out known vulnerabilities. The attacker might also try to manually assess vulnerabilities. The latter can be done in many ways. We discuss one of these methods later in this section.

![](bbox=[0.119, 0.103, 0.768, 0.442])