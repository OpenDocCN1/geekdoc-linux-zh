
## Process Monitoring with ps

Rather than being an interactive, real-time monitoring program like top, ps works a lot more like ls (hence the name). It's an instantaneous listing of all the processes that are running at the time you execute it. It provides all the information that top does as well as extra details about many of the values.

By default, if you run ps without any arguments, you will get a listing of only the processes owned by you that are attached to terminals (that is, those that have been run from a login session). A large array of command-line options can give you more wide-reaching results, and each can be found documented in man ps. You specify these options as follows:

```bash
# ps -waxu
```

This combination of options shows the following:

-   The output in wide format (w), which allows the output to wrap to multiple lines rather than being cropped to the width of your terminal
-   Usernames along with processes (u)
-   All users' processes, not just your own (a)
-   All processes, regardless of whether they have an associated terminal (x)

In short, this combination of options displays a list of every process on the system, with as much detail as possible.

You can filter the output in certain ways by using the built-in options. For instance, eliminate the x option to show all processes, whether they're attached to a terminal or not, and drop the a option to show only your processes (or use -U to specify another user—for example, -U frank). Many other options of this type can be found in the man page for ps. Beyond the built-in filters, though, you will need to use ps in conjunction with grep (as you saw in Chapter 8, "The FreeBSD Filesystem") to filter based on the process name. An example is shown in Listing 13.2.

### LISTING 13.2 Sample ps Output, Filtered Through grep

```bash
# ps -ax | grep httpd
40563 ?? S 0:54.73 /usr/local/sbin/httpd
40564 ?? S 0:55.30 /usr/local/sbin/httpd
40565 ?? S 0:56.03 /usr/local/sbin/httpd
40566 ?? S 1:00.16 /usr/local/sbin/httpd
40567 ?? S 1:05.13 /usr/local/sbin/httpd
```

## ps Output Explained

Listing 13.3 shows some sample output from ps -waux.

**Listing 13.3 Sample Output from ps**

| USER | PID | %CPU | %MEM | VSZ | RSS | T | STAT | STARTED | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| root | 1 | 0.0 | 0.0 | 528 | 72 | ? ?? | S1s | 31Jan01 | 1:05.94 | /sbin/init -- |
| root | 2 | 0.0 | 0.0 | | | 31Jan01 | 14:41.63 | | (pagedaemon) | |
| root | 3 | 0.0 | 0.0 | | | ? ?? | DL | 31Jan01 | 2:38.47 | (vmademoon) |
| root | 4 | 0.0 | 0.0 | | | ? ?? | DL | 31Jan01 | 0:33.21 | (burfdaemon) |
| root | 5 | 0.0 | 0.0 | | | ? ?? | DL | 31Jan01 | 79:52.61 | (syncer) |
| root | 24 | 0.0 | 0.0 | 208 | 0 | ? ?? | IWs | | 0:00.00 | adjkernztz -i |
| root | 80 | 0.0 | 0.1 | 916 | 320 | ? ?? | Ss | 31Jan01 | 3:27.80 | syslogd -s |

*Note: Some columns in the original OCR were misaligned. The table above attempts to restore logical structure based on standard `ps` output headers. Specific values like VSZ/RSS for kernel threads might be null or different, but I have preserved the text as faithfully as possible while formatting it into a table.*

Processes in the output from ps are sorted by PID rather than any of the reported metrics (unless you used one of the special sorting options described in the man page). You do get most of the same information that top gives you, albeit in a more cryptic format and with a few slight variations.

> **NOTE**
> Output from top differs from ps output in that the %CPU column in ps is not the same as the CPU field in top; it’s actually equivalent to the %CPU field. This value is a "weighted CPU" percentage that takes into account CPU cycles in which the process was in a "resident" state. Most of the time, this weighting makes no difference, but occasionally it can result in a significantly higher number reported in ps than in top or between the two columns in top. In either case, the %CPU column is calculated as an average over the preceding minute, so the values are approximate at best, and you shouldn’t expect them to add up to 100 percent.

## When to Use ps Instead of top

It’s generally more useful to use top to gather metrics on your processes; ps is intended for looking up PIDs of specific processes and seeing the complete command line for each one. It’s quicker than top, and scriptable. For example, you can write scripts that extract the PID for a process from the output of ps and send signals to that PID, all through the use of shell commands and pipes. This is particularly helpful when you need to rein in a runaway process or change the priority on a task. These are functions that we will now review in detail.

## Terminating Misbehaving Processes

