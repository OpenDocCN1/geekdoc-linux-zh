Although the CPU is the most watched resource on a system, it is not the only one. Memory use, disk use, IO activity, and number of processes all tie together in determining throughput of the computer. For example, consider that you have two groups, A and B. Both groups require large amounts of memory—more than is available when both are running simultaneously. Raising the priority of Group A over Group B might not help if Group B does not fully relinquish the memory it is using. Although the paging system will do this over time, the process of swapping a process out to disk can be intensive and can greatly reduce performance. A better alternative might be to completely stop Group B with a signal and then continue it later when Group A has finished.

# Changing the Priority of a Time-Sharing Process with nice

The nice command is supported only for backward compatibility to previous Solaris releases. The priocntl command provides more flexibility in managing processes. The priority of a process is determined by the policies of its scheduling class and by its nice number. Each time-sharing process has a global priority that is calculated by adding the user-supplied priority, which can be influenced by the nice or priocntl commands and the system-calculated priority.

The execution priority number of a process is assigned by the operating system and is determined by several factors, including its schedule class, how much CPU time it has used, and its nice number. Each time-sharing process starts with a default nice number, which it inherits from its parent process. The nice number is shown in the NI column of the ps report.

A user can lower the priority of a process by increasing its user-supplied priority number. Only the superuser can increase the priority of a process by lowering its nice value. This prevents users from increasing the priorities of their own processes, thereby monopolizing a greater share of the CPU.

In UNIX, nice numbers range from 0 to +19. The highest priority is 0. Two versions of the command are available—the standard version, /usr/bin/nice, and a version that is part of the C shell. Use the nice command as described in Table 10–6 when submitting a program or command.

**Table 10-6 Setting Priorities with nice**

*Lowering the priority of a process*

| Command | Description |
|---|---|
| nice command_name | Increases the nice number by four units (the default). |
| nice +4 command_name | Increases the nice number by four units. |
| nice +10 command_name | Increases the nice number by 10 units. |

*Increasing the priority on a process*

| Command | Description |
|---|---|
| nice -10 command_name | Raises the priority of the command by lowering the nice number. |
| nice - -10 command_name | Raises the priority of the command by lowering the nice number. The two minus signs are required. The first minus sign is the option sign and the second minus sign indicates a negative number. |