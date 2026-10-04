# Chapter 12 • Attacking and Defending Microsoft SQL Server

In order to illustrate the urgency of applying service packs and hotfixes, we discuss some of the more high-profile privilege escalation vulnerabilities that have occurred since SQL Server 2000 Service Pack 2. At the time of this writing, there are no less than 13 vulnerabilities that can escalate a user's privilege, usually via a buffer overflow. The escalation provides the attacker with operating system privilege equal to that of the service account, which easily gives the attacker access to the management-related Registry keys and read/write access to all database (.MDF) files. Table 12.5 lists some of the popular vulnerabilities that currently exist and where to find more information.

# Table 12.5 SQL Server 2000 Post SP2 Privilege Escalation Vulnerabilities

| Vulnerability | Link for more info |
|---||
| Microsoft SQL Server Extended Stored Procedure Privilege Elevation Vulnerability | www.ngsoftware.com/advisories/mssql-esppu.txt |
| Microsoft SQL Agent Jobs Privilege Elevation Vulnerability | www.ngsoftware.com/advisories/mssql-jobs.txt |
| Microsoft SQL Server 2000 and 7 Remotely Exploitable Buffer Overrun Vulnerability in the OpenRowSet Function | www.ngsoftware.com/advisories/mssql-ors.txt |
| Microsoft SQL Server 2000 Database Consistency Checkers Buffer Overflow Vulnerability | http://online.securityfocus.com/bid/5307 |
| Microsoft SQL Server 2000 Replication Stored Procedures Injection Vulnerability | http://online.securityfocus.com/bid/5309 |
| Microsoft SQL Server 2000 Service Heap Overflow Vulnerability | http://online.securityfocus.com/bid/5310 |
| Microsoft SQL Server 2000 Resolution Stack Overflow Vulnerability | http://online.securityfocus.com/bid/5311 |
| Microsoft MS-SQL Server Installation Password Caching Vulnerability | http://online.securityfocus.com/bid/5203 |
| Microsoft SQL MS Jet Engine Unicode Buffer Overflow Vulnerability | http://online.securityfocus.com/bid/5057 |

Continued

![](bbox=[0.067, 0.943, 0.296, 0.971])