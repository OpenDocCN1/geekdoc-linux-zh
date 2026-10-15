
![](img/02e070097d401d3bf7de4bf1c470b267_379_0.png)

## FIGURE 10.1 UNIX process state diagram.

## TABLE 10.1 A Brief Description of the UNIX Process States

| State | Description |
|-------|-------------|
| Ready | The process is ready to run but does not have the CPU. Based on the scheduling algorithm, the scheduler decided to give the CPU to another process. Several processes can be in this state, but on a machine with a single CPU, only one can be executing/running (i.e., using the CPU). |
| Running | The process is actually running (i.e., using the CPU). |
| Waiting | The process is waiting for an event. Possible events are an I/O operation to complete (e.g., disk/terminal read or write), a child process to complete (the parent is waiting for one or more of its children to exit), or the process itself is waiting to be reawakened having been put to sleep. |
| Swapped | The process is ready to run, but it has been temporarily put on the disk (on the swap space); perhaps it needs more memory and there is not enough available at this time. |
| Zombie | A dying process is said to be in a zombie state. Usually, when the parent of a process terminates before it executes the exit call, it becomes a zombie process. The process finishes and finds that the parent is not waiting. The zombie processes are finished for all practical purposes and do not reside in the memory, but they still have some kernel resources allocated to them and cannot be taken out of the system. All zombies and their live children are eventually adopted by the granddaddy, the init process, which removes them from the system. |

process and executes external commands. You can use the type command to determine if your command is built in or external, as shown in the following session. Under Bash, you can use the -a option to display all the locations of a command, as follows. You can see that the bg command is built in but also has an external version. However, by default, the built-in version is executed. The Bourne shell may be invoked through two executables available at two different places in your file system structure.

```
$ type bg
bg is a shell builtin
$ type -a bg
bg is a shell builtin
bg is /usr/bin/bg
$ type -a sh
sh is /usr/bin/sh
sh is /usr/sbin/sh
$
```

A UNIX process can create another process by using the fork() system call, which creates an exact main memory copy of the original process (i.e., the process that calls fork()). Both processes continue execution, starting with the statement that follows the fork. The forking process is known as the *parent process*, and the created (forked) process is called the *child process*, as shown in Figure 10.2. Here, we show a Bourne shell that has created a child process (another Bourne shell). We discuss the use of fork() and other system calls needed for the creation of processes and *interprocess communication* (IPC) in Chapters 18–21.

For executing an external binary command, a mechanism is needed that allows the child process to become the command to be executed. The UNIX system call exec() can be used to do exactly that, allowing a process to overwrite itself with the executable code for another command. A shell uses the fork() and exec() calls in tandem to execute an external binary command. Figure 10.3 shows the sequence of events for the execution of an external command sort, whose code is in a binary file, **/usr/bin/sort**.

The execution of a shell script (a series of shell commands in a file; see Chapters 12–15) is slightly different from the execution of a binary command/file. In the case of a shell script, the current shell creates a child shell and lets the child shell execute commands in the script file one by one. Each command in the script file is executed in the same way that commands from the keyboard are; that is, the child shell creates a child for every

![](img/02e070097d401d3bf7de4bf1c470b267_380_0.png)

FIGURE 10.2 Process creation via the fork system call.
