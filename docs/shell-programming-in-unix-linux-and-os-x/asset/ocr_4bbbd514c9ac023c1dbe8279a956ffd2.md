# The wait Command

General Format: wait job

This command causes the shell to suspend its execution until the process identified as job finishes executing. Job can be a process ID or a job_id. If job is not supplied, the shell waits for all processes to finish executing. If more than one process id is listed, wait wait for all to complete.

wait is useful for waiting for processes to have been sent to the background for execution.

Example

```
sort large_file > sorted_file & sort in the background
wait Continue processing
Now wait for sort to finish
plotdata sorted_file
```

The variable $! can be used to obtain the process ID of the last process sent to the background.

# The while Command

General Format:

```
while command_c
do
command
command
..
```

command, is executed and its status tested. If it is zero, the commands enclosed between the do and done are executed. Then command, it is executed again and its status tested. If it is zero, the commands between the do and done are once again executed. Execution of command_c and subsequent execution of the commands between the do and done continue until command, returns a non-zero exit status, at which point the loop is terminated. Execution then continues with the command that follows done.

Note that because command, gets evaluated immediately on entry into the loop, the commands between the do and done may never be executed if the test returns a non-zero exit status the first time.

Example

```
# fill up the rest of the buffer with blank lines
while [ $lines -le $maxlines ]
do
echo >> $BUFFER
lines=$((lines + 1))
d
```