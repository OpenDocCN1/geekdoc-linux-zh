# **fg: Brings A Job to the Foreground**

The shell assigns a job number to each command you run in the background. For each job run in the background, the shell lists the job number and PID number immediately, just before it issues a prompt:

```
```
$ xclock &
[1] 1246
$ date &
[2] 1247
$ Tue Dec 7 11:44:40 PST 2010
[2]+ Done                date
$ find /usr -name ace -print > findout &
[2] 1269
$ jobs
[1]-  Running     xclock &
[2]+ Running       find /usr -name ace -print > findout &
```
```

Job numbers, which are discarded when a job is finished, can be reused. When you start or put a job in the background, the shell assigns a job number that is one more than the highest job number in use.

In the preceding example, the **jobs** command lists the first job, **xclock**, as job 1. The **date** command does not appear in the **jobs** list because it finished before **jobs** was run. Because the **date** command was completed before **find** was run, the **find** command became job 2.

To move a background job to the foreground, use the **fg** builtin followed by the job number. Alternatively, you can give a percent sign (%) followed by the job number as a command. Either of the following commands moves job 2 to the foreground. When you move a job to the foreground, the shell displays the command it is now executing in the foreground.

```
```
$ fg 2
find /usr -name ace -print > findout
or
$ %2
find /usr -name ace -print > findout
```
```

You can also refer to a job by following the percent sign with a string that uniquely identifies the beginning of the command line used to start the job. Instead of the preceding command, you could have used either **fg %find** or **fg %f** because both uniquely identify job 2. If you follow the percent sign with a question mark and a string, the string can match any part of the command line. In the preceding example, **fg %?ace** also brings job 2 to the foreground.

Often the job you wish to bring to the foreground is the only job running in the background or is the job that **jobs** lists with a plus (+). In these cases **fg** without an argument brings the job to the foreground.