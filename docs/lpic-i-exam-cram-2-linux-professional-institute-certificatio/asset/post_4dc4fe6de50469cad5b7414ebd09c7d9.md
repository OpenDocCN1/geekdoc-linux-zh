
Queue: no printable jobs in queue
Status: job 'root@localhost*387' error 'aborting operations'
at 15:18:58.000

If you use the `-a11` option, the returned messages are more verbose, separating the information returned to a series of lines with one status message on each line.

![](img/49f4f38f3aec011238fa50f89e643db3_437_0.png)

lprm often appears in simple questions that test your knowledge of its existence. The -P, -a, and -all options might appear, too.

## Removing Print Jobs with lprm

The lprm command is used to remove, or dequeue, print jobs from any of the print queues.

Requests to remove print jobs with the lprm command take the following form:

```
lprm -option value keyword
```

![](img/49f4f38f3aec011238fa50f89e643db3_437_1.png)

Most lprm removal commands use the job ID of * or all, which means to act upon all jobs that can be removed by the user executing the command.

## lprm Command Options

lprm differs from the other lp commands in certain ways. If you have two queues that have print jobs in both queues, running the lprm command acts on the default queue's first job and removes it.

lprm offers a number of options with which to remove print jobs:

- `-a`—Removes all files from any and all spools that are modifiable by the user (can be used with the all keyword to specify all jobs in all queues).
- `-P`—Used for specifying a printer, this must be followed by a printer specifier, which is usually a name such as nplaser.
- `-U`—Used to remove a job with a specific user ID.
- `-0`—Contains debugging options.
- `-v`—Provides print version information.

Print jobs are often removed by job IDs but can be specified by the following types of information:

- `all`—This keyword affects all jobs in the default queue.
- `ID`—A number representing the print job ID, or several IDs separated by spaces.
- `User ID`—A user’s ID, such as rbrunson.
- `*`—Like all the others, it affects all jobs in the queue.

## Examples of Using lprm

To remove just the first listed print job in the default queue, use `lprm` by itself:

`lprm`

To remove just job 33 from the default queue, use this command:

`lprm 33`

To remove jobs 33 and 144 from the default queue, use the following command:

`lprm 33 144`

To remove just the first job from all queues, use

`lprm -a`

To remove all the jobs from the default queue, use

`lprm all`

To remove all jobs from all queues, use the command shown here:

`lprm -a all`

![](img/49f4f38f3aec011238fa50f89e643db3_438_0.png)

> The exam will test your knowledge of which options and specifiers are used to remove certain types of jobs, such as -a, all, and possibly a combination of the two.

## Monitoring Print Jobs with lpc

The `lpc` command is used to configure and control `lprd`, its child printers, their configuration settings, and the state of operations.

lpc is quite different from the rest of the lp commands. It can be used either in command-line or interactive (like ftp's interface) mode.

The lpc command syntax is as follows:

```
lpc -option value
```

## lpc Command-Line Options

The options used with lpc can be only on the command line; otherwise, you can use some of the options along with the internal commands while in the lpc interface. Options for lpc include

- `-a`—An alias that stands for -P all or that affects all queues.
- `-P`—If followed by a printer name or all, this affects the specified printers. If no specifier is set, it affects the default queue.
- `-s`—Followed by either the name or IP of the server the desired printer is on.
- `-v`—Shows version information about lpc.
- `-U`—Followed by the username to perform the actions as.
- `-D`—Followed by debugging options.

## Internal lpc Options

The lpc interface is similar to the ftp commands. Here you simply execute the lpc command and then are put into an interface where options and configuration settings are specified.

The lpc command and options are entered in two ways. They can be entered on the command line, like so:

```
lpc status all
```

This yields the following output:

```
Printer Printing Spooling Jobs Server Subserver Redirect Status/(Debug)
hp145er@localhost    enabled enabled    0    none     none
brother@localhost    enabled enabled    0    none     none
```

Or they are entered in the interface, like so:

```
lpc>status all
```

This yields the following output:

```
Printer Printing Spooling Jobs Server Subserver Redirect Status / (Debug)  
  hp laser @ localhost enabled enabled $ none none  
  brother @ localhost enabled enabled $ none none
```

lpc has a lot of internal options, some of which are used on the command line and are covered in the examples section. We'll not cover all lpc options because there isn't room and most aren't on the exam. Instead we'll cover the options most likely to appear on the exam.

Internal options for lpc include

- `?`- Shows help for the lpc interface.
- `defaultq`- Shows the default queue.
- `defaults`- Shows the configuration defaults for all parameters.
- `disable`- Disables printing to the print queue(s) you specify. (This does not delete the printer; it still exists but just does not print.)
- `enable`- This enables printing to the printer again.
- `exit` or `quit`- Quits the interface.
- `hold`- Causes jobs to be held when submitted, and they must be released to print with the release command. It's used with a job ID, such as hold 25.
- `kill`- This is usually followed by a printer name or the keyword all. This kills the printer daemon that governs the printer(s) specified.
- `client`- Shows the local machine's printcap file and configuration information for troubleshooting help.
- `move`- This allows a job to be moved from queue to queue, which is useful when a printer dies or someone wraps copier labels around the corona wire.
- `redirect`- Sends jobs that were submitted to a printer to another printer; it's essentially print job forwarding.
- `start`- Starts the printer and is followed by either a printer name or all.
- `status`- Prints the status for the printer or all printers, with one line of output per printer.
- `topq`- This is a very useful command and is followed by the printer name and the job ID. It moves that print job to the top of the print queue, causing it to be printed next.
- `up`- Followed by a printer name or all, this command brings up all printers and makes them available for printing.

## Examples of Using lpc

There are two methods of using lpc—interactive (with the interface and lpc> prompt) and noninteractive (where you type the lpc option parameter and press Enter to execute).

To use lpc interactively, just enter

`lpc`

You are presented with the following prompt:

`lpc>`

To use lpc noninteractively, you enter the command, with any options, as shown here:

`lpc status all`

This returns output similar to

```
Printer Printing Spooling Jobs Subserver Redirect Status/(Debug)
hplaser@localhost   enabled enabled  0   none   none
brother@localhost   enabled enabled  0   none   none
```

To bring up all the printers, use the following command:

`lpc up all`

This returns output similar to what is shown here:

```
Printer:  hplaser@localhost
service process PID 24938 exited
hplaser@localhost.localdomain: enabled and started
Printer: brother@localhost
service process PID 24947 exited
brother@localhost.localdomain: enabled and started
```

To bring a print job to the top of the queue, you should view the print jobs first with

`lpc`

This returns output that contains the print job IDs:

```
Printer: hplaser@localhost
Queue: 4 printable jobs
Server: pid 2795 active
Unspooler: pid 2796 active
Status: waiting for subserver to exit at 09:02:17.548
```

| Rank | Owner/ID | Class Job Files | Size | Time |
| :--- | :--- | :--- | :--- | :--- |
| 1 | active root@localhost+794 | A 794 /etc/printcap | 997 | 09:02:15 |
| 2 | root@localhost+811 | A 811 /etc/printcap | 997 | 09:02:16 |
| 3 | root@localhost+813 | A 813 /etc/printcap | 997 | 09:02:17 |
| 4 | root@localhost+815 | A 815 /etc/printcap | 997 | 09:02:17 |
