![](bbox=[0.038, 0.073, 0.484, 0.458])

Figure 10-5: System Monitor graphically displays your system’s CPU and memory usage.

On the System Monitor window, lines scroll from right to left, indicating the percentage of your CPU being used as it rises and falls. You can also see how much of your total memory (RAM) is being used at the moment (and over time), as well as the amount of swap space being used. Scroll the devices at the bottom of the window to see the space being consumed on each of your hard disk partitions.

Click the Process Listing tab to see a listing of processes that are running currently. Click the columns in that tab to sort processes by name, user (who launched the process), memory use, percentage of CPU being consumed by the process, and process ID.

The example in Figure 10-5 shows a computer that is running with only 128 MB of RAM. The Memory Used is running near the maximum, indicating the likely occurrence of performance problems as RAM fills up and data has to be moved to swap space. The CPU used is only about 19 percent, which indicates that the CPU is keeping up with the demand.

# # Monitoring CPU usage with top

Start the top utility in a Terminal window, and it displays the top CPU consuming processes on your computer. Every five seconds, top will determine which processes are consuming the most CPU time and display them in descending order on your screen.

By adding the -S option to top, you can have the display show you the cumulative CPU time that the process, as well as any child processes that may already have exited, has spent. If you