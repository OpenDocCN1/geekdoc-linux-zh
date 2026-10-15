
In SUSE Linux 10, a new log file is created each time the current /var/log/messages file reaches 4 MB in size; log files are rotated 99 times before being removed. The logrotate and syslog configuration files can be found in /etc/logrotate.* and /etc/syslog.conf locations.

For more information about logrotate and syslog configuration, refer to the corresponding manual pages.

Fine-tuning syslog and logrotate processes can be necessary to keep the correct number of log files according to your security and audit strategy.

## Centralized remote logging

The final noteworthy feature of syslog is its full remote logging capability; syslogd is able to send messages to a remote host running syslogd and to receive messages from remote hosts. The remote host does not forward the message again, but logs the messages locally.

Using this feature you are able to control all syslog messages on one host, if all other machines log remotely to that. This decreases administration needs.

Refer to the syslogd manual page for more details.

## 8.3.2 Error analysis tools

This section discusses dumps and traces used as error analysis tools.

### Dumps, as an error analysis tool

Sometimes not enough relevant information can be found in the log files. To analyze the reasons one of the Linux guests running in a z/VM partition has a bad behavior, run a dump tool on one of the virtual machines for further analysis. Depending on the environment, several tools can be used:

- DASD dump tool generates a dump on 3390 or 3380 disks.
- SCSI dump tool generates a dump on FCP/SCSI devices.
- Tape dump tool generates a dump on tape.
- VMDUMP creates a dump of a guest virtual memory.

Refer to Table 8-2 on page 373 for a list of the available tools.

| Tool | Stand-alone tools | | | VMDUMP |
| --- | --- | --- | --- | --- |
| | DASD | SCSI | Tape | |
| Environment | VM and LPAR | LPAR only | VM and LPAR | VM only |
| Speed | Fast | Fast | Slow | Medium |
| Medium | ECKD or FBA DASD | Linux file system on a SCSI disk | tape cartridges | VM reader |
| Compression possible | no | yes | yes | no |
| Disruptive | yes | yes | yes | no |

Describing how to use all these tools is beyond the scope of this book. A detailed process for using a dump tool is described in the Linux on System z: Using the Dump Tools, SC33-8412, which you can download from the developerWorks Web site at:

http://www.ibm.com/developerworks/linux/linux390/development_documentation.html#3

### Traces, as an error analysis tool

Another useful way of identifying the failing step in the execution of a program is to trace the program. Linux provides many tools to trace the execution of a program. One tool is called strace.

In the simplest case, strace runs the specified command until it exits. It intercepts and records the system calls which are called by a process and the signals which are received by a process. The name of each system call, its arguments and its return value are printed on standard error or to the file specified with the -o option. The strace tool is useful as a diagnostic, instructional, and debugging tool. System administrators, diagnosticians, and trouble-shooters find it invaluable for solving problems with programs for which the source is not readily available because they do not have to be recompiled to trace them. And programmers find that, because system calls and signals are events that happen at the user/kernel interface, a close examination of this boundary is very useful for bug isolation, sanity-checking, and attempting to capture race conditions.

Example 8-17 on page 374 shows the beginning of the strace output when stracing the ls command. All system calls are detailed, with their parameters and the return codes sent. This can be used to identify which step of a program fails.

### Example 8-17 Using stracing with the ls command

```
lnxguill:/mnt/backup # strace ls
execve("/bin/ls", ["ls"], [* 55 vars *]) = 0
brk(0)                               = 0x80018000
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x2000001f000
uname({sys="Linux", node="lnxguill", ...}) = 0
access("/etc/ld.so.preload", R_OK) = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=33471, ...}) = 0
mmap(NULL, 33471, PROT_READ, MAP_PRIVATE, 3, 0) = 0x200000020000
close(3)                             = 0
open("/lib64/librt.so.1", O_RDONLY) = 3
```

> Note: Working closely with the development team of the application is necessary to analyze the output of the strace program.

This section provided a brief overview of how z/VM and Linux tools handle errors, and detailed several tools that can be used when you analyze why an application causes problems.

Sometimes, an abnormal program termination can lead to data corruption, for example if an application was writing some data to a disk when it crashed. In this case, the only option might be to restore data from an already-existing backup, to return to a state in which the data is consistent. Backup and restore tools are described in the next sections of the chapter.

## 8.4 Backup and restore

Backup refers to making copies of data so that these copies can be used to restore the original after a data loss event. These additional copies are typically called backups and are useful for two primary purposes:

- To restore a state following a disaster (called disaster recovery)
- To restore small numbers of files after they have been accidentally deleted or corrupted

Backups can be classified according to the way they are created:

- Offline backups are disruptive, and require planning.
- Online backups do not interrupt operations.

This chapter introduces tools available for backing up and restoring z/VM and Linux data.
