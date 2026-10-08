![](bbox=[0.11, 0.11, 0.2, 0.23])

The GNOME Terminal is similar to the MS-DOS window in Windows. Opening an MS-DOS window provides a CLI in which to enter DOS commands. The underlying technology of a Windows CLI is different from that of a Linux CLI. However, its capabilities are more or less the same.

# Configuring Your Graphical Display

The Red Hat installation process is good at automatically configuring itself to use your video hardware and display — Linux uses the X Window System (X, for short) to display graphics. However, occasionally the X configuration process fails, or you may want to reconfigure it. Red Hat gives you access to the same configuration tool it uses during the installation process.

The Red Hat X configuration utility is the redhat-config-xfree86 program. We refer to it as simply the Display Configurator. Generally, the Display Configurator automatically detects your display (monitor) and graphics card. After they have been detected, you can set your display's resolution and color depth.

# Configuring with the Display Configurator

You can start the Display Configurator even if you're not running X Window (if you're running in nongraphical mode; nongraphical mode is run level 3):

+   1. **Log in as root.**

You're automatically placed in a CLI.
2. **Enter this command at the Bash prompt:**

`redhat-config-xfree86`

The Display Configurator window opens. The utility runs within a graphical interface.

You can, of course, start the Display Configurator if your computer is running X. You may want to reconfigure your system, for example. Follow these instructions to start the utility:

+   1. **Click the GNOME Menu.**
2. **Choose System Settings**→**Display**.
3. **Enter the root password, if you're prompted.**

The Display Configurator opens. Use the following set of steps to configure your graphical (X Window) interface.