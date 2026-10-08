# ps

# 1141

+   - Look at the C field to find unimportant processes that consume a large percentage of CPU time. If you do not think a process warrants so much attention, use the priocntl command to lower its priority. See the priocntl(1) manual page for more information.

+   - Look at the SZ field for processes that consume too large a percentage of memory. If a process is a memory hog, kill the process. If many processes are using lots of memory, the system may need more memory.

+   - Watch for a runaway process that progressively uses more and more CPU time. You can check this condition using the -f option to see the start time (STIME) of the process and by watching the TIME field for the accumulation of CPU time.

# Environment Variables

See environ(5) for descriptions of the environment variables that affect the execution of ps: LC_TYPE, LC_MESSAGES, LC_TIME, and NLSPATH. COLUMNS can override the system-selected horizontal screen size to determine the number of text columns to display.

# Exit Status

+   0 Successful completion.

+   > 0 An error occurred.

# Files

+   /dev/pts/* Terminal (TTY) names search files.

+   /dev/term/* Terminal (TTY) names search files.

+   /etc/passwd UID information supplier.

+   /proc* Process control files.

+   /tmp/ps_data Internal data structure.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwcsu |
| CSI | Enabled |

> Note — ps is enabled except for login names (user names).

# See Also

kill(1), nice(1), pagesize(1), priocntl(1), who(1), getty(1), proc(4), ttyschr(4), attributes(5), environ(5)