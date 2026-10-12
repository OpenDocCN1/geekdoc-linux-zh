# LOGGING ERRORS

# Chapter 10

postrotate
    /usr/bin/killall -HUP httpd 2> /dev/null || true
endscript
}

The most important thing about this file is defining where the log file is stored. If you decide to compile your own release of Apache and not use the RPM program, you can easily substitute your new directory in place of the RPM directory and let the system rotate your newer logs as well. This is a hybrid solution for using system-automated tasks along with your own source code.

![](bbox=[0.45, 0.35, 0.55, 0.37])

The next-to-last section consists of the system-handling tasks, which are best left alone by users. Here the file /var/log/wtmp is rotated and certain permissions are altered for the purpose of limiting users from seeing or altering the contents of this file. In the last section, root can define any additional rotational schemes. Any custom-installed programs that use log files can also be rotated in this section. This is for those additional files that you have either defined or are installed later and require rotation. For example, any firewall log files or tracking software that outputs to a static file can be defined in this last section of the /etc/logrotate.conf file and thus allow the system to handle the task of rotating the files.

# Manually Rotating Logs

Other files require manual setup. This is best applied to log files or files that see frequent modifications. For example, at a previous place of employment I kept a copious /etc/mail/access list for handling virtual domains and their users. These are lists of specialized email users who belong to a virtual domain or one of many domains that can exist on a single Linux box. This list saw much use and many of the help desk employees frequently needed to add new users or modify existing users. With so many hands changing the record, there was always a chance that something could be mistakenly deleted or corrupted.

I created a simple script that would rotate out the log file and keep backup copies. This script provided me with five additional days of backup, which I could use to discover any errors. Though I also took preventive measures of