Let’s say you notice the system running more slowly than you think it should; you use su to access root, fire up top, and look at the processes. Sure enough, you see something like what’s shown in Listing 13.4.

### LISTING 13.4 Output of top Showing a Possible Runaway Process

```text
last pid: 67469;  load averages:  8.32,  5.49,  2.47  up 53+01:04:22 20:34:42
90 processes:  1 running, 88 sleeping, 1 zombie
CPU states:  93.2% user,  0.0% nice,  0.2% system,  0.8% interrupt,  5.8% idle
Mem: 153M Active, 23M Inact, 60M Wired, 7252K Cache, 35M Buf, 5112K Free
Swap: 500M Total, 44M Used, 456M Free, 8% InUse

  PID USERNAME   PRI NICE SIZE RES STATE C   TIME    PCPU  P CPU COMMAND
19460 frank      2  0    25908K 2816K poll  0  131:15  0.00% 92.43% testprog
67468 root       28 0     2036K 1024K CPU0  0  0:00    0.43% 0.20% top
 245 root       2  0     868K 232K select 1 178:48  0.00% 0.00% healthd
18427 root       2  0     7592K 5124K select 0 81:01   0.00% 0.00% named
```

Aha! There’s your culprit. It seems that frank is running some experimental program that’s perhaps not written very well, and it’s taking up almost all the CPU’s available cycles. Sometimes such a "runaway" process results from an infinite loop (a piece of code that never reaches a point where it can terminate) or a memory leak (the program keeps trying to grab more memory, whether it needs it or not). Chances are, the process isn’t going to exit by itself cleanly; meanwhile, it’s becoming more difficult for other processes to execute and terminate. This testprog process has to go.

### Using the top kill Command

To get rid of testprog or other runaway processes, press the K key. This brings up the “kill” prompt within top; this prompt is an interface to the kill command (or at least a simplified version of the command). At the prompt, enter the PID of the offending process (19460, in this case). Because you’re running with root privileges, the process most likely will immediately terminate, and the system will breathe freely once more. Now, you’re safe to track down what happened; you’ll probably want to start by sending messages to the user and letting him know what his program did.

There are times when the top command doesn’t work, though, or you may need finer control over what signals you’re sending to the processes. The kill command within top is fine for simple process termination, but it’s only a subset of the functionality of the command-line kill program.

### The Command-line kill Program and Its Options

Its name is slightly misleading: kill does a lot more than simply terminate processes. Its full charter is to be a signaling mechanism by which processes can give each other commands of a fairly wide variety. Any user can use kill against any of his processes, but root is the only user who can kill other users’ processes.

The simplest and most common usage of `kill` is for the purpose of terminating a process:

```bash
# kill 12553
```

This, however, sends only a certain kind of signal to the process: the `TERM` signal. This is a universal “quit” message that all Unix programs understand, but it isn’t guaranteed to work. A number of other signals exist, too. Table 13.1 shows the more important ones.

**TABLE 13.1 Commonly Used `kill` Signals**

| Signal | Symbolic Name | Meaning |
| :--- | :--- | :--- |
| 1 | HUP | Hang up, or terminate and restart |
| 2 | INT | Interrupt |
| 3 | QUIT | Quit |
| 6 | ABRT | Abort |
| 9 | KILL | Non-ignorable `kill` |
| 14 | ALRM | Alarm |
| 15 | TERM | Terminate cleanly |

You can use any of these signals by specifying either the signal number or its symbol:

```bash
# kill -9 12553
# kill -HUP 12553
```

The first command sends a low-level “super-`kill`” signal that terminates the process, no matter what. This command makes the process `quit` in an unclean fashion and might leave files open or connections in an orphaned state. Use it only if plain `kill` (or `kill -TERM`) doesn’t work. The second command tells the process to shut itself down cleanly and restart itself with the same arguments—rereading any input files and taking on a new PID. This is useful when you’ve changed something in a program’s config file and need to restart the process to incorporate the changes.

> **NOTE**
> The `kill` program is not infallible; there are some occasions when even a `kill -9` will not terminate a process that has become completely unresponsive to signals. Some processes under certain circumstances can become “zombies,” meaning that they never die and can’t be `killed`. Most zombie processes just sit there and don’t take up any significant system resources. However, if in some rare case you have a zombie process that is interfering with general system operation, a reboot may be the only way to clear it.

These signals are the only ones you’re likely to use in everyday process control. The other signals are typically ignored by programs that aren’t specifically written to respond to them.
