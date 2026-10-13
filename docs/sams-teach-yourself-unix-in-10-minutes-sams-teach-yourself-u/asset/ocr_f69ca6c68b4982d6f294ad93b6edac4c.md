# SCHEDULING COMMANDS: at AND cron

With the capability to run processes in the background comes the ability to schedule processes to run at certain times—even when you're not logged into the computer. There are two ways to set up your UNIX computer to run a command at a certain time. Unfortunately, these might be disabled, depending on the level of control your administrator has chosen to implement. Allowing users to schedule commands for any time they want can be a bit dangerous. The two commands that you'll want to check out are cronbat and at: they are described as follows:

+   - cron—Runs constantly on your system, and is probably already in use to run log rotation and various cleanup commands. You can create a personal crontab file that holds information about the interval that you want a command to run, and then use the crontab <filename> command to add your request to the system's crontab file. cron enables you to run commands in intervals as small as a second or as long as a year. With some UNIX versions you can use crontab -e to bring up your currently set crontab entries directly into an editor as well.
+   - at—Enables you to run a command once, rather than at a repeating interval. This is useful if there is a processor-intensive task that you want to run after business hours so that other tasks aren't affected.

Before you attempt to use either crontab or at, check with your system administrator. Scheduling processes blindly can affect other users and degrade system performance tremendously if inappropriate processes are scheduled to run simultaneously.

# X WINDOWS PROCESSES

If you've been playing around in the X Window System, it is probably obvious that you can run multiple programs at a single time. Each of these programs runs with its own PID, just as you'd expect. Each of these programs is launched separately, so they are actually already sharing processor time—no one program is in the foreground or background. You can