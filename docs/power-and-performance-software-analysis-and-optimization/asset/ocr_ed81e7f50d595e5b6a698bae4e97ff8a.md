# 8.2 perf tool 161

moved to perf.data.old, and then perf.data will be created. However, a backup
will be made of perf.data.old if it already exists, resulting in data being
lost. The output file name can be changed by the -o command-line argument. If using
an output file name not the default, then all subsequent perf commands that
manipulate that file using the -i command line argument, specifying the correct
file name to use. For instance, continuing the example from the previous section,
which determines instructions are consuming the CPU time while compressing
a Linux kernel traceball using gzip:

```
$ perf record -e cycles -g /gzip -c /dev/shm/linux-3.15.tar > /dev/null
[ perf record: Woken up 14 times to write data ]
[ perf record: Captured and wrote 3.298 MB perf.data (~14096 samples) ]
```

Using the -g command-line argument instructs perf to record not only the
instruction pointer of the sample, but also the functionchain. Now that the data
has been collected, the perf report and perf annotate commands will allow for
accessing the collected data.

If the terminal supports, the perf report command will open an interactive
text user interface (TUI) for reviewing the results. This view consists of a list of
functions, sorted by the functions with which event counts, along with their
percentage of sampled events, the file, executable or shared library they reside in,
and their callchain. Otherwise, perf report will print a similar noninteractive view.
When navigating the TUI, the arrow keys move the cursor to the next or previous lines.
Press Enter when the cursor highlights a line beginning with " will expand that
to show the chain. Functions from executables or libraries that lack debug
information will be displayed as hexadecimal numbers. This can be remedied by
compiling or installing the appropriate debug flags or packages, and this does
not require the data collection.

Figure 8.2 shows the interactive TUI for the data collection from above. Looking
at the results, out of approximately sixty billion events recorded, 60.34% resided
in one function, longest_match. From there, it follows that optimizing this
function, or its calls to invoke it, has the potential to improve performance
more significantly than finding, say optimizing build_tree, which only accounts for
about 0.05%.

While knowing which functions to focus on is incredibly helpful, the profiler
can help even more. By highlighting an entry in the TUI and pressing the "a" key,
as disassembly for the function will be shown, annotated with the samples.
This is the same as invoking perf annotate [function name]. Like just perf
report, depending on the terminal capabilities, perf annotate will either launch
an interactive TUI or print the results to stdout. If the source code is available, perf
will interleave the instructions with their associated lines of code.

Figure 8.3 shows a snippet of the annotation for the longest_match function
highlight in Figure 8.2. On the far left side is the percentage of samples counted
to that instruction. By default, the cursor will start on the instruction with the