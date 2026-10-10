# Scheduling Jobs in Linux

As a system administrator, you may have to run some programs automati- cally at regular intervals or execute one or more commands at a specified time in the future. Your Linux system includes the facilities to schedule jobs to run at any future date or time you want. You can also set up the system to perform a task periodically or just once. Here are some typical tasks you can perform by scheduling jobs on your Linux system:

+   - Back up the files in the middle of the night.
+   - Download large files in the early morning when the system isn't busy.
+   - Send yourself messages as reminders of meetings.
+   - Analyze system logs periodically and look for any abnormal activities.

You can set up these jobs by using the `at` command or the `crontab` facility of Linux. In the next few sections, I introduce these job-scheduling features of Linux.

# Scheduling one-time jobs

If you want to run one or more commands at a later time, you can use the `at` command. The `atd` daemon — a program designed to process jobs sub- mitted using `at` — runs your commands at the specified time and mails the output to you.

![](bbox=[0.12, 0.55, 0.2, 0.64])

Before you try the `at` command, you need to know that the following con- figuration files control which users can schedule tasks using the `at` command:

+   - `/etc/at.allow` contains the names of the users who may submit jobs using the `at` command.
+   - `/etc/at.deny` contains the names of users not allowed to submit jobs using the `at` command.

If these files aren't present, or if you find an empty `/etc/at.deny` file, any user can submit jobs by using the `at` command. The default in Linux is an empty `/etc/at.deny` file; with this default in place, anyone can use the `at` command. If you don't want some users to use `at`, simply list their user- names in the `/etc/at.deny` file.