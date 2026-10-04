# Attacking and Defending Windows XP Professional · Chapter 4

# Table 4.4 Local User Rights Assignment

| User Rights Options | Minimum Value | Recommended Value |
| --- | --- | --- |
| Modify firmware environment values | Administrators | Administrators |
| Perform volume maintenance tasks | Administrators | Administrators |
| Profile simple process | Authenticated Users, Administrators | Administrators |
| Profile system performance | Authenticated Users, Administrators | Administrators |
| Remove computer from docking station | Everyone | Everyone |
| Replace a process level token | LOCAL SERVICE, NETWORK SERVICE | LOCAL SERVICE |
| Restore files and directories | Administrators, Authenticated Users | Administrators, Authenticated Users |
| Shut down the system | Everyone | Everyone |
| Synchronize directory data | NONE | NONE |
| Take ownership of files or other objects | Administrators | Administrators |

# Security Options

The Security Options segment of the local security and system configuration is the most comprehensive and the most significant. It ensures proper audit, account, network, domain, device, and system configurations have been implemented. Such configurations detect attacks at system users, remotely accessible Registry keys, and network access. Table 4.5 provides this author's recommendations for properly configuring your security options within your local station.

# Table 4.5 Local Security Options

| Option | Minimum Value | Recommended Value |
| --- | --- | --- |
| Accounts | | |
| Administrator account status | Enabled | Enabled |
| Guest account status | Disabled | Disabled |

www.synergy.com