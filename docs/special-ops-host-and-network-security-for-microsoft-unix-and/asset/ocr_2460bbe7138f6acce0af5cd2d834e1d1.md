# Chapter 12 • Attacking and Defending Microsoft SQL Server

Figure 12.7 shows some of the suggested events and their associated event codes. The tool to manage messages and isolate events for which you would like to create alerts can be found using Enterprise Manager | Tools | Manage SQL Servers.

# Figure 12.7 Use the Enterprise Manager to Isolate Events for Which You Would Like to Create Alerts

![](bbox=[0.288, 0.222, 0.663, 0.413])

# Dumping Permissions

It sometimes may be necessary to dump permissions for SQL Server objects, like the DumpSec tool from Somsart (www.somarsoft.com) does for file permissions. You can accomplish this with a few queries against the system tables. For example, the following query displays all stored procedures and extended stored procedures in the master database that can be invoked by members of the public role:

```
Use master
Select sysobjects.name
From sysobjects,sysprotects
Where sysprotects.uid = 0
AND xtype IN ('X','P')
AND sysobjects.id = sysprotects.id
Order by name
```

(Please see the book's companion Web site at www.sygress.com/solutions for more scripts to help enumerate permissions and configuration settings on your SQL Servers.)