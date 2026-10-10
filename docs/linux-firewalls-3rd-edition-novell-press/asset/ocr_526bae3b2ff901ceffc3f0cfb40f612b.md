# CHAPTER 12: Filesystem Integrity

The general AIDE configuration option called report_url1 configures how output is displayed. By default, output is displayed to STDOUT. Output can be displayed to any or all of the following:

+   STDOUT (default)
+   * STDERR
+   * Text file
+   * File descriptor

Of these four possibilities, STDOUT, STDERR, and text file are of interest. Future versions of AIDE may include output configurations for automated email and automated output to the SYSLOG facility.

Of particular interest is the text file type of output for AIDE. This output type is specified using this configuration line:

```
report_url1=file:/path>/<filename>
```

For example, to configure AIDE reports to go to a file called aiderreport.txt in the /var/log/aide directory that you create, you would use this configuration option in the AIDE configuration file:

```
report_url1=file:/var/log/aide/aiderreport.txt
```

However, the report_url1 configuration option is only one means for getting output into a file. Because you're running the AIDE report from cron, you could also simply redirect the output to a file. For example, recall the crontab entry shown earlier in the chapter:

```
0 2 * * * /usr/local/bin/aide --check
```

You could alter that cron entry to redirect the output to a file. Doing so would cause all output to go to that file and would also enable additional features such as date-based naming. This can be done with a little shell trick using runquotes (sometimes called a backtick, usually found with the tilde [~] on the keyboard). Here's the new cron entry:

```
0 2 * * * /usr/local/bin/aide --check > /var/log/aide/aiderreport-- date +%m%dY'' .txt
```

Now the AIDE report will run and redirect STDOUT to a file called /var/log/aide/aiderreport-<date>.txt

For example, for a report run on March 12, 2004, the file would be called /var/log/aide/aiderreport-03122004.txt