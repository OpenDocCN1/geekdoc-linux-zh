# # Explorational Exercises

+   1. The command `cat /proc/cpu_info` displays an error message because `/proc/cpu_info` is nonexistent. The command `cat /proc/cpu_info 2>1` redirects the error message to where?

+   2. Will it still be possible to discard content sent to `/dev/null` if the `noclobber` option is enabled for the current shell session?

+   3. Without using `echo`, how could the contents of the variable `$USER` be redirected to the stdin of command `sha1sum`?

+   4. The Linux kernel keeps symbolic links in `/proc/PID/fd/` to every file opened by a process, where *PID* is the identification number of the corresponding process. How could the system administrator use that directory to verify the location of log files opened by *nginx*, supposing its PID is *1234*?

+   5. It’s possible to do arithmetic calculations using only shell builtin commands, but floating point calculations require specific programs, like *bc* (*basic calculator*). With *bc* it’s even possible to specify the number of decimal places, with parameter `scale`. However, *bc* accepts operations only through its standard input, usually entered in interactive mode. Using a Here string, how can the floating point operation `scale=6; 1/3` be sent to the standard input of *bc*?