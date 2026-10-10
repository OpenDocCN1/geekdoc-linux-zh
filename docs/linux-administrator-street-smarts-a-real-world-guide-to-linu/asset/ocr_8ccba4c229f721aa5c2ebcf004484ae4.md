# Scope of Task

This task involves learning to use the `nice` and `renice` commands, which enable you to adjust process priorities. To do this, you’ll need multiple test processes on which to experiment so that you can judge the effect of the commands.

# Duration

This task should take about half an hour to complete. In day-to-day practice, adjusting the priority of a process takes just a few seconds once you’re familiar with the relevant commands.

# Setup

To begin this task, you should log in as an ordinary user. (Real-world applications of this task’s principles often require *root* access, though. As with killing processes, ordinary users may adjust their own process priorities, but only *root* may adjust the priorities of other users’ processes.) Either log in using a GUI login prompt or log in using text mode and start an X session by typing `startx`. I recommend using X simply because it lets you launch and easily control multiple programs. If necessary, you could use text-mode processes and multiple virtual terminals instead, but you’ll need to find another CPU-intensive program to use for experimentation.

# Caveats

This task can be performed as an ordinary user, although you won’t be able to increase the priority of your tasks except as *root*. Thus, if you want to experiment with this ability, you’ll need to perform some parts of the task as *root*, with all the usual caveats that entails. Even as an ordinary user, if you mistype a command, you could conceivably cause a program to begin behaving very sluggishly. Recovering from such problems should be possible, but you’ll need to either exit from and restart the affected process or increase its priority as *root*.

# Procedure

To perform this task, you’ll use the `nice` command to launch programs with priorities that you specify and you’ll use the `renice` command to alter the priorities of existing processes. Before you jump into these details, though, you should understand the meaning of the numbers you’ll be setting.

# Understanding Process Priorities

Every Linux process has an associated priority number, which ranges from −20 to 19. The default priority value is 0. Confusingly, negative priority numbers correspond to *increased* priority, whereas positive numbers correspond to *decreased* priority.

The Linux kernel is responsible for doling out CPU time; the kernel decides for how long a given process will run before giving CPU time to a competing process. When no programs are making major demands on CPU time, even a low-priority process will get plenty of CPU