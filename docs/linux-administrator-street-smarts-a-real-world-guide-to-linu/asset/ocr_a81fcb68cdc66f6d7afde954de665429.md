In addition to `kill` and `top`, another tool for killing processes is `killall`. This program works much like `kill`, but it accepts a process name, rather than a PID number, as a way to identify the process to be killed. Although `killall` can be a quick and easy way to kill a process if you know its name, it can be dangerous because it kills all instances of that process. For instance, if `root` were to type `killall bash`, all `bash` shells would be terminated. Thus, you should be sure you want to terminate all instances of a process before using `killall`.

![](bbox=[0.15, 0.25, 0.28, 0.33])

> Some Unix-like systems implement a `killall` program that kills all running processes, not just all running processes of a particular name. Thus, you should never use `killall` on an unfamiliar system unless you're sure that the program works in the way you expect!

After killing the `g1xgears` process, wait a short time and then use `uptime` and `top` again. You should find that your load average has dropped, although it will take a few minutes for the longer-term load average figure to change significantly.

# ## Criteria for Completion

To complete this task, you should have determined your system's CPU load, identified running processes with `ps`, used `top` to identify CPU-hogging programs, and terminated processes with `kill`, `killall`, or `top`. These tools will help you manage your Linux system, keeping misbehaving processes from causing too many problems. Running `uptime` every now and then on critical systems will help you keep the systems working well by enabling you to spot runaway processes before they cause too much damage.

# # Task 3.6: Adjust Process Priorities

Sometimes a program has a legitimate need to consume a lot of CPU time but you don't want it to consume that CPU time at the expense of other processes. For such situations, the ability to downgrade a process's priority is useful, and of course Linux provides that ability. You can also increase a process's priority if it should have precedence when the kernel doles out CPU time. Knowing how to make these adjustments will enable you to keep your system running smoothly without going to the extreme measure of terminating processes.

# ## Scenario

A computer is functioning as a multipurpose system with several important processes running. Some of these processes consume a lot of CPU time, but you want to keep them from interfering with other processes. Thus, you want to adjust their process priorities. You'll both adjust the priorities of existing processes and run new processes with modified priorities.