# The klogd Utility

The kernel logging daemon (klogd) tracks kernel messages by prioritizing them. It listens to the source for kernel messaging and intercepts the messages. klogd runs as a client of syslogd, where the kernel messages are sent through the syslogd daemon. klogd also acts as a standalone program.

The klogd command provides a number of options to manage specific functions. Some of the frequently used options are listed in the table.

| Option | Enables You To |
| :--- | :--- |
| -c n | Set the default log level to n for messages. Where n ranges from 0 to 7. |
| | * 0-Emergency |
| | * 1-Alert |
| | * 2-Critical |
| | * 3-Error |
| | * 4-Warning |
| | * 5-Notice |
| | * 6-Information |
| | * 7-Debug |
| -p | Load the kernel module symbol information. |
| -k file | Use the specified file as the source to store the kernel module symbol information. |
| -o | Read and log all kernel messages in the buffer in a single read. |
| -d | Switch to a debugging mode. |
| -f file | Log messages to the file that is specified. |
| -s | Use the system call interface for buffering the kernel messages. |

![](bbox=[0.76, 0.1, 0.9, 0.17])

# Syntax

The syntax of the klogd command is klogd [options].

# The /etc/syslog.conf File

The /etc/syslog.conf file controls the location where the syslogd information is recorded. This file consists of two columns. The first column lists the facilities and severities of the messages. The second column lists the files the messages should be logged to. By default, most messages are stored in the /var/log/messages file.

![](bbox=[0.76, 0.68, 0.9, 0.75])