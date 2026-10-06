While this example prints the raw results, a more sophisticated application could perform some automatic analysis on the results. For instance, branches show up in the profile, a running tally, associated with the instruction pointer, could be kept. After the workload finishes, this tally could be used to summarize the results, listing the hottest branches.

Additionally, the application could look up the source code associated with these instruction pointers for its report, by parsing the maps file in proffs, as /proc/self/maps. This will correlate virtual memory addresses with specific mapped files, including executables and shared libraries. Then, using debug information, the offset from the base address of the file can be translated into a source code and line. For simplicity's, this information can also be obtained on the sample application:

```
$ addr2line -e map 0x400c4c
/home/jtk/map.c:126
$ addr2line -e map 400c62
/home/jtk/map.c:125
$ addr2line -e map 400c52
/home/jtk/map.c:127
```

# 8.2 PERF TOOL

The perf tool leverages the functionality of the kernel's performance event infrastructure for profiling. In other words, perf provides access to counting and sampling events, handles the parsing of the results and relevant debug information, and produces reports that highlight the hotspots in the code.

Data collection can occur either for specific processes, either by perf for new process or attaching to an existing process, or for every process on the system. To monitor a new process, simply pass the command and related arguments to perf as the last arguments. Instance, perf stat would cause perf to create a new process. To attach to an existing process, the -p argument is used. For instance, perf record -p 12345 would cause perf to attach to an existing process with a process id of 12345, and then perform measurements. Finally, every process can be monitored instead using perf -a option.

# 8.2.1 EXPRESSING EVENTS

Events are selected using the -e command argument. Multiple events can be specified by repeating the argument per event, or by providing the argument with a comma-separated list of events. Event groups are created by enclosing the comma-separated list of events in brackets, e.g., perf stat -e "cycles,instructions". For most tools, if no events are specified, CPU cycles