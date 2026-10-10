section below. Headers may be renad (ps -o pid,:ruser=RealUser -o comm=Command) as desired. If all column headers are empty (ps -o pid= -o comm=) then the header line will not be output. Column width will increase as needed for wide headers; this may be used to widen up columns such as WCHAN (ps -o pid,:wchan=:WIDE,:WCHAN=:COLUMN -o comm). Exolicit width control (ps opid,:wchan=42,:cmd) is offered too. The behavior of ps -o pid=X,:comm=Y varies with personality; output may be one column nad “X,:comm=Y” or two columns nad “X” and “Y”. Use multiple -o options when in dout. Use the PS_FORMAT environtt variable to specify a default as desired; DefSysV and DefBSD are macros that may be used to choose the default UNIX or BSD columns.

+   - **s** Display signal format.
+   - **u** Display user-oriented format.
+   - **v** Display virtual mory format.
+   - **X** Register format.
+   - **-y** Do not show flags; show rss in place of addr. This option can only be used with -l.
+   - **Z** Add a column of security data. Identical to -M (for SELinux).