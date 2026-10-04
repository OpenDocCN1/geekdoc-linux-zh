Attacking and Defending Microsoft SQL Server • Chapter 12

# Dropping Dangerous Extended Stored Procedures

Extended stored procedures (XPs), which are implemented as DLLs that are loaded into the SQL Server's process space, provide extra functionality but can also be a security liability. The xp_cmdshell XP, for example, can be a great convenience to the DBA who needs to run an OS command or copy some files, but it can also be a boon for an attacker to gain access to the operating system. It is no problem to drop any XPs that you fear be abused but keep in mind that a person with system administrator privileges can add the XP back as long as the DLL still exists. This might lead you to believe that you should delete the DLL as well, but the problem with that solution is that one DLL usually services all XPs so you may end up removing more XPs than you had intended if you remove the DLL. The primary reason for dropping extended stored procedures is to thwart unanticipated attackers and worms. Refer Table 12.6 for a listing of XPs to consider dropping. Please be sure to thoroughly test, because some of these will retain functionality (such as the ability to run Enterprise Manager).

# Table 12.6 Extended Stored Procedures to Consider for Removal

| sp_bindsession | xp_dirtree | xp_perfsample |
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

Continuednwww.synergy.com