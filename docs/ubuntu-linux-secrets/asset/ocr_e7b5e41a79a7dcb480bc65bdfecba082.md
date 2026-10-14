Fortunately, you don’t have to hunt for each of these log files individually. Ubuntu provides a handy utility that helps manage all of the log files from a single graphical interface.

![](bbox=[0.108, 0.023, 0.227, 0.293])

> **The log files used by the** `syslogd` **process are defined in the** `/etc/syslog.conf` **file. This file defines what type of log entries are stored in which log files.**
> 
> **Log entries are classified by a tiered system, from lowest to highest priority:**
> 
> - **debug:** application debugging messages
> - **info:** informational messages
> - **notice:** event notices from applications
> - **warning:** minor error messages
> - **err:** an error condition in an application
> - **crit:** a critical system error
> - **alert:** a system error that requires immediate action
> - **emerg:** an error that prevents the system from running
> 
> Some Linux distributions provide a single log file for handling critical and alert messages, but Ubuntu doesn’t use this technique. Instead, it separates log messages by source and importance.
> 
> For example, you’ll find four log files for logging mail activity on the Ubuntu system: `mail.err`, `mail.info`, `mail.log`, and `mail.warn`. Each log file contains messages for the specified log level for the mail system.

# The System Log Viewer

The System Log Viewer is a utility in the Administration menu (select System ➜ Administration ➜ System Log from the Panel menu). It allows you to quickly view all of the configured log files from a single location. Figure 18-4 shows the main System Log Viewer window.

The System Log Viewer window has three sections:

+   - **The log file list:** Lists the log files available to view. Log files with data that have been added since the System Log Viewer was started appear in bold.
+   - **The calendar:** Allows you to select a day from the log files to view. Ubuntu creates a new version of each log file each day. You can view any of the available daily log files by selecting the date in the calendar. Days with available log files appear in bold.
+   - **The log viewer:** Displays the contents of the selected log file.

The System Log Viewer uses *monitored mode* to watch the log files in real-time. This mode notifies you of new log file entries by displaying the log filename in bold in the log file list and making the new entries appear in bold in the log viewer. If your system is experiencing a problem that is quickly filling up the log file, you can disable monitored mode by selecting View ➜ Monitor from the menu bar.