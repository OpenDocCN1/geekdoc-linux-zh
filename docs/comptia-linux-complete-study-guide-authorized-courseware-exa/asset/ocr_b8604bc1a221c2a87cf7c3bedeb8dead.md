When a program sends a message to the system logger, it includes a priority code; the logger logs the message to a file if you’ve configured it to log messages of that level or higher. Thus, if you specify a priority code of alert, the system will log messages that are classified as alert or emerg but not messages of crit or below. An exception to this rule is if you precede the priority code by an equal sign (=), as in =crit, which describes what to do with messages of crit priority only. An exclamation mark (!) reverses the meaning of a match. For instance, !crit causes messages below crit priority to be logged. A priority of * refers to all priorities.

You can specify multiple selectors for a single action by separating the selectors by a semicolon (;). Note that commas are used to separate multiple facilities within a single selector, whereas semicolons are used to separate multiple selectors as a whole. Examples of complete selectors appear shortly.

Most commonly, the action is a filename, typically in the /var/log directory tree. The messages, syslog, and secure files in this directory are three common and important log files, although not all distributions use all of these files. Other possible logging locations include a device filename for a console (such as /dev/console) to display data on the screen, a remote machine name preceded by an at sign (@) to log data to the specified system, and a list of usernames of individuals who should see the message if they’re logged in. For the last of these options, an asterisk (*) means all logged-in users.

Some examples should help clarify these rules. First is a fairly ordinary and simple entry:

```
mail.* /var/log/mail
```

This line sends all log entries identified by the originating program as related to mail to the /var/log/mail file. Most of the entries in a default /etc/syslog.conf file resemble this one. Together, they typically cover all of the facilities mentioned earlier. Some messages may be handled by multiple rules. For instance, another rule might look like this one:

```
*.emerg *
```

This line sends all emerg-level messages to the consoles of all users who are logged into the computer using text-mode tools. If this line and the earlier mail.* selector are both present, emerg-level messages related to mail will be logged to /var/log/mail and displayed on users’ consoles.

A more complex example logs kernel messages in various ways, depending on their priorities:

```
kern.* /var/log/kernel  
kern.crit @logger.pangaea.edu  
kern.crit /dev/console  
kern.info;kern.terr /var/log/kernel-info
```

The first of these rules logs all kernel messages to /var/log/kernel. The second line sends critical messages to logger.pangaea.edu. (This system must be configured to accept remote logs, which is a topic not covered in this book.) The third line sends a copy of critical messages to /dev/console, which causes them to be displayed on the computer’s main text-mode