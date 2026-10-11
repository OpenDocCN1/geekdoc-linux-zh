| **Log Filename** | **Purpose** |
|---|---|
| /var/log/wtmp | Stores the login times and duration for each user. This information is used by the command last. The last command shows all users listed in the file, and users may be listed more than once. |
| /var/log/utmp | Stores information on currently logged-in users. The who, w, and f inger commands use this information. The who and w commands display who is currently logged into the system. The w command also shows the time that the user logged in. The f inger command displays the comment field from the user's entry in /etc/passwd. |
| /var/log/lastlog | Stores login times for users. The lastlog command uses this information. If a user has never logged in before, that is also displayed. By default, entries are ordered by userid. The -t option can be used to show all login times for the specified number of days. The -u option displays the user's last login. |

Exam Tip Be sure to know which command uses which file for the exam.

# ## Rotating system logs

Depending on which data you log, your log files can grow to be quite large seemingly overnight. Log rotation can be very helpful in maintaining a manageable size for your log files. You simply need to decide which data you want to save and move it to another location. Moving the data to a new location will free up space in the default location, but you still have to deal with the old log files taking up space on your system. It is useful to have a standard regarding which log files to keep and for how long. Depending on your situation, you may want to track certain data over long periods of time. Whatever your needs may be, Linux includes a utility to help you manage your log files. The program /usr/sbin/logrotate is used to rotate the log files. Older logs are copied to a new location and new log files are created. The default log file used by logrotate is the /etc/logrotate.conf file. This file is well documented with comments and is configured by default to suit many administrative needs. However, other configuration files can be used by using the following command:

```
logrotate [options] config_file
```