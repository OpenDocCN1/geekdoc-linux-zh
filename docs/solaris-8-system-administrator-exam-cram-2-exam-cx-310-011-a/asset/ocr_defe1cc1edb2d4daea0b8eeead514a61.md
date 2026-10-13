# # Changing the System Run Level

Occasionally, you’ll need to change the system run level—for example, when you shut down the system to add or remove hardware, perform backups, prepare for an expected power outage, or prepare to physically move the system to another location. Table 4.6 lists the commands you use to change the system run level from the command line.

**Table 4.6 — Commands Used to Change the System Run Level**

| Command | Path | Run Level(s) | Description |
|---|---|---|---|
| `halt` | `/usr/sbin` | `0` | Stops the processor(s) |
| `init` | `/sbin` | `0, 1, 2, 3, 4, 5, 6, s` | Processes control initialization |
| `poweroff` | `/usr/sbin` | `5` | Stops the processor(s) and powers off the system (if possible) |
| `reboot` | `/usr/sbin` | `6` | Reboots the system |
| `shutdown` | `/etc` | `0, 1, 5, 6, s` | Used for compatibility (symbolically linked to /usr/sbin/shutdown) |
| `shutdown` | `/usr/sbin` | `0, 1, 5, 6, s` | Changes the system run level |
| `telinit` | `/etc` | `0, 1, 2, 3, 4, 5, 6, s` | Used for compatibility (symbolically linked to /usr/sbin/init) |
| `uadmin` | `/sbin` | `0, 5, 6` | Used for administrative control |

The halt(1M) command normally logs the shutdown to the system log, writes a shutdown record to the system accounting file, performs a call to the sync(1M) command to write any pending information to the disks, and halts the processor(s). You can prevent system and account logging, along with disk syncing, by using command-line arguments. The halt command changes to run level 0 but does not execute the rc scripts associated with run level 0 as the shutdown(1M) and init(1M) commands do.

You can use the init(1M) and telinit(1M) commands to change to any of the eight run levels. The commands identified in the /etc/inittab file for each run level are executed, and any running process not in /etc/inittab is sent a SIGTERM signal or possibly a SIGKILL signal (see Chapter 7, “Controlling Processes”) to cause it to terminate. For each run level, an entry in /etc/inittab runs the appropriate rc scripts to start and stop processes.