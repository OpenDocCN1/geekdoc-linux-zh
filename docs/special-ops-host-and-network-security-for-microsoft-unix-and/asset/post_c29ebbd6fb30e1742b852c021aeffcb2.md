
# Attacking and Defending Microsoft SQL Server • Chapter 12

Figure 12.5 Use the Local Security Policy to Remove Unnecessary Rights for the Service Account

![](img/729efc56f204a2ebffb8295c3a2dfdfb_677_0.png)

## Disabling Ad Hoc Queries

Ad hoc queries (using the OPENROWSET keyword) are a great way for users to pull data from other sources into SQL Server, but they also make a great way for attackers to target other data sources. In addition, several security issues have been associated with ad hoc queries in the past, including buffer overflows (www.microsoft.com/technet/security/bullet/MS02-007.asp) and a privilege escalation vulnerability (www.microsoft.com/technet/security/bullet/fq00-014.asp). For this reason, it is advised that you disable ad hoc queries on all data access providers by creating a Registry entry called DisableAdhocAccess and setting it to a hex (REG_DWORD) value of 1 (see Figure 12.6). This must be done for each provider individually but can easily be scripted or manually applied to the Registry via Regedit. Here is an example Registry import file that will allow ad hoc queries on the SQLOLEDB provider:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Providers\SQLOLEDB]
"AllowInProcess"=dword:00000001
"DisallowAdhocAccess"=dword:00000001
```

## Figure 12.6 Disallow Ad Hoc Access to Each Provider until Your Applications Require This Functionality

![](img/729efc56f204a2ebffb8295c3a2dfdfb_678_0.png)

When a user attempts to issue an ad hoc query using the OPENROWSET command, they will receive the message “Ad hoc access to OLE DB provider %’ has been denied. You must access this provider through a linked server.”You can always remove the Registry value (or set it to 0) when you are ready to allow access to the provider at some point. As a security precaution, it is recommended that all SQL Server installations include a script to disable the ad hoc query capability until it is required.

## Setting Operating System ACLs

What good would it to implement airtight security on the SQL Server and databases and leave the .mdf files hanging around with read permissions for all users, or worse, on a FAT partition! Take the time to ensure that your data files as well as all files in the \Microsoft SQL Server\ directory (and subdirectories) are accessible to Administrators, System, and the SQL Server/Agent service accounts. If you store the data files (.mdf and .ldf files) in another location, be sure to properly Access Control List (ACL) them as well. While you are checking all of those file system ACLs, take the time to double-check the Registry as well. Check all of the Registry permissions under the key HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer.

## Dropping Dangerous Extended Stored Procedures

Extended stored procedures (XPs), which are implemented as DLLs that are loaded into the SQL Server's process space, provide extra functionality but can also be a security liability. The xp_cmdshell XP, for example, can be a great convenience to the DBA who needs to run an OS command or copy some files, but it can also be a boon for an attacker to gain access to the operating system. It is no problem to drop any XPs that you fear be abused but keep in mind that a person with system administrator privileges can add the XP back as long as the DLL still exists. This might lead you to believe that you should delete the DLL as well, but the problem with that solution is that one DLL usually services all XPs so you may end up removing more XPs than you had intended if you remove the DLL. The primary reason for dropping extended stored procedures is to thwart unanticipated attackers and worms. Refer Table 12.6 for a listing of XPs to consider dropping. Please be sure to thoroughly test, because some of these will retain functionality (such as the ability to run Enterprise Manager).

## Table 12.6 Extended Stored Procedures to Consider for Removal

| sp_bindsession | xp_dirtree | xp_perfsample |
| :--- | :--- | :--- |
| sp_getbindtoken | xp_dropwetask | xp_perfstart |
| sp_GetMBCSCharLen | xp_dsninfo | xp_readrorlog |
| sp_IsMBCSCharLeadBy | xp_enumsdn | xp_readmail |
| sp_OACreate | xp_enumerrorlogs | xp_revoklogin |
| sp_OADestroy | xp_enumgroups | xp_runwetask |
| sp_OAGetErrorInfo | xp_enumqueuedtasks | xp_schedulersignal |
| sp_OAGetProperty | xp_eventlog | xp_sendmail |
| sp_OAMethod | xp_findnextmsg | xp_servicecontrol |
| sp_OASetProperty | xp_fixedrives | xp_snmp_getstate |
| sp_AO | xp_getfileetails | xp_snmp_raisetrap |
| sp_replcmds | xp_getname | xp_sprint |
| sp_replcounters | xp_grantlogin | xp_sqinventory |
| sp_replldone | xp_logevent | xp_sqlregister |
| sp_replflush | xp_logconfig | xp_sqtlrace |
| sp_replstatus | xp_logininfo | xp_scancf |
| sp_reptrans | xp_makewebtask | xp_startm |
| sp_sdebug | xp_msver | xp_stopmail |
| xp_availablemedia | xp_perfend | xp_subdirs |
| xp_cmdshell | xp_perfmonitor | xp_unc_to_drive |
| xp_deletemail | | |

## Tightening Permissions on Job-Related Stored Procedures

The SQL Server agent service allows for the creation of jobs that can be executed at a later date or on a recurring basis. Unfortunately, this capability is allowed by even the lowest user by default. A hostile user has the ability to create a procedure to continually submit an unlimited amount of jobs and have them execute at he chooses. This could represent a significant denial of service risk and also represents a clear case of excessive privilege. It is recommended that you remove permissions from the public role so that low-privilege users cannot issue jobs. The following procedures are located in the MSDDB database and should be secured immediately after installation:

- sp_add_job
- sp_add_jobstep
- sp_add_jobobserver
- sp_start_job

## Monitoring and Maintenance

In order to maintain your secure configuration, it is important to monitor the SQL Server for changes, attempted intrusions, updates, and anything that might suddenly bring what was once thought to be a secure installation to its knees. The single most important way to keep a secure configuration safe is to keep up to date on service patches and hotfixes. Without a doubt, besides another way SQL Servers are penetrated is an out of date installation caused by poor administration. Remember, no matter many checklists you compared your system against, a vulnerability could be released tomorrow that totally nullifies anything that you have done in the past. Keep your servers up to date, and you'll stay employed. A prime example is the remote Resolution

![](img/729efc56f204a2ebffb8295c3a2dfdfb_680_0.png)

## Keeping Up With Service Packs and Hotfixes

This is the most important area of your SQL Server maintenance, and it can be the most daunting. At the time of this writing, Windows Update does not support detection of SQL packs and hotfixes. You might think the SQLPing tool would be useful for determining patch levels, but the UPD 1434 Resolution Service does not show the version.

The most reliable way to detect service packs is to look under the server's Properties in Enterprise Manager or manually request the version by querying the server so

```
Select @version
go
```

Note that the version changes will reflect only service packs. Hotfixes do not alter the version numbers, so you'll need to keep track of those manually. You can return the version information from various lists like as http://yaskrip.com/sqljps.htm to be sure you are up to date. Another option is to use Microsoft's HFNetChk tool at www.microsoft.com/security to scan machines for out of date SQL Server installations. A nice feature of HFNetChk is that it scans each instance of SQL Server installed and reports on each instance separately, so it's easy to pinpoint rough changes that are woefully out of date and compromising your security. For more advanced functionality, the ability to push patches, HFNetChkPRO at www.shavlik.com

As far as applying the service packs and hotfixes, Microsoft has not made this process simple or straightforward for all large enterprises. Besides applying the fixes to all instances (or at least making the default), the process is still largely manual. You can automate this using your own enterprise management tools (such as SMS or Tivoli) or by using one of a myriad of third-party tools, such as HFNetChkPRO (www.shavlik.com), Service Pack Manager 2000 (www.securitybastion.com), or UpdateExpert (www.updateexpert.com).

## Implementing Change Control

This is a very important method to make a secured systems stay secure. Imagine you've spent hours setting up a server to be totally secure and distributed this update to a hundred servers. If just one person on those
