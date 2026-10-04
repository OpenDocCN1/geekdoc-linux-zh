# Attacking and Defending Microsoft SQL Server • Chapter 12

# Table 12.5 SQL Server 2000 Post SP2 Privilege Escalation Vulnerabilities

| Vulnerability | Link for more info |
|--- | --- |
| Microsoft SQL Server 2000 Password Encryption Buffer Overflow Vulnerability | http://online.securityfocus.com/bid/5014 |
| Microsoft SQL Server SQLXML Buffer Overflow Vulnerability | http://online.securityfocus.com/bid/5004 |
| Microsoft SQL Server SQLXML Script Injection Vulnerability | http://online.securityfocus.com/bid/5005 |
| Microsoft SQL Server 2000 Bulk Insert Buffer Overflow Vulnerability | http://online.securityfocus.com/bid/4874 |
| Microsoft SQL Server 2000 Incorrect Registry Permissions Vulnerability | http://online.securityfocus.com/bid/5250 |
| Microsoft SQL Server Multiple Extended Stored Procedure Buffer Overflow Vulnerabilities | http://online.securityfocus.com/bid/4231 |
| Microsoft SQL Server OLE DB Name Buffer Overflow Vulnerability | http://online.securityfocus.com/bid/4135 |

Never assume that unsophisticated attackers lack the ability to stage successful buffer overflow attacks against your servers. In many cases, they can simply make modifications to exploit samples written by security professionals that serve as a proof-of-concept. The following source code, written by David Litchfield of NGSSoftware, which remotely exploits a buffer overflow in the Microsoft Jet database engine using SQL Server the injection mechanism, was found on the Internet using a simple search engine. Keep in mind that the solution is not to stop professionals from releasing vulnerabilities and proof-of-concept exploits for administrators to do their jobs and protect their systems.

+   - Simple Proof of Concept
- Exploits a buffer overrun in OpenDataSource()
- Demonstrates how to exploit a UNICODE overflow using T-SQL
- Calls CreateFile() creating a file c:\SQL-ODJET-BO
- I'm overwriting the saved return address with 0x42B0C9CDC