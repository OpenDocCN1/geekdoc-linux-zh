
## Server Side Configuration of Syslog-ng

To receive messages, syslog-ng has to listen on a port, usually port 514. Unlike syslogd, which only supports UDP connections, syslog-ng also supports TCP.

To bind to a port, you have to add a line within a source section. You can either add it to the existing source src section, or create a new one, as in the following:

```
source network {
    udp("10.0.0.254") port(514);
};
```

Using 0.0.0.0 as the IP address causes syslog-ng to bind to all available interfaces.

Then a destination and a log entry are required:

```
destination digiair { file("/var/log/$HOST"); };
log { source(network); destination(digiair); };
```

The first line defines the destination digiair; each host’s log entries get written to a file with the hostname as file name. The log entry directs messages from the source network to the destination digiair.

## Exercise 13-1 Log to a Remote Host

In this exercise you work with a partner. Decide who will send messages and who will receive them. (If both of you send and receive messages to each other, you might create an endless loop.)

On the loghost configure syslog-ng to receive log messages from other hosts.

On the client configure syslog-ng to send log messages to the loghost.

## Detailed Steps to Complete this Exercise

- Part I: On the Computer Receiving Messages
- Part II: On the Computer Sending Messages

## Part I: On the Computer Receiving Messages

Do the following:

- 1. Open a terminal window and su - to root (password novell).
- 2. Open the file /etc/syslog-ng/syslog-ng.conf.in in vi.

Add another source section after the source src section, as in the following:

```
source network {
    udp(ip("0.0.0.0") port(514));
};
```

- 3. At the end of the file, add a destination and a log entry to log messages that arrive via the network:

```
destination digiair { file("/var/log/$HOST"); };
log { source(network); destination(digiair); };
```

- 4. Save the file and quit vi.
- 5. Run SuSEconfig:
  SuSEconfig --module syslog-ng
- 6. View /var/log/messages by entering
  tail -f /var/log/messages
  You should see a message that syslog-ng initialized its new configuration.
- 7. Quit tail by pressing ctrl+c.

Once messages are sent from the client, syslog-ng will create a file /var/log/daxx, for instance, /var/log/da20. View this file by entering:
tail -f /var/log/daxx
(Replace daxx by the hostname of your neighbor's computer.)

## Part II: On the Computer Sending Messages

Do the following:

- 1. Open a terminal window and su - to root (password novell).
- 2. Open the file /etc/syslog-ng/syslog-ng.conf.in in vi.

At the end of the file, add a destination and a log entry to send messages to the loghost:

```
destination tologhost { udp("daxx" port(514)); };
log { source(src); destination(tologhost); };
```

Replace daxx in the above example with the hostname of the loghost.

- 3. Save the file and quit vi.
- 4. Run SuSEconfig:
  SuSEconfig --module syslog-ng

SuSEconfig causes syslog-ng to reread its configuration, so there is no need to do this in an extra step.

- 5. Create log entries by using su - in a terminal window or by using the program logger. The entries should appear on the loghost.

***(End of Exercise)***

## Summary

| Objective | Summary |
|---|---|
| 1. Apply Security Updates | To get and apply security updates for SUSE Linux Enterprise Server 10, you need to do the following: <br>- Register SLES 10 at http://www.novell.com/center/ <br>- Download and apply updates with YOU. |
| 2. Understand Recent Match of iptables | The recent match can be used to dynamically create a list of IP addresses and create rules regarding those IP addresses. <br>The information is kept in /proc/net/ipt_recent/DEFAULT, unless you specify a different name. |
| 3. Log to a Remote Host | Logging to a log host prevents manipulation of log files after an intrusion. <br>The information in log files is only useful if someone sees it and acts accordingly. <br>Several programs, like logcheck, logsurfer, or custom scripts exist to help find relevant log entries. |
