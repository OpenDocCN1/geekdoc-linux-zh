# postio

# 1071

+   -l line

Connect to the printer attached to line. In most cases, there is no default and postio must be able to read and write line. If the line does not begin with a /, it may be treated as a Datakit destination.

+   -L file

Put data received on line in file. The default log file is standard error. Printer or status messages that don't show a change in state are normally written to file-but can be forced with the -D option.

+   -P string

Send string to the printer before any of the input files. The default string is simple PostScript code that disables timeouts.

+   -R num

Run postio as a single process if numis 1 or as separate read and write processes if numis 2. By default, postio runs as a single process.

+   -q

Prevent status queries while files are being sent to the printer. When status queries are disabled, append a dummy message to the log file before each block is transmitted.

The next two options are for users who expect to run postio on their own. Neither is suitable for use in spooler interfaces.

+   -i

Run the program in interactive mode. First, send any files, followed by the standard input. Separate read and write processes and override many other options. Use interrupt or quit character. To get a friendly interactive connection with the printer, execute on a line by itself.

+   -t

Write data received on line and not recognized as printer or status information to the standard output. Separate read and write processes. Convenient if you have a PostScript program that returns useful data to the host.

The following option is not generally recommended and should be used only if all else fails to provide a reliable connection.

+   -s

Slow the transmission of data to the printer. Severely limits throughput, as a single process, disable the -q option, limit the internal buffer size to 1,024 bytes. This option can use an excessive amount of CPU time and does nothing in interactive mode.

You obtain the best performance by using a large internal buffer (the -B option) and by running the program as separate read and write processes (the -R 2 option). In fact for for the additional process continues as a single read/write process. When one process is used, only data sent to the flow is controlled.

The options are not all exclusive. The -i option always wins, selecting its settings for whatever is needed to run interactive mode independently of anything read and write processes, and few of the other options accomplish anything in the presence of the -i option. The -t option needs a reliable two-way connection to the printer and therefore forces separate read and write processes. The -s option limits the status query mechanism, so -q is disabled and postio runs as a single process.

In many cases, postio starts by making a connection to line and then tries to force the printer into the IDLE state by sending an appropriate sequence of “T” (status query, interrupt), “C” (end-of-job characters). Files are transmitted with an occasional “T” (unless you use the -q option). After all the files are sent, postio waits until it is likely that the connection is