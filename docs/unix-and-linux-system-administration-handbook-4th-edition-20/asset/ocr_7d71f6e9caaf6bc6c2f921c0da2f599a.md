# Debugging

log_file_path = syslog : /var/log/exim_%s

would log to syslog (with facility "mail") to the files exim_main, exim_reject, and exim_panic in the /var/log directory. Exim submits the main log entries to syslog at priority info, the reject entries at priority notice, and the panic entries at priority alert.

The main log contains one line for the arrival and delivery of each message. It can be summarized by the Perl script eximstats, included in the Exim distribution.
The reject log records information on the messages that have been rejected for policy reasons: malware, spam, etc. It includes the summary line for the message from the main log and also the original headers of the message that was rejected. If you change your policies, check the reject log to make sure that all is still well.

The panic log is for serious errors in the software, exim writes here before it gives up. The panic log should not exist in the absence of problems. Ask cron to check for you and if it exists, the problem that caused the panic and delete the file. Exim will create it when the next panic-worthy situation arises.

When debugging, you can increase the amount and type of data logged with the log_selector option. For example:

```
log_selector = +smtp_connection +snmp_incomplete_transaction + ...
```

The categories that can be included or excluded by the log_selector mechanism are listed in the Exim specification, in the section called "Log files" toward the end. There are about 35 possibilities, including +all, which will really fill your disks!

exim also keeps a temporary log for each message it handles. It is named with the message ID and is in /var/spool/exim/mslog. If you are having trouble with a particular destination, you should check there.

# Debugging

Exim has powerful debugging aids. You can configure the amount of information you want to see about each potential debugging topic. exim -d tells exim to get into debugging mode, which stays in the foreground and does not keep logs of itself. You can add specific debugging categories to the -d with a or - in order requests debugging output extra details regarding string expansions and ACL requests extra details regarding ACL interpretation. (These two categories are common problems.) You can tune more than 30 categories of debugging information; see the page for a list.

A common technique when debugging mail systems is to start the MTA on a non-standard port and then talk to it through telnet. For example, to start exim in daemon mode, listening on port 26, with debugging info turned on, use

```
$ exim -d -OX 26 -bd
```

![](bbox=[0.953, 0.223, 0.993, 0.333])