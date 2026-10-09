The "->" spawned option causes all the print statements in `hitc` and in the slaves to appear in the console window. This can be a useful feature when debugging your first few PVM programs. You may wish to experiment with this option by placing print statements in `hitc.f` and `hive.slave.f` and recompiling.

To get an idea of XPVM’s real-time animation capabilities, you again can use `hitc`. Start up XPVM, and build a virtual machine with four hosts. Click on the “tasks” button and select “spawn” from the menu. Type “hitc” where XPVM asks for the command, and click on “start”. You will see the host icons light up as the machines become busy. You will see the `hitc.slave` tasks get spawned and see all the messages that travel between the tasks in the `Space Time` display. Several other views are selectable from the XPVM “views” menu. The “task output” view is equivalent to the “->” option in the PVM console. It causes the standard output from all tasks to appear in the window that pops up.

Programs that are spawned from XPVM (and the PVM console) are subject to one restriction: they must not contain any interactive input, such as asking for how many slaves to start up or how big a problem to solve. This type of information can be read from a file or put on the command-line as arguments, but there is nothing in place to get user input from the keyboard to a potentially remote task.

# ## 11.8 PVM Console Details

The PVM console, called `pvm`, is a standalone PVM task that allows you to interactively start, query, and modify the virtual machine. The console may be started and stopped multiple times on any of the hosts in the virtual machine without affecting PVM or any applications that may be running.

When the console is started, `pvm` determines whether PVM is already running and, if not, automatically executes `pvm`d on this host, passing `pvm`d the command-line options and hostfile. Thus, PVM need not be running to start the console.

```
```
pvm [-n hostname>] [hostfile]
```
```

The `-n` option is useful for specifying another name for the master `pvm`d (in case hostname doesn’t match the IP address you want). This feature becomes very useful with Beowulf clusters because the nodes of the cluster sometime are on their own network. In this case the front-end node will have two hostnames: one for the cluster and one for the external network. The `-n` option lets you specify the cluster name directly during PVM startup.

Once started, the console prints the prompt