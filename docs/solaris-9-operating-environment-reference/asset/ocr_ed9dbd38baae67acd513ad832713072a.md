# ps 1133

+   * Priority.
"* Control terminal.
"* Memory use.
"* CPU time.
"* Current status.

The ps command takes a snapshot of system activity at the time you type the command. Some data printed for defunct processes is irrelevant. If you are monitoring system activity, be aware that the results are already slightly out-of-date by the time you read them.

When you type the ps command without options, ps prints information about processes associated with the controlling terminal. The output contains only the PID, terminal identifier, cumulative execution time, and the command name. The other information that you can access by using the ps command is controlled with the options. If you use no options to select processes, ps reports all processes associated with the controlling terminal. If there is no controlling terminal, only the headers are printed.

# Options

The most frequently used options for the ps command are listed below.

+   -a List information about all processes most frequently requested: all except process group leaders and processes not associated with a terminal.

+   -e Report information about all processes now running.

+   -f Show the owner of the process, by name instead of UID, in the first column. This option turns off -1, -t, -s, and -r and turns on -a.

+   -l Generate a report that includes all fields except TIME.

Additional options for the ps command are listed below. Some options accept lists as arguments. You can separate items in a list by either using commas or by enclosing the entire argument in quotes and separating the items with commas or spaces. Many of the options are used to select processes to list. If you specify any processes, the default list is ignored and the ps command chooses the processes represented by the inclusive OR of all the selection-criteria options. Note that the proclist and grplist options require numeric values.

+   -A List information for all processes. Identical to -e.

+   -c Print information in a format that reflects scheduler properties described in procint(1). The -c option affects the output of the -f and -1 options.

+   -d List information about all processes except session leaders.

+   -g grplist List only processes whose group ID number(s) appears in grplist. (A leader is a process whose process ID number is identical to its process group ID number.)

+   -g gidlist List information for processes real group ID number are given in gidlist. The gidlist must be a single argument in the form of a blank or comma-separated list.

+   -j Print session ID and process group ID.