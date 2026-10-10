![](bbox=[0.24, 0.1, 0.52, 0.21])

+   2. Right-click the battery icon and select Preferences. The Power Management Preferences window appears.

+   3. Change any of the following values related to your battery monitor:

+   *   **On AC Power** — From the On AC Power tab, you can select how many minutes of idle time should elapse before putting the computer or display to sleep. You can also set what happens when the laptop lid is closed (Blank Screen Suspend, Hibernate, or do nothing). As for the Display, you can set how long to wait before putting the display to sleep (40 minutes is the default) or whether or not you want to dim the display when it is idle.

+   *   **On Battery Power** — The same options described for running on AC power are available for when your laptop is running on battery power. You can set what happens to the CPU and display after set amounts of idle time.

+   *   **General** — From the General tab, you can set the type of notification that occurs when the laptop’s power button is pressed or when the suspend button is pressed. You can also set when the battery icon is displayed (when a battery is present, when it is low, or when it is charging or discharging).

# ### Using apm to enter suspend mode

If the apm service is running, the apm command lets you view information about your computer’s power management and put the computer in suspend mode (if it is supported on your laptop). Here are some examples of using the apm command:

```
```
# apm -m
```
```

Using the -m option, the apm command displays the number of minutes of battery life remaining (if that information is available). It may also give you information about the status of how the battery is charging and whether or not the laptop is currently plugged in.

```
```
# apm -s
```
```

The -s option of apm causes the laptop to enter suspend mode. You can start up the laptop again, in most cases, by pressing a key on the keyboard.