information about this group.Windows 2000 also has a number of groups that are not detailed, but rather are present and utilized on actions being performed. For instance, the Interactive group contains users who are allowed to log locally on a machine. The Network group contains users who are allowed to connect from the Network. Membership in these groups is not assigned, but rather occurs during operation of the machine and network operations.

# Damage & Defense...

# What about the “Everyone” Group?

Those who have worked previously with Windows NT–based operating systems will recall that by default, the root of each drive contains a DACL that allows the Everyone group full control access to all files and folders. What's the problem with that? In this configuration, “Everyone” means just that, and includes anyone accessing the machine from anywhere, including anonymous FTP or Web access accounts. Obviously, this isn't acceptable if you want to control access under the concept of “least privilege,” which is the preferred option when assigning permissions to resources. In a default installation, Windows 2000 continues this default assignment of permissions to the Everyone group. Be sure to eliminate this contention early in your machine setup regimen. See Figure 5.8 for an example of this setting.

Figure 5.8 Default Permissions on the Root of a Drive in Windows 2000

![](bbox=[0.146, 0.643, 0.829, 0.878])