
some other means, such as your network monitoring system. On such a system, disable the periodic(8) checks in /etc/crontab.

While these daily reports are useful, they don't tell the whole story. Logs give a much more complete picture.

## Logging with syslogd

The FreeBSD logging system is terribly useful. Any Unix-like operating system allows you to log almost anything at almost any level of detail. While you'll find default system logging hooks for the most common system resources, you can choose a logging configuration that meets your needs. Almost all programs integrate with the logging daemon, syslogd(8).

The syslog protocol works through messages. Programs send individual messages, which the syslog daemon syslogd(8) catches and processes. syslogd(8) handles each message according to its facility and priority level, both of which client programs assign to messages. You must understand both facilities and levels to manage system logs.

### Facilities

A *facility* is a tag indicating the source of a log entry. This is an arbitrary label, just a text string used to sort one program from another. In most cases, each program that needs a unique uses a unique facility. Many programs or protocols have facilities dedicated to them—for example, FTP is such a common protocol that syslogd(8) has a special facility just for it. Syslogd also supports a variety of generic facilities that you can assign to any program.

Here are the standard facilities and the types of information they're used for.

- **auth**: Public information about user authorization, such as when people logged in or used su(1).
- **authpriv**: Private information about user authorization, accessible only to root.
- **console**: Messages normally printed to the system console.
- **cron**: Messages from the system process scheduler.
- **daemon**: A catch-all for all system daemons without other explicit handlers.
- **ftp**: Messages from FTP and TFTP servers.
- **kern**: Messages from the kernel.
- **lpr**: Messages from the printing system.
- **mail**: Mail system messages.
- **mark**: This facility puts an entry into the log every 20 minutes. This is useful when combined with another log.
- **news**: Messages from the Usenet News daemons.
- **ntp**: Network Time Protocol messages.
- **security**: Messages from security programs, such as pfctl(8).
- **syslog**: Messages from the log system about the log system itself. Don't log when you log, however, as that just makes you dizzy.
- **user**: The catch-all message facility. If a userland program doesn't specify a logging facility, it uses this.
- **uucp**: Messages from the Unix-to-Unix Copy Protocol. This is a piece of pre-internet Unix history that you'll probably never encounter.
- **local0** through **local7**: These are provided for the sysadmin. Many programs have an option to set a logging facility; choose one of these if at all possible. For example, you might tell your customer service system to log to local0.

While most programs have sensible defaults, it's your job as the sysadmin to manage which programs log to which facility.

### Levels

A log message's *level* represents its relative importance. While programs send all of their logging data to syslogd, most systems record only the important stuff that syslogd receives and discard the rest. Of course, one person’s trivia is another’s vital data, and that’s where levels come in.

The syslog protocol offers eight levels. Use these levels to tell syslog what to record and what to discard. The levels are, in order from most to least important:

- **emerg**: System panic. Messages flash on every terminal. The computer is basically hosed. You don’t even have to reboot—the system is doing it for you.
- **crit**: Critical errors include things such as bad blocks on a hard drive or serious software issues. You can continue to run as is, if you’re brave.
- **alert**: This is bad, but not an emergency. The system can continue to function, but this error should be attended to immediately.
- **err**: These are errors that require attention at some point, but they won’t destroy the system.
- **warning**: These are miscellaneous warnings that probably won’t stop the program that issued them from working just as it always has.
- **notice**: This includes general information that probably doesn’t require action on your part, such as daemon startup and shutdown.
- **info**: This includes program information, such as individual transactions in a mail server.
- **debug**: This level is usually only of use to programmers and occasionally to sysadmins who are trying to figure out why a program behaves as it does. Debugging logs can contain whatever information the programmer considered necessary to debug the code, which might include information that violates user privacy.
- **none**: This means, “Don’t log anything from this facility.” It’s most commonly used to exclude information from wildcard entries, as we’ll see shortly.

By combining level with priority, you can categorize messages quite narrowly and treat each according to your needs.

## Processing Messages with syslogd(8)

The `syslogd(8)` daemon catches messages from the network and compares them with entries in `/etc/syslog.conf` or files in `/etc/syslog.d/`. Files in `/etc/syslog.d/` are for your own entries and add-on programs, while `/etc/syslog.conf` is for integrated system programs. Syslogd only reads `/etc/syslog.d/` files ending in `.conf`. Both files have the same format, but I’ll refer to `/etc/syslog.conf` for clarity. That file has two columns; the first describes the log message, either by facility and level, or by program name. The second tells `syslogd(8)` what to do when a log message matches the description. For example, look at this entry from the default `syslog.conf`:

This tells `syslogd(8)` that when it receives a message from the `mail` facility with a level of `info` or higher, the message should be appended to `/var/log/maillog`.

The logger won’t log to a nonexistent file. Use `touch(1)` to create the log file before restarting `syslogd(8)`.

### Wildcards

You can also use wildcards as an information source. For example, this line logs every message from the `mail` facility:

To log everything from everywhere, uncomment the `all.log` entry and create the file `/var/log/all.log`:

This works, but I find it too informative to be of any real use. You’ll find yourself using complex `grep(1)` statements daisy-chained together to find even the simplest information. Also, this would include all sorts of private data.

### Excluding Information

Use the none level to exclude information from a log. For example, here, we exclude authpriv information from our all-inclusive log. The semicolon allows you to combine entries on a single line:

```
*.*; authpriv.none          /var/log/most.log
```

### Comparison

You can also use the comparison operators < (less than), = (equal), and > (greater than) in syslog.conf rules. While syslogd defaults to recording all messages at the specified level or above, you might want to include only a range of levels. For example, you could log everything of info level and above to the main log file while logging the rest to the debug file:

```
mail.info             /var/log/maillog
mail.=debug           /var/log/maillog.debug
```

The mail.info entry matches all log messages sent to the mail facility at info level and above. The second line matches only the messages that have a level of precisely debug. You can't use a simple mail.debug because the debugging log will then duplicate the content of the previous log. This way, you don't have to sort through debugging information for basic mail logs, and you don't have to sort through mail transmission information to get your debugging output.

### Local Facilities

Many programs offer to log via syslog. Most of these can be set to a facility of your choice. The various local facilities are reserved for these programs. For example, by default, dhcpd(8) (see Chapter 20) logs to the facility local7. Here, we catch these messages and send them to their own file:

```
local7.*              /var/log/dhcpd
```

If you run out of local facilities, you can use other facilities that the system isn't using. For example, I've once used the uucp facility on a busy
