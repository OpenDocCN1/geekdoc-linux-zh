![](bbox=[0.17, 0.12, 0.84, 0.38])

FIGURE 11-1. The differential incremental backup

# Cumulative Incremental Backup

With a cumulative incremental backup, all of the changes since the last full backup are backed up. Each cumulative incremental backup takes more space than a differential incremental backup, but in the event that a restore is required, only the full backup and the last cumulative incremental backup need be applied. This process is shown in Figure 11-2.

# How to Back Up the Database

There are several different ways that the Oracle database can be backed up. These various methods consist of

+   - Recovery Manager (RMAN)
+   - Automatic disk-based backup and recovery (flash recovery area)
+   - OS facilities
+   - Export and Data Pump
+   - Commercially available backup utilities

Each of these utilities can perform an effective backup. It is usually your own personal preference that can help you decide which one to use.