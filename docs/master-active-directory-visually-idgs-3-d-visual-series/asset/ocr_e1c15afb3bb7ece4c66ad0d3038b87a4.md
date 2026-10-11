# **MANAGING DNS SERVER TASKS**
**CONTINUED**

You can manually update the DNS server's database files, if desired, by using the Action menu and choosing Update Server Data Files. Data files are normally updated to the database at predefined intervals and when the server is shut down, but you can choose to manually update the files

as desired. This action causes the DNS service to write all changes to the zone data files immediately.

As with most MMC snap-in tools, you can also choose to stop, start, pause, and restart the DNS service by clicking the Action menu and accessing the All Tasks feature. In

case of server maintenance or problems, you can pause or stop the service while the problem is being resolved. When you do this, the server is not available to answer name resolution queries, but other DNS servers in the zone can take on the query load while the server is offline.

![](bbox=[0.04, 0.47, 0.94, 0.79])

+   **MANUALLY SCAVENGING DATABASE RECORDS**
+   **1.** *Choose Action*\> Scavenge Stale Resource Records to manually scavenge records.
+   **2.** Click OK to continue the scavenge operation.