# syslog Security

One of the most significant skills of sophisticated intruders is their ability to clean up all evidence that an attack has taken place. This is the electronic equivalent of a criminal using gloves at the scene of the crime, and it’s a constant source of frustration for those who make a living out of tracking down the actions of these intruders.

You should go to whatever lengths are necessary to make sure that you can safeguard some evidence that your system was tampered with. The problem is that it’s very difficult to guarantee that your log files are correct when attackers could be modifying them with their root privileges. You should take advantage of the syslog program’s ability to send a copy of all log events to a remote server.

For example, in order to send all your kernel, mail, and news messages to a remote syslog server (hostname “zurich”), add the following line to your /etc/syslog.conf configuration file:

```
kern.*, mail.*, news.*[TAB]@zurich
```

(Don’t forget that the syntax of this file calls for a tab character to be inserted between fields.)

After making this modification, you must send the -HUP (hang-up) signal to the syslog daemon to force it to read its configuration:

```
[ramon]$ sudo killall -HUP syslogd
```

Keep in mind, however, that some services may not be configured or able to log events via syslog. You should use cron to move those services’ log files to a remote server several times throughout the day—the more often the better.

# Filesystem Encryption

However strong your physical and system security measures are, you need to be ready for the time when a user gains access to some other user’s files. Cryptography is your last line of defense. By encrypting the contents of sensitive directories, users can protect the privacy of their data even after an intrusion has succeeded.

This section describes two different ways to do this, both of which are based on secret-key technology using standard encryption algorithms. Let’s take a look at each of them in more detail.