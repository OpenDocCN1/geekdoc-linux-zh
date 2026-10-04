# Attacking and Defending Microsoft Terminal Services • Chapter 9

# File Security

Without NTFS, you don't have permissions or the ability to audit file accesses. Use them and use them. They can be the last line of defense when a user is trying to do or see something they are not supposed to. For a more secure solution, separate the %systemroot% and required applications in different volumes. This will allow for easier securing of the file system. Be sure to verify permissions required for your Terminal Server. The first step is to remove all but SYSTEM and Administrators rights to c:\ and its subdirectories and then add the permissions back as needed to achieve functionality. Some areas that require read and execute permissions are Windows system folder and Program Files (including subdirectories). Modify access is required for some applications as well as needed for Documents and Settings folders.

# Disallow User Access to Shared Clipboard

I recommend that you limit the ability to use the Shared Clipboard feature to administrative accounts only. You can disable it via the TS Configuration Manager and remove virtual channels for users to restrict this functionality. I recommend that you add an Access Control Entry (ACE) that explicitly denies Everyone from Virtual Channels if this is a big concern to you.

# Disallow Remote Control

Terminal Server features a Remote Control option to view or control other users sessions. Terminal Server privileged users should not have access to this functionality. This access is controlled via the RDP-Tcp properties and should be disallowed for nonadministrators.

# Specify an Initial Starting Program

The RDP-Tcp properties can be set to automatically open a specified application when a user connects. The TS session will be restricted to only that application and will close if the user closes the application. The caveat is if the user can “break out” of the application session will remain. Details on these techniques are listed in the “Attacking Terminal Servers” section of this chapter.

# Restrict Application Usage

AppSec.exe is available in the Windows 2000 Resource Kit and can be used to specify what applications can be run in a TS session or which ones can not

![](bbox=[0.712, 0.943, 0.928, 0.966])