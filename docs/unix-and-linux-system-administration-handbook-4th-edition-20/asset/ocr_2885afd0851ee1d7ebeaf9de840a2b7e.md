# Chapter 9

# Periodic Processes

hand, whereas /etc/cron.d is provided as a depot into which software packages can install any crontab entries they might need. Files in /etc/cron.d are by named after the packages that they install, but cron doesn't care about or enforce this convention.

Time ranges in Vixie-cron crontabs can include a step value. For example, the series 0,3,6,9,12,15,18 can be written more concisely as 0-18/3. You can also use three-letter mnemonics for the names of months and days, but not in combination ranges. As far as we know, this feature works only with English names.

You can specify environment variables and their values in a Vixie-cron cron file. See the cron(5) man page for more details.

Vixie-cron logs its activities through syslog using the facility "cron", with most messages submitted at level "info". Default syslog configurations generally send cron log data to its file.

For reasons that are unclear, cron has been renamed cron on Red Hat. But it is still the same Vixie-cron we know and love.

# 9.5 COMMON USES FOR CRON

A number of standard tasks are especially suited for invocation by cron, and these usually make up the bulk of the material in root's crontab. In this section we look at a few common chores and crontab lines used to implement them.

Systems often come with crontab entries installed. If you want to deactivate the standard entries, comment them out by inserting a pound sign) at the beginning of each file. Don't delete them; you might want to refer to them.

In addition to /etc/cron.d mechanism, Linux distributions also reinstall crontab entries that run the scripts in a set of well-known directories, providing another way for software packages to install jobs without editing of a crontab file. For example, scripts in /etc/cron.weekly are run once a day, and you can put files in these directories by hand.

Many sites have experienced subtle but recurrent glitches that occur cause administrators have configured cron to run the same command on hundreds of machines at exactly the same time. Clock synchronization with NTP accelerates the problem. It is easy to fix with a random delay script or config file adjustment, but it can be tricky to diagnose because the symptoms solve quickly and completely.

# Simple reminders

It's not going to put Google Calendar out of business, but cron can be quite useful in its own geeky way for simple reminders: birthdays, due dates, recurrent tasks, etc. That's especially true when the reminder process has to integrate with other home-grown software such as a trouble ticket manager.