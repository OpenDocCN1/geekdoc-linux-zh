+   - It creates SHA1 or MD5 signature files for each backed-up file.
+   - It allows encryption of both network traffic and data stored on tape.
+   - It can back up files larger than 2GiB.
+   - It supports tape libraries and autchangers.
+   - It can execute scripts or commands before and after backup jobs.
+   - It centralizes backup management for an entire network.

# The Bacula model

To deploy Bacula, you should understand its major components. Exhibit A illustrates Bacula's general architecture.

# Exhibit A Bacula components and their relationships

![](bbox=[0.22, 0.47, 0.92, 0.68])

The Bacula director is the daemon that coordinates backup, restore, and verification operations. You can submit backup or restore jobs to the director daemon by using the Bacula console. You can also ask the director daemon to query the Bacula storage daemon or the file daemons located on client computers.

You communicate with the director daemon through the Bacula console, which can be run as a GNOME or MS Windows GUI or as a command-line tool. The console can run anywhere; it doesn't have to be located on the same computer as the director daemon.

A storage daemon is the Bacula component that reads and writes tapes or other backup media. This service must run on the machine that is connected to the tape drive or storage device used for backups, but it does not have to be installed on the same server as the director (although it can be).

A Bacula file daemon runs on each system that is to be backed up. File daemon implementations for each supported operating system send the appropriate file data and attributes to the storage daemon as backup jobs are executed.