On the other hand, *whatis* (equivalent to man *-t*) tries to match a complete command name only on the part before the hyphen. Consequently, *whatis* *cc* will report if there is a cc manual and remain quiet for gcc, while *apropos* would successfully find both.

# **Key Concept**

Be sure to know the usage of *whereis*, *which*, *whatis*, and *apropos* as listed in Table 1.4. You will see all four on the exam.

Table 1.4 The Usage of *whereis*, *which*, *whatis*, and *apropos*

| whereis | Returns the path to the command |
| which | Tells you which command is being executed |
| whatis | Gives a short description of what a command does |
| apropos | Searches short descriptions from man pages |

# ### Writing Documentation

One of the softer skills that you will be tested on is your ability to document your system. This is the one task that most people like the least; however, it is one of the most important tasks that administrators do. You can expect to see one or two questions on the exam covering the importance of system documentation.

The first step in creating system documentation is to create and maintain a system log. For each computer you should record type of hard drive controller, number and size of disks, partitioning scheme, hostname, IP address, attached peripherals, and special keystrokes or commands for the machine such as how to configure the BIOS.

Whenever a problem occurs, you should document the details of the problem, what you tried, and what finally worked. For example, if you have a *cronjob* that fails, you should record the symptoms of the failure and what you did to correct it. That way when the same problem occurs at a later date, you will be able to solve it in a minimum amount of time.

As changes are made to each computer, record what they are and why they were made. This should include new hard disks, new partitions, applications you install, changes to configuration files, and so on. In other words, record everything you do. This documentation should be complete enough that the system can be rebuilt in a minimum amount of time.