You can also insert the SMSSTART command in the server's Autoexec.ncf startup file. (See Chapter 2 for a description of using the server startup files.)

+   4. In addition, you should also load the SMDI.NLM module in the Autoexec.ncf startup file by typing LOAD SMDI.NLM and pressing Enter. This command loads the SMS device module interface used to let the SBCON program communicate with the backup device.

+   5. Load the SBCON program on the host server by typing SBCON from the server console and pressing Enter to display the menu shown in Figure 11-25.

![](bbox=[0.12, 0.27, 0.55, 0.41])

+   6. You can use the Job Administration menu item to display the Select Job screen, which you can use to perform backup and restore tasks, as shown in Figure 11-26.

![](bbox=[0.12, 0.48, 0.32, 0.58])

+   7. Select Backup to display the Backup Options screen shown in Figure 11-27. You can use this screen to select the target server to be backed up, the directory or volume to back up, and the device or medium to use.

![](bbox=[0.12, 0.7, 0.55, 0.81])

+   8. Select Advanced Options to select the backup type and time (see Figure 11-28).

+   9. You can use the Backup Type option to select a full, incremental, or differential backup. After making your selection, press Esc to submit the job and then return to the Select Job screen.

+   10. Press Esc again to return to the SBCON main menu. The backup job is then started at the time specified in the Advanced Backup Options screen.