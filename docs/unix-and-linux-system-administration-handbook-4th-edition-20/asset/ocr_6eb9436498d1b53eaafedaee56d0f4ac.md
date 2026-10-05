# 11.7 EXERCISES

+   * E11.1 What are the main reasons for keeping old log files?

+   * E11.2 What is the difference between lastlog and wtmp? What is a reason-rotation policy for each?

+   * E11.3 Dissect and understand the following syslog.conf line:

```
notice:kern.debug:lpr.info:mail.crit:news /var/log/log/messages
```

+   * Does it seem sensible?

+   * E11.4 Look through your log file for entries from the SSH service. What events are logged when a login attempt is successful? What if a login attempt fails? What steps would you take to increase the logging verbosity of the SSH daemon

+   * E11.5 Many IT industry standards and regulations impose logging or audit-requirements. Choose one of these standards and discuss how you might tune a syslog configuration to achieve compliance.

+   * E11.6 Where would you find the boot log for your Linux machine? What issues affect logging at boot time? How does klogd solve these issues?

+   * E11.7 Investigate the logging policy at your site, including the log file rotation policy. How much disk space is dedicated to logging? How long are log files kept? Can you foresee circumstances in which your site's policy would not be adequate? What solution would you recommend? (Requires root access.)

+   * E11.8 Some log messages are extremely important and should be reviewed by an administrator immediately. What could you set up to make sure that this happens as quickly as possible?