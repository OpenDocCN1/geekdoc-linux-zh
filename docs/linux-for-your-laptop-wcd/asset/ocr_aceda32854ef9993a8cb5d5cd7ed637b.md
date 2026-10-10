# Controlling APM

Although most mobile Linux users use hardware keyboard commands to initiate APM events, you should know about the finer controls available by using APM control software. Several APM support programs besides the apmd daemon are provided by the apmd package:

+   * apm. An APM query and command tool used to display remaining power, print APM BIOS information, or put your computer into standby or suspend mode. For example, the -v command-line option returns status, percent, and time remaining:
+   
+   ```
+   $ apm -v
+   
+   APM BIOS 1.2 (kernel driver 1.9)
+   
+   AC off-line, battery status high: 99% (3:18)
+   ```

+   * apmsleep. A utility that suspends your laptop. It can also be used to set an alarm to have your notebook wake up. For example, you can set your notebook to wake up at 3:15 p.m. from a standby mode like this:
+   
+   ```
+   $ apmsleep -S 15:15
+   ```

+   * on_ec_power. A shell script that provides a function to determine whether your notebook is on battery or AC power.

+   * tailf. A handy version of the tail command that doesn’t cause your hard drive to spin while you’re monitoring your system logs in a console or X11 terminal window.

+   * xapm. An X11 client that displays your notebook’s remaining battery life in hours or minutes or as a percentage (see Figure 7.2). Includes a bar indicator that uses colors—blue for charging, green for charged, and red for critical discharging.

![](bbox=[0.07, 0.75, 0.26, 0.79])

Figure 7.2 The xapm client included with the apmd package is a handy battery gauge for mobile Linux users.