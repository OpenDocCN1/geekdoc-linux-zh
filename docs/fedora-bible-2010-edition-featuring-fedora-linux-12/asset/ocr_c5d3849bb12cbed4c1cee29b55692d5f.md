up and data has to be moved to swap space. The CPU used is only about 6 percent, spread over two processors, which indicates that the CPU is currently keeping up with the demand.

# ## Monitoring CPU usage with top

Start the top utility in a Terminal window, and it displays the top CPU consuming processes on your computer. Every five seconds, top will determine which processes are consuming the most CPU time and display them in descending order on your screen.

By adding the -S option to top, you can have the display show you the cumulative CPU time that the process, as well as any child processes that may already have exited, has spent. If you want to change how often the screen is updated, you can add the -d secs option, where secs is replaced by the number of seconds between updates.

By default, processes are sorted by CPU usage. You can sort processes numerically by PID (press N), by resident memory usage (press M), by time (press T), or back to CPU usage (press P). The following output shows an example of top running, with information sorted by memory use. The system shown is running a GNOME desktop, with OpenOffice.org Writer, Firefox Web browser, and several other applications active. Notice that the amount of memory free is very low. To get good performance out of a Fedora desktop system, 256MB (as shown in this example) may not be enough once you start running a lot of big applications.

![](bbox=[0.17, 0.4, 0.89, 0.64])

# ## Monitoring power usage on laptop computers

To effectively use a laptop computer, you need to be able to monitor and manage the laptop’s power usage. Using tools provided in Fedora, you can configure your laptop to:

+   - Monitor the battery level
+   - Notify you when the battery is low
+   - Notify you when the battery is fully charged
+   - Show when the laptop is plugged in
+   - Suspend the current session

Fedora offers two facilities that do power management: APM and ACPI.