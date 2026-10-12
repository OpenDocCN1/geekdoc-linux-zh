When you have the `ntsysv` application open, you can scroll through the list of services and toggle a service on or off by pressing the spacebar on the keyboard. When finished, use the Tab key to highlight the OK or Cancel button. Your changes are saved and used the next time Fedora is booted.

> **NOTE**
> `ntsysv` is simple to use and it's an excellent tool for a system without X, but it works for only the runlevel you are currently in. Use the `--level` option to modify other runlevels.

The Fedora tool setup is an ncurses-based menu for all the available ncurses-based command-line configuration tools (see Figure 15.2). It can be used to access `ntsysv` and all the other command-line configuration tools.

![](bbox=[0.2, 0.37, 0.85, 0.69])

**FIGURE 15.2** Use the setup command's System Services item to access the `ntsysv` command.

# Using the GUI-Based Service Configuration Tool

Fedora's developers have added GUIs to many text-only, command-line-based system administration tools as Linux has matured. These tools provide an easier-to-use interface and don't require memorization or lookup of command-line options. Fedora provides its own Service Configuration tool for the control and administration of services (see Figure 15.3). You can access the GUI menu selection from the System Settings/Server Settings menu, and then select Services. The command-line name of this tool is `system-config-services`.