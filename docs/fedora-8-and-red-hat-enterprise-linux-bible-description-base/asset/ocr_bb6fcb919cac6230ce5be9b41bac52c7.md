| Command Line | When the Command Is Run |
| :--- | :--- |
| at now next hour | The job will start in exactly 60 minutes. |
| at now next day | The job will start at the same time tomorrow. |
| at now next month | The job will start on the same day and at the same time next month. |
| at now next year | The job will start on the same date and at the same time next year. |
| at now next fri | The job will start at the same time next Friday. |
| at teatime | The job will run at 4 p.m. They keywords noon and midnight can also be used. |
| at 16:00 today | The job will run at 4 p.m. today. |
| at 16:00 tomorrow | The job will run at 4 p.m. tomorrow. |
| at 2:45pm | The job will run at 2:45 p.m. on the current day. |
| at 14:45 | The job will run at 2:45 p.m. on the current day. |
| at 5:00 Apr 14 2008 | The job will begin at 5 a.m. on April14, 2008. |
| at 5:00 4/14/08 | The job will begin at 5 a.m. on April 14, 2008. |

# ## Submitting scheduled jobs

The at facility offers a lot of flexibility in how you can submit scheduled jobs. There are three ways to submit a job to the at facility:

+   * **Piped in from standard input** — For example, the following command will attempt to build the Perl distribution from source in the early morning hours while the machine is likely to be less busy:

```
```
echo "cd /tmp/perl; make ; ls -al" | at 2am tomorrow
```
```

An ancillary benefit to this procedure is that a full log of the compilation process will be e-mailed to the user who submitted the job.

+   * **Read as standard input** — If no command is specified, at will prompt you to enter commands at the special at> prompt, as shown in the following example. You must indicate the end of the commands by pressing Ctrl+D, which signals an End of Transmission (\<EOT\>) to at.

```
```
$ at 23:40
at> cd /tmp/perl
at> make
at> ls -al
at> <Ctrl-d>
```
```