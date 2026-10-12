# # Reading your logs

You are ultimately your own best intrusion-detection system (IDS). Log files store information about nearly every one of your Fedora Core systems. Reading your logs lets you discover what has been happening on your computer — and it’s one way to detect intrusions.

Unfortunately, exploring log files is somewhat akin to reading tea leaves. No mechanical method exists for sifting through log-files. You have to look for unusual and suspicious occurrences. As you read more, you realize what is usual and, of course, unusual. Experience counts for a great deal when you’re an IDS.

Red Hat provides two good systems for viewing log files. The e-mail-based **Logwatch** log-alert system sifts through the log files in `var/log` and e-mails the root user any alerts or errors. You can configure the Logwatch operational parameters to better fit your operation. However, the default works well at alerting you to the happenings on your computer. The Red Hat **Logviewer** graphical utility provides one-stop shopping for all standard log files. This manual tool helps you to remember which log files to look at.

# ## Using Logwatch

Logwatch, installed by default during the Red Hat installation process, is a Perl script that is run nightly by cron. It reads through every log file in the `var/log` directory and picks out items that it thinks are interesting.

The Logwatch Perl script is in `/etc/log.d/scripts/logwatch.pl`. The soft link, 00-logwatch, in the `/etc/cron.daily` directory, directs the cron system to run the script nightly.

Logwatch is controlled by the `/etc/log.d/conf/logwatch.conf` file. This file controls such options as who is e-mailed the results. The logwatch configuration file is self-documented and simple to configure.

# ## Using Logviewer

Logviewer is a simple utility designed to display any of the standard Fedora Core log files in the `var/log` directory. Logviewer displays by default the raw log information and leaves sifting out suspicious entries to your eyes.

Nothing is special about Logviewer, except it helps you access common log files and look at their data. Don’t underestimate the value of that simple assistance. Although our busy lives make reading log files a difficult task, it’s one of those mind-numbing but necessary jobs — boring but essential!