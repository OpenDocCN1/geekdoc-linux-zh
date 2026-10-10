# Part II: Shell Scripting Basics

It's a little tedious to check and recheck for correct PIDs. So in **the next section**, you learn how to use commands to interact with the default process using no PID or job number.

# ## Restarting stopped jobs

Under Bash job control, you can restart any stopped job as either a background process or a foreground process. A foreground process takes over control of the terminal you're working on, so be careful about using that feature.

To restart a job in background mode, use the `bg` command:

```
```
$ ./jobcontrol.sh
Script Process ID: 3343
Loop #1
^Z
[1]+  Stopped                     ./jobcontrol.sh
$ bg
[1]+  ./jobcontrol.sh &
Loop #2
$ jobs
[1]+  Running                    ./jobcontrol.sh &
$ Loop #3
```
```

Because the job was the default job, indicated by the plus sign, only the `bg` command was needed to restart it in background mode. Notice that no PID is listed when the job is moved into background mode.

If you have additional jobs, you need to use the job number along with the `bg` command to control the ones that are not the default job:

```
```
$ jobs
$ ./jobcontrol.sh
Script Process ID: 3381
Loop #1
^Z
[1]+  Stopped                     ./jobcontrol.sh
$ ./jobcontrol.sh
Script Process ID: 3387
Loop #1
^Z
[2]+  Stopped                     ./jobcontrol.sh
$ bg 2
[2]+  ./jobcontrol.sh &
Loop #2
$ jobs
[1]+  Stopped                     ./jobcontrol.sh
[2]-  Running                    ./jobcontrol.sh &
$ 
```
```

The command `bg 2` was used to send the second job into background mode. Notice that when the `jobs` command was used, it listed both jobs with their status, even though the default job is not currently in background mode.