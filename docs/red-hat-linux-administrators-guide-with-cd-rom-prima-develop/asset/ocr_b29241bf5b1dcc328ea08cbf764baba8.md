# ## Setting Correct crontab Syntax

The manner in which cron jobs are implemented is important. Even though jobs are unique to each user, they still share the same syntax. The cron daemon recognizes a specific set of instructions and uses them to run the jobs as needed. The basic format is first to lay out the time in which the job needs to be performed and then give the command. It is customary also to explain the function of each cron job by placing a commented-out line at either the beginning or end of the job. Comments are lines that you don't want the program to read, but which serve as explanatory statements for other users. You usually indicate that a line is a comment by marking it with a pound sign (#). When reading the crontab file, the cron daemon will usually ignore these lines or the words following any pound sign on the same line.

The standard syntax for creating a crontab entry is as follows:

| minute | hour | day | month | weekday | command |
| :----- | :--- | :-- | :---- | :------ | :------ |
| 0–59 | 0–23 | 1–31 | 1–12 | 0–7 | /usr/local/bin/runme |


Some older UNIX systems provide an additional field that inputs the username for a particular function. Generally Red Hat doesn't provide such a field, but instead confines itself to the six-field format. The user field is sometimes found in the system's own crontab file, /etc/crontab.

Only certain numbers can be used for each field. Fields are separated by a single space, whereas multiple numbers in a field are grouped together with commas. As is customary with most UNIX systems, counting begins with zero. The only exception, in this instance, is in the weekday field, where both 0 and 7 equal Sunday and 1 equals Monday.

Generally, a tab separates the time fields from the command field. If the desired scheduling is for every day, then an asterisk is placed in the field instead of a number. Similar to a wildcard feature, the asterisk represents all possible numbers.

TIP
Be mindful of changes in time, such as daylight savings time, that might play havoc with some scheduling and can cause programs to run either twice or not at all. Red Hat Linux compensates for such changes if you specify them during the install, but it is best to double-check that your computer's time is in sync with standard time.