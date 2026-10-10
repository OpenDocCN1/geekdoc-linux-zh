# ## Job Control

In the previous section you saw how to use the CtrL+Z key combination to stop a job running in the shell. After you stop a job, the Linux system lets you either kill or restart it. Restarting a stopped process requires sending it a signal continue (SIGCONT) signal.

The function of starting, stopping, killing, and resuming jobs is called job control. With job control, you have full control over how processes run in your shell environment.

The following sections describe the commands you can use to view and control jobs running in your shell.

# ### Viewing Jobs

The key command for job control is the jobs command. The jobs command allows you to view the current jobs being handled by the shell. Listing 26.1 uses a shell script to demonstrate viewing a stopped job.

```
**Listing 26.1:** Stopping a running job

$ cat test2.sh
#!/bin/bash
# testing job control

echo "This is a test program $$"
count=1
while [ $count -le 10 ] ; do
 echo "Loop #$count"
 sleep 10
 count=$[ $count + 1 ]
done
echo "This is the end of the test program"
$ ./test2.sh
This is a test program 29011
Loop #1

[1]+ Stopped .,./test2.sh
$ ./test2.sh > test2.sh.out &
[2] 28861
$
$ jobs
[1]+ Stopped .,./test2.sh
[2]- Running .,./test2/sh >test2.shout &
$
```