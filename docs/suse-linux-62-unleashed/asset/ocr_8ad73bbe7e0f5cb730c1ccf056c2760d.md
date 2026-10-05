# ash

ash is a simple shell with features much like the sh or Bourne Again SHell. The ash shell is run by the symbolic link bsh, which is found under the /bin directory.

# at

at runs a program at a specified time. You can use the at command to schedule a task or job to run at a time you specify on the command line or in a file.

# atq

Use atq to list the queue of waiting jobs. The atq command prints a list of waiting jobs or events for the at command (usually found under /var/spool/at directory).

# atrm

Use atrm to remove a specified job. The atrm command removes one or several jobs waiting in the queue. The atrm command can be used by users or the root operator to delete pending events (stop at commands from running).

# bash

bash is the GNU Bourne Again SHell. The default shell for SuSE Linux, bash has many features, such as command-line editing, built-help, and command history. The bash shell can also be run by the symbolic link sh, which is found under the /bin directory.

# batch

The batch command runs jobs according to load average. This program is used to run events when the computer reaches a certain load average, as determined by real-time values found in the loadavg file in the /proc directory. batch also has other options; read the command manual pages for details.

# bc

A calculator language, bc is an interpreter and language for building calculator programs and tools. You can use this interpreter and language to program custom calculators.

# bg

The bg command is used to force a suspended process to run in the background. For example, say you have started a command in the foreground (without using the & after the command) and realize it is going to take a while, but you still need your shell. You can use