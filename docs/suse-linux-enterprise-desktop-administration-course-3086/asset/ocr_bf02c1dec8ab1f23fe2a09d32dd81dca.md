# top

The top command allows you to watch processes continuously in a list that is updated in short intervals, thus providing a real-time view of a running system. This command can also be used to assign a new nice value to running processes or to end processes.

The information displayed in top can be filtered by a specific user and can be sorted on any displayed field. If you have sufficient privileges, you can type r to adjust the priority of a process.

![](bbox=[0.119, 0.176, 0.306, 0.247])

The same restrictions described for the renice command apply when changing process nice levels using top. Nonroot users can increase the nice level, but they cannot lower it.

When you enter top, a list similar to the one shown in Figure 10-4 appears.

![](bbox=[0.053, 0.302, 0.971, 0.834])

**Figure 10-4**

The displayed list is sorted by computing time and is updated every three seconds. You can terminate the display by typing q.