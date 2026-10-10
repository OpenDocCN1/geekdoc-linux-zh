# **OPTIONS (CONT.)**

| **Use This Option** | **To Do This** |
| :------------- | :------------- |
| -r *directory* | Use the specified directory as the root directory |
| -v | Show all messages |
| -X | Skip link updating but update the cache unless **-N** is also specified |

# **ldd**

**ldd** [ *option* ] *program* | *library*

Displays the shared libraries required by the specified program or library.

# **OPTIONS**

| **Use This Option** | **To Do This** |
| :------------- | :------------- |
| -v | Display the version number |
| -V | Display the version number of the dynamic linker utility (**ld.so**) |

# **logrotate**

**logrotate** [ *option* ] [ *filename* ]

Launches a utility that makes backup files of system logs, which might otherwise become so voluminous that they would take up all available disk space. The rotation schedule involves moving logs to backup files, which are retained for a specified number of rotation cycles. At the conclusion of the rotation, the backup files are deleted. **logrotate** is normally run by commands specified in the root user's *crontab* file (*/etc/crontab*). (See the section “Scheduling Maintenance Processes with