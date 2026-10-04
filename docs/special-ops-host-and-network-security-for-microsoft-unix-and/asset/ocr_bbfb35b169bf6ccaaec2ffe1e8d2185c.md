Attacking and Defending Microsoft SQL Server • Chapter 12

# Overcoming a Sybase Past

In 1987, Microsoft and Sybase joined forces to develop a version of Sybase’s SQL Server product for OS/2. Eventually, Microsoft decided that the SQL Server product it was developing jointly with Sybase had a better future on the Windows NT platform. In 1993, version 4.2 of Microsoft SQL Server was released for Windows 3.1. Shordly after this release, in April of 1994, as it became obvious that their development efforts were headed in somewhat opposite sites, Microsoft and Sybase parted ways. Since the breakup, Microsoft has enhanced the product further, and in 1998 released SQL Server 7.0, which it claimed to be a complete rewrite of the query engine.

From the security angle, it is important to understand the history of SQL Server because it places some perspective on how the current authentication and authorization mechanisms evolved. When faced with a seemingly undocumented function or a strange column in a system table, it may help to know that some areas of SQL Server’s vestigial components remain only for purposes of backward compatibility. According to Microsoft, the incarnation of SQL Server contains very few code scraps from the Sybase version, but do not forget to keep old Sybase tech support handy in case you wander across an undocumented function—you never know what you might find.

Primarily, the security implication of SQL Server’s evolution from a Sybase product is that it inherited the intrinsic security model present in the product. Because of this, it has always existed in the product to support other platforms (Netware clients, for example) and for backwards compatibility. The native SQL Server security model has not changed much over the years because Microsoft seems squarely focused on integrating SQL Server into the Microsoft model. Unfortunately, the side effect has been that the native SQL security model contains none of features that one would expect to find in most modern, robust authentication mechanisms.

# Understanding SQL Server Editions

Each version of SQL Server that has been released over the years has come in a variety of licensing editions. Each edition is targeted for a specific purpose and has different features and, sometimes differing security implications. In this chapter, the focus is on SQL Server 2000 (all editions except CE), which is the latest version available. Also keep in mind that the features and examples shown to refer to SQL Server 2000, but many of the techniques and vulnerabilities explored apply to previous versions as well.

![](bbox=[0.708, 0.946, 0.928, 0.966])