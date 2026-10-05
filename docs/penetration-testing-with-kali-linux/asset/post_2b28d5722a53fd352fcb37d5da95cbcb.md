
# OffSec Penetration Testing with Kali Linux

| | | | |
|---|---|---|---|
| d---- | 9/29/2022 | 1:49 AM | Music |
| d---- | 9/29/2022 | 1:50 AM | OneDrive |
| d---- | 9/29/2022 | 1:50 AM | Pictures |
| d---- | 9/29/2022 | 1:49 AM | Saved Games |
| d---- | 9/29/2022 | 1:50 AM | Searches |
| d---- | 9/29/2022 | 4:30 AM | Videos |
| a---- | 10/10/2022 | 7:25 AM | 11995 822210072521_BloodHound.zip |
| a---- | 10/10/2022 | 7:23 AM | 131897 SharpHound.ps1 |
| a---- | 10/10/2022 | 5:02 AM | 1936384 winPEAS.exe |
| a---- | 10/10/2022 | 7:25 AM | 8703 |

Zjc50GNlNTkmZn0i9OTYtkhWEZEtnHNkWZGnlDDzl.bin
Listing 95 - Directory listing to identify the name of the SharpHound zip

Let's filter to use the Kali machine then start neo4j and BloodHound. Once BloodHound is started, we'll upload the zip archive with the Upload function.

![](img/336d6ea891e7464f18ad64426619ced4_836_0.png)

Figure 294: Upload Zip Archive to BloodHound

Once the upload is finished, we can start the enumeration of the AD environment with BloodHound.

Before we start, let's briefly review BloodHound's capabilities. As we have learned, BloodHound contains various pre-built queries as *Find all Domain Domains*. These queries are built with the *Cypher Query Language*.¹198 In addition to the pre-built queries, BloodHound also allows us to use custom queries via the *Raw Query* function at the bottom of the GUI.

Since we are currently interested in basic domain enumeration, such as listing AD users and computers, we have to build and create custom queries as the pre-built functions don't provide these capabilities.

Let's build a raw query to display all computers identified by the collector. The query starts with the keyword `MATCH`, which is used to select a set of objects. Then, we set the variable m containing all objects in the database with the property Computer. Next, we use the RETURN keyword to build the resulting graph based on the objects in m.

> ¹198 Neo4j Cypher, 2022), neo4j.com/developer/cypher/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 837

```
MATCH (m:Computer) RETURN m
```

Listing 916 - Custom query to display all computers

Let's enter this query in the Raw Query section and build the graph.

![](img/336d6ea891e7464f18ad64426619ced4_837_0.png)

Figure 295: Show all Computer objects in the BEYOND.COM domain

Figure 295 shows there are four computer objects in the domain. By clicking on the nodes, we can obtain additional information about the computer objects, such as the operating system.

- DCSRV1.BEYOND.COM - Windows Server 2022 Standard
- INTERNLSV1.BEYOND.COM - Windows Server 2022 Standard
- MAILSRV1.BEYOND.COM - Windows Server 2022 Standard
- CLIENTWK1.BEYOND.COM - Windows 11 Pro

Listing 917 - Identified computer objects and their operating system

In addition to CLIENTWK1, where we have an interactive shell, BloodHound has also identified the already known domain controller DCSRV1 and dual-homed mail server MAILSRV1. Furthermore, it discovered another machine named INTERNALSRV1.

Let's obtain the IP address for INTERNALSRV1 with nslookup.

```
PS C:\>Users\marcus> nslookup INTERNALSRV1.BEYOND.COM
nslookup INTERNALSRV1.BEYOND.COM
Server: Unknown
Address: 172.16.6.240
```

# OffSec BEYOND.COM

Name: INTERNALSRV1.BEYOND.COM
Address: 172.16.6.241

> Listing 918 - Looking up the IP address of INTERNALSRV1 via nslookup

Listing 918 shows that the IP address of INTERNALSRV1 is 172.16.6.241. Let's add this information to computer.txt on our Kali machine.

```
172.16.6.240 - DCSRV1.BEYOND.COM
-> Domain Controller
172.16.6.241 - INTERNALSRV1.BEYOND.COM
172.16.6.254 - MASRV1.BEYOND.COM
-> Mail Server
-> Dual Hosted Host (External IP: 192.168.50.242)
172.16.6.243 - CLIENTWK1.BEYOND.COM
-> User marcus_ fetches emails on this machine
```

> Listing 919 - Documenting results and information in computer.txt

Next, we will display all user accounts on the domain. For this, we can replace the Computer property of the previous query with User.

![](img/336d6ea891e7464f18ad64426619ced4_838_0.png)

Figure 296: Show all User objects in the BEYOND.COM domain

Figure 296 shows that apart from the default AD user accounts, there are four other user accounts in the domain.

- BECCY
- JOHN
- DANIELA MARCUS

Listing 920 - Discovered domain users

We already identified john and marcus as valid domain users in previous steps. However, we haven't established if daniela is also a domain user or just a local user on WEBSRV1. In addition, we discovered a new user name becky. Let's update usernames.txt.

To be able to use BloodHound's pre-built queries, we can mark marcus (interactive shell on CLIENTWK1) and john (valid credentials) as Owned. To do this, we right-click on the MARCUS@BEYOND.COM and JOHN@BEYOND.COM nodes and select Mark User as Owned.

Next, let's display all domain administrators by using the pre-built Find All Domain Admins under the Analysis tab.

| Search for a node | Node Info | Analysis |
|---|---|---|---|
| Pre-Built Analytics Queries Domain Information | Find All Domain Admins | Map Domain Trusts | Find Computers with Unsupported Operating Systems |
| Dangerous Privileges | Find Principals with DCSyncRights | Users with Foreign Domain Group Membership | Groups with Foreign Domain Group Membership |
| Find Computers where Domain Users | | | |

![](img/336d6ea891e7464f18ad64426619ced4_839_0.png)

Figure 297: Show all User objects in the BEYOND.COM domain

Figure 297 shows that apart from the default AD user accounts, becky is also a member of the Admins group.

- Workstations where Domain Users can RDP
- Servers where Domain Users can RDP
- Computers where Domain Users are Local Admin
- Shortest Path to Domain Admins from Owned

# OffSec Penetration Testing with Kali Linux

24.4.2 Services and Sessions
