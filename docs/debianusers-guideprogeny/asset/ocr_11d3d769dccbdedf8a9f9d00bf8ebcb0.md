Logs are generally found in the /var/log directory. Their purposes are usually obvious: cron.log lists messages from crontab, daemon.log lists messages from daemons, and so on. The general log file is /var/log/messages. See “Standard Log Files,” page 257.

Logs are controlled by syslogd daemon. This daemon starts almost as soon as your computer starts, and records most events that happen on the system. It is configured in the /etc/syslog.conf file.

You can view logs from either the desktop or the command line. Information is in four column in standard log files.

A few log files are not in the standard format. They cannot be read by using desktop tools, nor, in several cases, by using the standard command line viewing tools. See “Non-Standard Log Files,” page 259

# ## Reading Standard Log Files From the Desktop

+   1 From the menu, select Programs > System log monitor. The System log viewer window opens.

![](bbox=[0.05, 0.54, 0.95, 0.72])

+   2 Choose a log to display. Select File > Open log. The default is /var/log/messages.

+   3 If necessary, select an item from the View menu: