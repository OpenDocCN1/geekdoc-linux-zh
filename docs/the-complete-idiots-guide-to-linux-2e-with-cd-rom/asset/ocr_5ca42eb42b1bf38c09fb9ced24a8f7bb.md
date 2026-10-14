```
119 root      0  0  476  476  276 S      0  0.0  1.2   0:00 klogd
```

At the beginning of the listing, top displays general information about the system. The first line displays the current time, amount of time the system has been up, number of users, and load average for the last 1, 5, and 15 minutes.

The second line displays the total number of processes running in the system and what they are doing: sleeping processes, those that are not currently doing anything; zombie processes, those that are processes that should be dead but for some reason are still around; and stopped processes.

The third line displays the various CPU states, such as how much time your computer has spent executing user or system code, or nice time. Nice time represents time spent by processes that are executing with a lower priority. These processes are represented by a positive priority because they are nice to other processes (typical priority is 0). Negative priority processes are allocated more CPU so they have a higher priority and get additional chances to run.

On the fourth and fifth lines, you see information regarding real and virtual memory. Virtual memory is the one that uses the swap disk to accommodate more processes than you can run given your RAM.

Following the general information area is a listing of all the main processes, including the ID for the process (PID) owner and priority and resource consumption for CPU and memory.

When top is running, there are a number of options you can specify to customize the information it displays. Some of the more useful are shown in Table 22.1.

# Table 22.1 Top Options

| Interactive Commands | Description |
|---|---|
| Space | Updates display |
| Ctrl+L | Redraws the screen |
| ? | Prints help |
| i | Toggles display of idle processes |
| c | Toggles display of command name/line |
| l | Toggles display of load average |
| m | Toggles display of memory information |
| t | Toggles display of summary information |
| k | Kills a task (with any signal) |
| r | "Renices" a task (change its current priority) |
| P | Sorts by CPU usage |
| M | Sorts by resident memory usage |
| T | Sorts by time/cumulative time |
| n | Sets the number of processes to show |
| s | Sets refresh rate |
| q | Quits |