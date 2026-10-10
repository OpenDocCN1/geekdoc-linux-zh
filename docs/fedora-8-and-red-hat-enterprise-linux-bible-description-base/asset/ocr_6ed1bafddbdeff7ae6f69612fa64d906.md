# ## Using the batch command

If system resources are at a premium on your machine, or if the job you submit can run at a priority lower than normal, the `batch` command (equivalent to `at -q b`) may be useful. It is controlled by the same `atd` daemon, and it allows job submissions in the same format as `at` submissions (although the time specification is optional).

However, to prevent your job from usurping already scarce processing time, the job will run only if the system load average is below a particular value. The default value is 0.8, but specifying a command-line option to `atd` can modify this. This was used as an example in the earlier section describing startup and shutdown. Here is an example of the `batch` command:

```
```
$ batch
at> du -h /home > /tmp/duhome
at> <Ctrl+d>
```
```

In this example, after I type the `batch` command, the `at` facility is invoked to enable me to enter the command(s) I want to run. Typing the `du -h /home > /tmp/duhome` command line has the disk usages for everything in the /home directory structure output to the /tmp/duhome file. On the next line, pressing Ctrl+D ends the batch job. As soon as the load average is low enough, the command is run. (Run the `top` command to view the current load average.)

# ## Using the cron facility

Another way to run commands unattended is via the `cron` facility. Part of the xixie-cron rpm package, `cron` addresses the need to run commands periodically or routinely (at least, more often than you’d care to manually enter them) and allows lots of flexibility in automating the execution of the command.

As with the `at` facility, any output or error messages that haven’t been redirected elsewhere are e-mailed to the user who submitted the job. Unlike using `at`, however, cron jobs are intended to run more than once and at a regular interval (even if that interval is only once per month or once per year).

Also like the `at` facility, `cron` includes two access control files designed to limit which users can use it. The file `/etc/cron.allow` contains a list of those users who are granted access, and the file `/etc/cron.deny` contains a similar list of those who may not submit `cron` jobs. If neither file exists (or if `cron.deny` is empty), all users are granted access to `cron`.

There are four places where a job can be submitted for execution by the `cron` daemon `crond:`

+   * The `/var/spool/cron/username` file — This method, where each individual user (indicated by `username`) controls his or her own separate file, is the method used on UNIX System V systems.