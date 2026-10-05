# # OffSec Penetration Testing with Kali Linux

| | | | |
|---|---|---||
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

![](bbox=[0.125, 0.345, 0.875, 0.585])

Figure 294: Upload Zip Archive to BloodHound

Once the upload is finished, we can start the enumeration of the AD environment BloodHound.

Before we start, let's briefly review of BloodHound's capabilities. As we have learned, BloodHound contains various pre-built queries as *Find all Domain Domains*. These queries are built with the *Cypher Query Language*.¹198 In addition to the pre-built queries, BloodHound also allows us to use custom queries via the *Raw Query* function at the bottom of the GUI.

Since we are currently interested in basic domain enumeration, as listing AD users and computers, we have to build and create custom queries as the pre-built functions don't provide these capabilities.

Let's build a raw query to display all computers identified by the collector. The query starts with the keyword `MATCH`, which is used to select a set of objects. Then, we set the variable m

> ¹198 Neo4j Cypher, 2022), neo4j.com/developer/cypher/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 837