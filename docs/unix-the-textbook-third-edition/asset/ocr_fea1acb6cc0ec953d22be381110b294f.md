```
26087 /usr/lib/ssh/sshd
26088 /usr/lib/ssh/sshd
    26095 -bash
        26192 ptree -a 516 26087 26088
$
```

Under PC-BSD, you can use the ps -auxd command to display the parent–child relationship between processes. However, the output for this command is not as complete and fancy as it is for the ptree command, as can be seen in the following session. You can try running the ps -auxfd | more command on your system to see the complete process hierarchy on your system.

```
% ps -dU sarwar
  PID TT  STAT      TIME COMMAND
 93204 -   S   0:00.18 sshd: sarwar@pts/1 (sshd)
 93207 1   Ss  0:00.45 -csh (csh)
 96636 1   R+  0:00.02 -- ps -dU sarwar
%
```

On PC-BSD, you can run the ps -aflx | more command to display all the processes running on your system and some of their important attributes, including PID, PPID, priority, nice value, virtual size, size currently in main memory, status, event waiting for, and full command name used to start the process. You can display the usernames, PIDs, PPIDs, and full command names of all the processes running on Solaris by executing the ps -e -o user,pid,ppid,comm command. We used the outputs of these commands to construct the process hierarchies on the two systems, shown in Figures 10.7 and 10.8.

# SUMMARY

A process is a program in execution. Being a time-sharing system, UNIX allows execution of multiple processes simultaneously. On a computer system with one CPU, processes are executed concurrently by scheduling the CPU time and giving it to each process for a short time called a quantum. Each process is assigned a priority by the UNIX system, and when the CPU is available, it is given to the process with the highest priority. The priority classes and the way priorities are assigned to various categories of processes are different on PC-BSD and Solaris.

The shell executes commands by creating child processes using the fork and exec system calls. When a process uses the fork system call, the UNIX kernel creates an exact main memory image of the process. The shell itself executes an internal command. An external binary command is executed by the child shell overwriting itself by the code of the command via an exec call. For an external command comprising a shell script, the child shell executes the commands in the script file one by one.