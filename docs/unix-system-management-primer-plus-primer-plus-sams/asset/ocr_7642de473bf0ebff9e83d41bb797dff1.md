# Chapter 7 PATCHES, UPGRADES, AND DECOMMISSIONS

# Check Hardware Before Applying Patches

If critical hardware like a disk or CPU fails during a patch application, or if the power fails, patch applications could be stopped in their tracks, resulting in partially applied patches and a potentially corrupted system. Verify the condition of your hardware before you apply any patches, in order to prevent this system from happening to your servers.

If you suffer a patch application failure, first examine any error messages the system displays, and fix the problems associated with those errors if you can. Some common errors that occur during patch applications and their remedies are listed here:

+   **Inadequate space on a file system** Remove unnecessary files from the file system and reapply the patch.

+   **A file that needs to be replaced is locked** Find the process that owns the lock and kill it; you can then re the patch. You can use the fuser command on both Solaris and Red Hat Linux to determine which processes are opening a particular file.

+   **The software you are installing is not on your system** This is common when you are installing an entire collection of patches at once—you can ignore this error message.

+   **A file is missing that needs to be patched** Reinstall the software that you are patching and then reapply the patch.

# Solaris and RPM Calculate Space Requirements for You

The patching mechanisms on both Solaris and Red Hat Linux (RPM and patchchadd, respectively) verify that you have sufficient disk space before making any changes to your system. This precaution minimizes that you will apply only part of a patch due to space constraints.

If the patching process continues to fail, contact vendor support to see if the vendor can help you work through the problem with the system designed.

When all fails, you must reload the system with a fresh copy of the operating system and add the patch to the fresh copy. Reloading the OS takes all of time and carries the risk of data loss, so make sure you've exhausted all the other options before considering reloading.

Before reloading any system whose stability is questionable, make sure you perform the following tasks to help preserve data and minimize downtime:

+   **Back up any important data files stored on local disk.** If your backup software is not functional, copy files over the network to another machine (see Chapter 12, “Process Automation,” for instructions on how to do this), or attach a tape drive to copy the files directly to tape.

+   **Back up configuration files, especially in /etc and any application-specific directories.** Even if you don't need most of them, it is best to back up everything in case you get about about a particular configuration.