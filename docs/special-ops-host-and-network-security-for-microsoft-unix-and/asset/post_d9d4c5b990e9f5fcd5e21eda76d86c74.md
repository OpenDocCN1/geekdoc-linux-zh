
# Attacking and Defending Microsoft Terminal Services • Chapter 9

I have read articles about using Stunnel (www.stunnel.org) and IPSec tunnels to perform similar extraordinary measures, but I feel it is overkill for most situations. You should calculate your risk for a particular network, host, or data, decide what fits your needs.

## Remote Administration Mode Specific Defenses

If you are using the Terminal Server for remote administration, the biggest thing to worry about is limiting who has access to connect; do not give permissions to administrators that do not require access and be the ones that have strong passwords. The easiest way to do this is by creating a Global Terminal Server group and making them local administrators on the Terminal Server.

## Rename the Administrator (RID=500)

Rename the Administrator (RID=500) and create a new administrator with a strong password and no privileges. Watch your logs to see if this user attempts to log on. If you see failed logins, investigate further. Don't forget to remove the description, otherwise an attacker can easily figure out that you renamed the account.

## Remote Administration Specific Group Policy Settings

The settings shown in Table 9.1 are what I consider the most relevant for securing your Terminal Server.

**Table 9.1** Remote Administration–Specific Group Policy Settings

| Setting | Recommended Value | Justification |
|---|---|---|
| Do not allow administrators to customize permissions | Enabled | If you have problems with Administrators changing your security settings, applying this to your TS organizational unit. If you apply it locally, another administrator may just change the value |
| Sets rules for remote control of Terminal user sessions | Enabled | If enabled, this will override the user settings as well as the Terminal Services Configuration (TSC) tool settings. This is useful if you have Continued |
| Disable TSInternetUser and Remove Licensing Service | [No value provided in cell] | problems with local administrators changing these settings on the Terminal Server. If you select anything other than enable, the permission will be based on the TSC tool setting and the user setting. The TSC takes precedence out of the two. |

## Application Server Mode Specific Defenses

You can disable the TSInternetUser account when you are using Terminal Server for remote administration. This account allows anonymous access if Terminal Services Internet Connector Licensing is enabled. You should also be sure that Internet Connector Licensing is not enabled. To remove account permissions from some objects, Microsoft offers a security template (notsid.inf) in the %SystemRoot%\Security\Templates directory.

Special care needs to be taken in Application Server mode since unprivileged users have the ability to run code in the processor of the server. This is because most attacks against a Terminal Services application will be privilege escalation attacks. When allowing unprivileged users to connect to TS, precautions such as file and directory access control and auditing need to be carefully considered. Application mode also has the additional overhead of maintaining Terminal Server Licensing Servers to do out application licenses to each console user.

Application Server mode needs to be secured in the same way that you would secure a server that allowed users to log locally. Review Chapter 4 and Chapter 5 for these critical OS-specific tasks. Another option is the use of OUs to reduce the impact of an administrative level compromise; please review Chapter 6 for information on creating and using OUs in Active Directory.

# Attacking and Defending Microsoft Terminal Services • Chapter 9

## File Security

Without NTFS, you don't have permissions or the ability to audit file accesses. Use them and use them. They can be the last line of defense when a user is trying to do or see something they are not supposed to. For a more secure solution, separate the %systemroot% and required applications in different volumes. This will allow for easier securing of the file system. Be sure to verify permissions required for your Terminal Server. The first step is to remove all but SYSTEM and Administrators rights to c:\ and its subdirectories and then add the permissions back as needed to achieve functionality. Some areas that require read and execute permissions are Windows system folder and Program Files (including subdirectories). Modify access is required for some applications as well as needed for Documents and Settings folders.

## Disallow User Access to Shared Clipboard

I recommend that you limit the ability to use the Shared Clipboard feature to administrative accounts only. You can disable it via the TS Configuration Manager and remove virtual channels for users to restrict this functionality. I recommend that you add an Access Control Entry (ACE) that explicitly denies Everyone from Virtual Channels if this is a big concern to you.

## Disallow Remote Control

Terminal Server features a Remote Control option to view or control other users sessions. Terminal Server privileged users should not have access to this functionality. This access is controlled via the RDP-Tcp properties and should be disallowed for nonadministrators.

## Specify an Initial Starting Program

The RDP-Tcp properties can be set to automatically open a specified application when a user connects. The TS session will be restricted to only that application and will close if the user closes the application. The caveat is if the user can “break out” of the application session will remain. Details on these techniques are listed in the “Attacking Terminal Servers” section of this chapter.

## Restrict Application Usage

AppSec.exe is available in the Windows 2000 Resource Kit and can be used to specify what applications can be run in a TS session or which ones can not run. Only applications that are required by the TS users should be given access.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_523_0.png)

# Chapter 9 • Attacking and Defending Microsoft Terminal Services

## Limit and Log Access from Older Clients

TSVer.exe is in the Windows 2000 Resource Kit and can be used to restrict older versions of Terminal clients from making connections. Additionally, this tool will record an IP as well as a hostname to the system logs when attempted fail due to older versions. TSVer should be used to force users to use the current RDC client due to 128-bit encryption requirements.

## Case Study: Attacking Terminal Server

In this brief case study, I detail each successful step of my internal attack chronology from CorpLAN to FinanceLAN using Terminal Server as an integral part of the attack. The goal was to compromise the production MSSQL database in the FinanceLAN.

My first step was to attempt to enumerate the hosts in the FinanceLAN domain using the net view /domain:FinanceLAN command. I was unable to see any hosts because there was a screening router in the way. So my other option was to attack the CorpLAN to find a server that would allow me to jump into the FinanceLAN.

Using the HSVAdmin.bat script, I was able to discover 24 out of 252 hosts with blank administrator passwords in the CorpLAN domain. Using these credentials, I was able to execute commands interactively on these hosts using a tool called psexec.exe (www.internals.com/ntw2k/freeview/pstools.html).

```
NET USE \VICTIME\admin$ "" /u:VICTIME\administrator
Psexec cmd exe
```

This interactive access allowed me to enumerate and the hosts in the FinanceLAN domain using net view /domain. Next, I used a tool (sqllhf.exe) that checked for blank SA (database administrator) passwords and found a host that contained a blank SA password. Using the xp_cmdshell stored procedure, I was able to execute commands on the server and add myself as an administrator. I connected to the Terminal Server with my new account and began to pillage the server for data to further my attack.
