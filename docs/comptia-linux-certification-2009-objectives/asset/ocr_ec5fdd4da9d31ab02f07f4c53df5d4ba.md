There are many options available with the `kill` command. These options are referred to as kill signals. Some processes cannot be eliminated by the `kill` command. To terminate these processes, use the `kill` command with the -9 signal. This terminates the processes immediately.

# Process States

Process states enable you to identify the stage that a process is in currently. They are indicated by a single letter notation in the process table.

The various process states are given in the table below.

![](bbox=[0.78, 0.18, 0.88, 0.25])

| State | Description |
| --- | --- |
| Uninterruptible sleep (D) | The process is permanently inactive. |
| Running (R) | The process may be running or ready to be run. |
| Interruptible sleep (S) | The process is waiting to be run after some specific trigger. |
| Stopped (T) | The process may be temporarily stopped by a job control tool or because it is being traced. |
| Dead (X) | The process has been killed. This state is never displayed. |
| Defunct (Z) | The process has ended, but only after its parent process. This implies that it has not been killed properly and it will remain as a “zombie.” |

# The top Command

The `top` command lists all tasks running on a Linux system. It acts as a process management tool by allowing users to prioritize, sort, or terminate processes interactively. It displays a dynamic process status, reflecting real-time changes. Different keystrokes within this tool execute process management actions.

![](bbox=[0.78, 0.54, 0.9, 0.61])