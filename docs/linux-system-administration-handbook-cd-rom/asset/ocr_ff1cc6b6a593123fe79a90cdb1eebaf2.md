# 19.1 Facilities and Priorities

+   * notice
* warning
* err
* crit
* alert
* emerg

# 19.1 Facilities and Priorities

The facility/priority combination that you list will then report all the messages that get sent to syslog for that priority and higher. A priority of degug report all messages, and a priority of none report no messages.

Replacing either the facility or priority with an * will report for all facilities or all priorities, depending on where you put the * (before or after the period). You can combine multiple facilities to one priority by separating them with a comma.

The syslog that Linux uses a few extensions to it that are not in the original BSD version of syslog. Putting a a = sign in front of a priority says to report only this priority in a list. Putting a ! in front of a priority says to ignore that priority and all higher priorities. Combining the two (!=) would ignore only that priority.

The man pages for the particular programs you want to monitor usually list what facilities the program uses. You'll note that there are eight user-defined facilities you can use in your programs or other scripts.

# 19.2 Actions

The second field lists where the message should be sent. This can be a file (if the destination starts with a /), a remote host (if the destination starts with an @), all logged-in users (if the destination is a *), or a specific user (if it starts with none of the above three characters). The file destination can also be a tty file, such as /dev/console, which will send the message to the Linux console.

You can also use the | character to pipe the message to an external command or a fifo.

Using the remote host logging can randomize a group of computers to log all their messages to one machine. However, if there was a severe enough