# Table 12.9 **Logging levels available in sendmail (continued).**

| Level | Logs |
| :--- | :--- |
| 8 | Mail delivery output and information about rebuilding internally used **sendmail** databases |
| 9 | Deferred messages (the default) |
| 10 | Expansion of the various **sendmail** database files |
| 11 | NIS errors and finished jobs |
| 12 | SMTP connections |
| 13 | Errors due to file permission problems or bad links |
| 14 | Refused connections |
| 15 | SMTP commands |

+   4. Press the Esc key, and then type "ZZ" to save and close the file.
+   5. Type "/etc/rc.d/init.d/sendmail restart" to load the new configuration file.

# ### Reducing Server Load

If your mail server continually has problems managing the traffic that passes through it, do the following:

+   1. Log in to the mail server as root.
+   2. Type "vi /etc/sendmail.cf" to open the **sendmail** configuration file, if you don't already have the file open.
+   3. Type "load average" and press Enter to jump down to the text you want to look at. It should look similar to the following:

```
```
# load average at which we just queue messages
#0 QueueLA=8

# load average at which we refuse connections
#0 RefuseLA=12

# maximum number of children we allow at one time
#0 MaxDaemonChildren=12

# maximum number of new connections per second
#0 ConnectionRateThrottle=3
```
```

+   4. You can choose to try the defaults given for one or more options by deleting the hash mark in front of the appropriate **O**, so that it is no longer commented out.