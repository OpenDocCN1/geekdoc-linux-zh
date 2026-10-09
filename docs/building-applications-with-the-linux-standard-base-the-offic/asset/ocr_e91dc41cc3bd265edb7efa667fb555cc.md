The emphasis is again on defining things required to make applications portable. There is a section on the preferred syntax for new utilities’ arguments and options. In some cases user portability was considered, such as the inclusion of the vi editor.

# ### 2.2.2 Single UNIX Specification

The Single UNIX Specification (SUS) is a set of specifications required for UNIX trademark compliance. It is developed and managed by The Open Group, an industry consortium and marketing group. The Open Group establishes the definition of what a UNIX system is and holds its associated trademark in trust for the industry. The SUS specifies the programming and user environment that must be offered by an operating system before the system can use the UNIX trademark.

Version 3 of the Single UNIX Specification is the latest in the series of UNIX specifications that began with the X/Open Company Portability Guides (XPGs), which were operating system specifications created prior to, and then concurrently with, the initial POSIX efforts. In late 1998, The Open Group, IEEE, and ISO/IEC SC22/WG15 agreed to work together to form a single common set of specifications with the development group known as the Austin Group (described later in this section).

The Single UNIX Specification has always been aligned with the formal API standards such as POSIX and ISO C, being an upward compatible superset. It contains more APIs and features than POSIX, and it makes mandatory some features that POSIX keeps optional. POSIX threads, for example, are required for UNIX trademark compliance. The SUS also covers X11, Curses, and many more mandatory utilities than POSIX.

An HTML version of the specification is freely available from The Open Group’s Single UNIX Specification Web site.3