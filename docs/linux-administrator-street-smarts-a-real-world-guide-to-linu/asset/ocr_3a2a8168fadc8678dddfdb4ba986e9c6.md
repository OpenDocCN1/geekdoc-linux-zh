# Task 3.5: Manage Running Processes

This example shows load averages of 2.24, 2.28, and 1.79, meaning that programs are demanding roughly twice as much CPU time as is available. This could indicate that two programs are trying to run full out and other programs are making lesser demands or that more than two programs are requesting something less than full CPU time. You'll need to perform additional tests to find out precisely what's happening. The fact that the CPU load is higher for the shorter intervals (1 and 5 minutes) than for the longer one (15 minutes) is a clue that the CPU hogging began in the last few minutes.

# Obtaining Static Process Listings

The main process-monitoring tool in Linux is **ps**. This program supports a huge number of options, which fall into three broad classes:

+   **Unix98 options**  These single-character options may be grouped together and are preceded by a single dash (-).

+   **BSD options**  These single-character options may be grouped together and must *not* be preceded by a dash.

+   **GNU long options**  These multi-character options are never grouped together. They're preceded by two dashes (–).

For a complete list of **ps** options, consult the program's *man* page. Some of the more useful **ps** features include the following:

+   **Display help**  The `--help` option presents a summary of some of the more common **ps** options.

+   **Display all processes**  By default, **ps** displays only processes that were run from its own terminal (`xterm`, text-mode login, or remote login). The `-A` and `-e` options cause it to display all the processes on the system, and `x` displays all processes owned by the user who gives the command. The `x` option also increases the amount of information that's displayed about each process.

+   **Display one user's processes**  You can display processes owned by a given user with the `-U` *user*, `U` *user*, and `--user` *user* options. The *user* variable may be a username or a user ID.

+   **Display extra information**  The `-f`, `-l`, `j`, `l`, `u`, and `v` options all expand the information provided in the **ps** output. Most **ps** output formats include one line per process, but **ps** can display enough information that it's impossible to fit it all on one 80-character line. Therefore, these options provide various mixes of information.

+   **Display process hierarchy**  The `-H`, `-f`, and `--forest` options group processes and use indentation to show the hierarchy of relationships between processes. These options are useful if you're trying to trace the parentage of a process.

+   **Display wide output**  The **ps** command output can be more than 80 columns wide. Normally, **ps** truncates its output so that it will fit on your screen or `xterm`. The `-w` and `w` options tell **ps** not to do this, which can be useful if you direct the output to a file, as in `in ps w > ps.txt`. You can then examine the output file in a text editor that supports wide lines.