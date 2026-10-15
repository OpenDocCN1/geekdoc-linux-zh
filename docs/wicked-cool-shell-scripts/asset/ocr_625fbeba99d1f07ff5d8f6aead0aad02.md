specified in the script), which can be set explicitly within a crontab file. That could be quite tricky. . . . Lastly, you could add support for values such as @hourly or @reboot, special values in cron used to denote the common times scripts can run.

# #49 Ensuring that System cron Jobs Are Run

Until recently, Linux systems were all designed to run as servers—up 24 hours a day, 7 days a week, forever. You can see that implicit expectation in the design of the cron facility: there’s no point in scheduling jobs for 2:17 AM every Thursday if the system is shut down at 6:00 PM every night.

Yet many modern Unix and Linux users are running on desktops and laptops and therefore do shut down their systems at the end of the day. It can be quite alien to OS X users, for example, to leave their systems running overnight, let alone over a weekend or holiday.

This isn’t a big deal with user crontab entries, because those that don’t run due to shutdown schedules can be tweaked to ensure that they do eventually get invoked. The problem arises when the daily, weekly, and monthly system cron jobs that are part of the underlying system are not run at the specified times.

That’s the purpose of the script in Listing 6-11: to allow the administrator to invoke the daily, weekly, or monthly jobs directly from the command line, as needed.

# The Code

```
#!/bin/bash

# docron--Runs the daily, weekly, and monthly system cron jobs on a system
#   that's likely to be shut down during the usual time of day when the system
#   cron jobs would otherwise be scheduled to run.

rootcron="/etc/crontab"   # This is going to vary significantly based on
                           #   which version of Unix or Linux you've got.

if [ $# -ne 1 ]; then
  echo "Usage: $0 [daily|weekly|monthly]" >&2
  exit 1
fi

# If this script isn't being run by the administrator, fail out.
#  In earlier scripts, you saw USER and LOGNAME being tested, but in
#  this situation, we'll check the user ID value directly. Root = 0.

if [ "$(id -u)" -ne 0 ]; then
  # Or you can use $(whoami) != "root" here, as needed.
  echo "$0: Command must be run as 'root'" >&2
  exit 1
fi
```