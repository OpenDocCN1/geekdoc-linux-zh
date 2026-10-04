# Chapter 5 • Attacking and Defending Windows 2000

# Figure 5.9 A Custom Security Configuration Management Console

![](bbox=[0.198, 0.101, 0.738, 0.413])

# Table 5.3 Default Templates Available for Various Security Levels

| Template | Purpose |
| --- | --- |
| basicdc | Default security settings. Requires environment variables DSDIT DLOG and SYSVOL be set. Must be joined to a domain in order. User Rights|Restricted Groups not included. (Windows 2000 DCs). |
| basicsv | Default security settings. User Rights|Restricted Groups not included. (Windows 2000 Server). |
| basiccwk | Default security settings. User Rights|Restricted Groups not included. (Windows 2000 Professional). |
| compatws | Assumes clean-install NTFS file|registry ACLs. Relaxes ACLs for Users. Empties Power Users group. |
| DC security Default security settings updated for domain controllers Assumes clean-install NTFS file|registry ACLs. Includes SecureDC settings with Windows 2000–only enhancements. Empty Power Users group. |
| hisecws | Increases SecureWS Settings. Restricts User and Terminal Server ACLs. |
| notssid | Removes the Terminal Server Session ID (SID) from Windows 2000 Server. |
| ocfiless | Optional Component File Security. Many of the files may not be installed. (Windows 2000 Server). |

Continued