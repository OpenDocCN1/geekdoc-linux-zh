# Chapter 28: Backing Up and Restoring Files

The bottom of the screen in Figure 28-4 displays a hierarchical listing of the files and directories that are contained in the full or incremental backup that you selected. If you selected an incremental backup, the contents of that incremental backup are overlaid the contents of the previous backup full to give you an accurate snapshot of your system when the backup was done. You can drill down into the backup by selecting directories from the tree view, or drill down into individual directories by selecting from the view of the current directory shown at the right of the main window.

To mark files and directories for restoration, select the checkbox beside their names. Once you have selected all of the files and directories that you want to restore, scroll to the bottom of the Restore page and click "Restore files." A page that allows you to specify how you want to restore those files appears, as shown in Figure 28-5.

# Figure 28-5

Specifying the restore method in BackupPC's Web interface

![](bbox=[0.062, 0.396, 0.903, 0.735])

You have three options when restoring files using the BackupPC Web interface:

+   * **Direct restore:** Selecting this option restores files directly to the host from which they were backed up. When doing a direct restore, you have the option of restoring files from the locations from which they were originally backed up, or into a subdirectory that