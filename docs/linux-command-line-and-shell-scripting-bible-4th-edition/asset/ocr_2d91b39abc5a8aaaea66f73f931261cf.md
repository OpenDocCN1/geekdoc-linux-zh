With the use of `nohup`, you can run scripts in the background, log out of your terminal session to accomplish other tasks without stopping the script process, and check on its output later. There's even more flexibility to managing your background jobs, which is covered next.

# Controlling the Job

Earlier in this chapter, you saw how to use the `Ctrl+C` key combination to stop a job running in the shell. After you stop a job, the Linux system lets you either kill or restart it. You can kill the process by using the `kill` command. Restarting a stopped process requires that you send it a `SIGCONT` signal.

The function of starting, stopping, killing, and resuming jobs is called *job control*. With job control, you have full control over how processes run in your shell environment. This section describes the commands used to view and control jobs running in your shell.

# Viewing jobs

The key command for job control is the `jobs` command. The `jobs` command allows you to view the current jobs being handled by the shell. Though it doesn't contain the `jobs` command, the following script will help us demonstrate the command's power:

```
```
$ cat jobcontrol.sh
#!/bin/bash
#Testing job control
#
echo "Script Process ID: $$"
#
count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 10
    count=$[ $count + 1 ]
done
#
echo "End of script..."
exit
```
```