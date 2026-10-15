# SYNTAX

```
fg [%jobid]
bg [%jobid-list]
```

Purpose: Syntax 1: Resume execution of the process with job number jobid in the foreground or move background processes to the foreground; a jobid starts with %
Syntax 2: Resume execution of suspended processes/jobs with job numbers in jobid-list in the background; a jobid starts with %

# Commonly used options/features:

+   % or %+  Current job
+   %-  Previous job
+   %N  Job number N
+   %Name  Job beginning with Name
+   %?Name  Command containing Name

If there are multiple suspended processes, the fg command without an argument brings the current process into the foreground, and the bg command without an argument resumes execution of the current process in the background. The job using the CPU at any particular time is called the current job.

You can use the jobs command to display the job numbers of all suspended (stopped) and background processes and identify which one is the current process. The current process is identified by a + and the previous process by a - in the output of the jobs command. The following is a brief description of the command.

# SYNTAX

```
jobs [option] [%jobid-list]
```

Purpose: Display the status of the suspended and background processes specified in jobid-list; with no list, display the status of current job

# Commonly used options/features:

+   -l  Also display PIDs of jobs

In the following sessions, we show the use of the fg, bg, <Ctrl+Z>, and jobs commands. We run the sort and cp commands in the background. The jobID and PID pairs of these processes are [1] 60149 and [2] 60156 for the sort and cp commands, respectively. The sort bigdata command is in the currently running process/job, as shown in the output of the jobs and jobs -l commands, as well as the R state of the process in the output of the ps command. The cp bigdata bigdata1 command has been swapped on the disk, as indicated by the D state of the process in the output of the ps command.

```
% sort bigdata > bigdata.sorted &
[1] 60149
```