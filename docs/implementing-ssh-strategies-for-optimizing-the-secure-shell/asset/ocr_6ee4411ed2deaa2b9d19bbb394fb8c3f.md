# Authorizing Users with VShell

Lastly, I will discuss VShell in terms of authorized system users. Typically, VShell installations allow all users on the operating system to log in to the service, which is the default. With VShell, however, specific accounts can be denied SSH/SFTP access, despite their having an account on the system, as shown in the previous example. A specific list of users who have access can include all accounts, which is the default, or a subset of the accounts.

To illustrate, suppose 500 accounts have access to a machine running VShell, possibly by using a domain architecture, but only 72 of those accounts need access to the operating system itself. VShell can allow or deny SSH/SFTP access by specifying account names and/or account variables that are authorized to log in. If the purpose of the SFTP subsystem is to allow all users in the Engineering Department to access, upload, and download files to and from the operating system, adding the group Engineering as the only one that can use SSH or SFTP is a relatively easy process. Furthermore, if the Engineering accounts only need access to the d:\share directory, VShell is a good solution. For example, say the Engineering Department needs to transfer files, such as compiled binaries, source code, or configuration files, to and from the d:\share directory. If they are using SSH for secure terminal access, using SMB or FTP for file transfer would be counterproductive. The security they gain from the encrypted SSH connection is cancelled out by the insecurity of the SMB or FTP sessions.

# SFTP with SSH Communications' SSH Server

SSH Communications' SSH Server is also a great solution when requiring the use of the SFTP subsystem. No additional or extra steps are required to enable the SFTP subsystem on the SSH Communications' SSH server. By default, the SFTP subsystem is enabled. In order to verify that the SSH Communications' SFTP subsystem has been enabled, complete the following steps:

+   1.  Go to Start $\diamond$ Programs $\diamond$ SSH Secure Shell Server $\diamond$ Configuration.
+   2.  Highlight the SFTP server.
+   3.  Ensure the appropriate directories are enabled, such as the users' home directory.
+   4.  Select Apply.

Now that you have ensured that the SFTP subsystem is enabled, consider SSH Communications' SSH server in terms of management, file transfer, and authorized user access.