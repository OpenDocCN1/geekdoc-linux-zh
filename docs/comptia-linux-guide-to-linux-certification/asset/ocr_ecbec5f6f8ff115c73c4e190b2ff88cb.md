| Name | Number | Description |
| --- | --- | --- |
| SIGHUP | 1 | Also known as the hang-up signal, it stops a process, then restarts it with the same PID. If you edit the configuration file used by a running daemon, that daemon might be sent a SIGHUP to restart the process; when the daemon starts again, it reads the new configuration file. |
| SIGINT | 2 | This signal sends an interrupt signal to a process. Although this signal is one of the weakest kill signals, it works most of the time. When you use the Ctrl+c key combination to kill a currently running process, a SIGINT is actually being sent to the process. |
| SIGQUIT | 3 | Also known as a core dump, the quit signal terminates a process by taking the process information in memory and saving it to a file called core on the hard disk in the current working directory. You can use the Ctrl+\ key combination to send a SIGQUIT to a process that is currently running. |
| SIGTERM | 15 | The software termination signal is the most common kill signal used by programs to kill other processes. It is the default kill signal used by the kill command. |
| SIGKILL | 9 | Also known as the absolute kill signal, it forces the Linux kernel to stop executing the process by sending the process’s resources to a special device file called /dev/null. |

Table 9-2 Common administrative kill signals

Some processes have the ability to ignore, or trap, certain kill signals that are sent to them. The only kill signal that cannot be trapped by any process is the SIGKILL. Thus, if a SIGINT, SIGQUIT, and SIGTERM do not terminate a stubborn process, you can use a SIGKILL to terminate it. However, you should only use SIGKILL as a last resort because it prevents a process from closing temporary files and other resources properly.

If you send a kill signal to a process that has children, the parent process terminates all of its child processes before terminating itself. Thus, to kill several related processes, you can simply send a kill signal to their parent process. In addition, to kill a zombie process, it is often necessary to send a kill signal to its parent process.

Another command that can be used to send kill signals to processes is the killall command. The killall command works similarly to the kill command in that it takes the kill signal as an option; however, it uses the process name to kill instead of the PID. This allows multiple processes of the same name to be killed in one command. An example of using the killall command to send a SIGQUIT to multiple sample processes is shown in the following output:

```
[root@server1 ~]# ps -ef | grep sample
root 1729 1 0 Jun30 tty3 00:00:00 /sbin/sample
root 20198 1 0 Jun30 tty4 00:00:00 /sbin/sample
[root@server1 ~]# killall -3 sample
[root@server1 ~]#
[root@server1 ~]# ps -ef | grep sample
[root@server1 ~]# _
```

![](bbox=[0.14, 0.81, 0.33, 0.92])

Alternatively, you could use the command killall -SIGQUIT sample to do the same as the killall -3 sample command used in the preceding output.