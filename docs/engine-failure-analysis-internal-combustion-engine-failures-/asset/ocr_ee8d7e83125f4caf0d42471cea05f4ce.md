invisibly. To place a job in the background, you use the **bg** command. You must also give the job a *job ID*, using the syntax discussed in the following table.

# SPECIFYING JOB IDS

| Use This Job ID | To Refer to This Job |
|---|---|
| %n | Job n |
| %string | The job that uses a command with a name starting with *string* |
| %?string | The job that uses a command with a name containing *string* |
| %% | The current job |
| %+ | The previous job |
| %- | The previous job |

# EXAMPLES

| This Command | Does the Following |
|---|---|
| make & | Begins compiling a program and places the process in the background. |
| stop %% | Suspends the current process. |
| Ctrl + z | Suspends the current process. |

# Signals

Linux processes can send *signals* to each other, and each signal has both an identifying number and a fixed message. For example, to kill a process, you use the *kill* command, which sends the *SIGKILL* signal (identified by number 9) to the process. The following table lists the available signals, their ID numbers, and a brief description of the message that each signal sends.