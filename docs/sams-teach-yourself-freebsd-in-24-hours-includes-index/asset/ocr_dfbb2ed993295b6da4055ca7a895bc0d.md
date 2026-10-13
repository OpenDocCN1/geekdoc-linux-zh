6. If I set a certain facility in syslogd to my username, what happens when that facility is triggered?

+   A. Messages from that facility will be emailed to you.
+   B. Messages from that facility will be printed to any console where you are logged in.
+   C. Messages from that facility will be appended to /var/log/syslog.<user-name>.
+   D. Messages from that facility will vanish into the ether.

# Quiz Answers

+   1. The correct answer is D.
+   2. The correct answer is B.
+   3. The correct answer is D.
+   4. The correct answer is A.
+   5. The correct answer is D. Remember, your changed configuration doesn't take effect until you restart the daemon and force it to reread the config file.
+   6. The correct answer is B.

# Exercises

+   1. Reconfigure syslogd so that all warning messages from all services are directed into a file called /var/log/warn.log.
+   2. Use inetd to disable Telnet connections. Now send out a message to anybody who might be using your machine: Telnet is no longer allowed; SSH is now the only way to access your machine via a remote terminal. It's not just a good idea, it's now the law—your law!
+   3. Use /etc/rc.conf to synchronize your system's time via NTP. Hint: use the ntpdate_enable statement. A good NTP server to use is tick.usno.navy.mil.