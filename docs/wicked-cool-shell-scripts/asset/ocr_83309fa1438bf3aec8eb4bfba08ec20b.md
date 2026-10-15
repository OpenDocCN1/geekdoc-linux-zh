```
# We assume that the root cron has entries for 'daily', 'weekly', and
# 'monthly' jobs. If we can't find a match for the one specified, well,
# that's an error. But first, we'll try to get the command if there is
# a match (which is what we expect).

job="$ (awk "NF > 6 && $1/ { for (i=7;i<=NF;i++) print $i }" $rootcron)"

if [ -z "$job" ] ; then  # No job? Weird. Okay, that's an error.
 echo "So: Error: no $1 job found in $rootcron" >&2
 exit 1
fi

SHELL=$(which sh)      # To be consistent with cron's default

eval $job              # We'll exit once the job is finished.
```

Listing 6-11: The docron script

# How It Works

The cron jobs located in /etc/daily, /etc/weekly, and /etc/monthly (or /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly) are set up completely differently from user crontab files: each is a directory that contains a set of scripts, one per job, that are run by the cron facility, as specified in the /etc/crontab file. To make this even more confusing, the format of the /etc/crontab file is different too, because it adds an additional field that indicates what effective user ID should run the job.

The /etc/crontab file specifies the hour of the day (in the second column of the output that follows) at which to run the daily, weekly, and monthly jobs in a format that is completely different from what you've seen as a regular Linux user, as shown here:

```
$ egrep '(daily|weekly|monthly)' /etc/crontab
# Run daily/weekly/monthly jobs.
15   3   *   *   *   root    periodic daily
30   4   *   *   6   root    periodic weekly
30   5   1   *   *   root    periodic monthly
```

What happens to the daily, weekly, and monthly jobs if this system isn't running at 3:15 AM every night, at 4:30 AM on Saturday morning, and at 5:30 AM on the first of each month? Nothing. They just don't run.

Rather than trying to force cron to run the jobs, the script we've written identifies the jobs in this file ① and runs them directly with the eval on the very last line ②. The only difference between invoking the jobs found from this script and invoking them as part of a cron job is that when jobs are run from cron, their output stream is automatically turned into an email message, whereas this script displays the output stream on the screen.