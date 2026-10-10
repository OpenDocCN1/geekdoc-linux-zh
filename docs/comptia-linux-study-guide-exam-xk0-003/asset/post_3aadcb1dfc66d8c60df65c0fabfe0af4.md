
## TABLE 3.1 Common ps Options (continued)

| Unix98 Option(s) | BSD Option(s) | GNU Long Option(s) | Description |
| :--- | :--- | :--- | :--- |
| `-u user` | `U user` | `--User user` | You can obtain a list of processes owned by a specified user with this option. The *user* variable may be a username or a user ID (UID) number. |
| `-f, -l` | `j, l, u, v` | | These options display extra information. The details of what is displayed vary with the specific option used. |
| `-H, -f` | | `--forest` | These options group processes and use indentation to show the hierarchy of relationships between processes. They're useful if you're trying to trace the parentage of a process. |
| `-w` | `w` | | The *ps* command output can be more than 80 columns wide. Normally, *ps* truncates its output so that it will fit on your *screen* or *xterm*. The `~w` and *w* options tell *ps* not to do this, which can be useful if you direct the output to a file, as in *ps w > ps.txt*. You can then examine the output file in a text editor that supports wide lines. |

You can combine these *ps* options in many ways to produce the output you want. You'll probably need to experiment to learn which options produce the desired results because each of these options modifies the output in some way. Even those that would seem to influence just the selection of processes to list sometimes modify the information that's provided about each process.

## Interpreting ps Output

Listing 3.1 and Listing 3.2 show a couple of examples of *ps* in action. Listing 3.1 shows the output from typing *ps ~u rodsmith --forest*, and Listing 3.2 shows the output from typing *ps u U rodsmith*.

### Listing 3.1: Output of ps -u rodsmith --forest

```bash
$ ps -u rodsmith --forest
  PID TTY      TIME CMD
2451 pts/3    00:00:00 bash
2551 pts/3    00:00:00 ps
2496 7        00:00:00 kvt
2498 pts/1    00:00:00 bash
2505 pts/1    00:00:00  \_ nedit
2506 ?        00:00:00     \_ csh
2544 ?        00:00:00       \_ eye
19221 ?      00:00:01 dfm
```

### Listing 3.2: Output of ps u U rodsmith

```bash
$ ps u U rodsmith
USER     PID %CPU %MEM   VSZ   RSS TTY      STAT START   TIME COMMAND
rodsmith 19221  0.0   1.5  4484  1984 ?  S May07  0:01 dfm
rodsmith 2451  0.0   0.8  1856 1048 pts/3 S 16:13  0:00 -bash
rodsmith 2496  0.2   3.2  6232 4124 ? S 16:17  0:00 /opt/kd
rodsmith 2498  0.0   0.8  1860 1044 pts/1 S 16:17  0:00 bash
rodsmith 2505  0.1   2.6  4784 3332 pts/1 S 16:17  0:00 nedit
rodsmith 2506  0.0   0.7  2124 1012 ? S 16:17  0:00 /bin/csh
rodsmith 2544  0.0   1.0  2576 1360 ? S 16:17  0:00 eye
rodsmith 2556  0.0   0.7  2588  916 pts/3 R 16:18  0:00 ps u U
```

The output produced by ps normally begins with a heading line, which displays the meaning of each column. Important information that might be displayed (and labeled) includes the following:

