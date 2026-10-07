
- Promote a particular print request to the top of the queue
- Make changes to the `lpd` printer daemon

The `lpc` program can’t be used for remote printers. It affects only those directly attached and configured on the local machine.

> **WARNING**

Be warned that `lpc` is one of the most unpredictable and unreliable programs included with the Linux operating system! It can hang up for no obvious reason, and it can also display erroneous status messages. In some cases, the only way to fix a severely screwed-up printer system is to reset the machine completely!

When used without any arguments, `lpc` prompts you for a command. The following are several valid `lpc` commands and their arguments (a vertical bar indicates a choice of arguments):

- `abort` *`printer_name`* `|` `all`: This is similar to the `stop` command except it doesn’t allow any print job that is currently being printed to finish before stopping the printer. When used with the `all` argument, all printers are stopped. Any job that is abnormally terminated by the `abort` command is requeued when the printer is started again. See the `stop` command for more details about the printer daemon and lock files.
- `clean` *`printer_name`* `|` `all`: This removes all print jobs that are queued, including any active print jobs. In many cases, the currently printing job proceeds normally because it has been passed to the printer daemon or the printer’s buffer. All other jobs are removed, though. If the `all` argument is used, all printers have their print queues cleaned.
- `disable` *`printer_name`* `|` `all`: This disables the spooling of print requests to the printer (or all printers, depending on the argument). Any jobs that are already queued are unaffected. Any user trying to send a print job to the disabled printer receives a message indicating that the printer is disabled and the print job is refused. Printers are enabled and disabled through changes in the `lock` file in the spool directory.
- `down` *`printer_name`* `message`: This is used to take a printer completely offline, usually for an extended period. If a message is included, it can be as long as you want. It is placed in the status file in the spool directory and displayed to users trying to queue to the printer. The down command is usually used when a printer has serious problems and must be removed from the system for more than a day.
- `enable` `printer_name` `|` `all`: This enables the spooling of print requests to the printer or all printers.
- `exit`: This exits from `lpc` (the same as `quit`).
- `help` or `?`: This shows a short list of all `lpc` commands. If an argument is supplied, it displays a one-line description of that command (such as `help abort`).
- `quit`: This exits from `lpc` (the same as `exit`).
- `restart` `printer_name` `|` `all`: This restarts the printer daemon and is usually used after the printer daemon has died for an inexplicable reason (which the BSD printer daemons tend to do). If the argument `all` is supplied, all printer daemons are restarted.
- `start` `printer_name`: This starts the printer, allowing it to print requests. This command starts the printer queue daemon for that printer.
- `status` `printer_name`: This displays the printer name, whether it has the spool queue enabled, whether printing is enabled, the number of entries in the print queue, and the status of the daemon for that printer. If there are no entries in the queue, no printer daemon will be active. However, if there are entries in the queue and the printer daemon shows as no daemon present, the daemon has died and must be started again with the `restart` command.
- `stop` `printer_name`: This stops the printer. Print requests can still be spooled, but they are not printed until the printer is started. If a job is being printed when the `stop` command is issued, the job completes the print process and then stops printing. The `start` and `stop` commands alter the contents of the `lock` file in the print spool directories. The `stop` command also kills the daemon for spooling to that printer.
- `topq` `printer_name` `print_ID`: This moves the print request with `print_ID` to the top of the print queue.
- `topq` `printer_name` `username`: This moves all print requests owned by `username` to the top of the queue. (This is very handy for system administrators who don't want to wait!)
- `up` `printer_name`: This is used to reactivate a printer that was taken down. See the `down` command for more information.

The `lpc` utility isn't very user-friendly, but it's the only way to handle printers and their queues in Linux. Several front-end menu-driven utilities are beginning to appear that simplify this task.

## Managing the Printer Queue with lpq and lprm

Several commands help you administer the printer queue specifically, instead of relying on the `lpc` command. Two tasks are commonly required by a system administrator: displaying the current queue and removing print jobs in a queue.

To display the current print queue for any printer, use the `lpq` command. It has the following syntax:

```
lpq [ -l ] [ -P printer_name ] [ job_ID . . . ] [ username . . . ]
```

With no arguments at all, `lpq` displays information about the current printer queues. The `lpq` command normally displays information about who queued the print job, where it is in the queue, the files being printed, and the total size of the files. The `-l` option displays more information about each entry in the printer queue. Usually, only one line of information is displayed.

A specific printer can be displayed with the `-P` option, followed by the printer’s name. If no name is supplied, the default system printer is displayed. If one or more `job_IDs` or *usernames* is provided, only information about the job or jobs queued by the user is shown.

> **NOTE**

Because users can’t access the Linux printer spooling directories, they can remove queued print jobs only with the `lprm` command. If you are a system administrator, you might want to let all system users know how to use this command to keep unwanted print jobs from printing.

The `lprm` command is used to remove files from a printer queue. This command is often mistyped as `lpr`, which doesn’t remove the file from the queue. To use `lprm`, you must know the print job ID; or, if you are logged in as *root*, you can remove all jobs for a particular printer. The syntax of the `lprm` command is as follows:

```
lprm [ -P printer_name ] [ - ] [ job_ID . . . ] [ username . . . ]
```

If the single-hyphen argument is used, `lprm` removes all jobs owned by the user who issues the command. If you are logged in as *root*, all print jobs are removed. A particular printer’s jobs can be removed by using the `-P` option. For example, the command

```
lprm -Phplj -
```

removes all print jobs queued on the printer `hplj` by the user who issues the command or all print jobs for that printer, if issued by `root`.

> **WARNING**

It is easy to accidentally remove all print jobs for a printer when you use the `lprm` command as `root`. Take care to use the proper syntax, or you may get frustrated at having to requeue all the jobs!

If a print job ID or a username is supplied as an argument, `lprm` removes that job or all jobs submitted by the user. If no arguments are supplied at all, the currently active job submitted by the user is deleted.

When `lprm` removes files from the queue, it echoes a message to the display. If there are no files to remove, nothing is echoed (and you will be left wondering what, if anything, happened).

If you try to use `lprm` on a job that is currently being printed, it might not be terminated properly because the file might already reside in the printer's buffer. In some cases, terminating a job that is currently printing can cause the printer to lock because some output format files can't handle the termination instructions and freeze when the lock file in the spool directory changes. In cases such as this, the `ps` command must be used to find the output filter process ID, and then it must be killed.

> **NOTE**

In cases of printer lockup that don't seem to resolve themselves with the `lpc` utility, try killing the `lpd` daemon and restarting it. If that doesn't work, you will probably have to reboot the entire system.

## Terminals

Most Linux systems use only the system console that came with the PC (the PC's screen and keyboard act as the system console). You won't have to make any configuration changes to Linux to use the system console effectively.

Some system administrators want to add remote terminals to allow other users to work with Linux simultaneously (it is a multiuser system, after all). New terminals can be added to the system in one of two ways: through a serial port on the back of the PC or through a multiport card with many serial ports on it.
