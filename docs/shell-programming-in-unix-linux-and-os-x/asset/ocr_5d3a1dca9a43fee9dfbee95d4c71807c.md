# The wait Command

The eval command can also be used to effectively create “pointers” to variables:

```
$ x=100
$ ptrx=x
$ echo \$ptrx
100
$ eval $ptrx=50
$ echo $x
50
$
```

Dereference ptrx
Store 50 in var ptrx points to
See what happened

# The wait Command

If you move a command into the background for execution, command line runs in a subshell independent of your current shell (the job is said asynchronously). In some situations, you may want to wait for the background process (also known as a child process because it is spawned from your current shell—the parent) to finish execution proceeding. For example, you may have sent a large sort into the background and need to wait for it to finish before you access the sorted data.

The wait command does its general format

```
wait process-id
```

where process-id is the ID of the process you want to complete. If the process ID is omitted, the shell waits for all processes to complete execution. Execution of your current shell will be suspended until the process or processes finish execution.

You can wait the command at your terminal:

+   $ sort big-data > sorted_data &
  [1] 3423
$ date
Wed Oct 2 15:05:42 EDT 2002
$ wait 3423

Send it to the background
Job number & process id from the shell
Do some other work

Wait for the sort to finish
When sort finishes, prompt is returned

# The $ Variable

If you have only one process running in the background, the wait with no argument suffices. However, if you're running more than one background command and you want to wait on the most recently launched, you can access the process ID of the most recent background command as the special variable $!. So the command command

```
wait $!
```