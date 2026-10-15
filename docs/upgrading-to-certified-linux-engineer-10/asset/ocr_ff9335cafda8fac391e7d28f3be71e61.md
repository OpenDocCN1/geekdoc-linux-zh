# Exercise 13-1 Log to a Remote Host

In this exercise you work with a partner. Decide who will send messages and who will receive them. (If both of you send and receive messages to each other, you might create an endless loop.)

On the loghost configure syslog-ng to receive log messages from other hosts.

On the client configure syslog-ng to send log messages to the loghost.

# Detailed Steps to Complete this Exercise

+   - Part I: On the Computer Receiving Messages
+   - Part II: On the Computer Sending Messages

# Part I: On the Computer Receiving Messages

Do the following:

+   1. Open a terminal window and su - to root (password novell).

+   2. Open the file /etc/syslog-ng/syslog-ng.conf.in in vi.

Add another source section after the source src section, as in the following:

```
source network {
    udp(ip("0.0.0.0") port(514));
};
```

+   3. At the end of the file, add a destination and a log entry to log messages that arrive via the network:

```
destination digiair { file("/var/log/$HOST"); };
log { source(network); destination(digiair); };
```

+   4. Save the file and quit vi.