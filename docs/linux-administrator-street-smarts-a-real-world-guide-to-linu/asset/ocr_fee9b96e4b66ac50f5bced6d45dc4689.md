should review Phase 1's coverage of scripting and read the **man** pages for `grep` and `cut`. These two commands will enable you to extract any data you like from the system summary commands; you can then recombine your extracted data into convenient columns.

# Criteria for Completion

To complete this task, you should have obtained baseline performance data on your CPU load average, free memory, disk speed, and disk free space. With this information recorded in your system log book, you can begin planning how to monitor such data over the long term. Such monitoring will enable you to spot trouble before it occurs.

# Task 4.3: Use System Log Files

You're not the only one who should be creating logs concerning system activities: Your computer should, too. Linux systems run a *log daemon* or *system logger*, which is a tool that copies messages from other processes (mostly servers, but also the kernel and occasionally non-server processes) to log files. These log files typically reside in the `/var/log` directory. Log file street smarts entails the ability to do three things with log files: configure the log daemon to log data in appropriate files, rotate the log files so they don't fill your hard disk, and interpret the data found in your log files.

# Scenario

You need to make several changes to your system's logging facility. Specifically, you want to display emergency log entries on the consoles of logged-in users, log all kernel activities to the `/var/log/kernel` file, and send non-trivial kernel events to a second system (`logger.pangaea.edu`). You also want to modify your system's log rotation schedule to keep old compressed log files for longer than it currently does and to rotate the `/var/log/kernel` file. Once these tasks are completed, you need to examine current log files to check on your mail server's activities over the past day or so because several messages that should have arrived on the system have not appeared in users' inboxes.

# Scope of Task

This task involves three distinct subtasks, each of which is fairly complex in and of itself: modifying system logging, modifying log file rotation, and examining current log files.

# Duration

This task should take about an hour to complete. Once you're familiar with the procedures involved, you can perform individual log file tasks in considerably less time. Examining log files is particularly speedy, although if you need to trace activity over time, you can spend hours porusing log files.