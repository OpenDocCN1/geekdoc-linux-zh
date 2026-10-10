# Managing Processes

It's often necessary to find specific processes. You might want to find the PID associated with a particular command in order to kill it, for instance. This information can be gleaned by piping the ps output through grep, as in `ps ax | grep bash` to find all the instances of bash.

Although you may need a wide screen or xterm to view the output, you may find `ps -A --forest` to be a helpful command in learning about your system. Processes that aren't linked to others were either started directly by `init` or have had their parents killed, and so they have been “adopted” by `init`. (Chapter 5 describes `init` and the boot procedure in more detail.) Most of these processes are fairly important—they're servers, login tools, and so on. Processes that hang off several others in this tree view, such as `xeyes` and `nedit` in Listing 2.4, are mostly user programs launched from shells.

# ## top: A Dynamic ps Variant

If you want to know how much CPU time various processes are consuming relative to one another, or if you want to quickly discover which processes are consuming the most CPU time, a tool called `top` is the one for the job. The `top` tool is a text-mode program, but of course it can be run in an xterm or similar window, as shown in Figure 2.2; there are also GUI variants, like `kpm` and `gnome-system-monitor`. By default, `top` sorts its entries by CPU use, and it updates its display every few seconds. This makes it a very good tool for spotting runaway processes on an otherwise lightly loaded system—those processes almost always appear in the first position or two, and they consume an inordinate amount of CPU time.

Looking at Figure 2.2, you might think that `FahCore_65.exe` is such a process, but in fact, it's legitimately consuming a lot of CPU time. You'll need to be familiar with the purposes and normal habits of programs running on *your* system in order to make such determinations; the legitimate needs of different programs vary so much that it's impossible to give a simple rule for judging when a process is consuming too much CPU time.

![](bbox=[0.12, 0.65, 0.88, 0.9])