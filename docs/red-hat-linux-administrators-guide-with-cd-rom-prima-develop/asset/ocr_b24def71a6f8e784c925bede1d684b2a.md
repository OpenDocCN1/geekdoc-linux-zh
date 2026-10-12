# # ADMINISTERING THE SYSTEM

command and then check the bash_history log file common to nearly every user's directory. In one of myriad locations, depending upon the situation, I can trace the cause of the error to either a user or the system.

There are also varying levels of logging. Most system logs are configurable and can be set to generate a minimal number of files. If you need more information, you can set system logs to the debug level, and thus generate extremely verbose logs. The syntax for the Red Hat Linux syslog.conf file, which determines the logging level, is fairly standard across most all Linux distributions. How those options listed under this configuration file are implemented vary. Some programs suggest an extremely high debug level whereas others require only the most minimal of logging information. However, I suggest allowing all programs to generate at least a minimal number of logs if only to ensure that the system files are operating correctly.

Table 10.1 lists examples of fairly standard abbreviations of logging levels used for most system files. The levels range from the fewest files generated to the most effusive.

These levels are program-specific and can be set or reset depending upon the program in question. Often, when changing these values, you must either restart the processes or send their PID a hangup or -HUP signal. This restart causes the process to reread the system configuration and effect the logging level.

You can read more descriptive explanations for each of these different levels in the syslog and syslog.conf man pages.

| **Table 10.1** The Different Logging Levels Available | | | | | | | | |
|---|---|---|---|---|---|---|---|---|
| **Level** | **Description** | | | | | | | |
| emerg | Sends emergency messages for panic situations | | | | | | | |
| alert | Posts an alert if the situation is urgent | | | | | | | |
| crit | Notifies the administrator if critical errors are detected | | | | | | | |
| err | Sends general error messages | | | | | | | |
| warn | Warns of unusual conditions | | | | | | | |
| notice | Informs of system notices | | | | | | | |
| info | Sends verbose informative messages | | | | | | | |
| debug | Generates extremely verbose messages for debugging purposes | | | | | | | |