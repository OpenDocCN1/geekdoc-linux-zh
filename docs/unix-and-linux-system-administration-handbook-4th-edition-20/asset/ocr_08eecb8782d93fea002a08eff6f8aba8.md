# Chapter 11 Syslog and Log Files

The action field tells syslog what to do with each message. The options are listed in Table 11.5.

# Table 11.5 Syslog actions

| Action | Meaning |
| --- | --- |
| filename | Appends the message to a file on the local machine |
| @hostname | Forwards the message to the syslog on hostname |
| @ipaddress | Forwards the message to the syslog on host ipaddress |
| |fifone | Writes the message to the named pipe fifone * |
| user1,user2,... | Writes the message to the screens of users who are logged in |
| * | Writes the message to all users who are currently logged in

+   a. See mkfifo for more information (Linux versions of syslog only).

If a filename (or fifone) action is used, the name should be an absolute path. If you specify a nonexistent filename on a Linux system, syslog will create the file when a message is first directed to it. On other systems, the file must already exist; syslog will not create it.

On Linux distributions, you can prefix a filename action with a dash to indicate that the filesystem is not synced after each log entry. syncing helps preserve as much information as possible in the event of a crash, but for busy files it can be devastating in system performance. We recommend the dashes (and thereby inhibiting syncing) as a matter of course. Remove the dashes only temporarily when investigating a problem that is causing kernel panics.

If you specify a hostname in lieu of an IP address, it must course be resolvable through a translation mechanism such as DNS or NIS.

Solaris syslog implementation runs the syslog.conf file through the m4 macro preprocessor. Check your page and use quotes literally so that your configuration matches what you want. For example, you must quote anything that is an m4 keyword or contains a comma. Here is a typical m4-style example:

```
auth.notice  ifdef([HOSTNAME], '/var/log/authlog', `localhost`)
```

Note that the quotes used are the back-tick and the single apostrophe. This directs messages to the file /var/log/authlog if LOGHOST is not defined. Otherwise, messages are forwarded to the machine host. m4'ifdef statements are very powerful; they allow sysadmins to create a single syslog.conf that be used on all machines.

Although multiple facilities and levels are allowed in a selector, there is no provision for multiple actions. To send a message to two places (such as to a local file and to a central logging host), you simply include two lines in the configuration file that have the same selectors.