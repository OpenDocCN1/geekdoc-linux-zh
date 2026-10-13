```
mail.err
```

To save these messages to the /var/log/maillog file, you specify that file as the action, giving you the following entry:

```
mail.err /var/log/maillog
```

syslogd also supports the use of * as a matching character to match either all the facilities or priorities in a sector. cron.* would match on all cron messages no matter what the priority, * .err would match on error messages from all the facilities, and * . * would match on all messages. The following example saves all mail messages to the /var/log/maillog file and all critical messages to the /var/log/mycritical file:

```
mail.* /var/log/maillog
```

```
*.crit /var/log/mycritical
```

# Priorities

When you specify a priority for a facility, all messages with a higher priority are also included. So the err priority also includes the crit, alert, and emerg priorities. If you just want to select for a specific priority, you qualify the priority with the = operator. For example, mail.=err will select only error messages, not crit, alert, and emerg messages. You can also restrict priorities with the ! operator. This will eliminate messages with the specified priority and higher. For example, mail.!crit will exclude crit messages, and the higher alert and emerg messages. To specifically exclude all the messages for an entire facility, you use the none priority. mail.none excludes all mail messages. This is usually used when you're defining several sectors in the same entry.

You can list several priorities or facilities in a given sector by separating them with commas. You can also have several sectors in the same entry by separating them with semicolons. The first example saves to the /var/log/messages file all messages with info priority, excluding all mail, and authentication messages (authpriv). The second saves all crit messages and higher for the uucp and news facilities to the /var/log/spooler file:

```
*.info;mail.none;news.none;authpriv.none /var/log/messages
```

```
uucp,news.crit /var/log/spooler
```

# Actions and Users

In the action field, you can specify files, remote systems, users, or pipes. An action entry for a file must always begin with a / and specify its full path name, such as /var/log/messages. To log messages to a remote host, you simply specify the hostname preceded by an @ sign. The following example saves all kernel messages on rabbit.trek.com:

```
kern.* @rabbit.trek.com
```

To send messages to users, you list their login names. The following example will send critical news messages to the consoles for the users chris and aleina:

```
news.=crit chris,aleina
```

You can also output messages to a named pipe (FIFO). The pipe entry for the action field begins with a |. The following example pipes kernel debug messages to the named pipe |/usr/adm/debug:

```
kern.*debug |/usr/adm/debug
```

Table 27-9: Syslog Facilities, Priorities, and Operators

| Facilities | Description |
|---|---|
| auth-priv | Security/authorization messages (private) |
| cron | Clock daemon (cron and at) messages |
| daemon | Other system daemon messages |