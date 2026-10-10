# kill

**Purpose:** Terminate a process.

**Usage syntax:** `kill [OPTIONS] [PID]`

```
# pgrep -l mysqld
5540 mysqld
# kill 5540
```

Using the kill command to terminate a process

The `kill` command terminates the specified PID. In the above example, the *mysqld* process with a PID of 5540 is terminated using `kill`.

The default behavior of the `kill` command requests the process to gracefully exit. If a process fails to properly terminate, optional kill signals can be sent to force the process to end. The most commonly used kill signal in this situation is `–9` which forcefully terminates the specified PID as displayed in the next example.

```
# pgrep -l mysqld
5545 mysqld
# kill -9 5545
```

Using the -9 option to kill a hung process

> It is recommended to only use the `kill –9` command in rare situations where a hung process refuses to gracefully exit. The `–9` signal is only used in these extreme situations, as it can cause undesired results such as system instability and “zombie” child processes.

Common usage examples:

| | |
|---|---|
| `kill [PID]` | Terminate the specified process |
| `kill -9 [PID]` | Force an unresponsive process to terminate |