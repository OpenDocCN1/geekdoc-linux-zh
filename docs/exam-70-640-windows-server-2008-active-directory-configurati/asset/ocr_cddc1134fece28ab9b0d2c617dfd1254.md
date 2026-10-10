**B. Select** one of the following backup types and click **Next**. The Confirmation window is displayed, as shown in Figure 11-7.

+   a. **Copy backup.** This backup type will retain the Application log files on the local server. Select this backup type if you will be using a third-party backup tool in addition to Windows Server Backup.
+   b. **VSS full backup.** This backup type will update each file’s backup history and will clear the Application Log files.

+   **Figure 11-7**
+   Confirming backup selections

![](bbox=[0.26, 0.2, 0.69, 0.49])

**9. To begin** the backup process, click **Backup**. The Backup progress window is displayed, as shown in Figure 11-8.

+   **Figure 11-8**
+   Viewing an in-progress backup

![](bbox=[0.26, 0.55, 0.69, 0.84])

**10. When** the backup is complete, click **Close**.

PAUSE. LEAVE the Windows Server Backup window open for the next exercise.

You have just configured a one-time backup of the critical volumes on a Windows Server 2008 domain controller. In the next exercise, you will configure a backup schedule to provide regular backup protection for your domain controller.