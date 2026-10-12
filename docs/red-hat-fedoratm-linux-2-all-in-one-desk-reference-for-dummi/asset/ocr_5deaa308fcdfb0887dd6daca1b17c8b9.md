# **420 Scheduling Jobs in Fedora Core**

Here is an example showing how to execute the `ps` command at a future time:

```
```
at> ps
at> <EOT>
job 1 at 2004-02-29 21:30
```
```

After you press Ctrl+D, the `at` command responds with a job number and the date and time when the job will execute.

| **Table 1-7** | **Formats for the Time of Execution with the at Command** |
|---|---|
| **Command** | **When the Job Will Run** |
| `at now` | Immediately |
| `at now + 15 minutes` | 15 minutes from the current time |
| `at now + 4 hours` | 4 hours from the current time |
| `at now + 7 days` | 7 days from the current time |
| `at noon` | At noontime today (or tomorrow, if already past noon) |
| `at now next hour` | Exactly 60 minutes from now |
| `at now next day` | At the same time tomorrow |
| `at 17:00 tomorrow` | At 5:00 p.m. tomorrow |
| `at 4:45pm` | At 4:45 p.m. today (or tomorrow, if it’s already past 4:45 p.m.) |
| `at 3:00 Aug 16, 2004` | At 3:00 a.m. on August 16, 2004 |

After you enter one or more jobs, you can view the current list of scheduled jobs with the `atq` command:

```
```text
atq
```
```

The output looks similar to the following:

```
```text
4       2004-08-16 03:00 a root
5       2004-10-26 21:57 a root
6       2004-10-26 16:45 a root
```
```

The first field on each line shows the job number — the same number that the `at` command displays when you submit the job. The next field shows the year, month, day, and time of execution. The last field shows the jobs pending in the queue named a .

If you want to cancel a job, use the `atrm` command to remove that job from the queue. When removing a job with the `atrm` command, refer to the job by its number, as follows:

```
```text
atrm 4
```
```