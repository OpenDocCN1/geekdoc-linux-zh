# Table 13-4 Message Priorities Used in syslog.conf (continued)

| Priority description | Priority name |
|---|---|
| Information about noteworthy events occurring as a program executes | notice |
| Warnings about potential problems with a program | warning (formerly called warn) |
| Notices about errors occurring within a program | err (formerly called error) |
| Critical error messages describing events that will likely cause a program to shut down | crit |
| Error messages that will cause a program to shut down and may also affect other programs | alert |
| Messages about events serious enough to potentially crash the system | emerg (formerly called panic) |

As a software developer writes a program, he or she decides which events are associated with which priority levels. For example, the developer might design a program so that a certain event generates a message with the priority of warning. Another programmer might decide that the same event should generate a message with the priority of notice. Thus, the programs themselves determine to which facility they pertain and what priority individual events or messages should have. As a system administrator, you simply determine where messages are logged, based on their facility and priority.

# The Actions

Once you set up a selector (consisting of a facility and a priority), you can assign an action to that selector. The action determines what syslogd and klogd do with the messages defined by the selector. Possible actions are listed here:

+   - Write the message to a regular file using the given file name. (This is by far the most commonly used action.)
+   - Write the message to the terminal indicated. This can be a standard virtual terminal name, from /dev/tty1 to /dev/tty6, or the console device, /dev/console.
+   - Write the message to the screen of any users who are logged in from a given list of users. For example, if the action is root,lsnow, the messages in the selector are written to the screen of users root and lsnow if they are logged in. This ensures that root and perhaps other users are immediately informed when a serious error occurs that might cause a program to shut down.
+   - Write the message to the log file on a remote system. This is done using the symbol @ in the action. You could specify the action as @incline.xyz.com, for example, to send log messages for the given selector to the syslogd daemon running on the system named incline.xyz.com.

The option of writing messages to a remote system is useful in several circumstances:

+   - To consolidate important messages: Many systems in an organization can send log messages to a single system so they can be archived and studied as a group.