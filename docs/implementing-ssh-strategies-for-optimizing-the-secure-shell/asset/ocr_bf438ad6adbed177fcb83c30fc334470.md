case, the SFTP access control features of V$Shell should be used. In order to allow access to only the d:\share folder, which can be the root directory on the corporate file server, to all accounts on the system, complete the following steps:

+   1.  Go to **Start Æ Programs Æ V$Shell Æ V$Shell**.
+   2.  Highlight the SFTP section.
+   3.  Under SFTP options, select **Add**.
+   4.  For the SFTP root field, type `d:\share` or **simply browse to it using the ... button**.
+   5.  Type **CorpFileServer** for Alias.
+   6.  Select **Add** on the right hand section.
+   7.  Add the **Everyone** group.
+   8.  Choose **OK**.
+   9.  Select **Apply**.

Now all accounts on the operating system, or the domain, can have SFTP access to the D:\share directory. In order to ensure that access to the rest of the operating system is denied, complete the following steps:

+   1.  Highlight the <Unrestricted> option in the SFTP section and select **Edit**.
+   2.  Remove all accounts, including **Everyone** and any other accounts that exist.
+   3.  Enter any accounts, such as the administrator account, that you would like to provide full SFTP access to the system. If no accounts need to be added, select **OK**.
+   4.  Select **Apply**.

Now no accounts, or only the administrator account, have unrestricted access. Furthermore, every other account on the system or domain only has access to D:\share, despite whatever NTFS permissions that account has. The V$Shell access control lists override the NTFS permissions on the V$Shell server when using SSH or SFTP subsystem. Figures 8.6 and 8.7 show the final result.