- **Username**: The name of the user who runs the programs. Listings 3.1 and 3.2 restricted this output to one user to limit the size of the listings.
- **Process ID**: The process ID (PID) is a number that's associated with the process. This item is particularly important because you need it to modify or kill the process, as described later in this chapter.
- **Parent process ID**: The parent process ID (PPID) identifies the process's parent. (Neither Listing 3.1 nor Listing 3.2 shows the PPID, though.)
- **TTY**: The teletype (TTY) is a code used to identify a terminal. As illustrated by Listings 3.1 and 3.2, not all processes have TTY numbers—X programs and daemons, for instance, do not. Text-mode programs do have these numbers, though, which point to a console, xterm, or remote login session.
- **CPU time**: The TIME and %CPU headings are two measures of CPU time used. The first indicates the total amount of CPU time consumed, and the second represents the percentage of CPU time the process is using when ps executes. Both can help you spot runaway processes—those that are consuming too much CPU time. Unfortunately, just what constitutes “too much” varies from one program to another, so it’s impossible to give a simple rule to help you spot a runaway process.
- **CPU priority**: As described shortly, in “Restricting Processes’ CPU Use,” it’s possible to give different processes different priorities for CPU time. The **NI** column, if present (it’s not in the preceding examples) lists these priority codes. The default value is 0. Positive values represent *reduced* priority, while negative values represent *increased* priority.
- **Memory use**: Various headings indicate memory use—for instance, **RSS** is resident set size (the memory used by the program and its data), and **%MEM** is the percentage of memory the program is using. Some output formats also include a **SHARE** column, which is memory that’s shared with other processes (such as shared libraries). As with CPU use measures, these columns can help point you to the sources of difficulties, but because legitimate program needs of programs vary so much, it’s impossible to give a simple criterion for when a problem exists.
- **Command**: The final column in most listings is the command used to launch the process. This is truncated in Listing 3.2 because this format lists the complete command, but so much other information appears that the complete command won’t usually fit on one line. (This is where the wide-column options can come in handy.)

As you can see, a lot of information can be gleaned from a *ps* listing—or perhaps that should be the plural *listings*, because no one format includes all of the available information. For the most part, the **PID**, **username**, and **command** are the most important pieces of information. In some cases, though, you may need specific other components. If your system’s memory or CPU use has skyrocketed, for instance, you’ll want to pay attention to the memory or CPU use columns.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_152_0.png)

> It’s often necessary to find specific processes. You might want to find the PID associated with a particular command in order to kill it, for instance. This information can be gleaned by piping the ps output through grep, as in
> `ps ax | grep bash` to find all the instances of Bash.

Although you may need a wide screen or xterm to view the output, you may find `ps -A --forest` to be a helpful command in learning about your system. (The ps tree command produces a similar display.) Processes that don’t fall off others were either started directly by init or have had their parents killed, and so they have been “adopted” by init. Most of these processes are fairly important—they’re servers, login tools, and so on. Processes that hang off several others in this tree view, such as eyes and nedit in Listing 3.1, are mostly user programs launched from shells.

## Viewing Processes Dynamically

If you want to know how much CPU time various processes are consuming relative to one another, or if you simply want to quickly discover which processes are consuming the most CPU time, a tool called top is the one for the job. The top tool is a text-mode program, but of course it can be run in an xterm, as shown in Figure 3.2, and there are also GUI variants, like bpm and gnome-system-monitor. By default, top sorts its entries by CPU use, and it updates its display every few seconds. This makes it a very good tool for spotting runaway processes on an otherwise lightly loaded system—those processes almost always appear in the first position or two, and they consume an inordinate amount of CPU time. By looking at Figure 3.2, you might think that mencoder is such a process, but in fact, it’s legitimately consuming a lot of CPU time. You’ll need to be familiar with the purposes and normal habits of programs running on your system in order to make such determinations; the legitimate needs of different programs vary so much that it’s impossible to give a simple rule for judging when a process is consuming too much CPU time.

### **FIGURE 3.2** The top command shows system summary information and information on the most CPU-intensive processes on a computer.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_153_0.png)

Like many Linux commands, top accepts several options. Table 3.2 summarizes the most useful of these options.

### **TABLE 3.2** Common top Options

| Option Name | Meaning |
|---|---|
| -d delay | This option specifies the delay between updates, which is normally 5 seconds. |
| -p pid | If you want to monitor specific processes, you can list them using this option. You’ll need the PIDs, which you can obtain with ps, as described earlier. You can specify up to 20 PIDs by using this option multiple times, once for each PID. |
