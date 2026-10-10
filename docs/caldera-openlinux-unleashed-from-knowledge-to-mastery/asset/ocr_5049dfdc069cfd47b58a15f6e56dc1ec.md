As you can see from this window, you can change various settings such as incremental backups, mount point handling, compression settings, and logging options.
There is one option here that I would recommend always checking, and that is Create On-Tape directory. By selecting this for your backups, they will always contain a table of contents that BRU-PE can use to determine quickly what they contain.
To save your settings for future use, select Save Options from the Options menu.

# ## Running the Backup

After you have selected at least one file or directory for backup, click the **Continue** button. You will then be presented with a couple of dialog boxes for overwriting or appending to tapes and labeling backups.
Then, the *Estimate* window will appear, showing the number of files to be backed up and the size of the backup in kilobytes and approximately how many volumes the backup will take.

> If compression is being used, the volume estimation will not take that into account.

From this point on, the backup can be completed without further intervention, as long as volumes won't have to be changed. Once the estimate is complete, click the **Continue** button to perform the backup. If no selection is made in *30 seconds*, the backup will proceed automatically.

# ## Scheduling Backup Definitions

BRU-PE provides a scheduler for setting up backup definitions to run at future times. The Scheduler interface may be opened through the dialog window that appears after saving a definition or by selecting *Scheduler* from the *File* menu. The Scheduler interface is shown in Figure 23.7.