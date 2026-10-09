The line that begins with `1` specifies the job with the jobID of `cron.daily`. This job is run once a day with a delay of 5 minutes. It runs *nice*, which executes `run-parts` (page 609) with a low priority; the job passes *run-parts* an argument of `/etc/cron.daily`. Similarly, the next line runs `cron.weekly` every seven days with a delay of 2.5 minutes. Because a month does not have a fixed number of days, the last line uses the **@monthly** macro to run `cron.monthly` once a month with a delay of 45 minutes.

As explained earlier, the **crond** daemon runs the shell scripts in the `/etc/cron.hourly` directory.

# `at:` RUNS OCCASIONAL TASKS

Like the **crond** daemon, **at** runs a job sometime in the future. Unlike **crond**, **at** runs a job only once. For instance, you can schedule an **at** job that will reboot the system at 3:00 AM (when all users are probably logged off):

```
# at 3am
at> systemctl reboot
at> <EOT>
job 3 at Wed Jul 31 03:00:00 2013
```

It is also possible to run an **at** job from within an **at** job. For instance, an **at** job might check for new patches every 18 days—something that would be more difficult with **crond**. See the **at** *man* page for more information.

By default, Fedora/RHEL is not set up with restrictions that prevent users from running **at**. See **at.allow** and **at.deny** on page 506 for more information.

# SYSTEM REPORTS

Many utilities report on one thing or another. The `who`, `finger`, `ls`, `ps`, and other utilities, for example, generate simple end-user reports. In some cases, these reports can help with system administration. This section describes utilities that generate more in-depth reports that can provide greater assistance with system administration tasks. Linux has many other report utilities, including `sar` (system activity report), `iostat` (input/output and CPU statistics), and `mpstat` (processor statistics), all part of the `sysstat` package; `netstat` (network report; `net-tools` package); and `nfsstat` (NFS statistics; `nfs-utils` package).

# `vmstat:` REPORTS VIRTUAL MEMORY STATISTICS

The `vmstat` utility (virtual memory statistics; `procps-ng` package) generates virtual memory information along with (limited) disk and CPU activity data. The following example shows virtual memory statistics at three-second intervals for seven iterations (from the arguments `3 7`). The first line covers the time since the system was booted; each subsequent line covers the period since the previous line.