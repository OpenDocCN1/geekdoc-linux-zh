
## Example 12.11 nohup

When the user redirects output,

```
$ nohup ls -R > fileout &
[1] 384
```

When the nohup command redirects output,

```
$ nohup ls -R &
[2] 574
nohup: appending output to 'nohup.out'
```

> **NOTE** If more than one background process is started with nohup in the same current directory and the owner/user has not deliberately redirected output, the nohup.out file contains the output from all of those processes (either mixed or appended). This situation might create unpredictable results. If no output is required, the output could be directed to a log file or even to the null device (/dev/null).

Because all processes require affiliation with a parent process, commands started with nohup are affiliated with the init process as their parent after the owner/user logs out of the system.

After the nohup command is sent for execution, the shell replies by displaying numbers (such as [1] 384 in Example 12.5). In this case, the numbers translate to "This is the first command this user is running in the background, and the PID is 384."

## Job Control in the bash and tsh Shells

There may be times when you, in your role as administrator, have to change the priorities of the jobs running on your system. For example, in some organizations, routine processes are periodically suspended or given lower priorities when payrolls are calculated and checks are generated. Some organizations will interrupt otherwise routine processing for special technical tasks or for special reports. At those times, it is valuable to know how to access, suspend, resume, terminate, and otherwise manipulate the jobs on the system, whether they run in the foreground or the background. This section introduces several handy commands which enable you to do so.

### Creating a List of Background or Suspended Jobs

When you are running multiple processes, it is important to be able to identify which processes are running in the background. You cannot always determine which jobs are in the background with the `ps` command; that is where the `jobs` command comes in handy.

Looking at Example 12.11, You can see that the results from the `jobs` command indicate that there are two jobs and that each has been given a job number (in square brackets). The first is still running, and the second has run and completed. (If we invoked `jobs` again, the second job would not appear.) The `jobs` command does not list jobs that were started with the `nohup` command if the user has logged out of the system and then logged back in. If the user invokes a nohup job and issues the `jobs` command before logging out, however, that nohup job is displayed.

### Example 12.12 Listing Background Processes with the `jobs` Command

```
$ jobs
[1] - Running yes > /dev/null
[2] + Done nohup ls -R
```

### Suspending and Resuming a Foreground Task

Ctrl-Z is used to suspend, not terminate, a foreground process. No CPU resources are used for the suspended process, although it is still a process—it still occupies system memory and is subject to swapping to the hard disk. In other words, the suspended process’s data, functions, scripts, and so on remain mapped in RAM until higher-priority processes are invoked that will occupy the same RAM space. If that happens, that will cause the suspended process’s attributes to be saved in the swap space on the hard disk until the suspended process is resumed or terminated. You can tell the job to continue as needed in the foreground or background.

On some older ASCII-Z terminals, Ctrl-Z might not be capable of suspending a foreground task. If that is the case, try entering the following to force the shell to use the key sequence to suspend processes:

```
$ stty susp <Ctrl>-z
```

As seen in Example 12.13, to resume a foreground suspended task, simply enter fg at the prompt.

### Example 12.13 Foreground Task Control

In this example, we use the yes utility that, in this case, simply enters the characters y and n+line (that is, Enter) ad infinitum, using system resources until it is deliberately terminated. Thus, we are using yes as a utility with predictable and controllable outputs. If you are curious about more useful ways to use yes, consult your information sources.

So, to suspend a foreground task,

```
$ yes >/dev/null
<Ctrl>-z
[1]+ Stopped yes >/dev/null
```

And then, to resume the suspended task,

```
[1]+ Stopped yes >/dev/null
$ fg
yes ./dev/null
```

### Suspending and Resuming a Background Task

If the job you want to suspend is running in the background, you will find that Ctrl-Z does not work because it is strictly a foreground-related command. In this case, use the fg command to bring the command into the foreground and then suspend it with Ctrl-Z. You might have to use the job number as supplied by the jobs command.

As shown in Example 12.13, you would issue fg $jobnumber, press Enter, and then press Ctrl-Z. Assume that you want to resume a suspended job and return the job processing to the background. Simply type bg (background) at the prompt. The shell returns a job number in square brackets followed by a plus sign (+). The plus sign indicates that the job is the most recently started or stopped. The returned display also includes the ampersand (&) at the end of the listed job name, indicating that the job is in the background.

### Example 12.14 Background Task Control

To suspend a background task, use the fg command to move it to the foreground. Then, suspend it:

```
$ fg 1<jobnumber>
<Ctrl>-z
[1]+ Stopped yes > /dev/null
```

To resume the same suspended task and move it to the background,

```
[1]+ Stopped yes > /dev/null
$ bg
[1]+ yes > /dev/null &
```

> **NOTE** When you execute jobs to check background processes, the shell assigns a job number (in square brackets) to each job. With the kill command, you can use the job number or the PID. With the bg or fg command, you must use the job number; the PID will not work.

## More Job Control Examples

Example 12.15 illustrates how a job can be created and controlled by using the commands covered in this chapter.

### Example 12.15 Job Creation and Control

A job is initiated in the background, and the shell assigns it job number 1 and PID 273.

```
$ ls -R > out &
[1] 273
```

The jobs command indicates that the job is running in the background:

```
$ jobs
[1]+ Running ls -R > out &
```

The job is brought to the foreground:

```
$ fg 1
ls -R > out
```

The job is stopped with Ctrl-Z, and the shell reports that it has indeed stopped:

```
<Ctrl>-z
[1]+ ls -R > out &
```

Again, jobs indicates that the job is running in the background:

```
$ jobs
[1]+ Running ls -R > out &
```

kill terminates the job in the background:

```
$ kill %1
```

The jobs command verifies that the job has terminated:

```
$ jobs
[1]+ Terminated ls -R > out
```

## Daemons: Never-Ending System Processes

Daemons are constantly running processes that were not started by the user and are not associated with the terminal. They start when you start your system and run until you shut down your system.

Daemons wait for a specific event to take place, such as the submission of a print job to a print queue. The printing daemon detects the event and then takes responsibility for the task, seeing that it gets processed. More specifically, Linux's printing daemon, called lpd, tracks print job requests as well as the printers available to handle those requests. The daemon maintains queues (that is, spool directories) of outstanding requests and sends each request to the appropriate device at the proper time.

In Linux, most of the filenames associated with daemons end with d and are found in configuration file directories (such as /usr/bin). You can usually view them by entering the following command:

```
$ ps -guax
```

If you have a moment, take a look at them. You will see common daemons such as lpd, syslogd, inetd, and crond. System administrators typically maintain these directories and files.
