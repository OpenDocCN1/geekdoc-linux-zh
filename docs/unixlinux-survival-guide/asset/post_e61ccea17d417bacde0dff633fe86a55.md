
## TABLE 5.2 syslog Facility Levels

| Level | Description |
|-------|-------------|
| emerg | The highest level a message can use; a message with this level is usually broadcasted to all users of the system. These are so-called panic-conditions. |
| alert | This level is used for messages that require immediate attention, but are not as severe as emerg. A good analogy would be emerg = "The house is collapsing." and alert = "If no one does something about this, then the house will collapse." |
| crit | Used for critical errors, like a failing hard disk. |
| err | Used for all other error conditions not covered by the previous three levels. |
| warning | Used for warnings of a more general nature. |
| notice | Used for conditions that would not be considered as error, but need attention nevertheless. |
| info | Informational messages. |
| debug | Used to allow a program to communicate while it is debugged. |
| none | A special case, this level can be used to suppress all messages of a given facility, for example, news.none instructs syslog to ignore all messages sent by the news facility. |

The table should clear things up a bit. If you would activate auth.info in syslog.conf, for example, then all messages with auth.notice, auth.warning, auth.err, auth.crit, auth.alert, and auth.emerg would be included automatically. Telling syslog what you are interested in is just part of the configuration; you need to tell the program where to store the messages as well (see Table 5.3).

## TABLE 5.3 Telling syslog Where to Store Messages

| Target | Example |
|--------|---------|
| A filename instructs syslog to store the message in the given file. The file has to exist, though. The message would disappear otherwise. | /var/adm/messages |
| The name of another system denoted by the @ sign. That system needs to be configured in a way that it is able to receive the sent messages. This approach allows you to | @companyloghost |

```
user.emerg				*

# log what the authentication system is doing
auth.info					/var/log/authlog

# local facilities
# local1 is used for the baseline skripts
local1.info				/var/log/baselinelog

# local2 - local7 unused at the moment
# if used, document usage here and in system docs
```

The example in Listing 5.11 contains some special cases that warrant an explanation. The instruction mark.debug /var/adm/messages means to write a message with the contents -- MARK -- to /var/adm/messages. The interval (20 minutes) is usually compiled into the syslog binary. There are two reasons for that configuration. First, there will be a message every 20 minutes, regardless of system load. Machines with a very low load level usually write only once in a while to the syslog otherwise; this setting allows you to see if the syslog process is still running. Second, the command grep MARK /var/adm/messages should show a continuous list of the marking entries, thus allowing you to determine if syslog was up and running all the time. If an intruder tried to hide his presence by disabling syslog or modifying the log files, then there is a slight possibility that one of the markings is missing. This is not a real monitor, but every detail counts. The entry user.emerg seems to overdo it a little, but if a program starts to behave erratically in user space or even crashes, then all users of the system should know about it and decide if they need the presence of the program. The facility local1 is used for the messages of the baselining-scripts. Remember: Listing 3.19 used user.crit, but only for one reason; this facility usually writes messages with crit in the system-wide log file, thus making sure that the command works in the examples. Because you know now how to customize the behavior of syslog, you should make use of the local0-7 facilities.

Here are some hints for the configuration of syslog. You should always make sure to create the files to be written to with the command touch if they do not exist; syslog does not create files. Test changes to syslog.conf to avoid losing important messages. The program will re-read the configuration either if it is restarted or if you send the HUP signal to the process. You should always test a new configuration by sending a message to the changed or added facility via the logger program. If this test should fail, you should try to correct the error and test again. If you cannot find the error, you should enable the old, working configuration and test the non-working configuration on a test system with the same OS release. One hint for finding bugs in this configuration: typos become apparent when you type the configuration again, making a copy to find the bugs usually does not help.
