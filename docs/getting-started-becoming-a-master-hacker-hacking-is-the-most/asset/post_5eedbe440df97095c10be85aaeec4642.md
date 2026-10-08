
command known as `clearev`. This command clears the event logs in Windows systems.

`metpreter > clearev`

In some cases, you may not be able to get a metpreter on the target system, or the `clearev` command won’t work. In those cases, you can use the `wevtutil` utility in Windows. If you are using the metpreter, you will first need to drop into a command shell (cmd) on the target Windows system (if you do not have a metpreter but rather just a standard Windows command prompt, you can skip this step).

You can do this by simply entering `shell` at the metpreter prompt.

`metpreter> shell`

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_478_0.png)

```
C:\Users\OTW\Desktop>wevtutil
wevtutil
Command is not specified.
Windows Events Command Line Utility.

Enables you to retrieve information about event logs and publishers, install
and uninstall event manifests, run queries, and export, archive, and clear logs.

Usage:

You can use either the short (for example, ep /uni) or long (for example,
enum-publishers /unicode) version of the command and option names. Commands,
options and option values are not case-sensitive.

Variables are noted in all upper-case.

wevtutil COMMAND [ARGUMENT [ARGUMENT] ...] [/OPTION:VALUE [/OPTION:VALUE] ...]

Commands:

ei  | enum-logs         List log names.
gl  | get-log           Get log configuration information.
sl  | set-log           Modify configuration of a log.
ep  | enum-publishers   List event publishers.
gp  | get-publisher     Get publisher configuration information.
im  | install-manifest  Install event publishers and logs from manifest.
um  | uninstall-manifest Uninstall event publishers and logs from manifest.
qe  | query-events      Query events from a log or log file.
gli | get-log-info      Get log status information.
epl | export-log        Export a log.
at  | archive-log       Archive an exported log.
cl  | clear-log         Clear a log.

Common options:

/r | remote):VALUE
If specified, run the command on a remote computer. VALUE is the remote computer
name. Options /im and /um do not support remote operations.
```

```
C:\Users\OTW\Desktop>wevtutil cl security
wevtutil cl security

C:\Users\OTW\Desktop>
```

Windows has a little-known utility named the Windows Event Utility, or `wevtutil` for short. You can access it from the command line. To be able to clear event logs, you will need system admin privileges.

Let’s begin by simply running the `wevtutil` to get a help screen.

`C:\Windows\System32> wevtutil` As you can see, this utility has a number of options, but to clear logs we simply need to run the `wevtutil`, followed by `cl` (clear), and then the event log category we want to delete. So, if we wanted to clear the “security” logs, we would simply enter: `C:\Windows\System32>wevtutil cl security` This command prompt will echo back your command and then return you a new command prompt. To check to see whether anything happened, you can go to the Windows GUI and open the “Computer Management” console.

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_480_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_481_0.png)

There, you can click on Windows logs and then click on Security. As you can see, all the logs were cleared in the Security logs directory!

## Timestomp

In some cases, your post-exploitation activities may include accessing or altering documents, reading emails, and other file access. In all of these cases, you will leave evidence behind for a skilled investigator. Every operating system and file system timestamps files. These timestamps include the last Modify, Access, and Creation (MAC) dates and times. They are a staple of the forensic investigator looking for evidence of compromise and recreating a timeline of events.

- **M** Modify
- **A** Accessed
- **C** Created

These timestamps can be evidence of accessing and alteration of files. A thorough and skilled forensic investigator can use these timestamps to recreate the events on the system, including any alteration of files. To cover your tracks, you will need to alter these timestamps if you have “touched” any files.

Luckily, altering timestamps is not difficult to do. If you plan to access or alter any files, first record the original timestamps. Once you have accessed or altered the file, you can then use a utility within your meterpreter to return the timestamps to their original status. It’s called `timestomp` (note that it is the same as timestamp but with an “o”). To understand how it works, enter `timestomp` with the help option.

```
meterpreter > timestomp help
```

```
meterpreter > timestomp help

Usage: timestomp <file(s)> OPTIONS

OPTIONS:
        -a <opt>  Set the "last accessed" time of the file
        -b        Set the MACE timestamps so that EnCase shows blanks
        -c <opt>  Set the "creation" time of the file
        -e <opt>  Set the "mft entry modified" time of the file
        -f <opt>  Set the MACE of attributes equal to the supplied file
        -h        Help banner
        -m <opt>  Set the "last written" time of the file
        -r        Set the MACE timestamps recursively on a directory
        -v        Display the UTC MACE values of the file
        -z <opt>  Set all four attributes (MACE) of the file
meterpreter >
```

```
meterpreter > timestomp malwarevnc.exe -z "06/25/2015 09:25:03"
[*] Setting specific MACE attributes on malwarevnc.exe
meterpreter > timestomp malwarevnc.exe -v
[*] Showing MACE attributes for malwarevnc.exe
Modified : 2015-06-25 10:25:03 -0600
Accessed : 2015-06-25 10:25:03 -0600
Created : 2015-06-25 10:25:03 -0600
Entry Modified: 2015-06-25 10:25:03 -0600
meterpreter >
```

Let’s assume there is a piece of malware on the system named “malwarevnc.” Presumably, this malware is used to give the attacker a VNC GUI on the system. We can change all the timestamps (MAC) by using `timestomp` with the `-z` option followed by the date and time we want “stomped” on the file, such as: `meterpreter> timestomp malwarevnc.exe -z “06/25/2015 09:25:03”`

Note that the date and time must be enclosed in double quotation marks. If we only wanted to change only the M attribute (Modified) we would use the same command but with the `-m` option; if we wanted to change only the A attribute (Accessed) we would use the `-a` option; and if we only wanted to change the C attribute we would use the `-c` option (that’s pretty easy to remember). Often, it would be wiser to change each of these attributes separately, thereby avoiding any red flags to investigators. These files seldom have the same timestamps in the wild.

## Covering Your Tracks on Linux Systems

Covering your tracks on Linux systems is a bit more complex as Linux systems place their logs in many different places. Each application maintains its own logs, and the kernel and utilities maintain their own separate logs. Most Linux systems have a utility named `rsyslog` to send all the logs to a central server.

To manage your footprint on the target system, you can manipulate this utility to stop logging while you are in the system.

Probably the simplest way to cover your tracks while on a Linux system is to stop the `rsyslog` service.

`systemctl rsyslog stop` This will stop the `rsyslog` service and disable logging to the log server. Of course, this will leave a significant time gap in the logs, but few administrators watch their logs that closely. The last thing before leaving the system would be to restart the `rsyslog` system, making it less obvious that someone has tampered with the logs.

`systemctl rsyslog start`

### Removing Your Command History

Finally, you may want to make certain that your command history is not left behind should your computer fall into your adversary’s hands. In that case, your BASH history can be critical for recreating your actions.

You have at least two strategies here. First, you can keep your system from storing your commands, and the second is to remove the commands from your history.

You can view your history of commands by entering the command `history` at the prompt.

`kali > history`

To turn off your command history, you will need to change the value of your environment variable `$HISTSIZE`. You can do this by setting your `HISTSIZE` variable to zero (no commands stored) and exporting the variable (for more on environment variables in Linux, see *Linux Basics for Hackers*).

`kali > HISTSIZE=0`

`kali > echo $HISTSIZE`

```
root@kali-2019:~# HISTSIZE=0
root@kali-2019:~# echo $HISTSIZE
0
root@kali-2019:~#
```
