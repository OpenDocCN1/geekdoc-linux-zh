# 10.3 Compiling and Installing INN

The Linux version of the config.data file should provide a mostly accurate starting point for the compilation, but for detailed information on each section of the configuration file, refer to the INN installation notes. The configuration file is generally divided into the following sections:

+   - Make config parameters: Identifies the path to the C compiler and defines what libraries and command-line switches are needed.
- Logging levels: Identifies what log levels innd and other programs should log under. Be sure to put the correct log levels in the /etc/syslog.conf file.
- Ownership and file modes: Defines the user and group ownership of files, the unmask, and the mail contact for the machine.
- C library differences: Identifies what library routines the operating system will use as well as the value of some commonly variable types and sizes.
- C library omissions: Library routines that may be missing from the OS.
- Miscellaneous config data: Defines various macros to be included in INNSRC/include/configdata.h. This section greatly determines how the news server will act and is one of the largest sections.
- Paths to common programs: Defines where news binaries and general system programs like sendmail and shell utilities reside.
- Paths related to the spool directory: Defines where the news spool, incoming and outgoing database, tmp, and bad articles should go.
- Execution paths for innd and news: Defines some paths to programs used by innd.
- Sockets created by innd or clients: Defines where the socket files reside.
- Log and config files: Defines where the INN configuration and log files reside.
- Innwatch configuration: Defines at what points innwatch should throttle and unthrottle the news server.
- Tcl filtering configuration: Defines if tcl support is included or not where tcl header and library files reside.
- PGP control-message verification configuration: Determines if PGP authentication will be used and what the path to the PGP binary is.
- Local configuration: Defines the news user's home directory.
- Actync configuration: Defines what host to synchronize to and how.