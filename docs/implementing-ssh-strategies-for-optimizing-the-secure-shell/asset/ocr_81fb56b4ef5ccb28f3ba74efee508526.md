# **Using SSH Communications' SSH Server for File Sharing**

As with OpenSSH, with SSH, in order to provide the use of the SFTP subsystem in a complementary fashion to SSH, valid accounts have to be made on the operating system. They need to be made, as SSH Communications' SSH server also uses operating system accounts, not their own specific SSH accounts. That being the case, having an account on the operating system means the account has rights to all files on the operating system that NTFS permissions allow, such as \winnt, \winnt\system32, and \winnt\repair. If the purpose of the SFTP server is for file sharing only, all SSH accounts will still have rights to other parts of the operating system because they are operating-system accounts.

In a file-server situation, you may want users to have access to a root folder for general organization-wide file sharing but not want them to have exposure to the operating system directories or the entire directory architecture for SFTP access. For example, you may want users to be able to download files in a specified directory such as d:\share but not want everyone to be able to download a copy of \winnt\repair\sam. In this case, the use of the SFTP access control features of SSH Communications' SSH server should be used. In order to allow access to only the d:\share folder, which may be the corporate file server, to all accounts on the system, complete the following steps:

+   1. Start \h Programs \h SSH Secure Shell Server \h Configuration.
+   2. Highlight the SFTP Server section.
+   3. Under Accessible directories options, select New (insert) icon.
+   4. Type CorpFileServer=D:\share (syntax is virtual dir=real dir).
+   5. Select Apply.

Now all accounts on the operating system, or the domain, can have SFTP access to the d:\share directory. All accounts will not have access to any other part of the operating system except the virtual directory that is listed. Further- more, in addition to the virtual directories, the users' home directory can also be accessible, listed by the %D variable in the User home directory text box. In this example, the users' home directory is accessible, in addition to the corpo- rate file server directory, as shown in Figure 8.10.