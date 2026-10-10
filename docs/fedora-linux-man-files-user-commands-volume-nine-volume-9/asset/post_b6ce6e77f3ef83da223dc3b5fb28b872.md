
in the pidlist and doesn't apply additional filtering rules. The order of pids is unsorted and preserved. No additional selection options, sorting and forest type listings are allowed in this mode. Identical to **q** and **--quick-pid**.

- `--quick-pid` *pidlist*
  Select by processID (quick mode). Identical to **q** and **--quick-pid**.
- `-sess` *sesslist*
  Select by session ID. This selects the processes with a session ID specified in sesslist.
- `--sid` *sesslist*
  Select by sessionID. Identical to **-s**.
- **tty** *ttylist*
  Select by tty. Nearly identical to **-t** and **--tty**, but can also be used with an empty ttylist to indicate the terminal associated with **ps**. Using the **T** option is considered cleaner than using **t** with an empty ***ttylist***.
- `-tty` *ttylist*
  Select by tty. This selects the processes associated with the terminals given in ttylist. Terminals (ttys, or screens for text output) can be specified in several forms: /dev/ttyS1, ttyS1, S1. A plain "-" may be used to select processes not attached to any terminal.
- `--tty` *ttylist*
  Select by terminal. Identical to **-t** and **t**.
- **U** *userlist*
  Select by effective user ID (EUID) or name. This selects the processes whose effective user name or ID is in userlist. The effective user ID describes the user whose file access permissions are used by the process (see (2)). Identical to **-u** and **--user**.
- `-U` *userlist*
  Select by real user ID (RUID) or name. It selects the processes whose real user name or ID is in the userlist. The real user ID identifies the user who created the process, see (2).
- `-u` *userlist*
  Select by effective user ID (EUID) or name. This selects the processes whose effective user name or ID is in userlist.
  The effective user ID describes the user whose file access permissions are used by the process (see (2)). Identical to **U** and **--user**.
- `--User` *userlist*
  Select by real user ID (RUID) or name. Identical to -**U**.
- `--user` *userlist*
  Select by effective user ID (EUID) or name. Identical to -**u** and **U**.

# OUTPUT FORMAT CONTROL

These options are used to choose the information displayed by **ps**. The output may differ by personality.

- *c*
  Show different scheduler information for the **-l** option.
- *--context*
  Display security context format (for SELinux).
- *f*
  Do full-format listing. This option can be combined with many other UNIX-style options to add additional columns. It also causes the command arguments to be printed. When used with **-L**, the NLWP (number of threads) and LW PID (thread ID) columns will be added. See the c option, the format keyword **args**, and the format keyword **comm**.
- *F*
  Extra full format. See the **-f** option, which **-F** implies.
- *--format* *format*
  user-defined format. Identical to **-O** and **-o**.
- *j*
  BSD job control format.
- *-j*
  Jobs format.
- *l*
  Display BSD long format.
- *-l*
  Long format. The **-y** option is often useful with this.
- *-M*
  Add a column of security data. Identical to Z (for SELinux).
- *O* *format*
  Is preloaded **o** (overloaded). The BSD **O** option can act like **-O** (user-defined output format with some common fields predefined) or can be used to specify sort order. Heuristics are used to determine the behavior of this option. To ensure that the desired behavior is obtained (sorting or formatting), specify the option in some other way (e.g. with **-O** or **--sort**). When used as a formatting option, it is identical to **-O**, with the BSD personality.
- *-O* *format*
  Like **-o**, but preloaded with some default columns. Identical to -opid;:format;:state;:user;:tty;:command or **-opid;:format;:user;:tty;:cmd**, see **-o** below.
- *o* *format*
  Specify user-defined format. Identical to **-o** and **--format**.
- *-o* *format*
  User-defined format. *format* is a single argument in the form of a blank-separated or comma-separated list, which offers a way to specify individual output columns. The recognized keywords are described in the **STANDARD FORMAT SPECIFIERS** section below. Headers may be renamed (ps -o pid,:ruser=RealUser -o comm=Command) as desired. If all column headers are empty (ps -o pid= -o comm=) then the header line will not be output. Column width will increase as needed for wide headers; this may be used to widen up columns such as WCHAN (ps -o pid,:wchan=:WIDE,:WCHAN=:COLUMN -o comm). Explicit width control (ps -o pid,:wchan=42,:cmd) is offered too. The behavior of ps -o pid=X,:comm=Y varies with personality; output may be one column named “X,:comm=Y” or two columns named “X” and “Y”. Use multiple -o options when in doubt. Use the PS_FORMAT environment variable to specify a default as desired; DefSysV and DefBSD are macros that may be used to choose the default UNIX or BSD columns.
- **s**
  Display signal format.
- **u**
  Display user-oriented format.
- **v**
  Display virtual memory format.
- **X**
  Register format.
- **-y**
  Do not show flags; show rss in place of addr. This option can only be used with -l.
- **Z**
  Add a column of security data. Identical to -M (for SELinux).

# OUTPUT MODIFIERS

- *c*
  Show the true command name. This is derived from the name of the executable file, rather than from the argv value. Command arguments and any modifications to them are thus not shown. This option effectively turns the **args** format keyword into the **comm** format keyword; it is useful with the -f format option and with the various BSD-style format options, which all normally display the command arguments. See the -f option, the format keyword **args**, and the format keyword **comm**.
- `--colsn`
  Set screen width.
- `--columnsn`
  Set screen width.
- `--cumulative`
  Include some dead child process data (as a sum with the parent).
- *e*
  Show the environment after the command.
- *f*
  ASCII art process hierarchy (forest).
- `--forest`
  ASCII art process tree.
- *h*
  No header. (or, one header per screen in the BSD personality). The **h** option is problematic. Standard BSD **ps** uses this option to print a header on each page of output, but older Linux **ps** uses this option to totally disable the header. This version of **ps** follows the Linux usage of not printing the header unless the BSD personality has been selected, in which case it prints a header on each page of output. Regardless of the current personality, you can use the long options —**headers** and —**no-headers** to enable printing headers each page or disable headers entirely, respectively.
- *-H*
  Show process hierarchy (forest).
- `--headers`
  Repeat header lines, one per page of output.
- *k* *spec*
  Specify sorting order. Sorting syntax is [+,]-key[,[+,]-key[,...]]. Choose a multi-letter key from the **STANDARD FORMAT SPECIFIERS** section. The “+” is optional since default direction is increasing numerical or lexicographic order. Identical to —**sort**. Examples: **ps jaxkuid,-ppid,+pid ps axk comm o comm,args ps kstart-ti -ef**
- `--linesn`
  Set screen height.
- `-nnalist`
  Set name list file. Identical to N. The name list file is needed for a proper WCHAN display, and must match the current Linux kernel exactly for correct output. Without this option, the default search path for the name list is:
  SPS_SYSMAP SPS_SYSTEM_MAP /proc/*/wchan /boot/System.map-$(uname -r) /boot/System.map /lib/modules/$(uname -r)/System.map /usr/src/linux/System.map
