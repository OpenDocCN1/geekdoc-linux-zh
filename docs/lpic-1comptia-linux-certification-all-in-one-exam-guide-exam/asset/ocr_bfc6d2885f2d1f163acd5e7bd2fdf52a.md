+   You can also create system cron jobs by creating a crontab file in the /etc/cron.d directory.

+   A crontab file contains one line for each command that is to be run; each line contains six fields:
+       1 Minutes
+       2 Hour
+       3 Day
+       4 Month
+       5 Day of the week
+       6 Command to be run

+   You can use cron to create user jobs.

+   User cron jobs are stored in /var/spool/cron/tabs.

+   A user can create a crontab file by entering crontab -e at the shell prompt.

+   After creating the crontab file, you can use the crontab -l command to view your crontab file contents.

+   You can use the crontab -r command to remove your crontab file.

# ## Questions

+   1. Which of the following best describes a multitasking operating system?
+       A. An operating system that can run multiple tasks concurrently on multiple CPUs
+       B. An operating system that can run a single task concurrently across multiple CPUs
+       C. An operating system that runs multiple tasks concurrently on a single CPU
+       D. An operating system that constantly switches CPU time between loaded processes

+   2. You just entered vi at the shell prompt. What type of process was created on your Linux system?
+       A. User
+       B. System
+       C. Daemon
+       D. System V

+   3. Your current shell session has a PID of 3456. You run the su command to change to the root user account. The su process has a PID of 3457. You then run vi from the shell prompt as root. The vi process has a PID of 3458. What is the PPID of the vi process?
+       A. 3456
+       B. 3457