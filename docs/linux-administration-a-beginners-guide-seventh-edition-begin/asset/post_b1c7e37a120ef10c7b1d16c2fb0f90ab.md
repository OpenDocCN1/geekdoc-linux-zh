
# Linux Administration: A Beginner's Guide

| Property Name (propname) | Description |
|---|---|
| msg | The MSG part of the message; the actual log message |
| rawmsg | The message exactly as it was received from the socket |
| HOSTNAME | Hostname from the message |
| FROMHOST | Hostname of the system from which the message was received (not necessarily the original sender) |
| syslogtag | TAG from the message |
| PRI-text | The PRI part of the message in a textual format |
| syslogfacility | The facility from the message in numerical format |
| syslogfacility-text | The facility from the message in text form |
| syslogseverity | The severity from the message in numerical format |
| syslogseverity-text | Severity from the message in text form |
| timereported | Timestamp of the message |
| MSGID | The contents of the MSGID field |

Table 8-7 rsyslog's Message Property Names

- Any entry in the /etc/rsyslog.conf file that contains a dollar ($) sign is a directive.
Log properties refer to well-defined fields in any log message. Example common properties are shown in Table 8-7.
The percentage sign (%) is used to encode log message properties. Properties can be modified by the use of property replacements.
Any entry that begins with pound sign (#) is a comment and is ignored. Empty lines are also ignored.

## rsyslog Templates
As mentioned, rsyslog relies on the use of templates, and the templates define the format of logged messages. The use of templates is what allows rsyslog to produce log files that are formatted similarly to the traditional format that is produced by the older and traditional syslog. Templates that support the syslog log format are hard-coded in rsyslog and are used by default.
A sample template that supports the use of the rsyslog message format is here:

```
$template TraditionalFormat,"%timegenerated% %HOSTNAME% %syslogtag% %msg\n",<options>
```

# CHAPTER 8 Core System Services

The various fields of this sample template are explained in the following list and in Table 8-7.

- **$template** This directive implies that the line is a template definition.
- **TraditionalFormat** This is a descriptive name.
- **%timegenerated%** This specifies the `timegenerated` property.
- **%HOSTNAME%** This specifies the `HOSTNAME` property.
- **%syslogtag%** This specifies the `syslogtag` property.
- **%msg%** This specifies the `msg` property.
- **\n** The backslash is an escape character. Here, the `\n` implies a new line.
- **<options>** This entry is optional. It specifies options influencing the template as a whole.

# rsyslog Rules

Rules can be created in rsyslog.config using different filter criteria. The currently available filter criteria are shown in Table 8-8.

| Filter Type | Description | Syntax | Example |
|---|---|---|---|
| Facility and Priority based | Use traditional facility and priority selectors | facility.priority action_field | mail.info /var/log/messages |
| Property based | Allow filtering on rsyslog-defined properties as HOSTNAME, syslog, programname, and | :property,[] compare operation,"value" | :hostname, isequal,"fedora-server" |
| Expression based | Use rsyslog built-in scripting language called RainerScript to build filters | if EXPRESSION then ACTION else ACTION | action(type="omfile" file="/var/log.log") else { if $msg contains 'look' then { action(type="omfile" file="/var/log/nolook.log") } |

**Table 8-8 rsyslog Filter Criteria

# Linux Administration: A Beginner's Guide

Let's delve into the traditional Facility and Priority-based filter type rules a little more. This type of filter rule in the rsyslog.conf file is broken down into a selector field (facility:priority), an action (field or target), and an optional template name. Specifying a template name after the last semicolon will assign the respective action to that template. Whenever a template name is missing, a hard-coded template is used instead. It is, of course, important that you make sure that the desired template is defined before referencing it.

Here is the format for each line in the configuration file:

```
selector_field action_field ; <optional_template_name>
```

Here's an example:

```
mail.info /var/log/messages; RSYLOG_TraditionalFormat
```

Selector Field The selector field specifies the combination of facilities and priorities. Here's an example selector entry:

```
mail.info
```

Here, mail is the facility and info is the priority.

Action Field The action of rule describes the action to be performed on message. This action can range from simple things such as writing the logs to a file or slightly complex things such as writing to a database table or forwarding to another host. Here's an example action:

```
/var/log/messages
```

This action indicates that the log messages should be written to the file. Other possible values for the action field are described in Table 8-9.

| Action Field | Description |
|---|---|
| Regular file (e.g., /var/log/messages) | A full path to the file should be specified and begin with /. This field can also refer to device files, such as tty files, or the console, such as /dev/console. |
| Named pipe (e.g., /tmp/myfile) | A named pipe. A pipe symbol (| must precede the path to named pipe (FIFO). This type of file is created with mkfifo. With rsyslog feeding one side of the pipe, you can run another program that reads the other side of the pipe. |

8-9 Action Field Descriptions

| Action Field | Description |
|---|---|
| @loghost or @@loghost | A remote host. The @ symbol must begin this type of action, followed by destination host. A single @ indicates the log messages should be sent via traditional UDP. And double at (@@) imply the logs should be transmitted via TCP. |
| List of users (e.g., dude, root) | This type of action indicates that the log messages should be sent to list of currently logged-on users. The list of users is separated by commas. Specifying an asterisk (*) will send the specified logs to all logged-on users. |
| Discard This action means that the logs should be discarded and no action should be performed on them. This type of action is specified by tilde symbol (-) in the action field. |
| Database table (e.g., dbhost,dbname,dbuser:<dbtemplate>) | This type of action is of advanced new features that rsyslog supports natively. It allows the log messages to be sent directly to a configured database table. This type of location needs to begin with greater-than symbol (>). The parameters specified after > follow a strict order: After >, the database hostname (dbhost) must be given, a comma, the database name (dbname), another comma, the database user (dbuser), and then the database user's password (password). An optional template (dbtemplate) can be specified if semicolon is after the last parameter. |

8-9 Action Field Descriptions (Continued)

# Sample /etc/rsyslog.conf File

Following is an excerpt from a sample rsyslog.conf file that highlights Facility and Priority-based filter type rules. The sample is interspersed with comments that explain what the following rules do.

```
# A template definition that resembles traditional syslog file output
$template TraditionalFormat,"%timegenerated% %HOSTNAME% %syslogtag% %msg\n"
```

```
# Log all kernel messages to the console.
kern.* /dev/console
```

# Log anything(except mail) of level info or higher into /var/log/messages file.
 Exclude private authentication messages!
# The rule is using the hard-coded traditional format because a different template name has NOT been defined.
*.info.mail:none;authpriv:none;cron /var/log/messages

# log messages from authpriv (sensitive nature) to the /var/log/secure file.
# But also use the template (myTraditionalFormat) defined earlier in the file
authpriv.* /var/log/secure;myTraditionalFormat

# Log all the mail messages in one place.
mail.* -/var/log/mailog

# Send emergency messages to all logged on users
*.emerg

# Following is an entry that logs to a database host at the IP address# 192.168.1.50 into DB named log_database
*..* >192.168.1.50,log_database,dude,dude_db_password

# systemd-journal (journal)

systemd-journal is a component of systemd (discussed earlier in this chapter) that runs as a system service that collects and stores logging data. Like syslog, it is possible to receive logging data from various sources: user processes, the kernel, and standard output (STDOUT) and standard error (STDERR) of other system services. journal creates and maintains its logging differently from the traditional method of using flat files. It natively stores logging data in structured and indexed journals, which lends itself to rich of new possibilities and speed improvements.
Several RPM- and Debian-based distributions have integrated systemd-journal for work alongside the more traditional logging daemons such as syslog. It is possible to run both solutions concurrently on a system and feed data from one solution to the other. Even though this is possible, it is generally considered good system administration practice to standardize on a single logging solution on production systems.

# journalctl and journalctl Examples

The primary tool for interacting with the journal files collected and maintained by journal is called journalctl. It serves as the native utility for querying and viewing the contents of logging data collected systemd-journal.
We will walk through quick journalctl uses in the exercise.
