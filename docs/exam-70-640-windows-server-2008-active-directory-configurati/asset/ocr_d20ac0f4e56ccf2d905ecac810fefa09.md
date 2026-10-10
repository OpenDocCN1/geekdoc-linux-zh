bage collection process. Offline defragmentation is a manual process that requires the server to be restarted in Directory Services Restore mode. The Ntdsutil command-line utility is used to perform the offline defragmentation.

+   - The Active Directory database can be moved to a new location if you decide that there is a need to relocate it due to space limitations. This is accomplished with the Ntdsutil command-line utility.
+   - When you back up Active Directory, you must include the System State data. The System State data includes operating system-specific information needed for installed services and operating system components to function.
+   - In the event of a domain controller failure, two restore options are available in Windows Server 2008: nonauthoritative and authoritative. The nonauthoritative restore method restores the Active Directory database to its state before the backup. After a normal restore, replication of more recent object information from other domain controllers is used to update the database to match all other domain controllers. An authoritative restore uses the Ntdsutil command-line utility and allows you to mark records that supersede any existing records during replication.
+   - Active Directory cannot be restored from a backup that is older than the default tombstone lifetime of 180 days. Domain controllers keep track of deleted objects only for the duration of the tombstone lifetime.
+   - When monitoring the health of Active Directory, you can examine the Directory Service log to obtain information. The Directory Service log is created when Active Directory is installed. By default, it logs informational events, such as service start and stop messages, errors, and warnings. Additional diagnostic logging can be achieved by modifying the registry.
+   - Reliability and Performance Monitor in Windows Server 2008 allows you to collect real-time information on your local computer or from a specific computer to which you have permissions. This information can be viewed in a number of different formats that include charts, graphs, and histograms.
+   - Reliability and Performance Monitor uses performance objects, or categories, and performance counters to organize performance information. Performance counters are the specific processes to monitor. Many counters are available.

# # Knowledge Assessment

+   a. authoritative restore
+   b. checkpoint file
+   c. Directory Services Restore Mode
+   d. fragmentation
+   e. garbage collection
+   f. LDP
+   g. system volume
+   h. tombstone
+   i. transaction buffer
+   j. Windows PowerShell

1. This object is created when an object is deleted within Active Directory.
2. Active Directory changes are written here before they are committed to disk.
3. This is a new advanced command-line and scripting interface included in Windows Server 2008.
4. This volume houses the boot files for a Windows Server 2008 computer.
5. This describes the process of removing tombstoned objects from the NTDS.DIT file.