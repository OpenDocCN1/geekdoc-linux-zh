![](bbox=[0.13, 0.08, 0.6, 0.35])

**Figure 8.10** SFTP virtual directory.

Now all accounts only have access to d:\share using SFTP, despite their NTFS permissions. The SSH Communications' SSH server access control lists override the NTFS permissions on the SSH server when using SSH or SFTP subsystem. In addition to general user access, you may want to allow the administrator account, or equivalent power users, more access via SFTP. In order to provide power users with more access, while still restricting general SFTP users to the stated virtual directory, complete the following steps:

+   1. Highlight the Power Users section under SFTP server.
+   2. Select the Insert icon to add directories.
+   3. Type C:=C: and D:=D:
+   4. Select Apply.
+   5. In the Power Users textbox, type administrator (or any other account you wish to grant further access).
+   6. Select Apply.

Now the administrator account has full SFTP access to the SSH server, while general users are still restricted to the d:\share directory, as shown in Figure 8.11.