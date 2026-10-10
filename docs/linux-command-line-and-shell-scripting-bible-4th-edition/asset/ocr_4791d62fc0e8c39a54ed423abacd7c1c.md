When you use the at command, the job is submitted to a job queue. The job queue holds the jobs submitted by the at command for processing. There are 52 different job queues available for different priority levels. Job queues are referenced using lowercase letters, a through z, and uppercase letters A through Z, with A queue being a different queue than a queue.

**NOTE**

A few years ago, the batch command was another method that allowed a script to be run at a later time. The batch command was unique because you could schedule a script to run when the system was at a lower usage level. Nowadays the batch command is conusly a script, /usr/bin/batch, that calls the at command and submits your job to the b queue.

The higher alphabetically the job queue letter, the lower the priority (higher nice value) the job will run under. By default, at jobs are submitted to the at job a queue. If you want to run a job at a lower priority, you can specify a different queue letter using the -q parameter. And if you want your jobs to consume as little CPU as possible compared to other current processes, you'll want to put your job into the z (lowercase Z) queue.

# Retrieving job output

When an at job runs on the Linux system, there's no monitor associated with the job. Instead, the Linux system uses the email address of the user who submitted the at job as STDOUT and STDERR. Any output destined to STDOUT or STDERR is mailed to the user via the mail system.

Here's a simple example using the at command to schedule a job to run on a CentOS distribution:

```
$ cat tryat.sh
#!/bin/bash
```