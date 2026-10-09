starting and ending time of the prime shift. Subsequent lines indicate the data and description of each holiday scheduled over the year.

+   When manually configuring disk accounting, toggle disk accounting true or false for a filesystem by changing the accounting attribute for that filesystem. Use the chfs command to set the account stanza to true for each file system you intend to monitor. Do not edit the /etc/filesystems file directly.

+   When manually creating accounting files, create the report subdirectories nite, fiscal, and sum with adm ownership in the /var/adm/acct directory, or the /var/adm/pacct data file will remain empty after the accounting system has started.

+   The main command for starting and stopping the accounting system is accton.

+   A startup script is provided to start the accounting system at boot time.

+   The shutacct script is called from the system shutdown script to append shutdown data to /var/adm/wtmp.

+   Stop system accounting manually by using the turnacct or accton command.

+   You can display a general summary of data stored in /var/adm/pacct using the sa command.

+   Display connection histories with the BSD ac and last commands.

+   A standard set of reports is produced at intervals by the runacct and monacct commands. These commands should be run by the adm crontab.

+   The vmstat command reports information about kernel threads, memory, disk I/O, traps, and processor activity.

+   The timee command will display the elapsed, user, and system execution times for a command.

+   The iostat command reports processor statistics and all system input and output device statistics.

+   The sar command also collects CPU statistics from symmetric multiprocessor systems.

+   The default accounting procedures specified in the adm crontab periodically close and rename accounting files to assist in managing data. The systems administrator must implement procedures to archive and clean up the old data files.