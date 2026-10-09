# The pgrep Command Options

The pgrep command supports different options by which one or more conditions for search may be specified.

| Option | Used To |
| :--- | :--- |
| -f | Specify the full path name of the process. |
| -l | Print the name of the process along with its PID. |
| -u | Specify the UID of the user who started it. |
| -G | Specify the GID related to the process. |
| -n | Specify the most recent process. |
| -o | Specify the oldest process. |

# Signals

# Definition:

Signals are messages sent to a process to perform a certain action. They are used to suspend or terminate processes. Signals may affect only the process specified and its child processes. Signals may be executed, caught, blocked, or ignored by processes.

![](bbox=[0.77, 0.43, 0.85, 0.49])

# Example:

![](bbox=[0.13, 0.56, 0.65, 0.84])

**Figure 10-9:** A signal sent to a process.