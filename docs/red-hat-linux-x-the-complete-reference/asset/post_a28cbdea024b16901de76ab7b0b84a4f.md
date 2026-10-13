
To save these messages to the `/var/log/maillog` file, you specify that file as the action, giving you the following entry:

```
mail.err /var/log/maillog
```

syslogd also supports the use of `*` as a matching character to match either all the facilities or priorities in a sector. `cron.*` would match on all cron messages no matter what the priority, `*.err` would match on error messages from all the facilities, and `*.*` would match on all messages. The following example saves all mail messages to the `/var/log/maillog` file and all critical messages to the `/var/log/mycritical` file:

```
mail.* /var/log/maillog
*.crit /var/log/mycritical
```

## Priorities

When you specify a priority for a facility, all messages with a higher priority are also included. So the `err` priority also includes the `crit`, `alert`, and `emerg` priorities. If you just want to select for a specific priority, you qualify the priority with the `=` operator. For example, `mail.=err` will select only error messages, not `crit`, `alert`, and `emerg` messages. You can also restrict priorities with the `!` operator. This will eliminate messages with the specified priority and higher. For example, `mail.!crit` will exclude `crit` messages, and the higher `alert` and `emerg` messages. To specifically exclude all the messages for an entire facility, you use the `none` priority. `mail.none` excludes all mail messages. This is usually used when you're defining several sectors in the same entry.

You can list several priorities or facilities in a given sector by separating them with commas. You can also have several sectors in the same entry by separating them with semicolons. The first example saves to the `/var/log/messages` file all messages with `info` priority, excluding all mail, and authentication messages (`authpriv`). The second saves all `crit` messages and higher for the `uucp` and `news` facilities to the `/var/log/spooler` file:

```
*.info;mail.none;news.none;authpriv.none /var/log/messages
uucp,news.crit /var/log/spooler
```

## Actions and Users

In the action field, you can specify files, remote systems, users, or pipes. An action entry for a file must always begin with a `/` and specify its full path name, such as `/var/log/messages`. To log messages to a remote host, you simply specify the hostname preceded by an `@` sign. The following example saves all kernel messages on `rabbit.trek.com`:

```
kern.* @rabbit.trek.com
```

To send messages to users, you list their login names. The following example will send critical news messages to the consoles for the users `chris` and `aleina`:

```
news.=crit chris,aleina
```

You can also output messages to a named pipe (FIFO). The pipe entry for the action field begins with a `|`. The following example pipes kernel debug messages to the named pipe `|/usr/adm/debug`:

```
kern.*debug |/usr/adm/debug
```

### Table 27-9: Syslog Facilities, Priorities, and Operators

| Facilities | Description |
|---|---|
| auth-priv | Security/authorization messages (private) |
| cron | Clock daemon (cron and at) messages |
| daemon | Other system daemon messages |
| kern | Kernel messages |
| lpr | Line printer subsystem messages |
| mail | Mail subsystem messages |
| mark | Internal use only |
| news | Usenet news subsystem messages |
| syslog | Syslog internal messages |
| user | Generic user-level messages |
| uucp | UUCP subsystem messages |
| local0 through local7 | Reserved for local use |

| Priorities | Description |
|---|---|
| debug | 7. Debugging messages, lowest priority |
| info | 6. Informational messages |
| notice | 5. Notifications, normal, but significant, condition |
| warning | 4. Warnings |
| err | 3. Error messages |
| crit | 2. Critical conditions |
| alert | 1. Alerts, action must be taken immediately |
| emerg | 0. Emergency messages, system is unusable, highest priority |

| Operators | Description |
|---|---|
| * | Matches all facilities or priorities in a sector |
| = | Restrict to a specified priority |
| ! | Exclude specified priority and higher ones |
| / | A file to save messages to |
| @ | A host to send messages to |
| | | FIFO pipe to send messages to |

## /etc/syslog.conf Example

The default `/etc/syslog.conf` file for Red Hat systems is shown here. Messages are logged to various files in the `/var/log` directory.

```
# Log all kernel messages to the console.
#kern.*				/dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none    /var/log/messages

# The authpriv file has restricted access.
authpriv.*                                            /var/log/secure
# Log all the mail messages in one place.
mail.*                                                /var/log/maillog
# Log cron stuff.
cron.*                                                /var/log/cron
# Everybody gets emergency messages
*.emerg                                               *
# Save mail and news errors of level err and higher in a special file.
uucp,news.crit                                        /var/log/spooler
# Save boot messages also to boot.log
local7.*                                              /var/log/boot.log
# INN
news.=crit                                            /var/log/news/news.crit
news.=err                                             /var/log/news/news.err
news.notice                                           /var/log/news/news.notice
```

## Performance Analysis Tools and Processes

Linux treats each task performed on your system as a process, which is assigned a number and a name. You can examine these processes and even stop them. Red Hat provides several tools for examining processes as well as your system performance. Easy monitoring is provided by several GUI tools, like Red Hat's Procman System Monitor.

## ps Command

From the command line, you can use the `ps` command to list processes. With the `-aux` option, you can list all processes. Piping the output to a `grep` command with a pattern enables you to search for a particular process. A pipe funnels the output of a preceding command as input to a following command. The following command lists all X Window System processes:

```
ps -aux | grep 'X'
```

A number of utilities on your system provide detailed information on your processes, as well as other system information such as CPU and disk use (see Table 27-10). Although these tools were designed to be used on a shell command line, displaying output in text lines, several now have KDE and GNOME versions that provide a GUI interface for displaying results and managing processes.

### Table 27-10: Performance Tools

| Performance Tool | Description |
|---|---|
| vmstat | Performance of system components |
| top | Listing of most CPU intensive processes |
| free | Listing of free RAM memory |
| sar | System activity information |
| iostat | Disk usage |
| Procman System Monitor | Red Hat system monitor for processes and usage monitoring (System Monitor on System Tools menu). |
| KDE Task Manager and Performance Monitor | KDE system monitor for processes and usage monitoring |

## vmstat, free, top, iostat, Xload, and sar

The `vmstat` command outputs a detailed listing indicating the performance of different system components, including CPU, memory, I/O, and swap operations. A report is issued as a line with fields for the different components. If you provide a time period as an argument, it repeats at the specified interval-usually a few seconds. The `top` command provides a listing of the processes on your system that are the most CPU intensive, showing what processes are using most of your resources. The listing is in real time and updated every few seconds. Commands are provided for changing a process's status, such as its priority.

The `free` command lists the amount of free RAM memory on your system, showing how much is used and how much is free, as well as what is used for buffers and swap memory. `Xload` is an X Window System tool showing the load, CPU, and memory. `iostat` displays your disk usage, and `sar` shows system activity information.

## Procman System Manager

The current version of Red Hat provides the Procman System Manager for displaying system information and managing system processes, accessible from System Tools | System Monitor. There are two panels, one
