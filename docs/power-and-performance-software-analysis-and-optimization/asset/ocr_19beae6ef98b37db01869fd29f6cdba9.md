# 11.3 PowerTOP 195

second branch for the workload was never taken. Additionally, note that the number of statements each line was executed corresponds to the percentage, for example, 3244 × 100 = 77%.

```
1 204: if (zlikely)(*(unsigned short*)(match
+best_len - 1) = scan_end))
2 branch 0 taken 77% (fallthrough)
3 branch 1 taken 23%
4 3244: 205: continue:
5 966: 205: if (*(unsigned short*)match
   = scan_start
6 branch 0 taken 0% (fallthrough)
7 branch 1 taken 100%
8 ####: 207: continue:
9 ::: 208:
```

# LISTING 11.3

Excerpt from gcov(1) output.

# 11.3 PowerTOP

PowerTOP is a monitor, written by Arjan van de Ven, for measuring the system's behavior with regards to power consumption. This includes monitoring the number of processor wakeups, the P and C state residency, GPU state, and system settings. Additionally, PowerTOP is also capable of monitoring device power consumption through another power meter, RAPL, or software modeling. For its software modeling, PowerTOP records power consumption and utilization information over time, providing more accurate estimates as more results are collected. These collections are stored in /var/cache/powertop. By monitoring device power consumption for the system, PowerTOP can also estimate the cost of individual applications.

PowerTOP provides an interactive ncurses-based interface, as well as the ability to collect data and generate a report noninteractively. The noninteractive reports collect data for a predefined period of time, and then generate a report in either HTML or CSV format. By default the noninteractive mode will occur for 20 seconds and then produce a HTML report, in the file powertop.html. A custom period can be specified with the --time=parameter, which expects an integer representing the number of seconds for collection. A CSV report can be generated with the --csv=filename parameter, where filename represents the file for storing the report. Additionally, the HTML report file, powertop.html, can be similarly modified with the --html=filename parameter.

The ncurses interface is divided into five windows, each displaying a different metric. These windows are traversed with the Tab and Shift-Tab combinations. The contents of the current window can be shifted by the arrow keys. The data can be refreshed manually by pressing the "r" key. Finally, PowerTOP can be quit by pressing the Escape key.