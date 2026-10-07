# Table 8-9 siguesque Structure (Continued)

| Field Name | Data Type | Description |
| --- | --- | --- |
| sq_func | pointer | Function pointer—references destructor function |
| sq_backptr | pointer | Points to data structure related to above |

The sigqueue structure provides a framework for a linked list of siginfo structures, maintained at the process level, and for multithreaded processes at the LWP/kthread level. siginfo stores various bits of information for many different types of signals. Within the structure are several unions (and in some cases, nested unions), so the available data depends on how the structure is instantiated during runtime. In the interest of readability, not all union declarations are shown.

![](bbox=[0.095, 0.396, 0.951, 0.92])

Figure 8.22 Signal-Related Structures