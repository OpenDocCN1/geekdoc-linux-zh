
Attacking and Defending Microsoft SQL Server • Chapter 12

# Overcoming a Sybase Past

In 1987, Microsoft and Sybase joined forces to develop a version of Sybase’s SQL Server product for OS/2. Eventually, Microsoft decided that the SQL Server product it was developing jointly with Sybase had a better future on the Windows NT platform. In 1993, version 4.2 of Microsoft SQL Server was released for Windows 3.1. Shortly after this release, in April of 1994, as it became obvious that their development efforts were headed in somewhat opposite sites, Microsoft and Sybase parted ways. Since the breakup, Microsoft has enhanced the product further, and in 1998 released SQL Server 7.0, which it claimed to be a complete rewrite of the query engine.

From the security angle, it is important to understand the history of SQL Server because it places some perspective on how the current authentication and authorization mechanisms evolved. When faced with a seemingly undocumented function or a strange column in a system table, it may help to know that some areas of SQL Server’s vestigial components remain only for purposes of backward compatibility. According to Microsoft, the incarnation of SQL Server contains very few code scraps from the Sybase version, but do not forget to keep old Sybase tech support handy in case you wander across an undocumented function—you never know what you might find.

Primarily, the security implication of SQL Server’s evolution from a Sybase product is that it inherited the intrinsic security model present in the product. Because of this, it has always existed in the product to support other platforms (Netware clients, for example) and for backwards compatibility. The native SQL Server security model has not changed much over the years because Microsoft seems squarely focused on integrating SQL Server into the Microsoft model. Unfortunately, the side effect has been that the native SQL security model contains none of features that one would expect to find in most modern, robust authentication mechanisms.

# Understanding SQL Server Editions

Each version of SQL Server that has been released over the years has come in a variety of licensing editions. Each edition is targeted for a specific purpose and has different features and, sometimes differing security implications. In this chapter, the focus is on SQL Server 2000 (all editions except CE), which is the latest version available. Also keep in mind that the features and examples shown to refer to SQL Server 2000, but many of the techniques and vulnerabilities explored apply to previous versions as well.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_645_0.png)

# Explaining SQL Server 2000 Retail Editions

The security implications of the various editions from the capabilities of each edition and which platforms are supported by them. For example, given that a certain edition does not run on Windows 98, simply finding that edition on a machine alerts an attacker that the host is NT/2000/XP. In addition, the more powerful an edition's functionality, the more opportunities there are for an intruder to exploit, such as more connectivity options or the introduction of Online Analytical Processing (OLAP) capabilities. See Table 12.1 for a breakdown of the SQL Server editions and the security implications of each.

# Table 12.1 SQL Server Editions

| SQL Server Edition | Intended Purpose | Security Implications |
|---|---|---|
| Enterprise Edition | Large-scale production servers that need near unlimited scalability and decision support services (OLAP) | Runs only on server-level Windows editions, so an install guarantees that Windows authentication is possible, assuming full network connectivity. The added functionality of this edition (if enabled) means there may be more vectors for attack, such as full replication capability. |
| Standard Edition | Small workgroups do not require OLAP functionality | Same as Enterprise Edition but without some of the more advanced OLAP capabilities (standard OLAP features only). |
| Personal Edition | Mobile users who can live with a database tuned for five users or less | Is capable of running on Windows 9dx editions where integrated authentication is not an option. Forced SQL Server authentication means the weaker security model is always selected. |
| Developer Edition | Developers who need the full functionality of the Enterprise Edition but do not intend to use the database for production | Developers are sadly sometimes the least security conscious, and development systems are also change-sensitive. Expect these installations to be rarely up to date |

# Attacking and Defending Microsoft SQL Server • Chapter 12

# MSDE 2000

First appearing with the release of SQL Server 7.0, the Microsoft Data Engine (MSDE) is a freely distributable version of SQL primarily targeted at stand-alone applications. You'll find it lurking on Microsoft Office and Visual Studio distribution CDs, and it has several restrictions, including being tuned for five or less concurrent users (like the Personal Edition) and limited to 2GB in size. MSDE also includes no management tools such as Query Analyzer (QA) or Enterprise Manager (EM), so your only way of communicating with it is the osql.exe utility (unless you have the tools from the SQL Server CD installed somewhere.)

The security concerns with MSDE exist on several levels. The primary problem is that the user is completely oblivious to the installation of MSDE by an application. Because of this, MSDE installs are rarely configured securely and rarely kept up to date with the latest security patches. For example, we have all seen shops where every other development workstation both SQL Server Developer Edition and a MSDE install (usually installing the Visual Studio.NET samples).

# WARNING

An additional frightening "feature" of MSDE is that, by default, executes with LocalSystem security context, allowing anyone who can successfully stage a buffer overflow attack install administrative access to the machine. When designing applications that use MSDE, take the time to set a low-privilege account and assign it as the service account. For more information on customizing an MSDE installation http://support.microsoft.com/default.aspx?scid=KB;EN-US;q233312.

One additional security concern of MSDE is that service pack installations can be cumbersome. This is due to a variety of reasons. For one thing, the service pack for MSDE is a separate download from the normal SQL Server service pack. For example, at www://microsoft.com/sql/downloads/2000/engsp2.aspx you'll find that the MSDE patch is named SQL2DKSP2 and is totally separate from the normal SQL Server download. In addition, when you read the sp2readme.htm file that explains the installation details, you'll find that if your version of MSDE was installed using the file sqlrun0.msi you can upgrade to Service Pack 2, but if you've used any of the other 15 possible installers (sqlun02–16)

![](img/729efc56f204a2ebffb8295c3a2dfdfb_647_0.png)

to order the SQL Server Service Pack 2 CD from Microsoft. If you need help determining your MSDE installer file, see http://support.microsoft.com/default.aspx?scid=kb;en-us;q311762. Be sure to review the readme file that comes with the SQL2kdesktopSP2.exe download for more information regarding MSDE updating.

# Understanding SQL Server Security Basics

In order to effectively defend SQL Server, you must first understand its basic terminology and features. Even if you are completely familiar with SQL Server, take the time to at least reread this section in case there were some security-related subtleties you may have missed. Each facet of Server has security implications that may not be obvious at installation time, but it is important that you know them in order to match the risks with the specific threats that exist in your deployments.

# Explaining SQL Server Instances

Beginning with version 2000, SQL Server now supports multiple instances installed on a single machine. Primarily targeted at application service providers (ASPs) and Internet service providers (ISPs), this gives users the ability to completely keep a customer's data, settings, and executables (server executables only—client tools) shared from other customers SQL instance. Obviously, this could be a good thing from a security perspective. However, it can also have some serious implications (see the sidebar that appears in this section).

Try Ask a developer in your organization how many instances of SQL Server they have installed on their machines? The most likely answer will probably be a resounding “huh?” Truth to be, Microsoft has not made a very simple task to immediately identify all instances. One quick way to check is to look at the Services listing (in Control Manager or Computer Management) for any service that begins with MSSQL. The default instance of SQL Server will be called MSSQLServer, and any additional instances will be named MSSQL$(Instance Name), such as MSSQL\$Netsdk.
