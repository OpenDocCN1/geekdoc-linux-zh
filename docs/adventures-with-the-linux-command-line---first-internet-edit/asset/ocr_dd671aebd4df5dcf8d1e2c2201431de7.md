# Conditionals

Midnight Commander supports two types of conditionals that affect the behavior of a menu entry. The first, called an addition conditional determines if a menu entry is displayed. The second, default conditional sets the default entry on a menu.

A conditional is added to a menu entry just before the first line. A conditional starts with either a += (for an addition) or a =(for a default) followed by one or more sub-conditions. Sub-conditions are separated by either i (meaning) or by & (meaning) and allowing us to express some complex logic. It is also possible to have a combined addition and default conditional by beginning the conditional with +=. Separate conditionals, one addition and one default, are also permitted preceding a menu entry.

Let's look at sub-conditions. They consist of one of the following:

| Sub-condition | Description |
| f pattern | Match currently selected file |
| F pattern | Match last selected in other panel |
| d pattern | Match currently selected directory |
| D pattern | Match last selected directory in other panel |
| t type | Type of currently selected file |
| Type | Type of last selected file in other panel |
| x filename | File executable |
| ! sub-condition | Negate result of sub-condition |

+   - List of sub-conditions

pattern is either a shell pattern (i.e., wildcards) or a regular expression according to the global setting configured in the Options/Configuration dialog. This setting can be overridden by adding shell_patterns=0 as the first line of the menu file. A value of 1 uses shell patterns, while a value of 0 forces regular expressions instead.

type is one or more of the following:

| Type | Description |
| r | regular file |
| d | directory |
| n | not a directory |
| l | link |
| x | executable file |
| t | tagged |
| c | character device |
| b | block device |
| f | FIFO (pipe) |
| s | socket |

+   - List of file types