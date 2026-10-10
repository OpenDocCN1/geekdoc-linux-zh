# top

**Purpose:** Monitor system performance and running processes.

**Usage syntax:** `top [OPTIONS]`

```
$ top
top - 18:56:55 up 21 min,  2 users,  load average: 0.22, 0.35, 0.31
Tasks: 140 total,   2 running, 138 sleeping,   0 stopped,   0 zombie
Cpu(s): 9.0%us,  2.0%sy,  0.1%ni, 85.1%id,  3.5%wa,  0.1%hi, 0.2%si, 0.0%st
Mem: 3988516k total, 1089196k used,  2899320k free,    35832k buffers
Swap: 3951948k total,     0k used,  3951948k free,    66468k cached
```

![](bbox=[0.08, 0.3, 0.92, 0.55])

**top** is a process and performance monitor for Unix, Linux, and BSD systems. The first few lines of **top** output displays information about processor, memory, and swap utilization. The remaining portion of the screen is used to display information about running processes. The process listing updates every few seconds to display the most resource-intensive processes.

> **Tip**
> *There are several interactive commands that can be used to control the output of the* `top` *command. Press the* `?` *key within* `top` *for a complete listing of these commands.*

**Common usage examples:**

| Command             | Description                                          |
| :---                | :---                                                 |
| `top`               | Monitor system performance and processes             |
| `top -u [USER]`     | Only display processes owned by the specified user   |
| `top -d [SECONDS]`  | Update at the specified interval (in seconds)        |
| `top -i`            | Do not display idle processes                        |