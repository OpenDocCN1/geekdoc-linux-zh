The common SA Shell password on a system allows an attacker to use the XP\_CmdShell extended stored procedure to add a user, and make the user an administrator.

In Windows 2000, the File Copy provides the ability to copy, cut, and paste files to and from a Terminal Server. Windows XP allows the transfer of files within a Remote Desktop Connection via sharing of local drives.

An attacker with control of a Terminal Server can use techniques using the tools PWdump3 and LSADump2 to gain domain access.

# Defending Terminal Services

When not secured properly, the increased functionality of Terminal Services will cause a decrease in overall security for the host operating system. A vulnerability in one will probably lead to a compromise of the other.

Install current patches and secure the operating system. Set strong Windows passwords and use a tool like John the Ripper to test these passwords.

On Windows 2000 Terminal Services, force the setting of High encryption for all sessions.

Set permissions and control Terminal Services settings for local system administrators by implementing Group Policy restrictions at the Domain or OU in Active Directory.

Application Server mode needs to be secured in the same way that you would secure a server that allowed users to log on locally.